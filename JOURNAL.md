---
title: "USB PD Power Suply"
author: "Keyaan"
description: "USB-PD Based Power Supply to power your non-5V electronics"
created_at: "2024-05-23"
---
--------------
# Total Time Spent: 14 hours
# Also spent about 3 hours making the BOM and finalising components


# May 23 2025:
Today i will be finding the USB PD negotiation IC. So basically i have the idea of making the smallest(that i can create) power module to power my electronics projects,
when i am prototyping.

okay, found the IC, it is [AP33772SDKZ-13-FA01](https://www.mouser.in/ProductDetail/Diodes-Incorporated/AP33772SDKZ-13-FA01?qs=2wMNvWM5ZX4CLYQ4%252BLyimw%3D%3D), and now i have another idea, let's make a variable power supply, which gives variable power supply if PPS is available, or else it gives constant supply @ 5V, 9V, 12V, 15V or 20V.

i think i am gonna use some microcontroller (probably an rp2040) along with an OLED that displays voltage and current, and also rotary encoders/potentiometers, although i haven't decided on that.

### Total Time Spent - 20 Mins

--------------
# May 24 2025:
Today, i made a block diagram by hand, and i selected the [ams1117 3.3v LDO regulator](https://lcsc.com/product-detail/Linear-Voltage-Regulators-LDO_Advanced-Monolithic-Systems-AMS1117-3-3_C6186.html) for the RP2040, but then i came to realise that the max input voltage for ams1117 is 15V, while max voltage with PD is 20V, so i chose another regulator(it is so hard to find a proper regulator). the new regulator now is [AMS1117S-3.3](https://lcsc.com/product-detail/Voltage-Regulators-Linear-Low-Drop-Out-LDO-Regulators_JSMSEMI-AMS1117S-3-3_C917152.html)

<img src="https://github.com/user-attachments/assets/e52aae66-0bd2-412d-a26d-ffc273337d7d" alt="Handmade Block Diagram" width="500" height="282">

I have also decided that instead of using EasyEDA this time, i will be using "KICAD - THE DAD OF CIRCUIT DESIGN"(lol). I started working on the schematic. RP2040 is also finalised for now. so 2 USB-C connectors will be on the PCB, one for programming RP2040 and other for **POWER**

Ok, so let me just write out all the finalised parts here:
1. [I2C OLED](https://robu.in/product/4pin-oled-display-module-blue-color/)
2. [Rotary Encoders x2](https://robu.in/product/hongyan-ec11h-7ce15p1zy15f7-rotary-encoder-with-push-button-switch-vertical-plug-in/), [what i chose earlier](https://robu.in/product/4pin-oled-display-module-blue-color/)
3. Microcontroller: [RP2040](https://www.lcsc.com/product-detail/Microcontrollers-MCU-MPU-SOC_Raspberry-Pi-RP2040_C2040.html)
4. [Flash for RP2040](https://lcsc.com/product-detail/NOR-FLASH_Winbond-Elec-W25Q128JVSIQ_C97521.html)
5. USB PD Sink Controller: [AP33772SDKZ-13-FA01](https://www.mouser.in/ProductDetail/Diodes-Incorporated/AP33772SDKZ-13-FA01?qs=2wMNvWM5ZX4CLYQ4%252BLyimw%3D%3D)
6. [Push Button](https://lcsc.com/product-detail/Tactile-Switches_C-K-PTS810SJK250SMTRLFS_C221896.html)
7. [Crystal @ 12MHz](https://www.lcsc.com/product-detail/Crystals_Abracon-LLC-ABM8-272-T3_C20625731.html?s_z=n_ABM8-272-T3)

#### Why I chose a 128Mbit chip instead of a smaller one?
I chose a bigger chip rather than the typical 16Mbit because of mainly three reasons:  
    1. the difference in price is about $0.1.  
    2. The RP2040 design guide recommends it.  
    3. I dont know how long is the code gonna be.  

ok, so i have finished with the work for the day, today i completed the RP2040 connections, like the bare minimum connections required, and i also finalised the parts, and tomorrow i will be looking into the connections of the USB-PD controller, and i hope to make a 4 layer PCB, although i will try with 2 layers, if it will be possible.
![Schematic done on 24th may](https://github.com/user-attachments/assets/033630af-b5f1-48d7-bd09-a7f47c8bbd45)

PS: I am changing the rotary encoders as i found out about a new, more popular encoder, the [EC11H](https://robu.in/product/hongyan-ec11h-7ce15p1zy15f7-rotary-encoder-with-push-button-switch-vertical-plug-in/), which is the one that i will be using...  

okay, i had some free time tonight so i worked more on the schematic, i came to realise that i have to LOGIC-SHIFT the I2C communication, so that i dont burn the rp2040, so for logic shifting i found BS138 to be the most common and i went with them. So, for proper logic-shifting, we also need a proper 5V supply, so i chose another LDO regulator😭(it's a pain finding proper regulator). A wise legend once said, choose your components wisely.Btw, i also added a few capacitors to the PD controller.

Things added to schematic:  
![image](https://github.com/user-attachments/assets/a2c67a91-b5f2-40c4-9b77-74e53549e0ee)
![image](https://github.com/user-attachments/assets/7894817c-4af5-4eb1-8c2e-939a754048d4)

If i were to rate the experience using Kicad rather than EasyEDA, i would say that it is good, and you get A LOT of customisability, but EasyEDA is much simple.

### Total Time Spent today - 2 hours 10 mins
--------------
# May 25 2025:
Another New day, another new schematic making sesh...
Today i will likely complete the schematic

So i have added the rotary encoders in the schematic, and i also added ESD protection on the USB-C ports. worked on the schematic too, and i had a bit of issue with the PD controller, what happened was that there were two voltage pins, VCC and VOUT, and i wasn't sure what to cnnect to what, but now it is fixed, thanks to the application circuit. so the plan is, today i finish the schematic, i start with the PCB at night, and by tomorrow night i start with the cad, and i apply by day after tomorrow night, let's  see if i can apply by May 27 night, after that i will start with the code for it.  
#### Yay! the schematic is done!!  

![image](https://github.com/user-attachments/assets/13cf5eb4-abae-4cdd-bb6a-31a3ac82cb6d)
![image](https://github.com/user-attachments/assets/814ef4ec-9d0c-4317-b3b0-6e8084588675)
![image](https://github.com/user-attachments/assets/5fff4948-45a7-4b58-8890-0cd2044d3c3b)


Ok, it's evening now, and i completed all the work of assigning footprints to symbols, now i can finally start with pcb designing


Hell Yeah! Most of the placement on my PCB is like done, and tomorrow i will start with the routing and finish it ASAP.  
![image](https://github.com/user-attachments/assets/5167ee3c-844b-4157-a108-3768e571add0)  
![image](https://github.com/user-attachments/assets/bec21b0c-56a5-4cc1-a2e0-06aefbbd0601)  
Haha, i will add 3d models tomorrow.  
This is the Design till now, i've tried to keep it as small as possible(50mmx70mm) and i will reduce the size even more if needed, but i haven't yet found connectors. People on slack recommened me XT60 connector, but i am not sure what am i gonna use.  
Maybe i can integrate multiple kinds of connectors, but this is for tomorrow, i am really really tired today


### Total time spent: 6 hours
--------------
# May 26 2025:
Yup, i started the PCB routing, i added 4 M3 Mounting holes too, here is the current progress:  
![image](https://github.com/user-attachments/assets/ab1a7e60-d05f-438c-840f-0d3713f971ca)

#### Time spent this session: 1 hour 45 mins
### Time Spent Today: 1 hour 45 mins
--------------
# May 27 2025
Today was the day i was supposed to complete my project, it is ofcourse delayed, but i will try to complete by tomorrow, i completed the pcb today, got a few errors to deal with:  
![image](https://github.com/user-attachments/assets/ad562d0d-9157-43db-87c6-80385e1f40e0)  
All the errors are the same, just for different components.
Here is the finished PCB:  
![image](https://github.com/user-attachments/assets/8b8628a2-fccd-4477-9366-7fd374929320)

Here is the CAD file i started tonight:  
![image](https://github.com/user-attachments/assets/0a1edd0a-66b0-4d39-9e10-f3af15691466)  
(I spent 5 mins only on the CAD)  


### Time Spent Today: 1 hour 30 mins
--------------
# May 28 2025
Done with the PCB, rmeoved all the thermal errors by using a bunch of vias and got 0 errors and warnings! I also shifted the barrel jack to the right by 2mm so that it would not be a problem in 3d printed part... Now Working on the 3D Model
#### Time Spent this session: 20 mins
 Completed the CAD, here are the final images:  
   
 CAD:  
 ![image](https://github.com/user-attachments/assets/babcb920-5bb2-4972-af39-2042b7cf4a04)    
 ![image](https://github.com/user-attachments/assets/7cf7985a-c85c-4552-ae46-b0d065034048)

  
PCB:  
![image](https://github.com/user-attachments/assets/b1b06363-f7c4-4f2f-ad24-0d1307ba7d3d)  
![image](https://github.com/user-attachments/assets/72b781c0-492a-476f-b777-d17956618048)  

### Time Spent this session: 1 hour 45 mins

Now time to work on other things like writing README.md and writing total time on top and writing BOM and all that

# May 29 2025
Shit, i cant find any DC barrel jack connectors on LCSC and i made a mistake selecting the footprint of the regulator ic, so i got to change some stuff up😭  
Finally:  
![Final PCB](https://github.com/Keyaan-07/USB-PD-Power-Supply/blob/main/Images/pcb.png)
![image](https://github.com/Keyaan-07/USB-PD-Power-Supply/blob/main/Images/Final1.png)
# time spent today: 30 mins

# 17 June 2025 
A few components arrived a few days ago, the solder paste and few other things. I realised that i had ordered the wrong pin headers lol, they are angled but i needed straight....

# 18 June 2025
THE PCB IS HERE. It looks Beautiful <333 cuz it's my first pcb hehehe
I am now starting the Long wait for my LCSC components

# July 11 2025
last saturday, 7th july, i tried soldering my first pcb, but then, the 1.1v and 3.3v pins of the rp2040 were shorted and i burned the rp2040, and i am gonna try again for the 2nd and final time, if it doesn't work ,i just have no projects and i'll be very sad. :(

I'll update soon, tomorrow or day after tomorrow about what happends
