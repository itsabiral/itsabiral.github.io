---
layout: post
title: making a game in a weekend
tldr: tl;dr a space rover game for ludum dare game jam 59
---
#### ludum dare?
[`ludum dare game jam`](https://ldjam.com) is a 72 hour game jam where you create a game based on an announced theme. for all the non game devs, game jam is basically a hackathon but for games.. it's been almost five years since i worked on a game. this year's game jam theme was **signal**..

#### game idea?
i started a day late, so i had to find an idea asap. a few weeks ago i watched *project hail mary* and had a space themed game in mind, so quickly began to scratch down an idea for the game on an online whiteboard.<br>
after a few trials, i decided to work on something that doesn't end, something like a **procedural generation game**.
the game idea would be that the player acts as a computer on earth which sends commands (signals) to the rover to move through the platforms or the area without going off road.. we'll tweak a few things later on when we design the game

##### game design, isometric style puzzle platformer
i'm a big fan of top down isometric style games ever since the classics like __*age of empires and commandos*__.<br>
isometric basically uses a 3/4 perspective to display a 3D appearing world on a 2D screen, meaning it looks like a 3D world but it's a 2D view from a top down perspective.<br>

now we need a design tool to create game arts like the ui, the platforms and a player (rover) in isometric form for this a **FOSS tool named krita** was the best free option for me. while getting familiar with the new design tool, i found that we can use the isometric (Legacy) grid type with 30 degree angles on the left and right with custom cell spacing to create a visual layout to draw our game objects in an isometric view.<br><br>
![krita grid]({{ "/assets/images/ldjam59/krita-grid.png" | relative_url }}){: width="340"}
![isometric]({{ "/assets/images/ldjam59/krita-isometric.png" | relative_url }}){: width="920"}

##### mvp on unity and c#
i added an empty test isometric cube sprite that acts as the player and other small cubes to act as a list of platforms for now, until i design them once the mvp is ready, then created a platformManager script which has a list of gameobjects that is manually assigned as platforms.. i used a simple rigidbody position to the targetPosition (next platform) with a serialized moveSpeed to move the player..
```csharp
Vector2 direction = (Vector2)targetPoint.position - rb.position;

if (direction.magnitude > 0.1f)
{
    rb.linearVelocity = direction.normalized * moveSpeed;
}
else
{
    rb.linearVelocity = Vector2.zero;
    rb.position = targetPoint.position;
    isMoving = false;
}
```

##### generating platforms
as we talked earlier about it being a procedural generation type game that always generates platforms, i quickly set up a generatePlatform script attached to the platformManager. this script generates platforms on the go using some basic probability and also manages the difficulty of gameplay over time. the generation starts from numberOfPlatforms variable, which is set to five in the serialized field. once the player reaches the end of the generated platforms (fifth one in the first play), it counts as a point and generates another batch of platforms in random direction according to the %..
```csharp
// t calculates the difficulty curve of the game. 0 is start 1 is max difficulty
float t = Mathf.InverseLerp(numberOfPlatforms, 14f, currentGenerationCount);

float probRight   = Mathf.Lerp(0.40f, 0.25f, t);
float probUp   = Mathf.Lerp(0.30f, 0.25f, t); 
float probDown = Mathf.Lerp(0.15f, 0.25f, t);
float probLeft = Mathf.Lerp(0.15f, 0.25f, t);

// in early game when t=0 where the probability of getting Right=40%  Up=30%  Down=15%  Left=15% .. this is biased Right at first
// but in late game when there are around 14 platforms (t=1):  Right=25%  Up=25%  Down=25%  Left=25% , now its fully random with equal percentage..
```
this means by the time it's at the 14th platform the difficulty level will be at its peak, its bit early because in a game jam other players have limited time so i didn't want to bore them.

##### Building the main guy and designing the platform..
for the rover's game art, i made a truck like design part by part and added a solar panel to make it look like a rover. since it's an isometric game we had to create two sides of the rover and use **Quaternion.Euler** to rotate the player by 180 on the y-axis to flip the player for the other two sides... also created an isometric platform with some real life textures..<br>

![rover side view]({{ "/assets/images/ldjam59/rover-side.gif" | relative_url }}){: width="580"}
![rover side view]({{ "/assets/images/ldjam59/rover-back.gif" | relative_url }}){: width="580"}
<br>
_**after flipping the same art in y-axis by 180f**_<br>
![rover side view]({{ "/assets/images/ldjam59/rover-side.gif" | relative_url }}){: width="580" style="transform: scaleX(-1);"}
![rover side view]({{ "/assets/images/ldjam59/rover-back.gif" | relative_url }}){: width="580" style="transform: scaleX(-1);"}
<br>
<br>
![platform]({{ "/assets/images/ldjam59/platform.png" | relative_url }}){: width="320" style="display:block; margin: auto;"}
<br>

##### issues..
the platform was generating well but the main issue was overlapping platforms.. like i wanted the platform to always grow from the initial point and not overlap or go back, which would cause issues with overlapping platforms. it was solved by simply adding a 2D collider at the platform's top and added some conditions in the platformManager script to first follow the probability rule we talked about earlier and scan for overlapping colliders.. and if there is more than one overlapping collider then choose another location or point for spawning the platform.. this solved the issue and we were good to go..

##### finishing UI, sound effects, music..
then i quickly designed a monitor with arrows to make a space console for the ui. a good game needs good music. so i quickly began to search for a car crash sound, car move sound, coin collect sound.. pixabay.com had a great collection of real life sound effects. cropped the sounds, changed the pitch and voila the sounds were ready.. then used a no copyright music track from a guy named <a href="https://www.youtube.com/@dariodurbe">Dario Durbe</a>.
<br>
also added some particle effects like the car wheel mud thing, clouds for atmosphere and few designs here and there..

##### limitations and improvements needed..
we had a time limit so adding other effects or making the game non repetitive was actually a challenge for me.. a lot of things didn't go by plan like adding rocks as a destructible thing. but it was a good game jam experience and hopefully will participate in the october one.. i am open to collabs for the next one.<br><br>
the game is available on itch.io at <a href="https://itsabiral.itch.io/rov-r">https://itsabiral.itch.io/rov-r</a><br><br>
<img src="/assets/images/ldjam59/gameplay.gif" alt="Gameplay" loading="lazy" width="1084" style="margin:auto; display:block;">
