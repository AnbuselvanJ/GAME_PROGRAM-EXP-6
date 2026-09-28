# GAME_PROGRAM-EXP-6
AI Random Roam with Chase - Unreal Engine
Aim
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they come within a certain range, using Behavior Trees, Blackboard, and AI Perception.

Procedure
Setup Navigation

Add a NavMeshBoundsVolume to your level and scale it to cover the roamable area.
Press P to confirm the green nav area is visible (indicating navigable space).
Create AI Character

Create a Blueprint character (e.g., BP_AIEnemy) with a skeletal mesh and AIController class.
Create an AI Controller Blueprint (e.g., BP_AIController) and assign it to the character.
Enable AI Perception

In BP_AIController, add an AIPerception component.
Configure a Sight sense (set detection range, lose sight range, peripheral vision angle).
Bind OnPerceptionUpdated to update a blackboard value (e.g., CanSeePlayer and PlayerActor).
Set Up Blackboard

Create a Blackboard with the following keys:
TargetLocation (Vector)
PlayerActor (Object)
CanSeePlayer (Bool)
Create Behavior Tree (BT_AI)

Structure it like this:
```
Root
└── Selector
    ├── Sequence (Chase Player)
    │   ├── Blackboard Check: CanSeePlayer == true
    │   └── Move To: PlayerActor
    └── Sequence (Random Roam)
        ├── Task: Find Random Location → TargetLocation
        └── Move To: TargetLocation
```
6.Custom Task: Find Random Location

Create a new BTTask_BlueprintBase to get a random reachable point using:
```
UNavigationSystemV1::GetRandomReachablePointInRadius()
```
7.Test the AI

Add a player character to the level.
Place the AI enemy in the map and assign its controller and behavior tree.
Press Play: the AI should roam when the player is far and chase the player when within sight.

Output:
<img width="1200" height="871" alt="image" src="https://github.com/user-attachments/assets/cec260af-e079-4e9e-b851-18ced4fe8677" />
<img width="1016" height="428" alt="image" src="https://github.com/user-attachments/assets/28d9bda9-4dba-4d99-a3cb-948972a1d3e5" />
<img width="1297" height="498" alt="image" src="https://github.com/user-attachments/assets/9793abaa-086a-4930-b727-345862e40fd1" />

Result

The AI character roams randomly within a defined area. When the player enters its sight range, the AI stops roaming and begins to chase the player until the player is out of sight, after which it resumes roaming.
