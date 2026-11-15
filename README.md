# CollectAndAvoid

Used version of the engine: Unreal Engine 5.8.4

### HOW TO RUN THE GAME:
Google Drive link:  
https://drive.google.com/drive/folders/1piahYBG43t4GA02y_Ph3fXvwlXhZbKs3?usp=sharing
1) Unzip the downloaded archive (.zip) from the Google Drive ("Game" folder) on your PC
2) Open the extracted folder
3) Double-click on CollectAndAvoid.exe to launch the game

### CONTROLS:
- WASD - Move
- Mouse - Look
- Shift - Sprint
- Space - Jump
- Esc - Pause

### ANSWERS TO THE QUESTIONS:
Changed movement parameters:  
- Max Walk Speed is 500, while sprinting it's 600 (default player movement speed)  
- Jump Z Velocity is 400 (maximum jump height)  
- Air control is 0,6 (how much control over the character the player has during a jump)  

-On overlap, the coin checks with a Cast to the hero class, so that it continues execution only if overlapped actor is the hero  
-Score on a screen is updated with a function in order to not use per-frame binding (which is basically Event Tick) that heavily lowers performance when used a lot  
-Enemy Max Walk Speed is set on Event BeginPlay (value from Data asset)

### SHORT DESCRIPTION OF EACH BLUEPRINT (all use prefix BP_):
BP_PickUp: Parent class for collectable items  
BP_Coin: a child of BP_PickUp, has its own defaults  
Enemy:
- BP_Enemy: the physical body of the enemy with its 3D model  
- BP_EnemyAIController: the brain managing the enemy's logic (Behavior Tree) and senses (AI Perception)  
- BP_PatrolPoint: an invisible marker on the level that the enemy moves toward while patrolling  
- BTT_NextPatrolPoint: a custom Behavior Tree task that calculates the next patrol point  

Player & Game System:  
- BP_GameMode: manages core rules (win/loss conditions)  
- BP_GameState: stores global game data (score, current state)  
- BP_Hero: the physical representation of the player (handles movement mechanics)  
- BP_PlayerController: processes keyboard and mouse inputs, and controls the camera

### SCORING SYSTEM:  
score - number of coins - scale - Z rotation speed  
5 - 5 - 1 - 90  
10 - 4 - 1,5 - 72  
15 - 1 - 2 - 60  
20 - 2 - 2,5 - 45  
Overall: 12 coins, 120 points  
Goal score is 100, so that a player have multiple ways and paths to win the game

### PROFILING:
Scene: L_Arena  
FPS: 80.20 FPS  
Frame: 12.47 ms  
Game: 12.44 ms  
Draw: 0.00 ms  
GPU: 4.84 ms  
Init dynamic shadows: 0.24 ms (avg) / 0.61 ms (max)  
View Visibility: 0.10 ms (avg) / 2.61 ms (max)

#### Before and after optimization:
Before (Lumen, Ray Tracing ON, Default RHI DirectX 12): 80.20 FPS, frame 12.47 ms  
After (Screen Space, Ray Tracing OFF, Default RHI DirectX 11): 120.00 FPS, frame 8.3 ms

### KNOWN BUGS:
- Enemy walk animation stops playing after a few loops
- Output Log had "Attempted to access AudioComponent_7 via property ChaseSound, but AudioComponent_7 is not valid (pending kill or garbage)" error, which appeared when a player get close to the enemy and lose, while not being seen.
It was resolved by adding IsValid (with execution) node before Stop node for ChaseSound
- Output Log had "LogAutomationTest: Error: Condition failed" warning, which appeared on every launch of the Editor.
It was resolved by setting the "Editor Locale" to "English" under "Region & Language" in the "Editor Preferences"
- Output Log had "LogPlayerController: Error: InputMode:UIOnly - Attempting to focus Non-Focusable widget SObjectWidget [Widget.cpp(976)]!" warning, which appeared when a Pause, Lose or Win widget was visible.
It was resolved by flagging the widgets as isFocusable

### ASSET LIST:
#### Used from the Starter Content:
- Starter_Music01 as Chase_Wav
- Starter_Music_Cue as Chase_Cue
- Starter_Wind05 as BackgroundWeather_Wav
- SM_Ramp

#### Used from the Third Persom Template:  
/Characters/Mannequins/
- Anims/Unarmed/
- Materials/
- Meshes/
- Rigs/
- Textures/

#### Used from FAB:
Enemy animations: https://fab.com/s/70f5ca18b360  
License: https://www.fab.com/eula

### WHAT I LEARNED AND WHAT WAS HARD:
First af all, this is my very first time creating a complete game loop in an engine and packaging the game, so at the very least, I've learned how to do that. I also got better in understanding of the responsibilities of each game system blueprint and how to properly separate them.  
As for me, the hardest part was creating the enemy, its AI and animation, probably because it was the engine's part I was completely unfamiliar with.