# pypy 在线实验环境

## 软件简介

软件基本信息，License，所属的类别，作用，特点等。
PyPy是Python解释器和即时编译器。PyPy专注于速度，效率和与原始CPython解释器的兼容性。

PyPy开始是用Python语言编写的Python解释器。当前的PyPy版本从RPython转换为C代码并进行编译。PyPy JIT（“Just In Time”的缩写））编译器能够在运行时将Python代码转换为机器代码。

所属类别是编程语言

特点:

1.速度：由于它的即时编译器，Python程序通常在PyPy上运行得更快

2.内存使用：内存匮乏的Python程序（几百MB或更多）可能会比在CPython中占用更少的空间

3.兼容性： PyPy 与现有的python代码高度兼容。它支持cffi，并且可以运行流行的python库，如twisted 和django

4.Stackless：默认情况下，PyPy支持无堆栈模式，为大量并发提供微线程。

## 软件官网

http://pypy.org/

## Dockerfile 使用方法

Dockerfile在您的Python应用程序项目中创建一个
```
FROM pypy:3-onbuild
CMD [ "pypy3", "./your-daemon-or-script.py" ]
```
或者（如果需要使用PyPy 2）：
```
FROM pypy:2-onbuild
CMD [ "pypy", "./your-daemon-or-script.py" ]
```
这些图像包括多个ONBUILD触发器，这些触发器应该是引导大多数应用程序所需要的。该构建将COPY在该requirements.txt文件RUN pip install上的一个文件，然后将当前目录复制到/usr/src/app。

然后，您可以构建并运行Docker映像：
```
$ docker build -t my-python-app .
$ docker run -it --rm --name my-running-app my-python-app
```
运行一个Python脚本

对于许多简单的单个文件项目，您可能会发现编写完整的不方便Dockerfile。在这种情况下，您可以直接使用Python Docker映像运行Python脚本：
```
$ docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp pypy:3 pypy3 your-daemon-or-script.py
```
或者（再次，如果你需要使用Python 2）：
```
$ docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp pypy:2 pypy your-daemon-or-script.py
```
## 资源链接

- http://pypy.org/
