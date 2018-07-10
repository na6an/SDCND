# CarND-Controls-MPC
---

## Dependencies
See Udacity CarND-MPC-Project repo for detail.
[https://github.com/udacity/CarND-MPC-Project](https://github.com/udacity/CarND-MPC-Project)  

## Basic Build Instructions
1. Clone this repo.  
2. This repo does NOT include Eigen library.  
   Copy from src dir in CarND-MPC-Project repo above.
3. Make a build directory: `mkdir build && cd build`  
4. Compile: `cmake .. && make`  
5. Run it: `./mpc`.  

## Compiling  
This project is confirmed to compile on cmake 3.5.1, GNU make 4.1, gcc 5.4.0 in Ubuntu Bash on Windows 10.

## The model, Timestep Length and Elapsed Duration (N & dt)
The model used is standard MPC model.  
![model](https://github.com/na6an/SDCND/blob/master/T2-P5/img/mpc-model.PNG)  

I started from the base code of MPC quiz provided here:  
[https://github.com/udacity/CarND-MPC-Quizzes](https://github.com/udacity/CarND-MPC-Quizzes)  

Once latency was implemented, it worked fine regardless of different combination of parameter values,  
whether it was 5 & 0.5, 10 & 0.01 or 25 & 0.05 as long as it was not too extreme.  
In this repo, 25 & 0.05 is used. Of course, these values are dependent on the speed of vehicle.

## Polynomial Fitting and MPC Preprocessing
Polynomial was fitted to 3rd order to reflect the curve as follows.  
 `auto coeffs = polyfit(ptsx_transform, ptsy_transform, 3);`  
Unlike from the lecture, desired actuators are preprocessed like following since it was fitted to 3rd order.  
```
 f0 = coeffs[0] + coeffs[1]*x0 + coeffs[2]*x0*x0 + coeffs[3]*x0*x0*x0;  
 psi_des0 = CppAD::atan(3*coeffs[3]*x0*x0 + 2*coeffs[2]*x0 + coeffs[1]);
```

## Latency
Latency was a crucial part to run properly.  
With 100 milisecond was given as a default latency,  
The initial state values at each time was simply recalculated with latency like following in main.cpp before solved.  
 ```
          double lx = v*cos(steer_value)*latency;
          double ly = v*sin(steer_value)*latency;
          double lpsi = - v*steer_value*latency/Lf;
          double lv = v + throttle_value*latency;

          double lcte = coeffs[0] + v*sin(-atan(coeffs[1]))*latency;
          double lepsi = -polyeval(coeffs, lx) - v*polyeval(coeffs, lx)*latency/Lf;

          state << lx, ly, lpsi, lv, lcte, lepsi;
```


## Result

[https://github.com/na6an/SDCND/blob/master/T2-P5/img/video_mpc.mp4](https://github.com/na6an/SDCND/blob/master/T2-P5/img/video_mpc.mp4)
