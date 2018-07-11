# PID Controller Project
### Compiling  
This project is confirmed to compile on cmake 3.5.1, GNU make 4.1, gcc 5.4.0 in Ubuntu Bash on Windows 10.  
   ![bash](https://github.com/na6an/SDCND/blob/master/T2-P4/image/bash.PNG)  

### P,I,D Components & Tuning process
I began to tune P,I,D parameters in a few fellow peer students suggested in the discussion forum,  
began to increase P until it can handle the sharp turn but not enough to turn too much at the first corner.  
Then, increased D and I until it makes a lap stable. Following are some examples of different parameters.  

PID = (-1,0,0)  
![p-1](https://github.com/na6an/SDCND/blob/master/T2-P4/image/p-1.gif)  
(-0.4,0,0)  
![p-0.4](https://github.com/na6an/SDCND/blob/master/T2-P4/image/p-0.4.gif)  
(-0.6,0,0)  
![d-0](https://github.com/na6an/SDCND/blob/master/T2-P4/image/d-0.gif)  
(-0.6,0,-5)  
![i-0](https://github.com/na6an/SDCND/blob/master/T2-P4/image/i-0.gif)  

I also attempted basic twiddle in the model, but it appears making it work takes longer time than manual tuning at this point.  
What I adopted instead, is a dynamic speed change because I think tuning only the PID values to control steer is insufficient.  
Basically it slows down when the vehicle turns at the corner or as it deviates more from cte.  
This is the reason simulations above doesn't shoot out of the track even with poor PID tuning.  

### Result  
   [https://github.com/na6an/SDCND/blob/master/T2-P4/image/video.mp4](https://github.com/na6an/SDCND/blob/master/T2-P4/image/video.mp4)  

### Performance 
It appears spec and environment of the computer running the simulation influence vehicle performance.  
The vehicle was able to complete a lap without any issue when I don't run anything on background,  
but running the capturing software took resources away from the simulator and made the vehecle deviate away from the track.  

In such cases, modify `th` variable in following code from `main.cpp`, lower the base speed, which is currently 0.4.
```c++
          double th;
          if (abs(cte) > 1){
            th = 0.4 - cte * cte * speed * abs(angle)/ 1000; //0.4 + pid.UpdateError(cte);
          }else{
            th = 0.4 - abs(cte) * speed / 1000;
          }
```
