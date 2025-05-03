# Specification

## 2.1 Hardware Specification
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Row 1    | Data     | More     |
| Row 2    | Info     | Here     |

## 2.2 Dimension

## 2.3 Inertia

## 2.4 Understanding URDF
Understanding URDF (Universal Robot Description Format) with ABC

### 2.4.1 What is URDF?
URDF (Universal Robot Description Format) is an XML-based format used to describe a robot’s physical structure, kinematics, dynamics, and visualization properties. It is widely used in ROS (Robot Operating System) to define robot models for simulation, motion planning, and visualization.

URDF defines a robot using the following key elements:

Links: Define a robot’s visual representation, collision geometry, and inertial properties.
Joints: Define the connections and movement constraints between links.
Visuals: Describe how the robot appears in visualization tools.
Collisions: Define simplified geometries used for physics-based interactions.
Inertial properties: Specify mass, center of gravity, and inertia tensor for physics simulation.
For a more detailed understanding of URDF, we recommend referring to the URDF Tutorial on the ROS 2 Wiki. The best way to understand and learn URDF is to build a simple robot yourself.

### 2.4.2 Visualizing the ABC URDF Structure
#### Key Features of the URDF Graph
**Root Node(world)**:
The robot is fixed to the world frame via world_fixed.
**Link Structure**:(Represent the rigid bodies of the robot)
The manipulator consists of five main links (link1 to link5), which form the robotic arm.
The end-effector (end_effector_link) is attached to link5.
The gripper mechanism includes gripper_left_link and gripper_right_link.
**Joint Connections**: (Define how each link moves relative to another)
Each link is connected via revolute (joint1 to joint4) or prismatic joints (gripper_left_joint, gripper_right_joint).
The gripper operates with a mimic joint (gripper_right_joint_mimic), ensuring both fingers move symmetrically.

### 2.4.3 URDF with Xacro
The provided URDF uses Xacro (XML Macros) to simplify and modularize the robot description. Xacro allows reusing components and making the URDF more maintainable.
The following explanation is based on the Xacro file:

At the beginning of the file, a macro is defined:

This allows the reuse of the same structure with different prefixes, making it flexible for multi-robot environments.

### 2.4.4 Defining a Link
A link represents a rigid body in the robot. Each link has visual, collision, and inertial properties.

Example of link1 in ABC:

#### Explanation

**<visual>**: Defines how the link appears in a simulation or visualization tool (e.g., RViz) using a 3D mesh (link1.stl).
**<collision>**: Specifies the simplified geometry used for physics-based interactions (e.g., collisions).
**<inertial>**: Defines the mass, center of gravity, and inertia tensor, which are crucial for realistic physics simulations.

### 2.4.5 Defining a Joint
A joint connects two links and defines how they move relative to each other.

#### Explanation

**type="revolute"**: Defines a rotating joint (common in robotic arms).
**<parent> and <child>**: Specifies the two links connected by the joint.
**<origin>**: Defines the joint’s position relative to the parent link.
**<axis>**: Specifies the rotation axis (0 0 1 means rotation around the Z-axis).
**<limit>**: Defines movement constraints (speed, torque, and range).
**<dynamics>**: Includes damping, which affects how smoothly the joint moves.

### 2.4.6 Adding a Prismatic Joint
Prismatic joints allow linear motion rather than rotation.

#### Explanation

**type="prismatic"**: Allows linear motion along the defined axis.
**<limit>**: Restricts the movement range (from -0.010m to 0.019m).
**Used for**: The gripper’s movement (opening and closing).

### 2.4.7 Using a Fixed Joint
Fixed joints are used when a link **does not move** relative to another.

#### Explanation

**type="fixed"**: No relative motion between links.
**Used for**: End-effectors or components that do not move.
