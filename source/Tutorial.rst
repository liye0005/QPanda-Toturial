下载、编译、安装和使用
======================

下载QPanda-2
------------------

如果在您的系统上已经安装了git， 您可以通过git来获取QPanda2：

    .. code-block:: c

        $ git clone https://github.com/OriginQ/QPanda-2.git


当然了，对于一些未安装git的伙伴来说，也可以直接通过浏览器去下载QPanda-2， 具体的操作步骤如下：

1. 在浏览器中输入 https://github.com/OriginQ/QPanda-2 ， 进入网页会看到：

.. image:: images/QPanda_github.png
    :align: center  

2. 点击 ``Clone or download`` 看到如下界面：

.. image:: images/Clone.png
    :align: center  

3. 然后点击 ``Download ZIP``， 就会完成QPanda2的下载。

.. image:: images/Download.png
    :align: center  

编译和安装
------------------

Windows
>>>>>>>>>>>

在Windows平台下，QPanda-2支持使用Visual Studio和MinGW编译、安装。

Visual Studio 
****************

编译
`````````
这里以Visual Studio 2017为例，使用Visual Studio 2017 编译QPanda-2,只需要安装Visual Studio 2017，并需要在组件中安装CMake组件。安装完成之后，用Visual Studio 2017打开QPanda-2文件夹，即可使用CMake编译QPanda-2。


.. image:: images/VSCompiler.png
    :align: center 

安装
`````````
在QPanda-2编译完成后，用户可以安装QPanda-2，Visual Studio 2017的安装方式很简单，只需要在Cmake菜单中选择安装即可。

.. image:: images/VSInstall.png
    :align: center   


QPanda-2会安装在用户在CMakeSettings.json中配置的安装目录下。安装成功后会在用户配置的的目录下生成install文件夹，里面安装生成include和lib文件。如果有需求，用户可以在Visual Studio的CMakeSettings.json配置文件修改QPanda-2的安装路径。生成CMakeSettings.json的方法如下图所示：

.. image:: images/VSUpdateConfig.png
    :align: center   

修改QPanda-2的安装路径如下图所示：

.. image:: images/VSUpdatePath.png
    :align: center   

参数修改完成后，cmake选项下执行安装，Qpanda-2的lib库文件和include头文件会安装到用户指定的安装位置。(注意：需先进行编译成功后才能进行安装)

MinGW
**********************

编译
`````````

使用MinGW编译QPanda-2，需要自行搭建CMake和MinGW环境，用户可自行在网上查询环境搭建教程。（注意： MinGW需要安装64位版本）

CMake+MinGW的编译命令如下：

1. 在QPanda-2根目录下创建build文件夹
2. 进入build文件夹，打开cmd
3. 由于MinGW对CUDA的支持存在一些问题，所以在编译时需要禁掉CUDA，输入以下命令：

.. code-block:: c

    cmake -G"MinGW Makefiles" -DFIND_CUDA=OFF -DCMAKE_INSTALL_PREFIX=C:/QPanda2 ..
    mingw32-make


安装
`````````

在QPanda-2编译完成后，用户可以安装QPanda-2，安装命令如下：

.. code-block:: c

    mingw32-make install

Linux 和 MacOS
>>>>>>>>>>>>>>>

编译
*******

1. 进入QPanda-2根目录
2. 输入以下命令：

.. code-block:: c

    mkdir -p build
    cd build
    cmake ..
    make

如果有需求，用户通过命令修改QPanda-2的安装路径，配置方法如下所示：

.. code-block:: c

    mkdir -p build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local ..
    make


安装
*******

在Linux和MacOS下安装命令QPanda-2，命令是一样的，安装命令如下：

.. code-block:: c

    sudo make install


使用
------------------

我们接下来通过一个示例介绍QPanda-2的使用，下面的例子可以在量子计算机中构建量子纠缠态(|00>+|11>)，对其进行测量，重复制备1000次。
预期的结果是约有50%的概率使测量结果分别在00或11上。

    .. code-block:: c

        #include "QPanda.h"
        #include <stdio.h>
        using namespace QPanda;
        int main()
        {
            init(QMachineType::CPU);
            QProg prog;
            auto q = qAllocMany(2);
            auto c = cAllocMany(2);
            prog << H(q[0])
                << CNOT(q[0],q[1])
                << MeasureAll(q, c);
            auto results = runWithConfiguration(prog, c, 1000);
            for (auto result : results){
                printf("%s : %d\n", result.first.c_str(), result.second);
            }
            finalize();
        }

示例程序的编译方式与编译QPanda库的方式基本类似，在这里就不多做赘述。我们在QPanda-2的github库中添加了 `Template <https://github.com/OriginQ/QPanda-2/tree/master/Template>`_ 文件夹，用于展示各个平台的使用案例。

用户也可以使用g++编译test.cpp，编译命令如下所示：

    .. code-block:: c

        g++ -std=c++14  test.cpp  -I{安装目录}/include -I{安装目录}/include/ThirdParty/ -L{安装目录}/lib/  -lQPanda2 -lTinyXML -fopenmp -o test


编译之后的可执行文件会生成在build下的bin文件夹中，进入到bin目录下就可以执行自己编写的量子程序了。


计算结果如下所示：
    
    .. code-block:: c

        00 : 493 
        11 : 507
