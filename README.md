# ros_debug_vscode

### Goal
The goal of this project is to demonstrate how you can debug a C++ or python ROS Node in VSCode. While the debugging is done in the VSCode IDE, it uses the g++ compiler and C++ debugger tools under the hood. My [blog post](https://medium.com/@weihang.che/ros-node-debugging-b76fc38ba70b) contains a bit more info.

### Project Content
This project contains an example ROS project catkin_ws [catkin workspace](http://wiki.ros.org/ROS/Tutorials/catkin/CreatingPackage) in which two simple [talker and listener ROS nodes](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29) are present. Both a python version as a C++ version of these nodes is included in the project.

### C++ debugging steps

#### How to run
1. Remove the "devel" and "build" folders, rebuild using `catkin_make -DCMAKE_BUILD_TYPE=Debug`
2. Run "talker" as rosnode
3. [Find out the process id of the talker process](https://askubuntu.com/questions/180336/how-to-find-the-process-id-pid-of-a-running-terminal-program).
4. Modify the ".vscode/launch.json", by replacing "25159" with the id obtained from the previous step.
5. Set some breakpoints in the "src/talker.cpp", start debugger from vscode and be happy

### Python debugging steos

#### How to run
1. Make sure the [vscode-python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python) is installed.
2. Add the followin code snippet directly after your python includes.

```python
#################################################
## ptvsd Debugger initiation snippet ############
#################################################

## Import the ptvsd module ##
import ptvsd

## Allow other computers to attach to ptvsd at this IP address and port. ##
ptvsd.enable_attach(address=('127.0.0.1', 5678), redirect_output=True)

## Pause the program until a remote debugger is attached ##
ptvsd.wait_for_attach()
#################################################
```

3. Modify the ".vscode/launch.json",  by changing the `port` and `host` to the ones you specified in the code snippet.
4. Run the "Python: Remote attach" configuration and be happy.

### Troubleshooting

#### Catkin build -DCMAKE_BUILD_TYPE equivalent command
When you use `catkin build` instead of `catkin make` you can specify the build type by using the `catkin config --cmake-args -DCMAKE_BUILD_TYPE=Debug` command.

#### How to use in a singularity image 
When debugging a ROS Node in a singularity container the working directory while executing the `build` command and the working directory while debugging inside `vscode` have to be equal. This is because, in a singularity image, folders on the `home` and `root` folder can be accessed both by their absolute and relative paths. This can lead to path inconsistencies between the build package and the package scripts you are debugging.
