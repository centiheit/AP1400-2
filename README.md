### 仓库说明

这个仓库主要用于记录学习C++的AP1400-2课程，这个课程来自AmirKabir University of Technology，其中包括了六道题，我在完成这几道题的过程中也在网上参考了部分别人的解题方法，感觉或多或少都有些bug或者是我认为不是很好理解的地方，所以觉得需要把自己的结果记录一下。

- 课程仓库地址：https://github.com/courseworks

### 调试环境

课程使用了Docker管理环境，我自己是在Windows环境下进行调试和运行，这里记录一下在Windows环境下的调试流程。

1. 下载Docker并在VSCode中安装Docker插件，这样之后基本就不需要使用Docker的客户端了。至于Docker的原理可以参考以下：[Docker 10分钟快速入门](https://www.bilibili.com/video/BV1s54y1n7Ev?vd_source=c1a4fe488e28c685f3d2b18671221525)

2. 以HW1为例，对其进行调试时进入其目录AP1400-2-HW1随后在命令行依次执行命令：

   ``````powershell
   >>> docker build -t ap1400-2:hw1 .
   >>> docker run -p 8080:8080 -d ap1400-2:hw1
   ``````

​	随后可以在插件中打开对应容器的log以查看测试用例的运行情况和报错信息。

3. 下一次调试前，执行命令：

   ``````powershell
   >>> docker stop $(docker ps -aq); docker rm $(docker ps -aq); docker rmi ap1400-2:hw1
   ``````

   用以将之前的容器停止运行并删除，将之前生成的镜像删除，以便下一次执行步骤2中的命令。

