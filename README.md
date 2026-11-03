# CollectAndAvoid

Used version of the engine: Unreal Engine 5.8.4

Changed movement parameters:
Max Walk Speed is 500, while sprinting it's 600 (default player movement speed)
Jump Z Velocity is 400 (maximum jump height)
Air control is 0,6 (how much control over the character the player has during a jump)

On overlap, the coin checks with a Cast to the hero class, so that it continues execution only if overlapped actor is the hero