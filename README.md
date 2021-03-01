# Megaman 2 in GameMaker Studio 2
This game was my second game project in my CS339 class. This class was my first time designing a game, using Game Maker Language, and using GameMaker Studio 2. The assignment was to create a game based off of the Megaman 2 game, with at least 2 rooms, 2 weapon types, 2 enemy types, and a boss. The controls for this game are the right and left keys for moving side to side, space to jump, and down key to shoot. The enter key changes the weapon mode. My game features two enemy types, the first hurts upon contact, and the second shoots at you, so the game suggests that you try stomping or jumping on top of the first enemies and shooting the second enemies. The boss shoots at you and cannot be jumped on. 
There was a lot of freedom in how the game could look, so I designed the rooms myself. The first is outdoors and looks similar to Mario and the second is underground. The sprites, or designs, of the Megaman player, the boss, the enemies, and the green Mario pipe were sprites I found online and edited to fit the game and animate moving back and forth. The powerups, rooms, and other blocks were hand drawn by me in the GameMaker sprite editor. The background for both of the rooms was done by setting the color on the background layer of the rooms to blue and black, respectively. 
Into the code of the hero, his first event is a Create event, where you can set values. In line 1-6 I set values for the Draw GUI event, and in lines 8-11 I set values for the Step event. "bossHealth" is set in the create event for the hero (player/Megaman), so that this value will appear in the Draw GUI event. The hero's lives is set to 3, the first weapon's ammo is 5, the second weapon's ammo is 10. The weapon mode is set to 1 so that the player can switch weapon modes. The values in lines 8-11 refer to values that help the player run, jump, have gravity, and a position in the room. The last three lines of the Create event, "destRoom = Room2, destX = 1916, destY = 188" show the x and y values of Room2 that the player should appear on when they go to Room2. The Step event is something that happens at every step of the game, and there are many steps in a second. The Step event for the hero gives the player gravity to jump and land, and also to keep him out of objects, this code was given to the class from my professor as a starting point, but there are comments in the code to show what it is doing. In the Draw event for the hero, I used if/else statements to give him animation. If he is moving right (0 degrees) he draws the right version of his sprite, and the same goes for left (180 degrees), and up (90 degrees) drawing the jump sprite version. Lines 8-13 of the Draw event for the hero set the animation speed, so that he doesn't animate when he isn't supposed to, and line 14 tells the object to draw itself. The Draw GUI event for the hero draws each string on the designated x and y of the players screen, and exists as long as the hero does. I used this Draw Gui to draw the amount of lives the player has remaining, the weapon ammo for both weapons, the weapon mode, and the boss health. In the Key Press - Enter event, I used an if/else statement so that when Enter is pressed the weapon mode changes; if the mode is weapon one, it changes to weapon two and vice versa. In the Key Press - Down event a projectile object is created in the "Instance" layer in the direction the hero is facing, with a speed of 10, and then I repeated the code for weapon two, changing the speed of the projectile to 12. When the hero collides with the ammo object, a Collision event is used so that the weapon's ammo is increased and the player sees a message telling them they picked up ammo. In the Collision event for the hero colliding with an enemy projectile, 1 is subtracted from the player's lives and an if/else statement is used so that when a life is lost the player recieves a message telling them, and if they are out of lives it tells them that they lost and it restarts the game, this is the same when the player collides with the enemyStomp. When the player collides with the gun object, it tells the player that they have two weapon types and how to switch between them using the built in print() function. When the player collides with the life object, a life is added to the variable "lives" and a message tells the player. When the player collides with the info object, a print() message gives instructions. When the player collides with the "pipeDoor", or the green Mario pipe, the built in function room_goto() spawns the player in the destX and destY (set in the Create event for the player) of Room2. 
The objects wall, cloud, and block, do not have any events, but pipeDoor has the same variables as the hero for destRoom, destX, destY as the hero does in it's Create event. Moving on to the enemyStomp, in it's Create event the code "s = instance_create_layer(x, y - 30, "Instances", stomp), s.parentObject = id, childObject = s" creates a stomp object slightly above the stomp, sets itself as the parent object for the stomp, creating an id that the child and parent have so they can refer to eachother. Line 4 sets it's gravity. In the stompEnemy's Destroy event, it destroys it's child object if itself is destroyed. In the stompEnemy's Step event, the code is the same as the hero object so that it has gravity and can't pass through objects, but it also has code that only lets the stompEnemy notice the hero when it is within 300 pixels, then it can begin attacking. In the stompEnemy's Draw event, the code is the virtually the same as the hero's for changing animation based on direction, except the stompEnemy does not have a jump animation. If the enemyStomp collides with a projectile, the built in function instance_destroy() makes the enemyStomp destroy itself.
In the projectile object's events, it will destroy itself using instance_destroy() if it collides with anything, so that the bullet doesnt pass through anything. The same goes for the projectile2 object and the enemyProjectile object. The info, life, gun, and ammo objects will also destroy themselves after the hero(player) has collided with them. In the stomp object's Step event, the stomp's x and y are set to be whatever the parentObject's x and y are, with 15 subtracted from the y so that it sits above it's parentObject. 
The next enemy type is the "shootEnemy". In the shootEnemy's create event the following variables are set: shootInterval = 100, shootTimer = shootInterval, shootEnemyLives = 2. These variables are used in the shootEnemy's step event, so that the shootEnemy shoots every 100 steps and it has two lives. The shootEnemy has the same gravity setting code as the hero and the enemyStomp inside the Step event, but it also has code like the enemyStomp so that it doesn't notice the player until they are within 300 pixels. Using an if statement, once the player enters 300 pixels, the shootTimer can start counting down and the shootEnemy can create a projectile in the "Instance" layer just like the hero can, in the direction the shootEnemy is pointing and at a speed of 10. The code for the shootEnemy's animation in the Draw event is the same as that of the enemyStomp's Draw event. If the shootEnemy collides with the projectile object, shootEnemy's lives subtracts 1 and if it has less than one life, instance_destroy() is used and the shootEnemy is destroyed. If the shootEnemy collides with the projectile2 object, instance_destroy() is used ans the shootEnemy is destroyed, because the shootEnemy only has two lives.
The last enemy type and piece of the game is the boss. In the boss object's Create event, the bossHealth variable is set to 5, so the boss needs to be hit 5 times before it is destroyed and the player wins. The shootInterval is set to 80 and shootTimer = shootInterval. In the Step event of the boss object, the code is the same as the shootEnemy for gravity, and has an if statement that doesn't allow the enemy to shoot unless the player is within 500 pixels. Once the play is inside 500 pixels, the shootInterval starts to decrease and the boss shoots towards the location of the hero. The boss also has a Draw event with animation for left and right, the same as the enemyStomp and the shootEnemy. If the enemy collides with a projectile object, 1 is sutracted from the bossHealth, and if the bossHealth variable is less than 1, the enemy destroys and the player wins. The same goes for the projectile2 object, except 2 is subtracted from the bossHealth. In both Collision events an if statement is used so if the bossHealth variable is less than 3, "image_blend = c_red". This is a built in function that shades the boss red, so you know he is close to being destroyed. 
