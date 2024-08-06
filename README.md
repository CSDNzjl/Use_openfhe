# 开发文档

## 开发进度

- 虚拟机，vscode，git安装与配置	√
- openfhe安装、测试与虚拟机备份    √
- API掌握
- C++文件操作
- 程序设计与开发

## 开发环境

- ubuntu-24.04-desktop-amd64  
- VMware Workstation 16 Player
- gcc 13.2.0
- Visual Studio Code 1.92.0
- openfhe v.1.2.0
- git 2.43.0

## 配置环境

### VMware&Ubuntu安装

- [Windows10系统安装Linux虚拟机（Ubuntu）超详细教程_win10自带虚拟机安装ubuntu-CSDN博客](https://blog.csdn.net/weixin_43525386/article/details/108920902)
- [VMware虚拟机下安装Ubuntu20.04（保姆级教程）_ubuntu 20.04 虚拟机-CSDN博客](https://blog.csdn.net/qq_45657288/article/details/116084337)

### vscode安装

- [Ubuntu 22.04安装Visual Studio Code(VS Code)_ubuntu22.04安装vscode-CSDN博客](https://blog.csdn.net/u010044182/article/details/128977610)

- [Ubuntu20.04使用终端安装deb格式安装包教程（新人必备）_ubuntu20.04 deb wen jian ru he yun xing-CSDN博客](https://blog.csdn.net/Xeno233/article/details/118278311)

- sudo dpkg -i 文件名称.deb   安装deb格式安装包

### vscode环境配置

- (**存在一些问题**)     只能使用**ctrl+alt+n**或**./name**进行调试

- linux安装gcc  sudo apt-get install build-essential 检验:gcc --version
- [Linux环境使用VSCode调试简单C++代码_linux vscode c++-CSDN博客](https://blog.csdn.net/hypc9709/article/details/129413482?ops_request_misc=&request_id=&biz_id=102&utm_term=vscode使用C++linux环境&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-129413482.142^v100^pc_search_result_base5&spm=1018.2226.3001.4187)
- [【Linux】 VScode创建第一个C++程序 配置环境（图文教程）_在linux系统中如何调用vscode创建cpp文件-CSDN博客](https://blog.csdn.net/qq_41539778/article/details/122099689?ops_request_misc=&request_id=&biz_id=102&utm_term=vscode使用C++linux环境&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-122099689.142^v100^pc_search_result_base5&spm=1018.2226.3001.4187)

### git安装与仓库克隆

- [【Ubuntu安装git与git clone远程仓库】_ubuntu git clone-CSDN博客](https://blog.csdn.net/qq_41174671/article/details/124646723?ops_request_misc=%7B%22request%5Fid%22%3A%22172283775016800178531711%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=172283775016800178531711&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-124646723-null-null.142^v100^pc_search_result_base8&utm_term=ubuntu克隆仓库&spm=1018.2226.3001.4187)

### 虚拟机备份

- [把VMware虚拟机从一台电脑复制到另一台电脑_vm虚拟机备份一个还原到其他机器上-CSDN博客](https://blog.csdn.net/zsxy2019/article/details/120859129)

## 库学习

[openfheorg/openfhe-development：这是 OpenFHE 库的开发仓库。当前（稳定）版本为 v1.2.0（2024 年 6 月 25 日发布）。 (github.com)](https://github.com/openfheorg/openfhe-development?tab=readme-ov-file)

### 安装与测试

[在 Linux 上安装 OpenFHE — OpenFHE 文档 (openfhe-development.readthedocs.io)](https://openfhe-development.readthedocs.io/en/latest/sphinx_rsts/intro/installation/linux.html)

[OpenFHE 中的 CMAKE — OpenFHE 文档 (openfhe-development.readthedocs.io)](https://openfhe-development.readthedocs.io/en/latest/sphinx_rsts/intro/installation/cmake_in_openfhe.html)

```c++
cmake //用于生成构建系统makefile和cmakelist.txt
make //编译项目并进行连接生成可执行程序，使用makefile
cmake不用重新运行，make会自动检测更改

bin/examples/pke/simple-integers//运行示例代码
    
//用户可以为自己的 OpenFHE 应用程序开发创建 CMake 环境。 只需将 OpenFHE 源树中的文件CMakeLists.User.txt复制到 CMakeLists.txt源树中，并将您自己的程序的 CMake 指令添加到文件的末尾。
    
//库的每个组件（core、pke、trapdoor 等）都有自己的 CMakeLists.txt 文件。这些文件中的每一个都包含在主 OpenFHE CMakeLists.txt 文件中。所有这些组件CMakeList.txt文件的结构是相同的：
    /*确定内置于组件库中的文件
    设置 include 目录以构建组件库
    从 OpenFHE 版本号设置版本号
    添加规则以在组件库中构建对象
    添加规则以构建和安装组件库，包括动态和静态
    如果单元测试包含在生成中，请添加规则以生成单元测试
    添加规则，将 demo 目录下的所有源文件构建到 demos 中
    添加目标以构建组件各个部分的“所有”*/
```

### 库的使用与API调用

#### 暂时设想1（瑕疵）

1. 在`/home/luffy/桌面/openfhe/openfhe-development/src/pke/examples`下创建try.cpp文件
2. 终端执行make生成可执行程序（自动运行cmake生成构建系统）
3. 终端运行`bin/examples/pke/simple-integers-try`得到运算结果

#### 暂时设想2

构建CMakeLists.User.txt自行添加cmake指令单独执行，与源码分离

## 注意事项

- 账户：luffy 密码：luffy123

- ctrl+alt鼠标退出虚拟机
- ctrl+alt+T打开终端
- ctrl+alt+n编译运行

## 疑问

- make和cmake是用来做什么的

# 附录

### VSCODE配置代码

#### tasks.json

```c++
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "g++",
            "args": [
                "-g",
                "try.cpp"
            ],
            "group": "build"
        },
        {
            "type": "cppbuild",
            "label": "C/C++: gcc 生成活动文件",
            "command": "/usr/bin/gcc",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ]
}
```

#### c_cpp_properties.json

```c++
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "linux-gcc-x64"
        }
    ],
    "version": 4
}
```

