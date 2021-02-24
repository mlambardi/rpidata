You can turn your laptop or desktop computer into a data factory, so did I. Here you can find data from the internal sensors on my main workstation, every minute from February 6 through 22.

This is somewhat more challenging data, since I use the workstation to live, so its vitals are changing more through time due to my daily activities (the RPi instead acts only as a environmental monitoring system).

There are four types of variables in the *pc.csv* dataset.

* *time* variables:
  + timestamp: time at recording, in yyyy-mm-dd HH:MM:SS; see, recording is scheduled at HH:MM:00, but it takes a random (small) number of seconds to do;
  + session: counting sessions, or start ups;
  + sessiontime: minutes since startup;
  + sessionlen: total length of the session in minutes.
* *temperature* variables, in Celsius:
  + tempcore0,1,2,3: temperature of individual CPU cores, got four (old machine but sturdy);
  + tempradeon,cpu,mobo: temperature of video card, CPU, motherboard.
* *voltage* variables in... Volts:
  + volt3,5,12: the effective voltage for different types of devices;
  + voltcore: voltage aimed at the core, I'll check if it's ratio over nominal or actually in Volts.
* *fan speed* variables, in RPM:
  + speedfancpu,chassis: got two fans.

All variables are cheap to retrieve, so no need to surrogate anything, no regression nor the like. Probably it's more the case for unsupervised learning, like cluster analysis and stuff.

I'll detail this section later.. Enjoy!

## Data input

Try to load data in **R**, you don't need a local copy of the repository:

`data <- read.csv("https://raw.githubusercontent.com/mlambardi/rpidata/main/DIY/pc.csv", header=T, sep=",")`

It's best to convert the timestamp in POSIX so that plot utilities will handle it nicely:

`data$timestamp <- as.POSIXct(data$timestamp, format="%Y-%m-%d %H:%M:%OS")`
