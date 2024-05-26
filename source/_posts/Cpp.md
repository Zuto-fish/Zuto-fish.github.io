---
title: C++学习
category: [学习]
tags: [C++]
date: 2021-01-01 12:00:00
---
# C++学习

## 前言

补修一下跟没学一样的C++

熟悉linux的使用

## 工具

- 工欲善其事，必先利其器
  cmake
  vscode
  git

### cmake使用

**CMakeLists.txt**

```cmake

cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(notebook LANGUAGES CXX)

add_executable(hi src/main.cpp)


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../bin)

#设置可执行文件输出位置

```

然后

```bash

$mkdir-pbuild

$cdbuild

$cmake..

```

这样来生成文件在 build 下面  ".."参数是因为CMakeLists在上一级目录

然后只需要

`cmake --build build`

就可以了

#### 配置方式

在使用 CMake 构建的项目中，组织代码和构建目录的结构通常有一定的惯例。这些惯例有助于项目的清晰性、可维护性和可扩展性。以下是一个推荐的项目目录结构：

```
MyProject/
├── CMakeLists.txt
├── include/
│   └── MyProject/
│       ├── header1.h
│       ├── header2.h
│       └── ...
├── src/
│   ├── main.cpp
│   ├── source1.cpp
│   ├── source2.cpp
│   └── ...
├── build/
├── tests/
│   ├── CMakeLists.txt
│   ├── test1.cpp
│   ├── test2.cpp
│   └── ...
└── CMakeLists.txt
```

##### 目录和文件解释

- **CMakeLists.txt**: 顶级目录下的 CMake 配置文件，通常包含项目的总体构建配置。
- **include/**: 包含项目的公共头文件。为了避免命名冲突，常常在该目录下创建一个与项目名称相同的子目录（如 `MyProject`）。
- **src/**: 包含项目的源文件和私有头文件。通常包含一个 `main.cpp` 文件以及其他实现文件。
- **build/**: 生成的构建文件和中间文件。这个目录可以不放在版本控制系统中，因为它是由 CMake 和编译器生成的。
- **tests/**: 包含测试代码及相关的 CMake 配置文件。可以有多个测试文件和测试相关的源文件。

##### 示例 CMakeLists.txt

顶级 `CMakeLists.txt` 可能看起来像这样：

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 包含子目录
add_subdirectory(src)
add_subdirectory(tests)
```

在 `src/` 目录中的 `CMakeLists.txt` 可能看起来像这样：

```cmake
# 指定源文件
set(SOURCES
    main.cpp
    source1.cpp
    source2.cpp
)

# 包含头文件目录
include_directories(${PROJECT_SOURCE_DIR}/include)

# 创建可执行文件
add_executable(MyProject ${SOURCES})
```

在 `tests/` 目录中的 `CMakeLists.txt` 可能看起来像这样：

```cmake
# 查找 GTest 库
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# 设置测试源文件
set(TEST_SOURCES
    test1.cpp
    test2.cpp
)

# 创建测试可执行文件
add_executable(MyProjectTests ${TEST_SOURCES})

# 链接 GTest 库
target_link_libraries(MyProjectTests ${GTEST_LIBRARIES} pthread)

# 添加测试
enable_testing()
add_test(NAME MyProjectTests COMMAND MyProjectTests)
```

##### 构建和运行项目

1. 创建并进入 `build/` 目录：

   ```bash
   mkdir -p build
   cd build
   ```
2. 运行 CMake 配置命令：

   ```bash
   cmake ..
   ```
3. 构建项目：

   ```bash
   make
   ```
4. 运行可执行文件（假设可执行文件名为 `MyProject`）：

   ```bash
   ./MyProject
   ```
5. 运行测试：

   ```bash
   make test
   ```

通过这种目录结构和 CMake 配置，项目文件的组织会非常清晰，并且便于管理和扩展。

### vscode使用

vim对我来说上手还是有点困难了，老主要是老是忘记快捷键，所以还是用vscode比较舒服
但是记好vscode的快捷键，会提高效率
尽量让双手不要离开键盘

#### 个人常用的vscode的快捷键

- `Ctrl + Shift + P` 打开命令面板
- `>Preferences: Open Keyboard Shortcuts (JSON)` 打开快捷键配置文件
  也算是用上了一些比较舒适的插件
- `>Extensions` 打开插件市场
- 基础快捷键
  ctrl+o 打开文件
  ctrl+s 保存文件
  ctrl+e /r 打开文件/文件夹(p也是)
  ctrl+w 关闭当前文件

ctrl+f 全局搜索
ctrl+h 全局替换
enter 替换

ctrl+g 跳转到行

ctrl+f3 跳到下一个
ctrl + home / end 跳到文件开头/结尾

shift+选中代码块
shift+alt+左右箭头 快速扩选
ctrl + space 代码提示

ctrl +tab 切换文件（同一个编辑器之间）

ctrl+alt+左右 切换标签页位置
单纯按住ctrl+alt 切换焦点到左上角的标签页
将焦点切换到侧边栏，按下ctrl+alt+j、k 切换标签页位置

ctrl + shift + e 打开文件管理器
（单纯加e就是最近打开的文件）
ctrl + shift + g 打开git

ctrl +alt + k  书签（这是插件）

将焦点移到终端，按下ctrl+` 打开终端 切换回编辑器，按下ctrl+` 关闭终端
在编辑器之间切换，按下ctrl+1、2、3...

按住ctrl可以快速跳转

#### 插件推荐

- Clangd 代码补全

### git使用

#### 基本使用

git config的一些东西->这里的邮箱是虚拟的

````bash
git config --global user.name name
git config --global user.email mail
去掉参数就是查看

git init
初始化,创建版本库

````

#### 使用逻辑

首先是文件分区

我们能直接看到的这个文件夹里面的所有文件就是工作区

初始化后会新建一个*.git*文件夹，这是版本库

git add 是把文件添加到了 暂存区 *stage*

而commit 命令将其提交到了 版本库中

````bash
添加文件或目录到缓存区域
git add <file>
git add . //添加所有

提交缓存区域文件到版本库
git commit -m “what I have done”

git diff 查看做出了哪些修改
git log 产看提交记录 加 --preety=online 简化
````

回退

```bash
git reset --hard HEAD^ 回退一个版本 这里是改指针，可以切回去

取消工作区：
git checkout -- <file> （回到暂存区域，没有--则是版本库）

取消暂存区域
git reset HEAD <file>  删除暂存区域

```

下面是一些分支方面的命令

```bash
git branch -v  //查看
git branch <branch name> 创建分支

git checkout <branch name>

git merge <branch name>  把指定分支合并到当前分支
```

- 冲突合并
  原因：两处都修改了同一个地方
  现象：会提示你冲突文件，冲突文件会有奇奇怪怪的标记，此时，你会发现自己正处于 MERGING 状态
  解决方案：手动去修改就行了
- git手动更改后，需要的是 commit,这个时候后面就不能带文件名了
  合并完成之后自然也是只会改变当前的这个状态
  启示：Git 底层是head指针

#### Github

```bash
git remote  //创建别名
	-v //查看有哪些别名
	add <别名> <库地址> 

操作方面
最基础的俩
git push <仓库（可以用别名）>  <分支>   //这个是推送
git pull <仓库（可以用别名）>  <分支>  //拉取

克隆是不需要登录的

拉取代码，初始化仓库，创建别名-> 一步到位
别名会创建成 origin

```

### Gtest

主要是有些时候做一些题目会用到

- 单元测试框架
- 主要是用来测试函数的功能是否正确
- 一般来说，单元测试的目的是为了保证代码的质量，提高代码的可靠性
  使用方法：

```c++
#include <gtest/gtest.h>

// 测试函数示例
TEST(MyTestSuite, MyTestCase) {
    // 断言示例
    EXPECT_EQ(2 + 2, 4);
    ASSERT_TRUE(true);
    // 添加更多的断言
}

// 测试用例可以包含多个测试函数
TEST(MyTestSuite, AnotherTestCase) {
    // 测试逻辑
}
```

主函数

```c++
int main(int argc, char** argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

- 运行测试用例：`./a.out`
- 输出：

```
[==========] Running 2 tests from 1 test suite.
[----------] Global test environment set-up.
[----------] 2 tests from MyTestSuite
[ RUN      ] MyTestSuite.MyTestCase
[       OK ] MyTestSuite.MyTestCase (0 ms)
[ RUN      ] MyTestSuite.AnotherTestCase
[       OK ] MyTestSuite.AnotherTestCase (0 ms)
[----------] 2 tests from MyTestSuite (0 ms total)

[----------] Global test environment tear-down
[==========] 2 tests from 1 test suite ran. (0 ms total)
[  PASSED  ] 2 tests.
```

- 注意：
  - 单元测试框架的命名空间为 `testing`

## cs106L

- 这门课是UCSD的课程，主要是教C++的语法和一些基本的算法，还有一些数据结构的知识
- 课程内容主要是C++语法，数据结构，算法，还有一些系统编程的知识
- 课程的难度不高，但内容还是比较丰富的，可以作为C++学习的入门课程

### Stream

## C++知识

- 由于之前已经粗略学习过一次，本次主要以边写边学为基本方式，以及阅读一些参考书
  所以并不会按照由浅入深主要是分板块

### 文件操作

在Linux下，文件操作主要有以下几种方式：

- 标准C库函数：如fopen、fclose、fread、fwrite等。
- 文件描述符：通过文件描述符可以操作文件，如open、close、read、write等。
- 文件句柄：通过文件句柄可以操作文件，如fopen、fclose、fread、fwrite等。
- 系统调用：通过系统调用可以操作文件，如open、close、read、write等。

在C++中，文件操作主要有以下几种方式：

- 标准库：如ifstream、ofstream、fstream等。
- 文件描述符：通过文件描述符可以操作文件，如open、close、read、write等。
- 文件句柄：通过文件句柄可以操作文件，如fopen、fclose、fread、fwrite等。
- 系统调用：通过系统调用可以操作文件，如open、close、read、write等。
