
# Project

This project was developed because.

1.	I'm a giant nerd!
2.	If there is a more complex way of doing something. Hey, why not!
3.	My requirements could not be met by a commercial off the shelf (COTS) solution


**General disclaimer:** I write English like it’s a second language. Problem is it's my mother tongue, I firmly believe the English language was created by people who cheat at scrabble 😊 so if you see any spelling mistakes, don’t bother pointing them out.  


# Requirments
So in terms of requirements, they were pretty conventional generally speaking, I have a small back yard which has two hi yield sprinklers each covering an ark of about 15 meters, I also have a number of potted plants that are to be watered via some low volume sprays  as well as a small vegetable plot which is covered by five 2.5 meter ark sprays.
To drive all of these sprinklers I have two solenoids, I turn on one solenoid to water the yard as well as the pot plants and the other solenoid to water the vegetable garden. 
So far this is very easy and could be done with any COTS Sprinkler controller, but I also wanted to integrate my sprinklers into Home Assitant, this dramatically reduced the list of options. I also didn’t want to spend a load of cash which pretty much ruled out all the COTS options for my use case. But there is also one other requirement which would be very difficult to solve with a COTS solution. That is I need to be able to have my watering system decide if it should use water from a tank or if it should use water from the main. 
So all that said and done I decided to embark on an approach using a NodeMCU D1 Mini controller and a number of other bits and bobs, the whole project cost me less than $150.

# Bill of Materials

So here is the list of parts I used 
*	1 x NodeMCU, any version will do on average these cost about $6 

*	1 x 4 channel relay board that you can use with Arduino, there are loads of these on Ebay, and cost about $8.00

*	1 x pump start relay, believe it or not this is the most expensive part, apart from the pump its self, and cost about $70 this relay uses 24 volts in to control the relay and switches 240 volts out (because I live in Australia) 

*	1 x 24-volt transformer, because I am only driving two solenoids at a time (pump or main and garden or yard) I didn’t need a huge transformer. Generally, a watering solenoid only draws between 200 and 400 mA so half an amp transformer will be big enough, I purchased one for $15 but depending on your needs you may need a bigger one.  

*	1 x 5-volt power supply, for this I used one I had lying around, but you can pick one up for about $10

*	1 x ip54 weatherproof enclosure, this probably isn’t necessary, it all depends on your environment. But in my case I had one so I used it if you need one they cast about $20 but you can make up your own mind on what's required based on your needs.

*	3 x watering solenoids, these vary in pricing widely, mine cost about $30 each, and yes I realise this combined with everything else blows my budget, but you need these no matter what you do so get off my case!

*	1 x Non-contact Digital Water / Liquid Level Sensor For Arduino, this is what I use to tell if my water tank has water in it or not, this sensor cost about $10.00 and doesn't require any modification to the tank, in senses changes in the specific gravity around it. 

# The fun stuff

Ok so what we have now is a bunch of bits, so let's hook it all together. Now I'm going to assume that this is not your first BBQ and you know how to use an Arduino device because basically that’s all the NodeMCU is. 
If you want to, you could build an Arduino sketch that will be fit for purpose, but one of the reasons I chose the NodeMCU is because you can load Tasmota on it. so that’s exactly what I did, below is a screenshot of my Tasmota settings, as you can see I have set it up as a Generic Module and I am using D0 through to D4 for my controls

![Image of Tasmota Settings](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/TasmotaSettings.PNG)

One of the unfortunate things I have found however with Tasmota, which is kind of irritating is that you can't read an input GPI via MQTT, or at least I haven't been able to find a way of doing it. if anyone reading this happens to know then please tell me because that would be very helpful. The reason I want to be able to do that is that in my setup I need to read the status of the water level sensor to decide if I need to use the pump or not. 
So as a workaround what I have done is set the input as a switch, this is coming in on D0 (GPIO16) and in order to be able to read its status I have a corresponding dummy Relay setup on D8 (GPIO15), now its important to note, there isn’t actually a relay attached to D8, this is just set up so that we can see the status in Home Assitant as well as via the tasmota Dashboard which you can see below. 

![Image of Tasmota dashboard](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/TasmotaDashboard.PNG)

Ok, so hopefully this is all coming together, and its possibly safe to assume that anyone embarking on this kind of project has a basic understanding of how to connect things together, but I hate assumptions😊 I can’t begin to tell you how many of these kinds of tutorials I have read when the writer has left out a critical bit of info because of an assumption. I don’t want to be that guy. 
So below you should see a diagram of how my setup is connected together, I have also included the Fritzing file in the diagram folder
![Image of Circuit layout](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/Watering_system_Layout.png)

I have also included a collection of pictures of my actual installation, now I’m not the most detailed dude. So when I install stuff in my own place it tends to be a little slap dash, but you get the idea of what it is we are trying to do. So below in order are pictures of my system

![Image of Watering main controler](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/Watering_main_controler1.jpg)

![Image of Watering main controller alternative view](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/Watering_main_controler2.jpg)

![Image of Tank Empty Sensor](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/TankEmptySensor.jpg)

![Image of pump](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/Pump.jpg)

![Image of NodeMCU](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/NodeMCU.jpg)

![Image of Main Valve ](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/MainValve.jpg)


In my setup, I actually have a second controller setup for a different part of the garden, as you can see I have put a lot more effort into the setup of the box and it’s a lot neater

![Image of IP54 box ](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/IP54box.jpg)

![Image of Secondary Controler](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/SecondaryControler.jpg)

![Image of Secondary Controler](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/SecondaryControlerExternal.jpg)

![Image of Secondary Controler](https://github.com/tonyfitzs/homeAssitant-WateringSystem/blob/master/Images/SecondaryControleroverview.jpg)

# Integration into Home Assistant 
There are a couple of approaches with regard to getting all the buttons and switches into Home Assitant, the approach I choose to use is send the command “setoption19 1” from the console in Tasmota, this will enable Home Assitant to Autodiscover all the switches. 

Now this approach isn’t perfect, in fact it's pretty not perfect😊 once you issue that command whatever you have named your stitches as will be sent to Home assistant, and even if you change the names Home Assitant remembers the old ones and just makes new ones, this is annoying. So what I do is make sure that I have named all my switches in Tasmota first. You do that by going into configuration, then configure other. There you will see the place to name all the switches. 

The other approach is to use a switch.yaml file and include that in your configuration.yaml using the following line “switch: !include Includes/switch.yaml”
Below is an example of what the MQTT setings look like for my setup.

**Note:**  when I fist started using Tasmotta, I got traped by a setting that is often assumed you know. That is the Full Topic seting in the Tasmotta MQTT settings, in my case it is set to %topic%/%prefix%/ which means that the command topic and state topic are formatted as show below, but if the setting is %prefix%/%topic%/ needless to say the command topic and state topic will look like this " cmnd/sprinklers/POWER1” sorry for those who know this. But as I said I hate assumptions. 

########################
##       Watering     ##
########################
##       Pump         ##
########################
  - platform: mqtt
  
    name: "Pump"
    
    command_topic: “sprinklers/cmnd/POWER1”
    
    state_topic: “sprinklers/cmnd/POWER1"
    
    qos: 1
    
    payload_on: “ON”
    
    payload_off: “OFF”
    
    payload_available: “Online”
    
    payload_not_available: “Offline”
    
    retain: false 
    
########################
##        Main        ##
########################   
  - platform: mqtt
  
    name: "Main"
    
    command_topic: “sprinklers/cmnd/POWER2”
    
    state_topic: “sprinklers/cmnd/POWER2”
    
    qos: 1
    
    payload_on: “ON”
    
    payload_off: “OFF”
    
    payload_available: “Online”
    
    payload_not_available: “Offline”
    
    retain: false   
    
########################
##         Yard       ##
########################   
  - platform: mqtt
  
    name: "Yard"
    
    command_topic: “sprinklers/cmnd/POWER4”
    
    state_topic: “sprinklers/cmnd/POWER4"
    
    qos: 1
    
    payload_on: “ON”
    
    payload_off: “OFF”
    
    payload_available: “Online”
    
    payload_not_available: “Offline”
    
    retain: false 
    
########################
##      Garden        ##
########################   
  - platform: mqtt
  
    name: "Garden"
    
    command_topic: “sprinklers/cmnd/POWER3”
    
    state_topic: “sprinklers/cmnd/POWER3
    
    qos: 1
    
    payload_on: “ON”
    
    payload_off: “OFF”
    
    payload_available: “Online”
    
    payload_not_available: “Offline”
    
    retain: false  
    
once Home Assitant has the switches configured, I am going to assume you know what to do from there, of not go back to the getting started with Home Assitant videos, of which there are hundreds. 




# NodeRed. 
If you're not using Node-red. I have one question for you. **ARE YOU MAD?**

In my setup, I use NodeRed a lot, basically because the automation in Home assistant can get pretty unwieldy if you have to do something really complex. Now I’m not going to explain how to use NodeRed there are a heap of tutorials out there,  but what I have done is added the code from my NodeRed node that is used to control my watering system; hopefully you won't have to much trouble figuring out how to make it all work. 

But you will need to add a couple of components, the first one is Bigtimmer
https://flows.nodered.org/node/node-red-contrib-bigtimer 

the second one is bool-gate
https://flows.nodered.org/node/node-red-contrib-bool-gate

To add these to NodeRed it is pretty easy, all you need to do is navigate to the “manage palettes” menu in Node-red (click on the hamburger icon in the top right corner), from there you can see an install option in the top row of the form, (just under the close button) if you type into the search “bigtimer” you will see the big timmer option appear, you just need to then install it. the same applies to gate. 

I generally find that it is better to add these additional things before importing a flow, but don’t worry if you don’t, Node-Red will tell you if something is missing, the only problem is you need to pay attention during the import or else you won't know what's missing. 

I hope you have found this useful. Feel free to leave a comment or ask questions, I'm a pretty busy guy generally so if I don’t answer you right away, please don’t get offended. But I will do my best to get back to you as soon as I can. 


