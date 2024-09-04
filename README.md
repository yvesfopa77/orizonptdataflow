# YLIQO Payment Terminal Data Flows 

*Author : Yves Fopa
Version : 1.2
Date : 23 aug 2024*

**Introduction**

The purpose of this document is to present the data flow between the payment terminal and the mobile application gateway.
Demos applications are also provided below to allow development team to test prototypes they are working on.

**Terminology**

Some terms are used in our documentation, so it's good to define them below :

*Payment Terminal :* NFC device powered with NXP (PN7642 chip) to be used to acquire payment requests from MIFARE® ESFire® EV3 card

*Payment Gateway :* Mobile app deployed on android device to serve as gateway to backend payment system. Connection between Payment Terminal and Payment Gateway is done via Bluetooth (BLE)

## Data Flows

There are 2 data flow between the Payment Terminal and the Payment Gateway, **DESFire EV3 Card initiated Data Flow** and a **Payment Terminal initiated SYNC Data Flow**.

**DESFire EV3 Card initiated Data Flow**

As the title stated, this data flow is triggered by DESFire EV3 card presented to the PN7642 chip NFC reader/writer on the Payment Terminal.
![Figure1](Data%20Flow%202024-08-21%20205156.png)

 1. Step 01 : Card detected by NFC reader chip. Read card data
 2. Step 02 : To be defined
 3. Step 03 : To be defined
 4. Step 04 : Transmit to Payment Gateway data read at step 01 and processed at step 03
 5. Step 05 : Data reception by Payment Gateway
 6. Step 06 : To be defined
 7. Step 07 : To be defined
 8. Step 08 : Transaction data sent to Payment Terminal (via BLE)
 9. Step 09 : Transaction data received by Payment Terminal
 10. Step 10 : To be defined
 11. Step 11 : DESFire ev3 card data update

**Payment Terminal initiated SYNC Data Flow**

As the title states, this data flow is triggered by the Payment Terminal itself (means without DESFire ev3  card being presented). This flow is used to synchronize the Payment Terminal with the backend payment to push all registered offline transactions.
![Figure2](Data%20Flow%202024-08-23%20142748.png)

 1. Step 01 : Button pressed
 2. Step 02 : To be defined
 3. Step 03 : Transmit to Payment Gateway data read at step 01 and processed at step 02
 4. Step 04 : Data reception by Payment Gateway
 5. Step 05 : To be defined
 6. Step 06 : To be defined
 7. Step 07 : Transaction data sent to Payment Terminal (via BLE)
 8. Step 08 : Transaction data received by Payment Terminal
 9. Step 09 : To be defined
 10. Step 10 : To be defined


## POC (Proof of Concept) testing

**To run POC testing, I've build 2 app :**

 1. An Arduino application to simulate BLE communication by Payment Terminal, [see code here](https://github.com/yvesfopa77/orizonbleperipheralpoc/blob/main/sketch_aug19a/sketch_aug19a.ino)

 2. An Android application to simulate BLC communication by Payment Gateway, [see code here](https://github.com/yvesfopa77/orizonbleclientpoc)

**How to run Arduino BLE application ?**

I've used an Arduino Nano 33 BLE Rev2 board.
Connected to the board using Arduino IDE, I've deployed the above mentioned code (see comment in the code to understand what the code does). Basically to code allow to receive data via BLE and Notify any device who is connected to the board and has subscribed to notification.
1) Install Arduino Nano 33 BLE Rev2 board
![board install](Arduino%20Nano%20BLE%20Rev2%202024-08-21%20224506.png)

2) Compile and upload the code (see above) to the board and open serial console to send and listen message to/from Android Payment Gateway.
![IDE](Arduino%20IDE%202024-08-21%20225010.png)

**How to run Android BLE application**

1) Application install

Option 1 : You have been invited as tester to be able to download android app from Google Play Store [Download link](https://play.google.com/apps/internaltest/4700155119323285744)
Option 2 : Build the code from the repo (see above) and run it using your preferred IDE (Visual Studio Code, Android Studio, or else)

2) Run application

 1. Launch the application on Android device, approve the permissions requests.
 2. Make sure Arduino board is on.
 3. Once the application starts, it will scan for all reachable BLE device in the near, Arduino board should be listed with the name `YLIQO_TERMINAL`, click on connect to connect to it and you will see available "BLE characteristics" listed. Select the `7DEF8317-7300-4EE6-8849-46FACE74CA2A"` service and click on notify to start listening on strings sent from Arduino board (via connected Arduino IDE console)

![Android BLE app](Android%20BLE%202024-08-21%20232351.png)

**POC testing limitation**

The main limitation of the POC is the fact that data transmission from Payment Terminal BLE to Payment Gateway (Step 04 above) implementation doesn't take into consideration that `A characteristic value can be up to 512 bytes long.` This means Payment Terminal BLE Step 04 implementation should consider sending data in multiple chuncks.

**Testing from POC Terminal** 

The above testing process with Arduino has been provided for demonstration purpose. 
To run proper POC testing, use YLIQO Payment POC Terminal with provided Android Payment Gateway

## Documentation and reading

[BLE reading](https://www.arduino.cc/reference/en/libraries/arduinoble/)
		
[Android BLE reading](https://punchthrough.com/android-ble-guide/)




