# ORIZON Payment Terminal Data Flows 

*Author : Yves Fopa
Version : 1.0
Date : 21 aug 2024*

**Introduction**

The purpose of this document is to present the data flow between the payment terminal and the mobile application gateway.
Demos applications are also provided below to allow development team to test prototypes they are working on.

**Terminology**

Some terms are used in our documentation, so it's good to define them below
Payment Terminal : NFC device powered with NXP (PN7642 chip) to be used to acquire payment requests from MIFARE® _DESFire_® _EV3_ card
Payment Gateway : Mobile app deployed on android device to serve as gateway to backend payment system. Connection between Payment Terminal and Payment Gateway is done via Bluetooth (BLE)

## Data Flows

There are 2 data flow between the Payment Terminal and the Payment Gateway, one data flow for card payment and a second data flow for Payment Terminal synchronisation with backend payment system.

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

## POC (Proof of Concept) testing

**To run POC testing, I've build 2 app :**

 1. An Arduino application to simulate BLE communication by Payment Terminal, [see code here](https://github.com/yvesfopa77/orizonbleperipheralpoc/blob/main/sketch_aug19a/sketch_aug19a.ino)

 2. An Android application to simulate BLC communication by Payment Gateway, [see code here](https://github.com/yvesfopa77/orizonbleclientpoc)

**How to run Arduino BLE application ?**

I've used an Arduino Nano 33 BLE Rev2 board.
Connected to the board using Arduino IDE, I've deployed the above mentionned code (see comment in the code to understand what the code does). Basically to code allow to receive data via BLE and Notify any device who is connected to the board and has subscribed to notification.

		





