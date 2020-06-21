---
layout: post
title:  "Getting Started with the RTL-SDR"
description: "The future of radio is soft"
date:   2019-11-30 10:27:55 +0800
categories: sdr
---

The RTL-SDR is a very cheap 25 USD (I got it for 50 SGD, shipping fee included) USB dongle that can be used as a computer based radio scanner for receiving live radio signals in your area. Depending on the particular model it could receive frequencies from 500 kHz up to 1.75 GHz. The dongle I bought from Amazon could receive frequencies from 500 kHz to 1.7 GHz and has up to 3.2 MHz of instantaneous bandwidth (2.4 MHz stable) and HF reception below 24 MHz in direct sampling mode. Most software for the RTL-SDR is also community developed, and provided free of charge. The origins of RTL-SDR stem from mass produced DVB-T TV tuner dongles that were based on the RTL2832U chipset. With the combined efforts of its creators it was found that the raw I/Q data on the RTL2832U chipset could be accessed directly, which allowed the DVB-T TV tuner to be converted into a wideband software defined radio via a custom software driver developed by one of it's creators.

{% assign imgs = "../../assets/images/RTL-SDR.jpg," | split: ',' %}
{% include image.html images=imgs height="600px" caption="The RTL-SDR software defined radio dongle." %}<br class="img">

Since its discovery, the RTL-SDR has become extremely popular and has democratized access to the radio spectrum. Now anyone including hobbyists on a budget can access the radio spectrum. It's worth noting that this sort of SDR capability would have cost hundreds or even thousands of dollars just a few years ago. The RTL-SDR is also sometimes referred to as RTL2832U, DVB-T SDR, DVB-T dongle, RTL dongle, or the "cheap software defined radio". There are now many other software defined radios better than the RTL-SDR, but they all come at a higher price. Currently the RTL-SDR is one of the best low cost RX only SDR available in the market. There is also the HackRF (costs about 300 USD) which can both transmit and receive.

# Software Defined Radio

Radio components such as modulators, demodulators and tuners are traditionally implemented in analogue hardware components. The advent of modern computing and analogue to digital converters allows most of these traditionally hardware based components to be implemented in software instead. Hence, the term software defined radio. This enables easy signal processing and thus cheap wide band scanner radios to be produced. However, a software defined radio does not include:

- A typical hardware-based RF communication system that can be modified in some way via software is not an SDR. For example, if a radio has hardware for both frequency modulation and amplitude modulation and allows the user to choose between the two by means of a software (or firmware) setting, we are not dealing with SDR. This might be called a software-controlled radio.

- A fully-hardware-based digital data link is not an SDR. The “software” in “software-defined radio” does not refer to the fact that the system transfers digital data for processing.

An SDR does not have to be a digital communication system. It may seem counterintuitive, but a very complicated digital (actually, mixed-signal) circuit board could be used to implement purely analog RF communication, such as the transmission of analog audio signals. An SDR does not have to provide both transmit and receive functionality. It might be only a transmitter or only a receiver. If it is capable of both transmitting and receiving, it might implement the Rx path in software and the Tx path in hardware.

{% assign imgs = "../../assets/images/sdrdia.png," | split: ',' %}
{% include image.html images=imgs height="200px" caption="Block diagram of a typical software defined radio system." %}<br class="img">

There is no reason why software has to be used for everything. Although SDRs such as the HackRF come with the transmit functionality, be sure to check out your local radio transmission guidelines before you transmit anything! In most countries transmitting requires a license of some sort, and transmitting without a license might get you into trouble.

# General Purpose RTL-SDR Software

There are many general purpose SDR software programs that allow the RTL-SDR to work like a normal wideband radio receiver. I'm on a Mac, so I'll be using the CubicSDR software to listen to radio signals with the RTL-SDR dongle. CubicSDR is a cross-platform Software-Defined Radio application which allows you to navigate the radio spectrum and demodulate any signals you might discover.  It currently includes several common analog demodulation schemes such as AM and FM and will support digital modes in the future.  Many digital decoding applications are available now that can use the analog outputs to process digital signals by “piping” the data from CubicSDR to another program using software like Soundflower, Jack Audio or VBCable.

{% assign imgs = "../../assets/images/cusdr.png," | split: ',' %}
{% include image.html images=imgs width="100%" caption="I used CubicSDR to tune into a local radio station at 96.8 MHz." %}<br class="img">

CubicSDR is the software portion of Software Defined Radio. By Using hardware that converts RF spectrum into a digital stream we are able to build complex radios to do many types of functions in software instead of traditional hardware. CubicSDR's modulation selector allows you to change modulation type for the active modem. There are currently several analog modulation types available:

|         Modulation        | Default Frequency | Minimum Frequency | Maximum Frequency |                                                    Note                                                   |
|:-------------------------:|:-----------------:|:-----------------:|:-----------------:|:---------------------------------------------------------------------------------------------------------:|
|       **Amplitude**       |       6 KHz       |       500 Hz      |      500 KHz      |                                                     -                                                     |
|       **Frequency**       |      200 KHz      |       500 Hz      |      500 KHz      |                                                    Mono                                                   |
|    **Stereo Frequency**   |      200 KHz      |      100 KHz      |      500 KHz      | Stereo (multiplex). Set the de-emphasis to balance the bass and treble to intended ranges (default 75us). |
| **Narrow-Band Frequency** |      12.5 KHz     |       500 Hz      |      500 KHz      |                                                    Mono                                                   |
|    **Lower-Side Band**    |      2.7 KHz      |       250 Hz      |      250 KHz      |                                                     -                                                     |
|    **Upper-Side Band**    |      2.7 KHz      |       250 Hz      |      250 KHz      |                                                     -                                                     |
|     **Dual-Side Band**    |      5.4 KHz      |       500 Hz      |      500 KHz      |                                                     -                                                     |


**Raw I/Q Pass-Thru (No Modulation):** raw I/Q samples that would normally go to a modem are passed through to the sound card for use elsewhere. Bandwidth is fixed to the selected sound card output frequency and will change along with it. Note that turning the Audio Gain down to a low level will disable gain completely and output the raw decimated samples.

# Squelch

The Squelch meter display the active signal level; to set squelch click or drag the meter to the desired trigger point. Right-clicking the squelch meter will set it just above the current signal level. Visible squelch floor and ceiling will be adjusted dynamically in an attempt to keep the relevant signal area in view. The set squelch level may also move with the signal when it changes but it remains at the same value.

# Audio Gain

By default CubicSDR will attempt to normalize the output from all active modems; if you want to adjust the gain of one modem versus another or enhance the automatic gain performance of an amplitude modulated signal you can use the audio gain to adjust the level. When using I/Q modulation dragging the gain to a low level will de-activate any automatic gain applied and output the original decimated signal input.

# Peak Hold

Activating Peak Hold will keep a maximum level history for the main and modem spectrum. Adjusting frequency or right-clicking the spectrum will reset the current Peak Hold history (and Visual Gain). Pressing ‘P’ will also toggle the Peak Hold button.

# Spectrum Averaging

Spectrum averaging speed can be adjusted by clicking / dragging the meter to the right of the main spectrum. Mouse wheel can also be used.

# Waterfall Speed

Waterfall speed can be adjusted from 1 to 1024 lines per second by clicking / dragging the meter to the right of the main waterfall. Mouse wheel can also be used. Waterfall history will continue to be collected and rendered at the desired rate while minimized; reducing speed before minimizing will reduce CPU load for this task.

# Manual Gain

If Automatic Gain is deactivated the Manual Gain sliders will appear. Available gain levels can be adjusted by click- ing/dragging or using the mouse wheel on the desired meter.

# Status Display

While hovering the Status Display will display relevant tips to the currently hovered UI element or action. Hover Tips are also enabled by default but can be disabled in the Settings menu.

# Solo

Enabling the Solo feature will mute all except the active modem. Selecting another modem will change the Solo focus. Solo mode is useful when you have many modems and want to focus on a particular one. Focus to the next and previous modem can be achieved with `TAB` and `SHIFT-TAB` on the keyboard. If modems are squelched while in Solo Mode the modem that breaks squelch will be focused and held for the duration of the squelch break. Pressing the `S` key will also toggle Solo Mode for the active modem.

# Mute

The Mute button shows the current mute state of the active modem and can be used to toggle it. The ‘M’ key can also be used to toggle mute for the active modem.

# Delta Lock

The Delta Lock button shows the current delta lock state of the active modem and is used to toggle it. When a modem is delta-locked it will remain at a fixed frequency relative to the center frequency. This allows you to tune freely without changing the relative modem position. The delta lock feature is useful in conjunction with sessions for creating band-plan relative set-ups. Changing bands via the center frequency won’t alter the active modem setup. Pressing the ‘V’ key will also toggle Delta Lock Mode for the active modem.

# Direct Input

Most numeric controls (speeds, levels, frequencies) in the CubicSDR application window can be entered directly on the keyboard. Hover over the desired value and press `SPACE` to open the input dialog; or just start typing a number and the dialog will appear automatically.
 
Pressing `SPACE` or typing a digit when not hovered over anything will open the Direct Input dialog for the Center Frequency.
For frequencies, Direct Input will also accept suffixes 'Hz', 'Mhz', 'KHz' and 'GHz' and will attempt to use the best suffix when presenting the existing frequency. If no suffix is used it will be assumed to be in MHz unless the value is greater than 3000, which will then default to Hz.

The type of modulation we set will determine if the radio signal can be decoded correctly and choosing the wrong modulation will render the signal inaudible and will be heard as noise. If you are on Windows I recommend you use SDR# because it's simple to use and has all the great features that CubicSDR offers. Using the RTL-SDR dongle and software such as CubicSDR, you can do anything from radio astronomy to wireless protocol analysis!
