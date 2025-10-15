**FILE STRUCTURE :**  
	/robo  
		/src  
			/ros2\_learners  
				/llm  
				/log  
				/logs  
				/my\_robot\_controller   
				/navigation\_tb3   
				/nodes   
				/pc   
				/point\_cloud\_perception  
				/resources   
				/robot\_math   
				/TaskAllocation  
				/transforms   
				/turtlebot3\_gazebo 

**LLM**:  
	This package contains source code to run the LLM interface.

**logs**:  
	This file contains the log of the following   
		1.Detected objects with their location  
		2.Robots location in real time  
		3.Updated task objects location when assigned  
		4.Name of the task object  
		5.Task object location with allotted bot

**my\_robot\_controller**:  
	This package contains swarm RL

**pc**:  
	This package contains necessary file to maintain log in real time

**point\_cloud\_perception:**  
	This package contains the respective launch files to visualize 3D mapping in real time.

**TaskAllocation**:  
	This file contains DQN task allocation model 

**turtlebot3\_gazebo**:  
	This is the main package which defines our robot model and their respective worlds. Also this file contains their respective launch files  
Rest all files are supporting files for the main packages.

### System Requirements
- **Operating System**: Ubuntu 22.04
- **ROS Version**: ROS 2 Humble
- **Python**: 3.10.12

## Installation Links
- [ROS 2 Humble Installation](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)
- [Gazebo Classic Installation](https://classic.gazebosim.org/tutorials?tut=install_ubuntu)

## Notes
- Ensure all prerequisites are met before installation
- Follow steps sequentially
- Consult official documentation for detailed guidance


### Software Dependencies
- Gazebo Classic
- PyTorch 2.3.1
- TensorFlow 2.15.0
- Numpy 1.21.5
- Matplotlib 3.5.1
- TensorBoard
- OpenAI 0.28

## Installation Procedure

### 1. Source ROS 2 Humble
```bash
source /opt/ros/humble/setup.bash
```

### 2. Verify Ubuntu Version
```bash
lsb_release -a
```

### 3. Install ROS 2 Gazebo Packages
```bash
sudo apt install ros-humble-gazebo-ros-pkgs ros-humble-gazebo-ros2-control
```

### 4. Install Xacro
```bash
sudo apt install ros-humble-xacro
```

### 5. Navigate to Project Directory
```bash
cd robo
```

### 6. Initialize ROS Dependencies
```bash
rosdep init
rosdep update
rosdep install -i --from-path src --rosdistro humble -y
```

### 7. Build the Package
```bash
colcon build
```

## Notes
- Ensure all prerequisites are met before installation
- Follow steps sequentially
- Consult official documentation for detailed guidance

## Environment Setup

### Source Package
```bash
source install/setup.bash
```

### Set TurtleBot3 Model
```bash
export TURTLEBOT3_MODEL=waffle
```

## Launch Environment

### Launch Gazebo Environment
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

### Visualize 3D Depth Mapping
In a new terminal:
```bash
cd robo
source install/setup.bash
# Replace {N} with bot number (e.g., 5)
ros2 launch point_cloud_perception 3d_depth_mapping_rtab{N}.launch.py
```

## LLM and API Setup

### OpenAI API Key
1. Visit: https://platform.openai.com/settings/organization/api-keys
2. Create new secret key
3. Create `api_key.txt` in the "llm" folder
4. Paste API key into the file

### Install OpenAI Package
```bash
pip install openai==0.28
```

## Running Modules

### Task Allocation
```bash
cd ~/robo/src/ros2_learners/TaskAllocation/
python3 script.py
```

### Maintain Bot Position
```bash
cd ~/robo/src/ros2_learners/TaskAllocation/
python3 TaskAllocationNode.py
```

### Object Position Log
```bash
cd ~/robo/src/ros2_learners/pc/pc/
python3 list1.py
```

### Task Object Position Log
```bash
cd ~/robo/src/ros2_learners/pc/pc/
python3 match.py
```

## TD3 Model Training and Testing

### Test Script
```bash
cd ~/robo/src/ros2_learners/my_robot_controller/my_robot_controller/td3/
python3 test_copy.py
```

### Training
```bash
cd ~/robo/src/ros2_learners/my_robot_controller/my_robot_controller/td3/
python3 train.py
```

### LLM Module
```bash
cd ~/robo/src/ros2_learners/llm
python3 scripts/run_llm.py
```
