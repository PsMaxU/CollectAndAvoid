# CollectAndAvoid

Used version of the engine: Unreal Engine 5.8.4

Answers to the questions:

Changed movement parameters:
-Max Walk Speed is 500, while sprinting it's 600 (default player movement speed)
-Jump Z Velocity is 400 (maximum jump height)
-Air control is 0,6 (how much control over the character the player has during a jump)
On overlap, the coin checks with a Cast to the hero class, so that it continues execution only if overlapped actor is the hero
Score on a screen is updated with a function in order to not use per-frame binding (which is basically Event Tick) that heavily lowers performance when used a lot
The most expensive performance-cost are:
-View Visibility: calculates what the camera currently sees, which causes the biggest sudden performance spikes
-Init dynamic shadows: prepares lighting and shadows, which creates the highest constant background performance load

Used assets:
https://fab.com/s/70f5ca18b360
License: https://www.fab.com/eula