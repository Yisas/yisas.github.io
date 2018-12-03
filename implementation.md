# Summary

The simulation uses the forward Euler method. In this method, a simulation is started with a given set of initial conditions, 
and then proceeds forward through fixed time step intervals where it must approximate its state after the next time step has 
passed, using all of the known conditions of the previous one. Since this is a rigid body dynamics problem, the initial conditions 
are the position, linear and angular velocity of the ball. Every time step the forces are computed, then applied to the rigid body 
using Newton's laws to calculate these modified conditions in its forwards state. The Magnus force is calculated as Fm = S (w x v), 
where:

* w is the angular velocity of the ball.
* v is the linear velocity of the ball.
* S is the air resistance coefficient. The program uses an empirically calculated coefficient by default, though you may edit it 
through the GUI.

# Step-by-step approach

In regard to the implementation of our simulation, our first task was to create a base OpenGL application. It needed to create a window 
and render a simple scene with a ground plane and a ball. We decided to the use a project called [Glitter](./acknowledgements) as the starting point, 
as it is a simple OpenGL boilerplate which provides a CMakeList which statically links all the required dependencies, namely 
[GLAD, GLFW, GLM, assimp and stb](./acknowledgements). Having statically linked library was important for us as we wanted to make sure that the application 
could be run on both Windows and Linux. For the base application, a lot of the code base was derived from LearnOpenGL tutorials, namely for model loading 
and shaders. Since it is important to have a good perception of the position of the ball in the 3D scene, we rendered the scene using Phong lighting and 
a simple two-pass shadow mapping algorithm.

Next, we had to implement rigid body physics simulation to the ball. We decided to use the explicit Euler for time integration. While it is not the most accurate time integration approach, it is easy and straightforward to implement. Furthermore, we concluded that since our application can be run in real time with small time steps, the drift would be kept minimal. Explicit Euler is also known to be unstable, but for our simple scene consisting of only one moving object, we figured it would not be an issue. We also added simple collision detection with the ground plane which makes the ball bounce. Note that the bounces are just for show and are not physically accurate, as that was not the aim of the project.

Having implemented the rigid body physics simulation using the aforementioned approach, we noticed two significant issues with it. First, the rotation matrices introduced a slight drift which slowly but surely deformed the ball. That deformation became very significant at higher angular velocities. We searched for alternatives and found out that it was possible to do the same with quaternions, which do not induce such issues. Making the change was trivial and the simulation behaved perfectly at any angular velocity afterward. Secondly, we realized that our simulation was not deterministic. With the time step being tied to the time delta between the rendered frames, we noticed that running the application multiple times yielded different results, depending on the current frame rate. Since we needed to find the best drag coefficient for the Magnus force on the ball, we had to ensure that the simulation was deterministic and that the results produced were identical each time. We therefore decoupled the time step and the frame rate. Giving the simulation a fixed time step and allowing the application to perform multiple time integrations per frame solved the issue. Furthermore, that procedure yielded a previously unconsidered side benefit in that we could now control the accuracy of the simulation by decreasing the time step as necessary.

Now, with the rigid body physics animation in place, introducing the Magnus force was only a matter of adding an extra force to the ball at every time integration, using a simple cross product between the angular velocity and the linear velocity of the ball at that time. Of course, the results were inaccurate as the proper Magnus force coefficient had yet to be determined.

To improve the convenience of the application, we next needed to implement a graphical user interface, which would let us change the simulation parameters on the fly without having to make changes to the code and recompile. For this purpose, we discovered and decided to use a library called NanoGUI which, as the name implies, allows for the creation of minimalist GUIs in OpenGL applications. To further improve visual clarity of the simulation, we also introduced the ability to draw the initial linear and angular velocity vectors in the scene. We also added the option to trace the trajectory of the ball and to keep the previous one to be able to visually tell the difference between two subsequent simulations. This allowed us to easily visualize the difference caused by applying the Magnus force to the ball.

