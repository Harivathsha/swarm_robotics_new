# 🐝 SwarmBot-LLM: Multi-Agent RL & Language Model Coordination

[![ROS 2](https://img.shields.io/badge/ROS_2-Humble-34a853?style=flat&logo=ros)](https://docs.ros.org/en/humble/)
[![Gazebo](https://img.shields.io/badge/Simulator-Gazebo_Classic-ff6600?style=flat)](https://classic.gazebosim.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.3.1-ee4c2c?style=flat&logo=pytorch)](https://pytorch.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?style=flat&logo=openai)](https://openai.com/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-E95420?style=flat&logo=ubuntu)](#)

An advanced multi-agent robotics platform utilizing **ROS 2 Humble**. This architecture integrates Large Language Models (LLMs) for high-level reasoning and mission planning, Deep Q-Networks (DQN) for dynamic task allocation, and Twin Delayed DDPG (TD3) for continuous swarm control, all augmented by real-time 3D RTAB-Map point cloud perception.

## 🎥 Demonstrations

* **[Watch: Dynamic Interactable Large Swarm Environment](https://github.com/user-attachments/assets/be5120e0-4375-47db-82c1-89e0c0020a13)**
* **[Watch: LLM-Guided Large Swarm Execution](https://github.com/user-attachments/assets/89d2a845-8c10-49f4-902a-0d0e0c357594)**

---

## ✨ Key Features

* 🧠 **LLM Mission Control:** Natural language interface for swarm command and contextual reasoning.
* 🎯 **DQN Task Allocation:** Intelligent, decentralized distribution of tasks across multiple agents.
* 🕹️ **TD3 Swarm Control:** Deep Reinforcement Learning for continuous, collision-free multi-robot navigation.
* 🗺️ **3D Point Cloud Perception:** Real-time depth mapping and visualization using RTAB-Map.
* 📊 **Live Telemetry Logging:** Continuous tracking of robot locations, detected objects, and task assignments.

---

## 📂 System Architecture

```text
/robo/src/ros2_learners
 ├── llm/                      # Source code for the OpenAI LLM interface
 ├── log/ & logs/              # Telemetry: Object locations, Bot positions, Task allocations
 ├── my_robot_controller/      # Swarm Reinforcement Learning (TD3 models)
 ├── navigation_tb3/           # Base navigation configurations
 ├── nodes/                    # Custom ROS 2 node executions
 ├── pc/                       # Real-time state and log maintenance scripts
 ├── point_cloud_perception/   # 3D depth mapping and RTAB-Map launch files
 ├── TaskAllocation/           # Deep Q-Network (DQN) Task Allocation models
 └── turtlebot3_gazebo/        # Main simulation package (Worlds, Models, Launch files)
```

🛠️ System Requirements & Dependencies
OS: Ubuntu 22.04

ROS Version: ROS 2 Humble

Python: 3.10.12

Software & Libraries:

Gazebo Classic

PyTorch 2.3.1 | TensorFlow 2.15.0

Numpy 1.21.5 | Matplotlib 3.5.1

TensorBoard | OpenAI 0.28

Note: Ensure ROS 2 Humble and Gazebo Classic are properly installed before proceeding.

🚀 Installation & Build
1. Install ROS 2 System Dependencies
```
source /opt/ros/humble/setup.bash
sudo apt update
sudo apt install ros-humble-gazebo-ros-pkgs ros-humble-gazebo-ros2-control ros-humble-xacro
```
3. Initialize and Build the Workspace
```

cd robo
rosdep init
rosdep update
rosdep install -i --from-path src --rosdistro humble -y
colcon build
```

4. Configure the OpenAI API
Generate an API key from your OpenAI Platform Settings.

Install the specific OpenAI Python wrapper: pip install openai==0.28

Create a file named api_key.txt inside the src/ros2_learners/llm/ directory and paste your raw API key inside it.

💻 Execution Guide
For optimal execution, open separate terminal tabs for each subsystem and source the workspace (source install/setup.bash) in every new tab.

Step 1: Launch the Gazebo Simulation
```

export TURTLEBOT3_MODEL=waffle
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
Step 2: Initialize 3D Depth Mapping
Replace {N} with the specific bot ID (e.g., 5).

```

ros2 launch point_cloud_perception 3d_depth_mapping_rtab{N}.launch.py
```
Step 3: Start Telemetry & Logging Daemons
```

# Terminal A: Track overall object positions
cd ~/robo/src/ros2_learners/pc/pc/ && python3 list1.py

# Terminal B: Track specific assigned task objects
cd ~/robo/src/ros2_learners/pc/pc/ && python3 match.py

# Terminal C: Maintain active Swarm positions
cd ~/robo/src/ros2_learners/TaskAllocation/ && python3 TaskAllocationNode.py
```

Step 4: Run Task Allocation & RL Control
```

# Initialize DQN Task Allocation
cd ~/robo/src/ros2_learners/TaskAllocation/ && python3 script.py

# Launch TD3 Swarm Testing (or use train.py for training)
cd ~/robo/src/ros2_learners/my_robot_controller/my_robot_controller/td3/ && python3 test_copy.py
```

Step 5: Engage the LLM Interface
```
cd ~/robo/src/ros2_learners/llm/
python3 scripts/run_llm.py
```


[DYNA_Interactable_LargeSwarm_LargeEnvironment.webm](https://github.com/user-attachments/assets/be5120e0-4375-47db-82c1-89e0c0020a13)

[LLM_LargeEnv_Large_Swarm.webm](https://github.com/user-attachments/assets/89d2a845-8c10-49f4-902a-0d0e0c357594)


