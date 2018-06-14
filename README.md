# ros_debug_vscode

### Goal
The goal for this project is to demonstrate the debugging ROS node implementation using VSCode, but of course the underlying compiler is g++ and debuger is C++ debugger, the VSCode is IDE invoking these underlying tools. My [blog post](https://medium.com/@weihang.che/ros-node-debugging-b76fc38ba70b) contains a bit more info.


### Project Content
this project contains project structure followed by the [catkin workspace creation](http://wiki.ros.org/ROS/Tutorials/catkin/CreatingPackage)
and it contains impelmentation for [talker and listener](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29).

## How to run
1. run "talker" as rosnode
2. find out the process id of the talker process
3. modify the ".vscode/launch.json", by replacing "25159" with the id obtained from previous step
4. set some break points in the "src/talker.cpp", start debugger from vscode and be happy
