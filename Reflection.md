# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Overview

This project implements a PID controller to control a car in Udacity's simulator. The simulator sends cross-track error, speed and angle to the PID controller(PID) using WebSocket and it receives the steering angle ([-1, 1] normalized) and the throttle to drive the car. The PID uses the uWebSockets WebSocket implementation.

## Dependencies

* cmake >= 3.5
* make >= 4.1(mac, linux), 3.81(Windows)
* gcc/g++ >= 5.4
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
* Udacity simulator

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## Describe the effect each of the P, I, D components had in your implementation.

* The proportional portion of the controller tries to steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly. 

* The integral portion tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present. 

* The differential portion helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it. 

## Describe how the final hyper parameters were chosen.
* The parameters were chosen manually by try and error. First, make sure the car can drive straight with zero as parameters. Then add the proportional and the car start going on following the road but it starts overshooting go out of it. Then add the differential to try to overcome the overshooting. The integral part only moved the car out of the road; so, it stayed as zero. After the car drove the track without going out of it, the parameters increased to minimize the average cross-track error on a single track lap. The final parameters where [P: 1.5, I: 0.0, D: 2.5].