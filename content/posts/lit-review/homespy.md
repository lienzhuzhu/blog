+++
title = "Your TV remote is not safe."
date = "2023-07-16T16:54:36-07:00"
# description = "A literature review abstract on HomeSpy"

tags = ["academic","literature",]
+++

You probably haven't thought about your TV remote giving away your passwords or your daily schedule, but researchers at The Chinese University at Hong Kong and UC Irvine demonstrated that an IR sniffer can extract such information from signals transmitted over devices as innoccuous as a TV remote.

### Introduction and Background

[HomeSpy](https://www.usenix.org/system/files/sec23summer_97-huang-prepub.pdf) is a demonstrated attack system that can sniff InfraRed \(IR\) signals used by TV remotes.

The communication between IR transmitters and their receivers like TV remotes and TVs was thought to be secure. TV remotes usually need to be pointed directly at the device they control and the data transmitted usually isn't sensitive. However, in recent times with the increase in IoT devices in homes and the discovery that IR signals can be captured out of direct line of sight, the security of these systems has been called in to question.

HomeSpy decodes and extracts meaning from intercepted signals using software running on top of just a Raspberry Pi 3 and an IR sensor module that costs less than 10 cents for hardware.

The researchers assume that the attacker is able to gain access to some IoT device with an onboard IR sensor near the TV, which can relay sniffed information back to the attacker. This is an extremely common scenario. It's common for consumers to have multiple IoT devices cohabiting a room.

Using this compromised device, the researchers show that it is possible to capture and decode IR signals into meaningful strings, which are then analyzed for sensitive information like account passwords.


### Methods and Contributions

I feel there are two main contributions of this work:

1. Translating captured sequences of IR codes into meaningful natural language
2. Demonstrating that rudimentary equipment is all that's needed

I will demonstrate the second contribution using an Arduino Uno and an IR commercial-off-the-shelf (COTS) receiver module almost identical to what was used by the authors in a future article.

The methods used to accomplish the first contribution are interesting. HomeSpy is composed of 3 components.

1. IR Sniffer made using a Raspberry Pi 3 and a COTS IR receiver module
    - At the link layer, the authors implemented a novel information recovery algorithm that learns the amount of time between key presses \(around 200ms\) and even parses through the more rapid REPEAT signals many vendors implement to ensure signal transmission (for instance, holding a key will result in redundant data being sent to the receiver every 25 to 40 ms). These sequences are sent to the IR Command Decoder.
2. IR Command Decoder receives the sequences from the hardware and decodes the keys into buttons. 
    - First the authors assembled a database mapping data sequences to buttons from online vendor data sheets.
    - Then each sequence is queried against the database.
3. Semantic Extractor
    - From the IR Command Decoder, we have sequences of buttons, but it is often still not enough to extract any meaningful information. Many TVs use virtual keyboards where a keyboard appears on screen and the user uses the D-pad to navigate this keyboard.
    - First the authors use some insight to identify which sequences correspond to keyboard input. Namely, when a user is in the keyboard, there will be many keys pressed in a short span of time and there will be many "OK" key presses alternating with character selection directions, which is distinct from when a user is selecting a video or application, where they will use the navigation keys more but only press "OK" once.
    - Then HomeSpy aligns presses to many possible virtual keyboard layouts to generate strings.

The authors were able to demonstrate HomeSpy was able to capture IR signals 45 degrees from direct line of sight, decode 70,000+ codes from 1,000+ unique devices, and extract top 5 candidate login credentials with 77% accuracy.

HomeSpy calls into question the disregard for home device IR security. In a following article, I hope to replicate their hardware set up.