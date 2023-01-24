# AD4630 Wideband Digital LNA
## Introduction
Output noise is an important metric when it comes to evaluating the performance of precision voltage references (temperature coefficient and stability being others). Of particular interest is the frequency band between 0.1Hz and 10Hz. Most long-scale integrating ADCs feature measurement periods that lie in this band, so the internal reference should ideally have noise lower than measurement resolution over this time period. To measure noise in this band, an amplifier, itself having low noise, is needed. Appropriate filtering is also desired to keep out excess noise (of other frequencies) from contaminating the band of interest. 
## Project Motivation
This idea was originally proposed to me by [Marco Reps](https://www.youtube.com/@reps), which was in turn based on an idea [Mark](https://github.com/macaba) had told him about - a digital sampler that would send raw samples to a computer program that would filter to the required bandwidth digitally. Given the 2Msps sample rate of the AD4630, the upper frequency limit could be expanded to several kilohertz. The addition of a chopper preamp would also greatly reduce input noise. DC-coupling the input and adding a few preamps in parallel would also make a crude nanovoltmeter. This project is intended mainly to explore the AD4630 itself, and evaluate possible front end circuits.
### Goals:
- Wideband sampling and digitally filtering samples to desired bandwidth
- Ultralow 1/f corner front end with AC and DC paths for noise and nanovolt measurements (TBD)
- Optically isolated digital and analog sections: This is achieved easiest using a separate controller for front-end side, and using something like a UART isolator and a UART-USB bridge on the other side. 
- Battery powered (front end at least, digital section USB powered): This one might be a bit challenging, for example, what kind of batteries will be used? What voltages to power the front end with? Single ended or bipolar?
### Challenges: 
- Evaluating noise performance
- Implementing optical isolation and battery power
## Usage
### Specifications:
- 10mHz to 10kHz input bandwidth    [calculated]
- x200000 (106dB)                   [calculated]
- ~3.5nV/rtHz noise floor (full BW) [calculated]
## List of Files
- Hardware: KiCAD PCB files.
![Prototype PCB layout](https://github.com/NNNILabs/AD4630-Wideband-Digital-LNA/blob/main/resources/front.PNG)
- Software: [under construction]
  - Simulation: LTspice .asc file.
- Resources: Infographics.
## Application Examples
[under construction]
- The LNA outputs raw samples that can be stored in a .csv file and interpreted by an [NSD](https://github.com/macaba/NSD) program. 
## Notes
- The AD4630 is pin-compatible with the AD4030, which opens up some interesting possibilities in the future.
- The input stage consists of a Sallen-Key filter that filters out frequencies below 10mHz while providing a gain of 330. It is possible to have gain and filtering in the same stage because of the low Thevenin resistance of the amplifier feedback resistors. The input filter/gain stage is followed by another x330 gain stage, which in turn is followed by a fully-differential amplifier to convert the input swing to a differntial swing for the ADC. It should theoretically be possible to cancel reference noise by setting fully differential amplifier common mode voltage to 1/2\*Vref as well as referencing one of the ADC differential inputs to 1/2\*Vref. Overall gain is 100000.
## Links
- https://github.com/macaba/NSD
- https://github.com/macaba/ad4630-pico-breakout
- https://github.com/macaba/Nuts/blob/main/images/NSD.png
- https://www.analog.com/media/en/technical-documentation/data-sheets/ad4630-24_ad4632-24.pdf
- https://www.analog.com/media/en/technical-documentation/data-sheets/ada4528-1_4528-2.pdf
- https://www.allaboutcircuits.com/technical-articles/Noise-Analysis-Using-LTspice-Tutorial/
- http://sim.okawa-denshi.jp/en/OPseikiHikeisan.htm
