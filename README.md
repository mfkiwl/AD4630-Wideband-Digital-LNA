# AD4630 Wideband Digital LNA [Work In Progress]
## AD4630-based 2Msps high resolution sampler
### Parts used:
- AD4630 2Msps 24-bit ADC
- ADA4528 Auto-zero op-amp
### Project goals:
- Wideband sampling and digitally filtering samples to desired bandwidth
- Ultralow 1/f corner front end with AC and DC paths for noise and nanovolt measurements (TBD)
- Optically isolated digital and analog sections: This is achieved easiest using a separate controller for front-end side, and using something like a UART isolator and a UART-USB bridge on the other side. 
- Battery powered (front end at least, digital section USB powered): This one might be a bit challenging, for example, what kind of batteries will be used? What voltages to power the front end with? Single ended or bipolar?
### Challenges: 
- Sample storage and processing
- Evaluating noise performance
- Implementing optical isolation and battery power
- Input analog circuitry to accomodate differential output and AC coupled input
### Data:
- Front end Falstad simulation: https://tinyurl.com/2ahfb8re
### Timeline:
1. Prototype AD4630 "breakout" board to test soldering and get used to the IC itself, try different SPI settings.
2. Prototype entire system on [prototyping platform](https://github.com/macaba?tab=repositories).
3. Fully integrated PCB.
### Resources:
- https://github.com/macaba/ad4630-pico-breakout
- https://github.com/macaba/Nuts/blob/main/images/NSD.png
