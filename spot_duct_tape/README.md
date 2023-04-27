# How to run PPO for Spot

This is a Hacky solution to get Spot training and demo using Anymal OIGE code. With as little modifications as possible.<br/>
Step 1 - Must Name the Joints on Spot USD file to match the ones in Anymal.<br/>
Step 2 - Change the name of the files and the Classes so there is no conflict<br/>
Step 3 - Add the task to utils/task_util.py<br/>
Step 4 - Change the code to grab the right assets (modify the path)<br/>

Changing the name of the joints fucksup the training algorithm<br/>

Source<br/>
https://github.com/boredengineering/Robots_for_Omniverse

Project<br/>
- [Boston Dynamics](https://www.bostondynamics.com/)
- [Spot](https://github.com/chvmp/spot_ros)

## **Setting up OIGE**

### Setting up **cfg/task** and **cfg/train**<br/>
- Place the YAML file **Spot.yaml** and **SpotTerrain.yaml** from **cfg/task** into your installed OIGE location of **omniisaacgymenvs/cfg/task/**<br/>
> **Spot.yaml** and **SpotTerrain.yaml** ---> **omniisaacgymenvs/cfg/task/**

- Place the YAML file **SpotPPO.yaml** and **SpotTerrainPPO.yaml** from **cfg/train** into your installed OIGE location of **omniisaacgymenvs/cfg/train/**<br/>
> **SpotPPO.yaml** and **SpotTerrainPPO.yaml** ---> **omniisaacgymenvs/cfg/train/**

### Setting up **robots/articulations/**<br/>
- Place the Python file **spot.py** from **robots/articulations/** into your installed OIGE location of **omniisaacgymenvs/robots/articulations/**<br/>
> **spot.py** ---> **omniisaacgymenvs/robots/articulations/**

- Place the Python file **spot_view.py** from **robots/articulations/views/** into your installed OIGE location of **omniisaacgymenvs/robots/articulations/views/**<br/>
> **spot_view.py** ---> **omniisaacgymenvs/robots/articulations/views/**

### Setting up **tasks/**<br/>
- Place the Python file **spot.py** and **spot_terrain.py** from **tasks/** into your installed OIGE location of **omniisaacgymenvs/tasks/**<br/>
> **spot.py** and **spot_terrain.py** ---> **omniisaacgymenvs/tasks/**

### Setting up **demos/**<br/>
- Place the Python file **spot_terrain.py** from **demos/** into your installed OIGE location of **omniisaacgymenvs/demos/**<br/>
> **spot_terrain.py** ---> **omniisaacgymenvs/demos/**

## **Running OIGE**
Creating a macro<br/>
> alias PYTHON_PATH=/isaac-sim/python.sh<br/>

Spot Training<br/>
Based on the Anymal training scripts **anymal.py** and **anymal_terrain.py** from **omniisaacgymenvs/tasks/**
> PYTHON_PATH scripts/rlgames_train.py task=SpotTerrain num_envs=64 headless=True<br/>

Optional<br/>
> To stream the training for visual inspection add: **enable_livestream=True** <br/>
> To continue training from checkpoint add: **checkpoint= path to checkpoint**<br/>

Spot Demo<br/>
based on the Anymal demo demos/anymal_terrain.py task=AnymalTerrain.<br/>
> PYTHON_PATH scripts/rlgames_demo.py task=SpotTerrain num_envs=64 checkpoint= **path to checkpoint** headless=True enable_livestream=True<br/>


## **Algorithms**
The training was done using 

## **Appendix**

Detailed Description<br/>

The folder **cfg** has the subfolders **task** and **train**.<br/>
Inside the folder **task** we have an YAML file that allows to configure the initial like baseInitState (initial state of the robot) or control parameters, or default joint angles.<br/>
Inside the folder **train** we have an YAML file that allows configuring the parameters of the RL algorithm to be used during training.<br/>

Joint Names

LF_HAA --> front_left_hip_x
LH_HAA --> rear_left_hip_x
RF_HAA --> front_right_hip_x
RH_HAA --> rear_right_hip_x

LF_HFE --> front_left_hip_y
LH_HFE --> rear_left_hip_y
RF_HFE --> front_right_hip_y
RH_HFE --> rear_right_hip_y

LF_KFE --> front_left_knee
LH_KFE --> rear_left_knee
RF_KFE --> front_right_knee
RH_KFE --> rear_right_knee