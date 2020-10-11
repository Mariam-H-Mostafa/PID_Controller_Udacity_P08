
**PID Controller Project**

The goal of this project is to implement a PID controller in C++ to maneuver the vehicle around the track.

CTE is obtained from the simulator as well as the speed.

First step, we initialize the PID coefficients (init_kp, init_kd, init_ki), and the errors.

![enter image description here](https://i.ibb.co/y5pRbST/Picture1.png) ![enter image description here](https://i.ibb.co/TLrydJ8/Picture2.png)

Then, update the error using CTE provided by simulator, and calculate the steer_value using the total error calculated.

![enter image description here](https://i.ibb.co/X7VDBXF/Picture3.png)

![enter image description here](https://i.ibb.co/tbwJ8GD/Picture4.png)

![enter image description here](https://i.ibb.co/YbM33xk/Picture5.png)


**Optimizing the parameters:**

I didn’t use the twiddle algorithm here because it is difficult to calculate the cost each time and then reupdate the parameters. I need the cost to be updated simultaneously. So I tried guess and check method.

The proportional term deals with how far I am off of where I want to be off of the center. The differential term is for try not to oscillate so hard around center line. The integral term is like we are consistently pulling to the left or to the right like if the wheels a little bit out of alignment.

 - Update P until I get steady oscillation.
 - Update the D gain until the oscillation goes away.
 - Repeat steps I and II until increasing the D gain does not stop the oscillations.
 - Set P and D to the last stable values.
 - Increase the I term to get a more descent drive.

To run the code kp = -0.2, ki = -0.0001,kd = -1
./pid -0.2 -0.0001 -1
