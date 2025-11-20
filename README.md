# GAME_PROGRAM-EXP-6
# AI Random Roam with Chase - Unreal Engine

# Aim
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they come within a certain range, using Behavior Trees, Blackboard, and AI Perception.

# Procedure
 1. Setup Navigation
      Add a NavMeshBoundsVolume to your level and scale it to cover the roamable area.
      Press P to confirm the green nav area is visible (indicating navigable space).

 2. Create AI Character
       Create a Blueprint character (e.g., BP_AIEnemy) with a skeletal mesh and AIController class.
       Create an AI Controller Blueprint (e.g., BP_AIController) and assign it to the character.

 3. Enable AI Perception
       In BP_AIController, add an AIPerception component.
       Configure a Sight sense (set detection range, lose sight range, peripheral vision angle).
       Bind OnPerceptionUpdated to update a blackboard value (e.g., CanSeePlayer and PlayerActor).

 4.  Set Up Blackboard
       Create a Blackboard with the following keys:
            TargetLocation (Vector)
            PlayerActor (Object)
            CanSeePlayer (Bool)
 
 5.Create Behavior Tree (BT_AI)
      Structure it like this:
Root
└── Selector
    ├── Sequence (Chase Player)
    │   ├── Blackboard Check: CanSeePlayer == true
    │   └── Move To: PlayerActor
    └── Sequence (Random Roam)
        ├── Task: Find Random Location → TargetLocation
        └── Move To: TargetLocation

 6.Custom Task: Find Random Location
        Create a new BTTask_BlueprintBase to get a random reachable point using:
            UNavigationSystemV1::GetRandomReachablePointInRadius()
        Set the result to the TargetLocation blackboard key.
 
 7. Test the AI
         Add a player character to the level.
         Place the AI enemy in the map and assign its controller and behavior tree.
         Press Play: the AI should roam when the player is far and chase the player when within sight.  

# Output

<img width="559" height="406" alt="516198871-be091a53-0a00-4977-9b83-e1b148b6a56d" src="https://github.com/user-attachments/assets/7ff13dc7-3722-47c4-a0d6-5e5abd7a3287" />

<img width="560" height="230" alt="516199059-68689a5d-93c3-4bbc-9dac-6cd2b0fc4b4e" src="https://github.com/user-attachments/assets/13d8655b-1d01-43d5-84b1-1a136d8fa08e" />

<img width="555" height="210" alt="516199243-ec6b54a7-71e1-43e3-b34b-8b23dece4285" src="https://github.com/user-attachments/assets/61a4f01c-5f5e-47ca-9f1d-a7132f79f0fc" />

# Result
The AI character roams randomly within a defined area. When the player enters its sight range, the AI stops roaming and begins to chase the player until the player is out of sight, after which it resumes roaming.
