---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

# Introduction

This project was developed for the "COMP477 - Animation for Computer Games" course at Concordia University.
It is a simulation of the Magnus Effect, which is the force exerted on rapidly spinning spheres moving through air.
This physical phenomenon is most recognizable in common culture when observing the curved paths that skilled players
can apply to golf, soccer and baseballs. This project intends to bring a visualization of the Magnus force, and allow
the users to tweak the parameters of the simulation, in order to further undestand the conditions that affect this phenomena.
We have also aimed to provide a comparative evaluation between the common theoretical equations used to describe this
force and a real life example, by recording the magnus effect in action and comparing the results to the simulation.

* * *

# What is the Magnus Effect?

When a ball is spinning within a fluid, most commonly air, one side of the ball drags the fluid in the direction of
its rotation, while the other side of the ball is pushed by the air being dragged towards it. This result in a
sideways force that is proportional to the angular and linear velocity of the ball, given that its cause is an angular
deflection of air flow. The following video provides an improved visualization of the above:

<video controls width="690" height="315">
	<source src="{{site.baseurl}}assets/video/magnus-effect-explanation.webm" type="video/webm">
</video>

_[Source](https://youtu.be/2OSrvzNW9FE)_

* * *

# [How to use the simulation?](./howTo)

Download either the compressed binary files for either [Windows]({{ site.baseurl}}/assets/binary/Magnus_Effect.zip) or 
[Linux]({{ site.baseurl}}/assets/binary/Magnus_Effect.tar), unzip the files, then run the "MagnusEffect" executable. 
The controls will be displayed in the GUI right away. 

* * *

# [How does the simulation work?](./implementation)

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

Further anecdotal description of the approach to the challenges of the implementation can be found [here](./implementation).

* * *

# [Simulation vs Reality](./comparison)

In order to verify the accuracy of our simulation and compare its results with a real life model, live recordings of a ping pong ball 
using various forms of backspin were taken. The initial conditions of said recordings were then simulated, and statistical analysis 
was conducted between both data sets to provide an estimation of the accuracy of the simulation. This allowed us to empirically produce
a drag coefficient for our model.

<video controls width="690" height="315">
	<source src="{{site.baseurl}}assets/video/comparison.webm" type="video/webm">
</video>

You can learn more [here](./comparison).

* * *

# Demo

<video controls width="690" height="315">
	<source src="{{site.baseurl}}assets/video/demo.webm" type="video/webm">
</video>

* * *

# Developed by

* [Brandon Baran-Goldwax](https://github.com/BGoldwax)
* [Jesus Imery](https://github.com/Yisas)
* [Mathew Knappe](https://github.com/MatKnappe)
* [Samuel Proulx](https://github.com/proulxsamuel)