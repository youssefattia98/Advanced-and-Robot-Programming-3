# arp_supergroup

## Contributors

|  Group name   |   Students                                                                     |
| ------------- | ------------------------------------------------------------------------------ |
| master        | Zhouyang Hong, Gesualdo Sinatra                                                |
| drone_bm3     | Bauyrzhan Zhakanov, Madi Nurmanov                                              |
| drone_awais   | Awais Tahir                                                                    |
| drone_yh11    | Ali Yousefi, Mohammad Reza Haji Hosseini                                       |
| drone_ja1     | Jabrail Chumakov, Ayan Mazhitov                                                |
| drone_ha1     | Alice Maria Catalano, Hussein Ahmed Fouad Hassan, Youssef Mohsen Mahmoud Attia |

Description
-----------
Third assignment of the course “Advanced robot programming”. We were asked to code a program which allows the user to control the motion of several drones avoiding collisions and visualizing them printed on the screen. 
The master is opened when the “./run” command is executed. The master is the server which will hosts the drones (clients) also in running time using sockets. The drones will connect and they start sending positions, the positions are confirmed after taking care that the direction is actually free by the server.

Run and installation
--------------------
To install and run the following code go to our dear collegue:
```
git clone https://github.com/BZWayne/arp_supergroup.git
```
Be sure to make all the make all the file executables by terminal with the following command:
```
chmod +x *
```
Then run the installation shell file.
```
install.sh 
```
As last command, run the maste code with:
```
run.sh 
```
## Drone_ha1 
---
Compilation
----
If there's the necessity to execute just this drone:
```
gcc drone.c -lpthread -o drone -lm
run with: ./drone
```
World description
---
The aim of the drone is to scan the area of the given map in 2D (80,40), avoiding to scan twice the same area.
The starting point of this drone is the center of the map (40,20), the movement is casual finding a new direction in a random way. 

Communication with the master
----
The new coordinates need to be sent to the master, asking for permission to go there, to not cause collision with other drones. This communication is estabilished with a message with a common structure between all the drones, which is: [group],[x],[y],[fuel_left].
If the master does not accept the coordinates given, new coordinates will be generated, because this means another drone is already scanning the area and this drone can come back later on that.
Once the master accepted the coordinate request, the drone will move using fuel, if the fuel will not be enough to complete the route, the drone will go back to the origin of the map (0,0) and refuel.

Functions
---
* `float genno(int a)`: generates two random number inside the boundaries of the map, that will represent the new coordinates to reach.
* `generate_msg()`: function is used to send to the master (IP addr is 127.0.0.1; port: 7777) the name of the group, the coordinates, the fuel's level of the drone in this format "[group],[x],[y],[fuel_left]" in which: 
  * x is a double/float type from 0～80，
  * y is a double/float type from 0~40, 
  * fuel_left is 0~100.
The message the master expects from this drone is `a,1.222,2.333,99.00`
* `void updateXY()`: get new coordinates from `genno()` to explore the space calculating the fuel usage with this rate of decreasment `(sqrt(pow(dif_x, 2) + pow(dif_y, 2))`, in which `dif_x` and `dif_y` are the magnitude of the difference between the starting point and the arrival point's coordinates.
* `void printingscannedarea()`: calculate the area scanned by the drone in position x,y in a 2D array, and print it on the screen.

Results
---
You will get a 2D map printed time by time highlighting the parts scanned by drone.
