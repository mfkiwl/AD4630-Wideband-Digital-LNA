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
- Sample storage and processing
- Evaluating noise performance
- Implementing optical isolation and battery power
- Input analog circuitry to accomodate differential output and AC coupled input
## Usage
[under construction]
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
- The AD4630 has a somewhat limited reference voltage range - 4.096V to 5V. Since it cannot directly handle negative input voltages, the input signal is required to be centered around 2.5V. This turned out to be much more difficult than expected, so I might just go with a fully differential amplifier (e.g. LT6362) between the preamp (chopper) and the ADC.
- Whether a minimum input frequency below 0.1Hz is useful or practical remains to be decided. 
- Noise analysis with x10000 gain and a fully-differential op-amp on the output to make interfacing to the ADC easier:
![Infographic](https://github.com/NNNILabs/AD4630-Wideband-Digital-LNA/blob/main/Resources/noise10001.png)
- After a few rounds of thinking, it was decided that having a minimum frequency of 0.1Hz (to facilitate a practical high-pass filter) would waste the ADA4528's spectacular 1/f performance, and a high gain would reduce usable bandwidth to a few hundred Hertz. One solution would be to have a low-value attenuator (1/5, 1/10) to reduce the input voltage range for direct sampling using the AD4630, although this would nullify most of the 1/f benefits. To achieve a wide amplification range, a composite amplifier would also be necessary. Schematic remains to be decided.
- A Sallen-Key high-pass filter with a cutoff frequency of 0.01Hz requires component values that are more or less practical (16K, 1mF), and adding a gain stage in front of the filter also seems feasible.
![Infographic](https://github.com/NNNILabs/AD4630-Wideband-Digital-LNA/blob/main/Resources/filterandgain.png)
### Choice of Parts:
- AD4630 2Msps 24-bit ADC: 6.5-digit capable, fast sampling, internal filtering
- ADA4528 auto-zero op-amp: Lowest measured 1/f corner frequency
## Links
- https://github.com/macaba/NSD
- https://github.com/macaba/ad4630-pico-breakout
- https://github.com/macaba/Nuts/blob/main/images/NSD.png
- https://www.analog.com/media/en/technical-documentation/data-sheets/ad4630-24_ad4632-24.pdf
- https://www.analog.com/media/en/technical-documentation/data-sheets/ada4528-1_4528-2.pdf
- https://www.allaboutcircuits.com/technical-articles/Noise-Analysis-Using-LTspice-Tutorial/
- http://sim.okawa-denshi.jp/en/OPseikiHikeisan.htm
