## 简介

本软件开发工具包应用于Innfos胶子系列，用于实现机械臂的二次开发，提供运动功能接口，目前支持类型GL_6L3

## 下载

目前支持linux-x86-64版本和linux-树莓派版本

x86-64版本：
推荐使用64位ubuntu16.04、ubuntu18.04等系统
访问该链接[download link](https://github.com/innfos/innfos-gluon-cpp-sdk.git)下载机械臂软件或者直接执行以下命令
```sh
$ git clone https://github.com/innfos/innfos-gluon-cpp-sdk.git
```
树莓派版本：
适用于Raspberry Pi 3 Model B 和 Raspberry Pi 3 Model B+
访问该链接[download link](https://github.com/innfos/innfos-gluon-cpp-sdk-raspi.git)下载机械臂软件或者直接执行以下命令
```sh
$ git clone https://github.com/innfos/innfos-gluon-cpp-sdk-raspi.git
```

## 使用

软件开发工具包中包含示例程序,用户可先编译示例程序了解使用方法，具体函数介绍可移步至[函数说明](https://innfos.com/instructions/html/index.html)

在编译之前请务必先查看example/src下的basic和advanced下的cpp文件，并配合函数说明文档，待了解每个函数作用后，开始编译示例程序
进入下载目录，执行：
```sh
$ cd innfos-gluon-cpp-sdk/example
$ mkdir build
$ cmake ..
$ make 
```
此时在example/bin 文件夹下会产生两个文件夹basic和advanced
basic文件夹中含有shutdown和startup两个可执行文件，分别用于开机使能和关机失能
advanced文件夹中有一个motion可执行文件，该命令执行的逻辑为：
关节运动到指定点
关节增量正方向移动
关节增量负方向移动
直线移动到指定点
沿x轴负方向平移
沿x轴正方向平移
沿y轴负方向平移
沿y轴正方向平移
沿z轴负方向平移
沿z轴正方向平移
绕x轴负方向旋转
绕x轴正方向旋转
绕y轴负方向旋转
绕y轴正方向旋转
绕z轴负方向旋转
绕z轴正方向旋转
圆弧运动至指定点
关节运动回原点
选择是否关机
