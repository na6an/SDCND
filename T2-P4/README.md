# PID Controller Project
### Compiling  
This project is confirmed to compile on cmake 3.5.1, GNU make 4.1, gcc 5.4.0 in Ubuntu Bash on Windows 10.  
   ![bash](https://github.com/na6an/SDCND/master/T2-P4/img/bash.PNG)  

### Result  
   ![video](https://github.com/na6an/SDCND/master/T2-P4/img/video.mp4)  

### Further Discussion  
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
