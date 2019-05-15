Ryan Yuzuki, Brandon Tran, Andrew Loera

Section 021

# cs135 Sonic Blue Sphere VR - Final Report

## Abstract

Our project focuses on revisualizing a classic Sonic 3 & Knuckles 2D mini-game in VR. We focused on making the player feel as though they are in Sonic’s shoes but doing so in a way that does not cause the user to experience much vection. It is a unique experience because it allows the use of automatic movement that does not disorient the user too much while also having a simple game concept that is easy to grasp. By giving the player more freedom in controlling their movement as opposed to the original game and reducing the movement speed to a reasonable amount, we successfully minimized vection that would have otherwise more disoriented players of our game.

## Introduction

Our project “Sonic Blue Sphere VR” is a reimagination of the game mode Blue Sphere in Sonic 3 & Knuckles, originally released in 1994.  In this minigame you control Sonic as he collects blue spheres and avoids red spheres. Levels are judged on both the amount of spheres hit and number of rings collected. By having these elements, the game provides a layer of depth between speed and completion. This project is interesting because the original game was one of the earliest adopters of the 3D genre; most other games at this time were side-scrolling RPGs e.g. Mega Man X and Donkey Kong Country. By “VR-ing” the original minigame, we hope to remaster and improve the core game experience while bringing it to a modern audience.

The addition of VR makes this experience more interesting by putting the player in the world, in place of Sonic. No longer are we watching and controlling from above in third-person - instead we take the place of Sonic and become immersed in an interactive world. This also adds a layer of complexity on top of the original game - it is more difficult to see one’s surroundings in a first-person view. In the original game, the player has a higher vantage point to see where they need to go and what they need to do, but in our reimagination it is more difficult to do so. This is an unintended side effect of bringing the game to a first-person perspective but we believe it is still a playable experience. Should we have more time and Unity know-how, we could possibly implement a mini-map that would show the player a view from the top. All in all, we consider this a faithful recreation and are proud to present this as our final project.


## Related Works

As vection is thoroughly researched in the area of virtual reality, there have been plenty of works that involve automatic movement, a main component of our project and the original Sonic 3 & Knuckles minigame. Such works include Minecraft VR and Lucky’s Tale.

Minecraft VR is virtually the same as the original Minecraft in terms of gameplay, with slight differences coming from experiencing the game in virtual reality. As with the original game, Minecraft VR has the player control an avatar in the first-person point of view. Since the point of view is identical to that in the original game, players will have an easy time jumping right into the virtual experience. However, it is noted that Minecraft (both the original and VR versions) requires vast amounts of movement through a virtual world, which may cause disorientation in the long term. According to Newegg, virtual heights of structures in the game can cause vertigo even though the world is constructed out of pixelated blocks. To counteract that, Minecraft VR has a shortcut that takes the player out of the virtual world and they can instead play on a virtual TV in a simulated living room. While we allow our users to control the starting and stopping of their movements to reduce the effects of vection, Minecraft VR cleverly has this method to allow players to ease out and back into the VR experience in cases of discomfort.

Lucky’s Tale is a 3D platforming game and is an example of Fish Tank VR, a subset of games that are not meant to be immersive. In the game, the player views and controls a cartoon character in the third person. As a result, while the game is considered more intense than other VR games, there is little chance of becoming motion sick because the player is not the character that is moving. This game follows the general VR guideline of using an in-game avatar as opposed to a first-person point of view to minimize the effects of vection. While we lacked the time to implement a third-person game like Lucky’s Tale, we were able to keep discomfort to a minimum using other methods.

## Design

In figure 1, the left image is the original implementation of the map and on the right is our recreation. We had to take some creative liberties in our version due to creating a larger map initially. As you can see, we have an extra block of blue spheres on the top and bottom to take up the extra space. In addition, we have a longer “maze” part on the left and right sides to offset the larger map size.

Figure 1             |  Figure 1
:-------------------------:|:-------------------------:
![](https://raw.githubusercontent.com/ryuzu001/cs135/master/real-level-layout.PNG)  |  ![](https://raw.githubusercontent.com/ryuzu001/cs135/master/level-layout.png)

The in-game playing screen is shown below in figure 2. Here we attempted to recreate the game from Sonic’s perspective. Instead of seeing the game from above, we show the spheres through the VR headset in place. In addition, we did not have enough time to place the score on the side of the screen (and according to lecture, that is a good thing). One thing that we did not implement are the rings that appear. Instead, we took a more simple approach in only counting down the number of spheres present on the stage. In this way, we avoided confusing the player with two counts and simplified the remaining count enough to display on the transparent walls. 

Figure 2             |  Figure 2
:-------------------------:|:-------------------------:
![](https://raw.githubusercontent.com/ryuzu001/cs135/master/real-game-perspective.PNG) | ![](https://raw.githubusercontent.com/ryuzu001/cs135/master/player%20start%20perspective.png) 

We chose this particular user interface because it made sense in the scope of the class; embedding information in the world space would make the experience less disorienting than if that information was fixed to the user’s point of view. The Oculus controllers were used to control starting and stopping in the virtual world and to control direction. We modified the “turn” via the right-controller’s joystick to instantly rotate the player 90 degrees. This is due to the original game only allowing 90° turns. Because Sonic is constantly running in the main game, we chose to add this action to the player controller as well.

We made the decision to have automated movement of the player to stay as close to the source material as possible. We understood that it could cause the user to experience large amounts of vection. To counteract that, we allow the player to be in control of their movement by pressing the A button on the Oculus right-controller to start moving and pressing the B button to stop moving. The speed was adjusted so that it is not too fast for the player but not too slow that the game is unplayable.

In addition, our design follows many of the Oculus Best Practices guidelines. Our project easily reaches the rendering, latency, and optimization guides which allow for a smooth experience for the user. The project uses a lot of head and positional tracking and it does so at a high performance level so that the user’s movements are not ahead of what they are seeing. Additionally, the user interface is not attached to the player and instead is attached to the world so that the player does not become uncomfortable looking at their score.

Next, there are some guidelines that we did not follow but did our best to reduce the negative effects. Acceleration was one thing that we added to our design that does not conform to the guidelines but we made the acceleration slow and controllable by the player. Another guideline that we did not follow states that the player should have an avatar to control; we did not have the time to add it in but tried to make the experience comfortable without one.

Overall, our design works best when the user is standing and using the Oculus controller to move and rotate in the virtual world. It also works well when the user uses a combination of head tracking and the controller to position themselves and direct their movement. The design is best experienced at high frame-rate so that the user is not out of touch with the movement that they see.

## Implementation

Our implementation of Sonic Blue Sphere VR is split into objects and their scripts for the player and for the world. For the player, we used Oculus’s standard utility files to generate a controller for the player. This controller takes care of the head and positional tracking and acceleration for our game. We modified its position update functions to create toggled automatic movement.

The “world” of our game consists of spheres, score displays, and a game-over scene. Red, blue and silver spheres dot the landscape. Passing through blue spheres is the objective of the game, and only after passing through them will they turn red and therefore act the same as the already-present red spheres. That being said, red spheres are to be avoided as simply colliding with one will result in a game over, at which point the player is sent to a black room with “Game Over” printed on a wall. After five seconds the game will terminate itself. Silver spheres are solid and act as walls - the player cannot walk through them.

In following the Oculus Best Practices guidelines, we embedded the score displays in the world itself. As opposed to being fixed to the user’s view, there is instead a score display on each of the four sides of the world space that takes the form of a square plane.
        
## Lessons Learned

Throughout the building process of this project, the three of us learned many things along the way. We each learned a lot about Unity and how to use its many functions since each of us had never used Unity beforehand. We also learned that level design is an important part about making a project such as this. We learned that making the level challenging but not too challenging can make for a good player experience so that the user is not too confused or lost.

While building this project we came across many obstacles and learned how to overcome them. We saw that propelling the user forward at a high acceleration is not the best way to simulate Sonic’s speed from the original game. To overcome this we were conservative with how much speed at which the player was able to move. This may not have achieved the exact “Sonic” feeling that we wanted but it was what we needed to do to create a better user experience. We also ran into some issues with how to allow the player to move throughout the level. We were unsure whether to tie the movement directly to the Oculus controllers or use head tracking to determine the direction of movement. We solved this by implementing both ways so that the user may use whichever control scheme feels most natural to them.

After we demoed our project we received good feedback. The professor said that our project was interesting because we were able to implement the movement close to the original but in a way that is not too out of control for the users. Also, our section TA said that our project was simple and implemented well for VR. Another student said that the experience was good and that the game concept easy to understand. Based on this feedback, we would improve on the other aspects of the game such as creating different levels and finding a way to possibly have the user move faster but without increasing the vection that they could feel.

Overall, throughout this project we shared the work equally by having all three of us there during development of the level and coding of the mechanics. We made sure that we all knew what was going on and what was added to the project as time went on. Together we were able to smoothly produce our project and are happy with the outcome and reception that is received.
