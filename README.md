# 16-662 Robot Autonomy
## Desktop Setup

### Install Prerequisites:
- **Setup Docker:** 
   - [Install Docker](https://docs.docker.com/engine/install/ubuntu/)
   - [Install Nvidia Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
   - (Optional) Add docker to [sudoers](https://docs.docker.com/engine/install/linux-postinstall)\
      Do not forget to logout and login after adding docker to sudoers\
      If not done, please run all docker commands with a `sudo` prefix.

- **Setup Frankapy:**\
   Follow instructions from the official [frankapy](https://github.com/iamlab-cmu/frankapy) repository and clone the frankapy repository at `/home/student`


### Setup the PC:
1. Clone the [16662_RobotAutonomy](https://github.com/vib2810/16662_RobotAutonomy) repository at `/home/student`
   ```bash
   git clone git@github.com:vib2810/16662_RobotAutonomy.git
   ```

2. Build the Docker Container:
   ```
   cd 16662_RobotAutonomy
   docker build -t frankapy_docker .
   ```

### Running Demo Code:
**Note:** Replace `[control-pc-name]` with the name of the control pc, for example, `iam-snowwhite`
1. Unlock robot joints
   ```bash
   ssh -X student@[control-pc-name]
   google-chrome
   ```
   In google chrome open `https://172.16.0.2/desk/` and press `Click to unlock joints`
      
2. Run the start_control_pc script from the frankapy package
   ```bash
   cd <frankapy package directory>
   bash ./bash_scripts/start_control_pc.sh -u student -i [control-pc-name]
   ```
   This should launch 4 terminals which sets up frankapy to communicate with the robot.
   
   **Note:** While developing, it might be a good idea to start `roscore` separately in a different terminal and then launch the above script. This allows frankapy to be reset without killing development nodes. When `roscore` is started separately, only 3 terminals open instead of 4, and to reset frankapy communication, just kill the 3 terminals and rerun the script.
   
4. **Running the Docker Container:**
   - Run the Docker Container. In a new terminal:
      ```bash
      cd frankapy_docker
      bash run_docker.sh
      ```

   - Attach a terminal connected to the Docker Container:
      ```bash
      cd frankapy_docker
      bash terminal_docker.sh
      ```

5. **Run the MoveIt Server:** <br>
    In a new terminal
    ```bash
    bash terminal_docker.sh
    roslaunch manipulation demo_frankapy.launch
    ```

6. **Run the demo_moveit.py script:** <br>
    In a new terminal
    ```bash
    bash terminal_docker.sh
    rosrun manipulation demo_moveit.py
    ```
    The script initially displays a planned path on rviz. Please checkout the comments in the main function in the demo_moveit.py script to run this script on the robot.  

### Other Useful Commands:
- To grant edit permissions for files created inside the docker container (in the `/data` shared volume)
   ```bash
   bash claim_files.sh
   ```
