# Firmware

**Not used in this project.** There is no microcontroller; the robot is entirely simulated in Isaac Sim.

What would have to be written to run the policy on a real robot (not done in this project):
1. A ROS / libfranka node that reads the joint angles and the cube position (from a camera) and assembles the 50 observations exactly as in the simulation (see [machine-skills/](../../machine-skills/README.md)).
2. Run `policy.onnx` at 50 Hz and convert the action → hand target → IK → joint commands (or use Franka's Cartesian impedance controller).
3. A safety layer: limit joint speeds and the distance to joint limits; stop when contact forces exceed a threshold.
