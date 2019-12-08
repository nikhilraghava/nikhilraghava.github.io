---
layout: post
title:  "Getting Started with the RTL-SDR"
date:   2019-11-30 10:27:55 +0800
categories: sdr
---

The RTL-SDR is a very cheap 25 USD (I got it for 50 SGD, shipping fee included) USB dongle that can be used as a computer based radio scanner for receiving live radio signals in your area. Depending on the particular model it could receive frequencies from 500 kHz up to 1.75 GHz. The dongle I bought from Amazon could receive frequencies from 500 kHz to 1.7 GHz and has up to 3.2 MHz of instantaneous bandwidth (2.4 MHz stable) and HF reception below 24 MHz in direct sampling mode. Most software for the RTL-SDR is also community developed, and provided free of charge. The origins of RTL-SDR stem from mass produced DVB-T TV tuner dongles that were based on the RTL2832U chipset. With the combined efforts of its creators it was found that the raw I/Q data on the RTL2832U chipset could be accessed directly, which allowed the DVB-T TV tuner to be converted into a wideband software defined radio via a custom software driver developed by one of it's creators.

![RTL-SDR]({{site.baseurl}}/assets/img/RTL-SDR.jpg)
*The RTL-SDR software defined radio dongle.*

Over the years since its discovery RTL-SDR has become extremely popular and has democratized access to the radio spectrum. Now anyone including hobbyists on a budget can access the radio spectrum. It's worth noting that this sort of SDR capability would have cost hundreds or even thousands of dollars just a few years ago. The RTL-SDR is also sometimes referred to as RTL2832U, DVB-T SDR, DVB-T dongle, RTL dongle, or the "cheap software defined radio". There are now many other software defined radios better than the RTL-SDR, but they all come at a higher price. Currently the RTL-SDR is one of the best low cost RX only SDR available in the market. There is also the HackRF (costs about 300 USD) which can both transmit and receive.

## Software Defined Radio

Radio components such as modulators, demodulators and tuners are traditionally implemented in analogue hardware components. The advent of modern computing and analogue to digital converters allows most of these traditionally hardware based components to be implemented in software instead. Hence, the term software defined radio. This enables easy signal processing and thus cheap wide band scanner radios to be produced. However, a software defined radio does not include:

- A typical hardware-based RF communication system that can be modified in some way via software is not an SDR. For example, if a radio has hardware for both frequency modulation and amplitude modulation and allows the user to choose between the two by means of a software (or firmware) setting, we are not dealing with SDR. This might be called a software-controlled radio.

- A fully-hardware-based digital data link is not an SDR. The “software” in “software-defined radio” does not refer to the fact that the system transfers digital data for processing.

An SDR does not have to be a digital communication system. It may seem counterintuitive, but a very complicated digital (actually, mixed-signal) circuit board could be used to implement purely analog RF communication, such as the transmission of analog audio signals. An SDR does not have to provide both transmit and receive functionality. It might be only a transmitter or only a receiver. If it is capable of both transmitting and receiving, it might implement the Rx path in software and the Tx path in hardware. 

![sdr]({{site.baseurl}}/assets/img/sdrdia.png)
*Block diagram of a typical software defined radio system.*


There is no reason why software has to be used for everything. Although SDRs such as the HackRF come with the transmit functionality, be sure to check out your local radio transmission guidelines before you transmit anything! In most countries transmitting requires a license of some sort, and transmitting without a license might get you into trouble.

## General Purpose RTL-SDR Software

There are many general purpose SDR software programs that allow the RTL-SDR to work like a normal wideband radio receiver. I'm on a Mac, so I'll be using the CubicSDR software to listen to radio signals with the RTL-SDR dongle. CubicSDR is a cross-platform Software-Defined Radio application which allows you to navigate the radio spectrum and demodulate any signals you might discover.  It currently includes several common analog demodulation schemes such as AM and FM and will support digital modes in the future.  Many digital decoding applications are available now that can use the analog outputs to process digital signals by “piping” the data from CubicSDR to another program using software like Soundflower, Jack Audio or VBCable.

![sdr]({{site.baseurl}}/assets/img/cusdr.png)
*I used CubicSDR to tune into a local radio station at 96.8 MHz.*

CubicSDR is the software portion of Software Defined Radio. By Using hardware that converts RF spectrum into a digital stream we are able to build complex radios to do many types of functions in software instead of traditional hardware. CubicSDR's modulation selector allows you to change modulation type for the active modem. There are currently several analog modulation types available:

#### AM: Amplitude Modulation

Amplitude Modulation with carrier signal, default 6KHz, minimum 500 Hz, maximum 500 KHz.

#### FM: Frequency Modulation

Default 200 KHz bandwidth, minimum 500Hz, maximum 500KHz, mono.

#### FMS: Stereo Frequency Modulation

Default 200 KHz, minimum 100 KHz, maximum 500 KHz, stereo (multiplex). Set the de-emphasis to balance the bass and treble to intended ranges (default 75us).

#### NBFM: Narrow-Band Frequency Modulation

Default 12.5 KHz, minimum 500 Hz, maximum 500 KHz, mono.

#### LSB: Lower-Side Band

Lower-Side Band of AM (no carrier), default 2.7 KHz, minimum 250 Hz, maximum 250 KHz.

#### USB: Upper-Side Band

Upper-Side Band of AM (no carrier), default 2.7 KHz, minimum 250 Hz, maximum 250 KHz.

#### DSB: Dual-Side Band

Same as AM but without carrier signal, default 5.4 KHz, minimum 500 Hz, maximum 500 KHz.

#### I/Q: Raw I/Q Pass-Thru (No Modulation)

Raw I/Q samples that would normally go to a modem are passed through to the sound card for use elsewhere. Bandwidth is fixed to the selected sound card output frequency and will change along with it. Note that turning the Audio Gain down to a low level will disable gain completely and output the raw decimated samples.

The type of modulation we select will determine if the radio signal can be decoded correctly and choosing the wrong modulation will render the signal inaudible and will be heard as noise. If you are on Windows I recommend you use SDR# because it's simple to use and has all the great features that CubicSDR offers. Using the RTL-SDR dongle and software such as CubicSDR, you can do anything from radio astronomy to wireless protocol analysis!
