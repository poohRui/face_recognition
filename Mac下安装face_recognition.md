# 安装 face_recognition

> 参考[博客](http://blog.csdn.net/hongbin_xu/article/details/76284134)，整个安装基于mac os

## 环境搭建

* python：python3/python2

* pip：和python版本对应的pip

* cmake

  * 检测

    在控制台输入命令`cmake`，显示`command not found`指令不存在，需要进行下面的安装。

  * 直接在cMake[官方](https://cmake.org)下载，下载成功后，运行安装，启动后，在左上角有`Tools`下有选项`How to install For Command Line Use`，点击后有提示，选择其中的任意一种方法加入cmake指令。

  * (在Ubuntu下，可直接使用`sudo apt-get install cmake`安装）

* boost

  * [官网下载`boost_1_65_1.tar.bz2`](http://www.boost.org/users/download/)

  * 解压

    ```
    tar jxvf boost_1_65_1.tar.bz2
    ```

  * 执行

    ```
    sudo ./bootstrap.sh --with-libraries=python --with-python=PYTHON3
    ```

    只需要安装`boost.python`，整个`boost`有点大。

    其中因为系统自带`python2.7`， 为了不使用默认的python版本，加`--with-python=PYTHON3`来指定使用python3，若使用系统默认的`python2`可以忽略这一句。

    注：如果python版本不一致，后面会出错，也可以通过修改boost目录下的`project-config.jam`文件来改配置，[参考这里](https://stackoverflow.com/questions/5539557/boost-and-python-3-x)。

    ```
    sudo ./b2
    ```

    执行完，控制台会提示

    > The following directory should be added to compiler include paths:
    >
    > ​    `/Path/to/boost_1_65_1`
    >
    > The following directory should be added to linker library paths:
    >
    > ​    `/Path/to/boost_1_65_1/stage/lib`

    需要将上面两个路径加到环境变量中，具体参考[这里](http://www.jianshu.com/p/36bf7a56b808)

    注：环境变量一般配置在根目录下的`.bashrc`文件中，修改完使用`source ~/.bashrc`命令使其立即生效，用`echo $PATH`可打印目前环境变量的所有配置。

    ```
    sudo ./b2 install
    ```

    完成。

* dlib

  * 下载，从github上clone下来

    ```
    git clone https://github.com/davisking/dlib.git
    ```

  * 编译dlib

    ```
    cd dlib
    ```

    ```
    mkdir build
    ```

    ```
    cd build
    ```

    ```
    cmake .. -DDLIB_USE_CUDA=0 -DUSE_AVX_INSTRUCTIONS=1
    ```

    ```
    cmake --build .
    ```

  * 编译并安装python的拓展包

    ```
    cd ..    //回到dlib根目录
    ```

    ```
    python3 setup.py install --yes USE_AVX_INSTRUCTIONS --no DLIB_USE_CUDA
    ```


  * 检测是否安装成功

    进入python交互环境，使用`import dlib`，如果不报错则安装成功，如果报错一般问题出在安装boost上，python版本不匹配，环境变量配置错误都有可能。

* face_recognition

  ````
  pip3 install face_recognition
  ````