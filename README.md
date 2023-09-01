Engineering materials
====

This repository contains engineering materials of a self-driven vehicle's model participating in the WRO Future Engineers competition in the season 2022.

## Content

* `t-photos` contains 2 photos of the team (an official one and one funny photo with all team members)
* `v-photos` contains 6 photos of the vehicle (from every side, from top and bottom)
* `video` contains the video.md file with the link to a video where driving demonstration exists
* `schemes` contains one or several schematic diagrams in form of JPEG, PNG or PDF of the electromechanical components illustrating all the elements (electronic components and motors) used in the vehicle and how they connect to each other.
* `src` contains code of control software for all components which were programmed to participate in the competition
* `models` is for the files for models used by 3D printers, laser cutting machines and CNC machines to produce the vehicle elements. If there is nothing to add to this location, the directory can be removed.
* `other` is for other files which can be used to understand how to prepare the vehicle for the competition. It may include documentation how to connect to a SBC/SBM and upload files there, datasets, hardware specifications, communication protocols descriptions etc. If there is nothing to add to this location, the directory can be removed.

## Introduction

Sensing capabilities of our vehicle:
Our vehicle has two types of sensors, ultrasonic sensors and colour sensors. With regards to colour sensors, our vehicle has two in the front facing forwards. This allows the vehicle to sense and identify the traffic sign colours and move left and right accordingly. We chose to use hue, saturation and value (HSV) in order to identify the colour of the traffic sign. We opted for HSV instead of red green blue (RGB) values as they are more reliable when considering lighting conditions. The colour sensors are facing front such that one is able to detect any traffic signs on the left and the other detects traffic signs on the right. From there, the vehicle identifies which colour the traffic signs are and carries out the appropriate movement to go left and right for the green and red traffic signs respectively. 

Additionally, our vehicle has two ultrasonic sensors, one facing front and the other facing the right side. The ultrasonic sensor facing front will be used to detect the outer wall of the game field. This will determine when our vehicle will turn to proceed to the next straightforward section, as it will begin to turn when it is a certain distance away from the outer wall. The front-facing ultrasonic sensor is also used to avoid any possible obstacles. The ultrasonic sensor facing the right side will be used to detect the inner wall of the game field when going clockwise and outer wall of the game field when going anticlockwise. This ensures that the vehicle will remain in the central lane when moving along the track.



Obstacle management mechanisms:
Following up on the sensing capabilities of our vehicle, they all allow the vehicle to identify traffic signs and manoeuvre from section to section. 

As previously discussed, the colour sensors sense for the HSV of objects in front of it. Once it reaches a certain value, it recognises it as a certain coloured traffic sign. From there, the vehicle is programmed to carry out specific actions in order to turn the correct direction where a green sign is to go left while a red sign is to go right. After identifying that there is a traffic sign in front of the vehicle, it proceeds to identify its colour by its hue. We used hue out of hue, saturation and value as we realised it differed the most between the red and green traffic signs. This would allow for more accurate sensing and identification of the traffic sign colour. Since the vehicle’s next set of movements are solely dependent on the colour of the traffic sign, it is extremely important that it is accurate in identifying the colours.

As for sensing the track walls and turning into the next section, we chose to go by the distance travelled by the vehicle as well as the distance from the front ultrasonic sensor. Going by just the front ultrasonic sensor may not be accurate as if the vehicle is slightly off, it will incorrectly detect the traffic sign as the outer track wall. This is not ideal. Hence, we chose to also include in the distance travelled by the vehicle. As it travels through a straightforward section, we measure the distance it travels. Once it hits a certain distance, it will start sensing for the outer track wall. Once it reaches a desired distance from the wall, it will turn into the next straightforward section of the game field. 

Additionally, we mounted an ultrasonic sensor to the side of our vehicle. This allows it to track the distance between itself and the track wall. This would work regardless of the direction our vehicle is travelling in, clockwise or counterclockwise. Besides staying in the middle of the lane, the side ultrasonic sensor also allows the vehicle to turn in the right direction. Since there is a possibility of our vehicle having to travel in a clockwise and/or anticlockwise direction, the side ultrasonic sensor allows it to turn in the right direction and not turn into the track walls.



Design choices for our vehicle:
Our vehicle is kept to a minimum height (<10cm) and our Robot Inventor hub is mounted low and in the centre of the robot’s length to ensure that its centre of gravity is centralised between the front and back wheels. Our sensors, both ultrasonic and colour, were placed considering the height of the track walls and traffic signs respectively. We ensured that they did not exceed 10 cm in height as they would be unable to detect the walls or sense the traffic signs. With the weight of two colour sensors and one ultrasonic sensor in the front, we aimed to balance it out by placing a motor(powering back wheels) at the very back of our vehicle. 

In terms of dimensions, our vehicle cannot exceed 30cm x 30cm x 20cm. Hence we opted for a more compact build. Having a smaller vehicle also allows it to turn sharper angles and navigate tight spaces should it go off track. We chose relatively large sized wheels to maintain stability of our robot and thinner wheels to allow it turn more easily

We also opted to mount the colour sensors on the sides of the robot facing forward so that they can sense the colour of the obstacles from the front rather than the side. This is more accurate compared to mounting home facing sideways since it will be hard for the robot to perfectly position itself in the gap between the 2 obstacle circles for sensing.

With regards to the steering mechanism of our vehicle, we made use of the Ackermann’s steering geometry with parallel tie rods. Additionally, the Ackermann angle is the angle between the steering axis and the line connecting the centres of the inside and outside wheels. This is meant to improve the turning capabilities of our vehicle. An approximation of this can be generated by moving the steering pivot point so as to lie on the centre of the rear axle. In the context of our vehicle, the lines drawn from the wheels should intersect at where our differential is.



Technical implementations:
There are two main parts of our code with regards to completing the obstacle challenge. Firstly, the colour sensors sense for the HSV of whatever is in front of i, once it detects a traffic sign, it then identifies the colour of the traffic sign it is facing and carries out specific actions. When the value sensed is more than 5, it means there is a traffic sign in front of it. Then going by the hue of the traffic sign, if it is more than 250, it is deemed to be a red one, if it is less than 250, it is deemed to be green. This same concept applies to both colour sensors. After identifying which colour it is and where it is(left or right), the vehicle carries out a series of movements in order to turn the right direction while avoiding the traffic sign.

In order to identify when to turn into the next straightforward section, we had 2 options. One was to mount a colour sensor facing downwards to sense the coloured lines(blue and orange) to determine when the next section would start. The other option was to go by the ultrasonic sensors as well as the distance travelled by the vehicle. The ultrasonic sensor would sense for the outer track wall only when the vehicle travels a fixed distance. This ensures that the vehicle does not mistake any traffic sign for the outer track wall and turn too early into the next section. We opted for the latter as it would allow more leeway as to when our vehicle was to turn into the next section. Sensing the coloured blue and orange lines would mean that the vehicle is already entering that section. Hence we opted to go by the ultrasonic sensors in order to determine when to turn into the next straightforward section.

To upload our code onto our vehicle, we made use of Bluetooth connectivity between the Robot Inventor Hub and our computer.
