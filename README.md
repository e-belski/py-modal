# py-modal
The goal of this project is to develop a low cost, open source modal analysis software and hardware suite. Sensors and signal processing hardware will make the trade off between cost and noise. We hope to document these clearly and provide insight into higher cost options that will improve measurement fidelity.

The accelerometers that we initially use are those on the IMU chip MPU9250. This is for a few various reasons:
* 16 bit resolution is the highest we've encountered on a digital, low cost MEMS accelerometer. A few of these bits may be consumed by noise, however there is little evidence that we've encountered that suggests the lower resolution options offer any advantages.
* The 4 kHz sampling rate is the highest that we've encountered from MEMS digital accelerometers. This will theoretically allow a higher measurement range.
* We're familiar with this chip and have used it in other applications
* It has a nice development board available from Sparkfun and can be drag and dropped with the depricated but still low cost MPU6250

For impact hammer testing, we plan on using a strain gauge based load cell and load cell which are widely available from Sparkfun and use a well established transducer configuration. The amplifier has the added benefit of communicating over I2C. <link to strain gage load cell> As of now the body and tips and mass of the hammer will be 3D printed.

In order to time align measurements of the accelerometers and impact hammer a multi-tiered approach will be taken to synchronize the digital measurements. A raspberry pi or similar SoC will control a GUI and the signal processing, while micro controllers handshake with individual sensors on I2C channels. Each micro controller, a Teensy 4.0 for now, will be able to interface with 2 sensors on separate I2C channels, time aligned within about 400 kHz? (TBD). Each micro controller will receive a signal from the Raspberry Pi when the user is ready to begin collecting a set of data. At this point, each micro controller will begin polling their accelerometers or load cells.

(Assuming a sensor update rate of 4 kHz, each sensor could be off by as much as a 4 kHz time slice even if the I2C busses are synchronized. This is due to the I2C accelerometers not sharing a synchronized clock. Even so a 4 kHz error in measurements should be inconsequential for the modal frequencies this device is targeting. However we will keep this in mind when qualifying the device.)
