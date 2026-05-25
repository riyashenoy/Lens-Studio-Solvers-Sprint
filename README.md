# Interactable Helper, Essentials Animations, and Solvers

> **Requirement:** Update to [Lens Studio 5.15.4](https://ar.snap.com/download/v5-15-4) before starting.

**Sprint Goal:** Learn about the InteractableHelper project, Essentials Animations, and Solvers. Reuse components from the Essentials Project for your second project.

---

## Setup

1. Open a new Essentials Project in Lens Studio.
2. Save the project as `April 9 Sprint`.
3. Disable the examples so the preview is clear.

---

## Feedback Methods

1. Under the Asset Browser, find the **InteractableHelper** package.
2. Drag `Examples_PLACE_IN_SCENE` into your scene hierarchy.

This serves as a reference for feedback methods. All components can be reused in your own projects to speed up development.

---

## Animations

The project includes three tween example animations.

**What is a tween?**
A tween animates a value from point A to point B over a set duration. You can define the shape of the motion to create different effects:

| Type | Behavior |
|---|---|
| `Linear` | Constant speed; robotic feeling |
| `Cubic.In` | Starts slow, accelerates into it |
| `Cubic.Out` | Arrives fast, decelerates to a stop |
| `Cubic.InOut` | Slow start, fast middle, slow end; the most natural feeling |

---

## Solvers

**What is a solver?**
A solver is a script component that computes where an object should be every frame and automatically updates its transforms based on rules. It takes inputs like the camera's position, distance, and angles, then applies a new position, rotation, or scale to the object's transform.

### Solver Scripts in This Project

**BillboardTS**
Rotates an object to face a target (usually the camera) on the Y-axis only. Good for labels and UI that should always face the user.

**TetherTS**
Keeps an object attached near a target with an offset and repositions it smoothly when it moves too far, using horizontal and vertical thresholds. Good for floating UI that follows the user's head or hand.

**TetherBetweenAngleRangeTS**
Only repositions when angle or distance conditions are exceeded. Good for smart repositioning so content does not constantly jump around.

**MatchTransformTS**
Copies another object's position, rotation, and scale smoothly. Good for follower objects.

**ScaleOverDistanceLinearTS**
Scales object size based on distance to target using min/max distance and min/max scale values. Good for keeping UI readable at various distances.

**DistanceEventsTS**
Watches distance thresholds and fires callbacks when they are crossed (enter/exit). Good for triggering hints, animations, audio, and state changes.

**DistanceEventsCallbacks**
A callback script with example functions to call by name. Good as a starting template.

**InBetweenRotationUtilityTS**
Computes and sets the rotation halfway between two targets or directions. Helpful for shared indicators.

**SharpTurnTS**
Tracks motion direction over time, detects sharp turns using the dot product, and emits an event. Good for gesture or movement-based triggers.

---

## Exercise: 3D Character with Billboard Solver

In this exercise you will make a 3D character move and rotate, and attach a billboard solver so it always faces you when you move around.

### 1. Create the Scene Object

- Right-click in the Scene Hierarchy and select **Create Scene Object**.
- Rename it to `Exercise`.

### 2. Add the Move + Rotate Object

- Copy the `Move + Rotate` object into your `Exercise` object.
- Select `Move + Rotate` and position it to the center of the scene.

### 3. Replace the Cube with a Character

- Open the Asset Library and find an object to use (the instructions use **Kitty**).
- Import it into your project.
- Drag the green prefab `Kitty_ADD_TO_SCENE` into the `Move + Rotate` object group in the Hierarchy.
- Adjust the object's scale uniformly so it sits above the box.
- Set the Y transform of `Interactable` to `0.00` so the button sits lower in the frame.
- Delete the `Move + Rotate Blue Box` object.

### 4. Update the InteractableHelper Component

- Select `Interactable` and find the **InteractableHelper** component in the Inspector.
- Under `SceneObject` assignments, replace the blue box reference with the Kitty prefab.

### 5. Configure Animations

**Rotate Local Animation Type**
- Set the A values to match your object's current rotation values.
- Set the B values to the target rotation after the animation triggers.

**Move Local Animation Type**
- Set the A values to match your object's current transform values.
- Set the B values to the target position after the animation triggers.

Play around with values to see different results. If you change values heavily, zoom out to see the effect.

### 6. Add Direct Interaction (Tap to Trigger)

- Expand the Kitty prefab in the Hierarchy until you find the `cat_body` mesh.
- Copy and paste the InteractableHelper object from `Interactable` onto `cat_body`.

You can now trigger the animation by either pinching the button (indirect) or tapping the Kitty's body directly.

### 7. Add the Billboard Solver

- Select the base `Exercises` object.
- Add the **BillboardTS** component to it.
- Uncheck the `Look Away` box.
- Drag the Camera object into the Target field.

The character will now face you as you move around. Try it on your Specs.

---

## Extra Challenges

**Syncing Animations**
Look at the `Play Animation` object in the InteractableHelper examples. Modify your button to play the Kitty's animation, starting in Idle.

**Sound Effects**
Download sound effects from the Asset Library. Copy the sound effect object from the InteractableHelper example and implement a custom sound for the button.

---

## Ideas for Future Projects

- Customize buttons with different materials and shaders, or replace them entirely with meshes.
- Add other objects to the scene.
- Connect physics objects the way we did in the physics lab.
