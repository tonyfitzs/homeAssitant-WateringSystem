<h1>Project

This project was developed because.
1.	I'm a giant nerd!
2.	If there is a more complex way of doing something. Hey, why not!
3.	My requirements could not be met by a commercial off the shelf (COTS) solution

<h1>Requirments
So in terms of requirements, they were pretty conventional generally speaking, I have a small back yard which has two hi yield sprinklers each covering an ark of about 15 meters, I also have a number of potted plants that are to be watered via some low volume sprays  as well as a small vegetable plot which is covered by five 2.5 meter ark sprays.
To drive all of these sprinklers I have two solenoids, I turn on one solenoid to water the yard as well as the pot plants and the other solenoid to water the vegetable garden. 
So far this is very easy and could be done with any COTS Sprinkler controller, but I also wanted to integrate my sprinklers into Home Assitant, this dramatically reduced the list of options. I also didn’t want to spend a load of cash which pretty much ruled out all the COTS options for my use case. But there is also one other requirement which would be very difficult to solve with a COTS solution. That is I need to be able to have my watering system decide if it should use water from a tank or if it should use water from the main. 
So all that said and done I decided to embark on an approach using a NodeMCU D1 Mini controller and a number of other bits and bobs, the whole project cost me less than $150.

<h1>Bill of Materials

So here is the list of parts I used 
*	1 x NodeMCU, any version will do on average these cost about $6 

*	1 x 4 channel relay board that you can use with Arduino, there are loads of these on Ebay, and cost about $8.00

*	1 x pump start relay, believe it or not this is the most expensive part, apart from the pump its self, and cost about $70 this relay uses 24 volts in to control the relay and switches 240 volts out (because I live in Australia) 

*	1 x 24-volt transformer, because I am only driving two solenoids at a time (pump or main and garden or yard) I didn’t need a huge transformer. Generally, a watering solenoid only draws between 200 and 400 mA so half an amp transformer will be big enough, I purchased one for $15 but depending on your needs you may need a bigger one.  

*	1 x 5-volt power supply, for this I used one I had lying around, but you can pick one up for about $10

*	1 x ip54 weatherproof enclosure, this probably isn’t necessary, it all depends on your environment. But in my case I had one so I used it if you need one they cast about $20 but you can make up your own mind on what's required based on your needs.

*	3 x watering solenoids, these vary in pricing widely, mine cost about $30 each, and yes I realise this combined with everything else blows my budget, but you need these no matter what you do so get off my case!

*	1 x Non-contact Digital Water / Liquid Level Sensor For Arduino, this is what I use to tell if my water tank has water in it or not, this sensor cost about $10.00 and doesn't require any modification to the tank, in senses changes in the specific gravity around it. 

<h1>The fun stuff

Ok so what we have now is a bunch of bits, so let's hook it all together. Now I'm going to assume that this is not your first BBQ and you know how to use an Arduino device because basically that’s all the NodeMCU is. 
If you want to, you could build an Arduino sketch that will be fit for purpose, but one of the reasons I chose the NodeMCU is because you can load Tasmota on it. so that’s exactly what I did, below is a screenshot of my Tasmota settings, as you can see I have set it up as a Generic Module and I am using D0 through to D4 for my controls

![Image of Tasmota Settings](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/TasmotaSettings.PNG)

One of the unfortunate things I have found however with Tasmota, which is kind of irritating is that you can't read an input GPI via MQTT, or at least I haven't been able to find a way of doing it. if anyone reading this happens to know then please tell me because that would be very helpful. The reason I want to be able to do that is that in my setup I need to read the status of the water level sensor to decide if I need to use the pump or not. 
So as a workaround what I have done is set the input as a switch, this is coming in on D0 (GPIO16) and in order to be able to read its status I have a corresponding dummy Relay setup on D8 (GPIO15), now its important to note, there isn’t actually a relay attached to D8, this is just set up so that we can see the status in Home Assitant as well as via the tasmota Dashboard which you can see below. 

![Image of Tasmota dashboard](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/TasmotaDashboard.PNG)


