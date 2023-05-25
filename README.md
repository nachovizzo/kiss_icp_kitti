# KISS-ICP KITTI-ROS Wrapper

https://user-images.githubusercontent.com/21349875/214578180-b1d2431c-8fff-440e-aa6e-99a1d85989b5.mp4

## Why are you obsessed with KITTI?

KITTI was not originally recorded in a rosbag format. Besides this fact, it has been 1 decade since
the data was released. Why are you trying so hard to use it with ROS? ROS is the **ROBOT** operating
system, it's for **ROBOTS** not to run experiments. If you want to change the KISS-ICP code and
experiment with KITTI, just use the **ORIGINAL** dataset. Why even bother converting all the data to
ROS format!?

Because this makes not sense at all, I removed all ROS-KITTI support from the main branch of
KISS-ICP. If you are still obsessed with doing this type of experimentation the go ahead, and clone
this repository. But I'm **not mantaining it**. Why don't you just `pip install kiss-icp` and enjoy
a nice python/notebook experimnetation framewrok? It's much easier. Leve ROS for robots!

### How to build

```sh
cd ~/catkin_ws/
git clone https://github.com/PRBonn/kiss-icp # <- Optional if you want to change the code
git clone https://github.com/nacho.vizzo/kiss-icp-kitti
catkin build  && source devel/setup.bash
```

### How to run

```sh
roslaunch kiss_icp_kitti kitti.launch bagfile:=<path_to_rosbag>
```

## Citation

If you use this library for any academic work, please cite our original [paper](https://www.ipb.uni-bonn.de/wp-content/papercite-data/pdf/vizzo2023ral.pdf).

```bibtex
@article{vizzo2023ral,
  author    = {Vizzo, Ignacio and Guadagnino, Tiziano and Mersch, Benedikt and Wiesmann, Louis and Behley, Jens and Stachniss, Cyrill},
  title     = {{KISS-ICP: In Defense of Point-to-Point ICP -- Simple, Accurate, and Robust Registration If Done the Right Way}},
  journal   = {IEEE Robotics and Automation Letters (RA-L)},
  pages     = {1-8},
  doi       = {10.1109/LRA.2023.3236571},
  volume    = {8},
  number    = {2},
  year      = {2023},
  codeurl   = {https://github.com/PRBonn/kiss-icp},
}
```


## Related ISSUES

- https://github.com/PRBonn/kiss-icp/issues/79
- https://github.com/PRBonn/kiss-icp/issues/67
- https://github.com/PRBonn/kiss-icp/issues/166
