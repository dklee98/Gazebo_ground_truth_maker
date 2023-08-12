# Voxblox Ground Truth
Convert Gazebo worlds to the ground truth files:
* voxblox TSDF maps
* pcd files
* ply files 

## Install
Make sure that [voxblox](https://github.com/ethz-asl/voxblox#table-of-contents) and [gazebo](http://gazebosim.org/tutorials?tut=ros_installing) are installed, then run
```bash
cd ~/catkin_ws
catkin build voxblox_ground_truth
source devel/setup.bash
```

## Gazebo plugin
#### Demo
Start the demo by running
```bash
roslaunch voxblox_ground_truth gazebo_plugin_demo.launch
```
Then wait for Gazebo and Rviz finish loading. Once they're ready, call
```bash
# tsdf output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/voxblox_ground_truth_demo.tsdf'"
# pcd output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/voxblox_ground_truth_demo.pcd'"
# ply output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/voxblox_ground_truth_demo.ply'"
```

The ground truth TSDF / pcd / ply map will now be available in your home folder as `~/voxblox_ground_truth_demo.xxx`.

#### Your own world
In order to use the plugin, it must be loaded as part of your Gazebo world.

To do this, add the following line to your `.world` file right after the `<world name='default'>` tag:
```xml
<plugin name="voxblox_ground_truth_plugin" filename="libvoxblox_ground_truth_plugin.so"/>
```

For an example, see the provided [sample.world](https://github.com/ethz-asl/voxblox_ground_truth/blob/8f868dc4290ebaffa8b4c6435491f3cfa386783d/sample_data/gazebo/worlds/burning_building_rubble.world#L4-L5).

Once your world is ready, launch your simulation in the same way you normally would.

Next, set the desired voxel size with
```bash
rosparam set /voxblox_ground_truth/voxel_size 0.05
```

And finally generate the ground truth map with
```bash
# tsdf output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/your_ground_truth_map.tsdf'"
# pcd output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/your_ground_truth_map.pcd'"
# ply output
rosservice call /gazebo/save_voxblox_ground_truth_to_file "file_path: '$HOME/your_ground_truth_map.ply'"
```
