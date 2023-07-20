+++
title = "Your TV remote is not safe."
date = "2023-07-16T16:54:36-07:00"
# description = "A literature review abstract on HomeSpy"

tags = ["academic","literature",]
+++

You probably haven't thought about your TV remote giving away your passwords or details about your personal life like when you tuck your kids in to bed, but researchers at The Chinese University at Hong Kong and UC Irvine have demonstrated just that.

### Introduction and Background

[HomeSpy](https://www.usenix.org/system/files/sec23summer_97-huang-prepub.pdf) is a demonstrated attack system that can sniff InfraRed \(IR\) signals coming from a remote that uses IR to transmit data to a TV.

Previously, not much thought has been given to the security of IR used in homes for entertainment device control. TV remotes usually need to be pointed directly at the device they control and the data transmitted hasn't been sensitive. However, in recent times with the increase in IoT devices in homes and the discovery that IR signals can be captured out of direct line of sight, the robustness of these systems has been called in to question.

HomeSpy has a suite of software that decodes and extracts meaning from intercepted signals running on top of just a Raspberry Pi 3 and an IR sensor module that costs less than 10 cents for hardware.

The researchers assume that the attacker is able to gain access to some IoT device with an onboard IR sensor near the TV, which can relay sniffed information back to the attacker. This is an extremely common scenario. Many people today have smart home devices like smart LEDs or air conditioners.

Using this compromised device, the researchers show that it is possible to capture and decode IR signals into meaningful strings, which are then analyzed for sensitive information like account passwords.


### Methods

