# ros_debug_vscode
:star: **UPDATE:** As of [31 aug 2019](https://discourse.ros.org/t/updating-the-vs-code-extension-for-ros-to-0-6-0/10508) the
debug functionalities described below are also included in the official ros [vscode extension](https://marketplace.visualstudio.com/items?itemName=ms-iot.vscode-ros). A guide on how to use this extension and its ROS debug functionality can be found [here](https://discourse.ros.org/t/updating-the-vs-code-extension-for-ros-to-0-6-0/10508).

### Goal
The goal for this project is to demonstrate the debugging ROS node implementation using VSCode, but of course, the underlying compiler is g++ and debugger is C++ debugger, the VSCode is IDE invoking these underlying tools. My [blog post](https://medium.com/@weihang.che/ros-node-debugging-b76fc38ba70b) contains a bit more info.

### Project Content
This project contains an example project structure followed by the [catkin workspace creation](http://wiki.ros.org/ROS/Tutorials/catkin/CreatingPackage)
and it contains implementation for [talker and listener](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29).

## How to run
1. remove the "devel" and "build" folders, rebuild using "catkin_make -DCMAKE_BUILD_TYPE=Debug"
2. run "talker" as rosnode
3. find out the process id of the talker process
4. modify the ".vscode/launch.json", by replacing "25159" with the id obtained from previous step
5. set some break points in the "src/talker.cpp", start debugger from vscode and be happy

## Troubleshooting

### Catkin build -DCMAKE_BUILD_TYPE equivalent command
When you use `catkin build` instead of `catkin make` you can specify the build type by using the `catkin config -DCMAKE_BUILD_TYPE=Debug` command.

### How to use in a singularity image 
When you want to debug a ROS package that was built inside a singularity container, you have to make sure that the working directory while executing the `build` command and the working directory you opened inside *vscode* to debug are equal. This is because, in a singularity image, folders on the `home` and `root` folder can be accessed both by their absolute and relative paths. This can lead to path inconsistencies between the build package and the package scripts you are debugging.
