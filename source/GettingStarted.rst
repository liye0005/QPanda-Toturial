快速入门
==============

.. _pyqpanda: https://qpanda-2.readthedocs.io/zh_CN/doucmentation-python/
QPanda2提供了C++ 和 Python两个版本，本文中主要介绍C++版本的使用。
如要了解和学习python版本的使用请移步 pyqpanda_。

编译环境
>>>>>>>>>

QPanda-2是以C++为宿主语言，其对系统的环境要求如下：

.. list-table::

    * - software
      - version
    * - CMake
      - >= 3.1
    * - GCC
      - >= 5.4.0 
    * - Python
      - >= 3.6.0  


下载QPanda-2
>>>>>>>>>>>>>>>>>

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

4. 解压下载的文件，就会看到我们的QPanda-2项目， 下面就以linux系统为例简单介绍QPanda2的使用。

    .. code-block:: c
    
        $ cd qpanda-2
        $ mkdir build
        $ cd build
        $ cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. 
        $ make
    
安装
>>>>>>>>

编译完成后，安装就简单的多，只需要输入以下命令：

    .. code-block:: c

        $ make install

开始量子编程
>>>>>>>>>>>>>>

现在我们来到最后一关，创建和编译自己的量子应用。

我相信对于关心如何使用QPanda 2的朋友来说，如何创建C++项目，不需要我多说。不过，我还是需要提供CMakelist.txt的示例，方便大家参考。

    .. code-block:: c

        cmake_minimum_required(VERSION 3.1)
        project(testQPanda)
        SET(CMAKE_INSTALL_PREFIX "/usr/local")
        SET(CMAKE_MODULE_PATH  ${CMAKE_MODULE_PATH} "${CMAKE_INSTALL_PREFIX} lib/cmake")

        add_definitions("-std=c++14 -w -DGTEST_USE_OWN_TR1_TUPLE=1")
        set(CMAKE_BUILD_TYPE "Release")
        set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -g -ggdb")
        set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3")
        add_compile_options(-fPIC -fpermissive)
        find_package(QPANDA REQUIRED)
        if (QPANDA_FOUND)

            include_directories(${QPANDA_INCLUDE_DIR}
                            ${THIRD_INCLUDE_DIR})
            add_executable(${PROJECT_NAME} test.cpp)
            target_link_libraries(${PROJECT_NAME} ${QPANDA_LIBRARIES})
        endif (QPANDA_FOUND)


我们接下来通过一个示例介绍QPanda2的使用，此例子构造了一个量子叠加态，在量子程序中依次添加H门和CNOT门，最后对所有的量子比特进行测量操作。此时，将有50%的概率得到00或者11的测量结果。

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

最后，编译，齐活。

    .. code-block:: c

        $ mkdir build
        $ cd build
        $ cmake .. 
        $ make

运行结果如下:

    .. code-block:: c

        00 : 512
        11 : 488 

