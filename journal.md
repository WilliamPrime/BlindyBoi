---
title: "Blindy Boi"
author: "William Wallace"
description: "videography light, BUT ITS VERY BRIGHT"
created_at: "05-06-25"
---

# START OF THE JOURNAL

# dumping my brain
inspired by this
![image](https://github.com/user-attachments/assets/752716ce-cdc8-407c-a5e2-f227bbe6f85a)


bms?
diy or something else

couple of rotary encoders for brightness and temp

rp2040 mcu
perhaps custom pcb for everything???

perhaps i do

power, charging, mcu, pots and all that on one pcb
then have that connect to another PCB 
with the other PCB only being LEDs

with the intent of that being the front pcb


# part selection

- what ic to use for usb pb?
	HUSB238
	- allows for selection of voltage and current with simple resistors, no need for i2c
	- not sure on availability
		- look for alternatives?? 

- 18650 cell with 4000mah capacity
	- assuming worse than the worst case, and the circuit draws 120w
		- (planned max draw is 80w)
		- then 120w/3.7 = 32a
		- split that between 6 cells
		- 5.5a per cell
		- https://www.fogstar.co.uk/collections/18650-batteries/products/fogstar-energy-4000-18650-battery
		- these are rated for 10a per cell
		- nominal v = 3.6
		- 10a x 6 x 3.6 = max theoretical power of 216w, ample

- use a relay for the first power stage
	- relay defaults to being powered by battery
		- once mains is connected, it powers relay and switches over to the usb power
		- add diodes to prevent back powering the relay from the battery
	- 


- which LEDs to use
	- needs to be fairly high power
		- rules out neopixels since would need a larger number
	- also needs to be fairly high CRI, 70+, ideally 80+
	- not a massive footprint, i need to be able to have a grid of them so they blend nicely without massive hotspots
	- found the lumileds, "LUXEON SunPlus 5050"
		- available in 6v or 24v , current would start getting ridiculous at 6v 24v seems smarter
			- the 24v have cri of 80 instead of 90, but 80 is already good
	- ideally i want some warm, and some cold so i can blend
		- 2200-3000k for the warm, 9000k for the cold
			- those lumileds are available above 6500k, but i think thats good enough, i tend to like warm lights anyway
	- this lands us with the following LEDs
	  
	  https://www.mouser.co.uk/ProductDetail/997-L150228050240H
	  - specs
		  - 6500k
		  - 24v @ 160ma , 3.8w
		  - 650lm
		  - 80 CRI
	  
	  https://www.mouser.co.uk/ProductDetail/997-L150658050240H
	  - specs
		  - 2200k
		  - 510lm
		  - 24v @ 160ma , 3.8w
		  - 80 CRI
	    
	    
- mosfet for switching the LEDs
	- https://www.mouser.co.uk/ProductDetail/771-PMV20XNER
		- power disipation of 1.2w
		- 30v max power
		- sustained current @ 25c = 5.7a
		- sustained current  @ 100c = 3.6a
			- 3.6a @ 24v --> 86.4w
			- i will have the current split across two of these anyway, one for the warm LEDs, one for the cool LEDs
	- https://www.mouser.co.uk/ProductDetail/511-STD17NF03L
		- NEW MOSFET
		  significantly more expensive,
			- 0.621 vs 0.145
		- sustained current @ 25c = 17a
		- sustained current  @ 100c = 12a
			- 12a @ 24v --> 288w
