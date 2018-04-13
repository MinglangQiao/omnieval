# omnieval
Gives the user the ability to convert omnidirectional images/video (yuv format) from one representation to another. For example, can convert an equirectangular video to a mercator video. Moreover, the difference in quality between the two videos can be computed. The user can choose between weighted and unweighted mean square error comparisons. Note that code can also be used to cutout a viewport (e.g., corresponding to the view seen through a head mounted display). 

Build
--------------
Remapping from one representation to another:
```
cd remap
mkdir build
cd build
cmake ../
make
```
Comparing two representations:
```
cd compsph
mkdir build
cd build
cmake ../
make
```
如果报错
```
/usr/bin/ld: 找不到 -lopencv_dep_cudart
```
这么解决, opencv版本为4.3也没问题：
```
cmake -D CUDA_USE_STATIC_CUDA_RUNTIME=OFF ../
```
[认真看别人的教程和解决办法，不要加错地方了](https://github.com/opencv/opencv/issues/6542)
-s 命令需要改源码， 找到yuv的某一帧的启始位置，读出那一帧的数据

Usage
--------------
Reamap: 注意不能当作命令执行时， 需要右击》》 权限 》》 勾选允许作为程序执行文件


Example 1: conversion from equirectangular (2048x1024) to equalarea (1024x512):
```
./remap -i rect -o eqar -m 1024 -b 2048 -n 512 -v 1024 rect.yuv eqar.yuv
```

Example 2: comparing an equirectangular (2048x1024) and an equalarea (1024x512) representation using using equal weighting:
```
./compsph -i rect -o eqar -m 1024 -b 2048 -n 512 -v 1024 rect.yuv eqar.yuv sphere_655362.txt
```

Example 3: comparing an equirectangular (2048x1024) and an equalarea (1024x512) representation using latitude weighted points:
```
./compsph -i rect -o eqar -m 1024 -b 2048 -n 512 -v 1024 -w latweights.txt rect.yuv eqar.yuv sphere_655362.txt
```

Note
--------------
This code builds on Environment Mapping Tools, created by Robert Kooima: https://github.com/rlk/envtools
