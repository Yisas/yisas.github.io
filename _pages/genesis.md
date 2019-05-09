---
title: "Genesis: Sands of Rebirth"
layout: posts
permalink: /genesis/
author_profile: true 
download: "https://github.com/Yisas/UbisoftGameLab2016/releases/download/untagged-e75f9e90c2caad48efed/Genesis.zip"
github: "https://github.com/yisas/ubisoftGameLab2016"
---
### Technology Requirements

1 Xbox controller is required.

### Summary

This was my team's submission for the [2016 Ubisoft Game Lab competition](https://montreal.ubisoft.com/en/ubisoft-game-lab-competition-2016/), where university level contestants 
are placed into groups of 8 developers and challenged to create a video game prototype within 10 weeks. This year's theme was "Ocean", and the technical mandate included requiremets 
like the game be executed in 3D, have at least two game systems that interact with each other, present three game mechanics that may interact with the systems, among others.

Genesis is an exploration game where the player (Damu) must revitalize a barren ocean bed by controlling the vegetation around him and directing it towards a "regeneration flower" objective, 
while fending off AI fauna that wants to consume any vegetation in sight.

The player can control the elements, allowing them to terraform the terrain to reach other areas, as well as fend off the animals that try to consume the limited and much needed vegetation. 
They can also manipulate the wind to perform a basic attack.

{% include video id="-DSK2mk6QYQ" provider="youtube" %}
## Before joining this project
This was the first video game project I ever participated in. Before this, I was interested in game dev but not sure if I should pursue it as a college specialization. After receiving a school email 
advertising the competition, I thought it was the perfect oportunity to get a small taste of what game development might be like. However, each school gets a limited number of spots, 
so I had to apply despite being very early in my program, which meant I hadn't taken any game development courses yet. That led me to look at some Unity3D tutorials in my spare time, and 
some 5 hours later I made [this monstrosity](https://users.encs.concordia.ca/~j_imery) you can barely call a video game. The point was to show some initiative, which I guess worked since I 
was selected for one of the Concordia teams.

## About my contributions to this project

### Song name? Sandstorm

After the first week of brainstorming and delibarating over what the game would be, I volunteered to tackle one of the systems we wanted to implement: a simulation of natural sand movement in a desert. 
Initially the game was much more puzzle oriented, and we had this very misguided idea that procedurally shifting terrain was going to play into the challenges. It was the typical error rookies make of 
having overscoped features that sound cool, without a good enough plan of how they would contribute to the fun of the game to make it worth the effort. 

I moved on to some exploratory work, where I looked at a few papers on mathematical simulations of dune migration. Some of them were good enough to work on, but at one point I landed on one about sand 
ripples waves that was accompanied by some sample MATLAB code. I then made some small edits using values from another paper where it had some estimations of horizontal-to-vertical translation ratios of individual 
particles. It was much less impressive than it sounds, though I still wish I had kept the reference or the code, but those got lost in one of the school lab wipes after the competition, before I had the foresight that 
I might write a blog like this someday. What remains is some videos I showed my teammates of the work in progress, though these have a flaw where particles leaving one end of the screen were re-entering on 
the other side, leading to pretty big "peaks" being formed after a while. I remember making a quick hack imposing a maximum height for the individual particles before they where forced to realocate in the 
direction of the simulated wind, which made it look better than the videos below, though still far from perfect.

{% include video id="Ts-etzZ5lho" provider="youtube" %}
{% include video id="P9J2-mKzyhE" provider="youtube" %}

It was at this point that we had our first mentor meeting with the Ubisoft employees that were assigned 4 hours a month to give us some advice. They took one look at our idea, and said: "cool, but... how is this 
going to make your game fun? Why are you doing this again?" Our answers were of course unsatisfactory, and they made us see that not only was this a big challenge for a bunch of students on a full-time courseload
who haven't made a prototype of this size before, but the payoff for it just wasn't there. Making procedurally generated content work in a way that's entretaining for the player takes a lot of fine tuning, and the 
environmental puzzles this system was supposed to interact with hadn't been designed yet, so it was all very etheral at this point. The feature was dropped, and wisely so.

### Digging

In order to acheive this mechanic the terrain mesh was modified at run time. The shape of the digging was determined using 3D mathematically well-defined shapes, most importantly an ellipsoid and a parabolliod, though 
others were tried. The points of a preset square area around where the player was digging would be scrubbed through, with points being excluded depending on the mathematical shape that was desired. For example, for an 
ellipsoid of horizontal dimensions (a,b), any point (x,y) within a rectalngular $$a\times b$$ area using the center of where the player is aiming at as the origin of this local cartesian system, if
$$\frac{x^{2}}{a^{2}}+\frac{z^{2}}{b^{2}}<1$$, that point would be outside of the 2D projection of an ellipse on the terrain, meaning these points would not be modified. For the remaining points, the elevation is 
determined as $$y(x,z)=\sqrt{(1-(\frac{x^{2}}{a^{2}})-(\frac{z^{2}}{b^{2}}))}*c$$, where c is effectively determining magnitude of a single elevation frame step.

![Dig shapes](/assets/gifs/genesis/dig-shapes.gif)

The ellipsoid shape sprouted the idea of having the player erect dune walls, which we hadn't considered during brainstorming. But ultimately the environmental puzzles that would use the mechanic were not included, and 
so for simplicity's sake, the player was restricted to raising parabolic mounds.

![Parabolic Mounds](/assets/gifs/genesis/dig-ingame.gif)

<a name="postmortem">
### Postmortem
<a>

Our team made a ton of mistakes on this project, some of which I've outlined above, but the one that I learned the most from became aparent towards the very end of development. Each member had spent time 
individually working on tasks they were assigned to, and concerned themselves with polishing them as much as they could. However, despite most mechanics being playable in some capacity midway through the 10 week 
time frame, there wasn't a real drive to put all of these together to see what the end result was. This step happened way too late, and once it was done we could see how many design assumptions didn't come together. But 
most egregiously, the game just wasn't all that fun. We had new insight on what was working at what wasn't, and not enough time to act upon it. We also got a crash course on the kind of tunnel vision you can experience if 
you're not careful, particularly with your team reinforcing what you think you know about what is fun about your game. Heck, we somehow made it so that most of the gameplay loop was literally watching grass grow, and 
nobody noticed until we played it in full. This made me a big believer in the importance of rapid prototyping, which I would proselytize as much as possible in further group video game projects, always to great results.

{% include figure image_path="/assets/gifs/genesis/beehive.gif" caption="Our AI enemies spawned from these \"beehives\" they used as shelter. It's not their turds, I swear." %}

![Credits](/assets/images/genesis/credits.png "Credits")