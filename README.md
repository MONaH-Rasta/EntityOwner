# EntityOwner

Oxide plugin for Rust. Show and modify entity ownership and cupboard/turret authorization

## Features

- Allows admins to prod an entire building (including deployables)
- Allows admins to change or remove ownership from an entire building (including deployables)
- Allows admins to see cupboard/turret authorization
- Allows admins to change authorization for all nearby cupboards/turrets
- Supports message localization
- Supports both authLevel and permission authentication.
- Provides an API for other plugins to integrate easily

## Chat Commands

- `/prod` -- Check ownership of entity you are looking at
- `/own` -- Set ownership of entity you are looking at
- `/own all` - Give yourself ownership of the entire structure (including deployables)
- `/own all <player name>` -- Give the specified player ownership of the entire structure  (including deployables)

- `/unown all` -- Remove ownership from an entire structure (including deployables)

- `/prod2` -- Check the ownership of the entire structure (including deployables)
- `/prod2 block` -- Check the ownership of the structure (and only the structure)
- `/prod2 cupboard` -- Check the authorization of nearby cupboards
- `/prod2 storage` -- Check the ownership of nearby storage containers

- `/auth` -- Check the authorization of the cupboard you are looking at
- `/auth cupboard` -- List all players currently authorized on cupboard
- `/auth turret` -- Check the authorization of the turret you are looking at
- `/auth PlayerName` - Give authorization on cupboard you are looking at to target player
- `/auth cupboard PlayerName` -- Give authorization on all nearby cupboards to target player
- `/auth turret PlayerName` -- Give authorization on all nearby turrets to target player

- `/deauth PlayerName` -- Remove authorization of cupboard you are looking at from target player
- `/deauth cupboard PlayerName` -- Remove authorization of all nearby cupboards from target player
- `/deauth turret PlayerName` -- Remove authorization of all nearby turrets from target player

## Own/Prod2/Unown Options

- all
- block
- storage
- sign
- sleepingbag
- plant
- oven
- turret
- door
- cupboard

## Permissions

- `entityowner.canchangeowners` -- Allows player to use auth and own commands
- `entityowner.cancheckowners` -- Allows player to use prod command
- `entityowner.cancheckcodes` -- Allows player to see code lock codes
- `entityowner.seedetails` -- Allows player to see additional details about object (prefab name, skin id, etc)

## Configuration

- **EntityLimit** *(default: 8000)*  
There is a hard cap on how many entities may be included in any given ownership command.  By default, this cap is 8000.

- **messages** *(Localization)*  
It is possible to change most of the messages sent by EntityOwner into a different language.

- **DistanceThreshold** *(default: 3)*  
It is suggested to ratchet the threshold down by 1 tenth each time (2.9, 2.8, 2.7 ..) until you are satisfied with the level of precision when using commands like /own and /prod2.

The DistanceThreshold option allows you to configure how far the ownership commands will seek for other nearby entities (starting from the first entity). Changing the threshold will make ownership commands more or less precise.

## Developer API

```csharp
// Gets the name and status of the owner player
// Returns null if no owner found
string GetOwnerName(BaseEntity entity)

// Get the BasePlayer instance (if known) of the owner player
// Returns null if no owner found
BasePlayer GetOwnerPlayer(BaseEntity entity)

// Removes the ownership data from a BasePlayer
RemoveOwner(BaseEntity entity)

// Changes ownership of a BaseEntity to the specified player
ChangeOwner(BaseEntity entity, BasePlayer player)

// Retrieves the owner player.userID in string format
// Returns false when no owner found
object FindEntityData(BaseEntity entity)

// Clears all deployable associations with a particular player
ClearDeployableProfile(BasePlayer player)

// Clears all construction associations with a particular player
ClearConstructionProfile(BasePlayer player)

// Grab all constructions associated with a particular player
List<BuildingBlock> GetProfileConstructions(BasePlayer player)

// Grab all deployables associated with a particular player
List<BaseEntity> GetProfileDeployables(BasePlayer player)
```
