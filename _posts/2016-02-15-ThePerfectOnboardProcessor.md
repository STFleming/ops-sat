---
layout: post
title: The Ideal on board Processor
author: shane_fleming
comments: True
---

![a misunderstood AI perhaps?]({{ site.url }}{{ site.baseurl }}/imgs/HAL9000.svg)

What would the ideal on board spacecraft processor look like? Me and my colleague [Felix Winterstein](http://cas.ee.ic.ac.uk/people/fw1811/) feel that it would have the following properties:

* High Processing Power
* Low power/energy consumption
* Flexibility to change things “in orbit”
* Rad-hard

###The ideal satellite processor would have high processing power...
High processing power is desirable in space applications but is often difficult to achieve.
One example is compression algorithms, these computationally intensive algorithms are useful as they reduce the amount of downlinking required (transmission back to earth) .
Such high processing power comes at a cost though, as fast CPUs generally use a lot of power and energy, taking us to our next point.

###The ideal satellite processor would have low power consumption...
Power consumption and energy usage are huge constraints in satellite designs, generally because everything needs to be powered from small solar panels.
The output from the solar panels is often not reliable; a tumbling satellite might not get full exposure to the sun, and power production degrades over time due to exposure to radiation.
This often requires a great deal of power *“slack”* further reducing the power/energy available for processing.

###The ideal satellite processor would be flexible...
Low Earth Orbit is a pretty difficult place to reach, and when designing big complex systems mistakes
happen and situations change.
In this regard software is great because it is flexible, patches/fixes can be tested on the ground and
applied to the craft remotely.
However hardware is inflexible, for example if a silicon bug causes an interrupt to occur with an incorrect priority then it might not be detected
during ground testing but could cause uncorrectable problems in orbit.

###The ideal satellite processor would be Rad-Hard...
Rad-Hard refers to radiation hardened, but is becoming a more general term for reliable, fault tolerant, electronics.
Radiation is a problem for on board computers as unwanted energy can cause memory bits
to flip from 1 to 0, or 0 to 1.
This radiation is usually in the form of high energy energy ionizing particles that are caught in the
earths magnetic field or emitted during high energy events such as a coronal mass ejection from the Sun.
Memory circuits, such as SRAM cells, are particularity sensitive to faults from this type of radiation
and for this reason cache memories are often heavily rad protected in space computers.


![an FPGA!]({{ site.url }}{{ site.baseurl }}/imgs/fpga.png)

One of the goals of the OPS-SAT experiment is to investigate how commercial FPGAs (ones that are not specifically designed for space) can be used to perform onboard computation.
So a good question is, how do **FPGAs** compare against the ideal spacecraft processor?

* *FPGAs have high processing power* - **True** for certain applications. They are great at parallel processing, this makes them great for applications like medical imaging or digital signal processing.

* *FPGAs have low power/energy consumption* - **True** in fact microsoft have been using [FPGAs in their Bing](http://research.microsoft.com/en-us/projects/catapult/) search engine for this very reason.

* *FPGAs are flexible* - **True** Once deployed FPGAs can be reprogrammed to perform a completely different task. 
Within a few hundred milliseconds they can be changed from a multicore processor to an application specific image processing unit.
(They even have “field programmable” in their name)

* *FPGAs are Rad-Hard* - **False** FPGA circuits are described in memory (SRAM) which is sensitive to bit flips caused by high energy particles.
Bit flips caused by these particles could alter the data the FPGA is processing, or worse still, reconfigure the actual structure of the circuit altering logic gates from one type to another or
by altering how components are connected together.

Our work (documented in this blog) aims to investigate how sensitive these commercial FPGAs are to bit flips in orbit and methods for protecting them, bringing
FPGAs closer to the ideal onboard processor.

