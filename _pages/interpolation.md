---
title: "Keyframe Animation & Interpolation Methods"
layout: posts
permalink: /keyframe-interpolation/
author_profile: true 
download: "https://github.com/Yisas/COMP477-Key-Frame-Animation/releases/download/1.0/Keyframe.Interpolation.zip"
github: "https://github.com/Yisas/COMP477-Key-Frame-Animation"
---
This is an assignment for the Animation for Computer Games course. It is a OpenGL implementation of 4 keyframe interpolation modes: linear interpolation of rotation matrices, linear interpolation of euler angles, 
liner interpolation of quaternions and spherical interpolation of quaternions.

You can use this demo to appreciate the velocity spikes that euler and matrix modes can produce, as well as the artifacts that quaternion LERP can present (notice the right arm of the gif macarena dance and the 
legs of the breakdance). The best option is the SLERP, which not only produces a constant interpolation velocity with a satisfying curve, but also yields the shortest interpolation path of the methods presented.

{% include figure image_path="/assets/gifs/keyframe-interpolation/macarena.gif" caption="Macarena" %}

{% include figure image_path="/assets/gifs/keyframe-interpolation/breakdance.gif" caption="Breakdance" %}

## Controls

You can make your own animations by clicking and dragging the model joints. Once the desired keyframe posed is loaded, you can press "t" to store the keyframe. You can use "+" or "-" to toggle between the saved 
frames, and insert new frames in-between existing ones. Once you have saved all the desired keyframes, switch from "editing" to "play" mode by pressing "m". "p" will begin playing the animation, and the numbered 
keys 1-4 will switch between the matrix, euler, quaterinion LERP and SLERP interpolation modes, respectively. Hold the "j" and "k" keys to decrease or increase the animation speed.

{% include figure image_path="/assets/gifs/keyframe-interpolation/demo.gif" %}
