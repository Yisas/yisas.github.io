---
title: "The Plight of Knights and Sight"
layout: posts
permalink: /plight/
author_profile: true 
github: "https://github.com/yisas/ubisoftGameLab2018"
download: "https://github.com/Yisas/UbisoftGameLab2018/releases/download/untagged-6aeb52f3482e4392eccd/A.Plight.of.Knights.and.Sight.rar"
---
### Technology Requirements

2 Xbox controllers and a LAN connection of 2 players is required.

### Summary

This was my team's submission for the [2018 Ubisoft Game Lab competition](https://montreal.ubisoft.com/en/ubisoft-game-lab-competition-2018-winners/), where university level contestants 
are placed into groups of 8 developers and challenged to create a video game prototype within 10 weeks. It received nominations in the best game design, best user experience and best 
overall prototype categories. This year's theme was "Change the world" (in a social context) and the technical mandate required the game to be executed in 3D and have a networked 
multiplayer experience.

The Plight of Knights and Sight is a storybook tale of a family reminiscing on the joy of playing together. Imagining themselves as Knights, Grampa and Grandma solve the puzzles 
of the dungeon, describing its perils to their grandchild. However, they both remember the story a bit differently, leading to each player seeing different versions of the dungeon.

As a collaborative game, every room requires both players to communicate with each other to reveal the path through the many obstacles. Paying attention to each other is key, as
players will soon realize that what is visible to one is not necessarily so for the other. Thus, it is only through communication and collaboration that the family will open the doors.

### Global Game Jam

After [experiencing the disadvantages](/genesis/#postmortem) of not being able to prototype your ideas to see if they work, I talked my team into using the global game jam as a rapid 
prototyping opportunity. We couldn't be sure of whether the concept of using visibility as the main challenge of the game would be as fun as we intended, and even if it was, the level 
design would then be crucial to its success, which meant that it was important to get a prototype ready for the designers to mess with. It was agreed to take advantage of [our university's 
global game jam](https://globalgamejam.org/2018/jam-sites/tag-concordia-university/games), since it would have a ton of willing playtesters that would help us see if we were on to something. 
We ignored the GGJ mandate completely and pretended like it was the game lab's. We presented [Dungeon of the Mind](https://globalgamejam.org/2018/games/dungeon-mind) 
[(github link)](https://github.com/yisas/ggj2018), which left us hopeful since it received some good feedback. But most importantly, our designers could take this feedback from the 
playtesters on-site and began iterating using the already built game. This proved invaluable for the end product, and in my opinion was a big reason why we received praise in the game design 
and user experience categories, since it allowed us to leverage our game designer talents in full.

### Networking "woes" & tunnel vision

I had taken point on the implementation of the third person character controller and mechanics for the [first prototype](https://github.com/yisas/ggj2018), but now that that was done, I began 
transitioning what was already there to a networked 2-player game as opposed to a dual screen one, while my teammates worked on new mechanics. It was mostly painless except for one thing: 
players being able to carry objects. These throwable objects were an important part of the game; they allowed players to lock down pressure plates and mark parts of the world that the other 
player couldn't see. Thus, they had to be a networked physics component. Or well, that's what I thought at first.

In the non-networked prototype each crate was a simple textured primitive with a rigidbody, and when it came time to carry it, it was connected to the player through one of Unity's 
joint objects. This not only produced the desired effect of moving with the player, it also allowed for the built-in physics engine to detect if force/torque between the carried object and the player 
was large enough for the joint to "break". If for example a scenario occurred where the player was hanging from a ledge using only the crate, the joint would break and the player would 
drop the object, no code required. Just a small step above the trivial approach of simply childing it to the player. When it came time to move to a networked game, the competing physics-enabled 
objects generated undesired artifacts, like stuttering or dragging, which could get pretty bad when latency was low.

{% include figure image_path="/assets/gifs/plight/crate-carry.gif" caption="Am I carrying that crate, or is it chasing me? This is much more noticeable on a fullscreen game." %}

The problem is that for some reason, I tried to make the joints work. I messed with the interpolation values, then wrote some code to detect and eliminate "noise" stutter translations. It was 
a bit of tunnel vision that lasted longer than I would like to admit. Childing a networked component to another was creating its own problems, but I eventually regained my sanity and resorted to the old 
"rubber ducky" method to ask myself what was the point of carrying this object through physics. So, I went for the safe route that could never cause problems: turn on a non-synced object with no physics 
attached to it that was just the mesh and the texture. It was obvious, but I guess I was low on coffee or something. It ultimately helped me improve at not falling into the trap of following the inertia 
of an idea that doesn't work anymore in the given context.

{% include figure image_path="/assets/gifs/plight/fake-objects.gif" caption='<a href="https://www.youtube.com/watch?v=7qKcJF4fOPs">Senator Vreenak would aprove</a>' %}

My favorite part about the above is that it wouldn't lead to any unexpected surprises with the synced UNET components since I had just reduced the synced components during the carry state to 
just the player. I then made it so that the object that was being picked up was destroyed as the fake object was turned on, and when the object was supposed to be thrown, a new, synced, physics enabled 
object was instantiated and thrown from the desired position. Except, well, surprise:

{% include figure image_path="/assets/gifs/plight/object-pop-in.gif" caption="Blinking vase? Yuck." %}

So yeah, as soon as latency got bad the spawning of the object was very noticeable. I wanted to make sure this was all spotless since I had no idea what the connection on the demo site was going to be like, 
especially with a bunch of other games on the same LAN. But that's ok, nothing a little object pooling won't fix.

{% include figure image_path="/assets/gifs/plight/object-pooling.gif" caption="Don't look up! Except you can't, but if you could, you'd notice the pop-in of the pooled vases (top right side)." %}

### Obligatory bloopers

It's not a bug, it's a whole new game!
{% include video id="lKKqjMYPoRQ" provider="youtube" %}
{% include video id="b51nyd0PPJA" provider="youtube" %}