# AD4630 Wideband Digital LNA [Work In Progress]
## AD4630-based 2Msps high resolution sampler
### Parts used:
- AD4630 2Msps 24-bit ADC
- ADA4528 Auto-zero op-amp
### Project goals:
- Wideband sampling and digitally filtering samples to desired bandwidth
- Ultralow 1/f corner front end with AC and DC paths for noise and nanovolt measurements (TBD)
- Optically isolated digital and analog sections
- Battery powered (front end at least, digital section USB powered)
### Challenges: 
- Sample storage and processing
- Evaluating noise performance
- Implementing optical isolation and battery power
### Resources:
- https://github.com/macaba/ad4630-pico-breakout
- https://github.com/macaba/Nuts/blob/main/images/NSD.png
