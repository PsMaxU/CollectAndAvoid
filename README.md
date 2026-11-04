# CollectAndAvoid

Used version of the engine: Unreal Engine 5.8.4

### HOW TO RUN THE GAME:
1) Unzip the downloaded archive (.zip) on your PC
2) Open the extracted folder
3) Double-click on CollectAndAvoid.exe to launch the game

### CONTROLS:
- WASD - Move
- Mouse - Look
- Shift - Sprint
- Enter - Jump
- Esc - Pause

### ANSWERS TO THE QUESTIONS:
Changed movement parameters:  
- Max Walk Speed is 500, while sprinting it's 600 (default player movement speed)  
- Jump Z Velocity is 400 (maximum jump height)  
- Air control is 0,6 (how much control over the character the player has during a jump)  

-On overlap, the coin checks with a Cast to the hero class, so that it continues execution only if overlapped actor is the hero  
-Score on a screen is updated with a function in order to not use per-frame binding (which is basically Event Tick) that heavily lowers performance when used a lot  

The most expensive performance-cost are:
- View Visibility: calculates what the camera currently sees, which causes the biggest sudden performance spikes  
- Init dynamic shadows: prepares lighting and shadows, which creates the highest constant background performance load

### SHORT DESCRIPTION OF EACH BLUEPRINT:
BP_PickUp: Parent class for collectable items  
BP_Coin: a child of BP_PickUp, has its own defaults  
Enemy:
- BP_Enemy: the physical body of the enemy with its 3D model  
- BP_EnemyAIController: the brain managing the enemy's logic (Behavior Tree) and senses (AI Perception)  
- BP_PatrolPoint: an invisible marker on the level that the enemy moves toward while patrolling  
- BTT_NextPatrolPoint: a custom Behavior Tree task that calculates the next patrol point  

Player & Game System:  
- GBP_GameMode: manages core rules (win/loss conditions)  
- GBP_GameState: stores global game data (score, current state)  
- GBP_Hero: the physical representation of the player (handles movement mechanics)  
- GBP_PlayerController: processes keyboard and mouse inputs, and controls the camera

### ASSET LIST:
Character animations: https://fab.com/s/70f5ca18b360  
License: https://www.fab.com/eula

### WHAT I LEARNED AND WHAT WAS HARD:
First af all, this is my very first time creating a complete game loop in an engine and packaging the game, so at the very least, I've learned how to do that. I also got better in understanding of the responsibilities of each game system blueprint and how to properly separate them.  
As for me, the hardest part was creating the enemy, its AI and animation, probably because it was the engine's part I was completely unfamiliar with.