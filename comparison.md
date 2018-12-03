# Model-simulation analysis

## Recording

In order to verify the accuracy of our simulation and compare its results with a real life model, live recordings of a ping pong ball 
using various forms of backspin were taken. Also onsecutive pictures of the ball were taken at varying distances from to camera for the 
purposes of calibration.



## Video Tracking

These recordings were then analyzed using [Tracker](https://physlets.org/tracker/). 

Our goal was to calculate initial velocity, direction and angular velocity from the first several key frames at the start of each test, as well as measure distance traveled and peak height during the trajectory of the ball.

A few methods were considered for analyzing the data. Default media players such as VLC player and Windows Media Player(WMP) were first considered, 
however, VLC was unable to handle the large amount of frames per second and WMP was unable to progress through the video frame by frame. 
A quick alternative was to use Blender as it was able to handle the high FPS videos; however Blender quickly proved to be a very manual experience. Searching for 
alternatives lead to two programs (Logger Pro and Tracker) specifically made for tracking objects and providing data.

[Tracker](https://physlets.org/tracker/) allows adding calibrations and overlays to the video to allow for accurate measurements of all our needed data points.

![tracker screenshot](/assets/img/tracker-1.png)

Each video was analyzed as follows
1. Set measurement from a known value. This was done with measurements taken between dots.
1. Determine the frame the ping pong ball left the users hand or paddle.
3. Setting the XY origin access to the middle of the ball in the frame determined in step two (Origin).
4. Create a "point mass" object and apply it to the ping pong ball’s trajectory frame by frame from the origin (Auto-tracking can be used if there is little to no rotation).
5. Determine distance traveled by adding a "Tape Measure" from the point of contact of the ball to the ground to the Y axis
6. Determine peak height by adding a "Tape Measure" from the peak of the arc of the ball to "Tape Measure" from point 5. The tape measure from step 6 is perpendicular to the tape measure from step 5
7. Determine initial height by adding a "Tape Measure" from the origin frame to the "Tape Measure" from step 5.  The tape measure from this step is perpendicular to the tape measure from step 5
8. To Determine Initial Velocity and Direction, the data points from step 4 are graphed inside of Tracker. Selecting the table for the point mass and enable the display columns for 0v (Angle) and V (velocity). The first 3 data points for each column are averaged to obtain our initial velocity and angle.
9. To find rotations per second, take note of the time for your first frame. Proceed to go frame by frame until a clear rotation is complete (1 full rotation if possible) and mark the final time. Use this data to calculate the rotations per second.
10. Save analysis in the Tracker file format.

All experiments and tracker files can be found [here](https://drive.google.com/open?id=13s44bDiHoIOLwxcdRP3JzrFp18kntRWG).

## Statistical analysis

Once all of the data from the tracker files was collected, the same initial conditions were simulated using the program. Both the traveled 
horizontal distance and the peak height of the trajectory of the ball were compared between the simulation and reality, using 
[Mean absolute percentage deviation](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error). This allowed us to empirically produce 
a drag coefficient that minimizes the error between the 2 data sets.

<video controls width="690" height="315">
	<source src="{{site.baseurl}}assets/video/comparison.webm" type="video/webm">
</video>