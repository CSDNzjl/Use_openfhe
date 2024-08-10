# 开发文档

## 开发进度

- 虚拟机，vscode，git安装与配置	√
- openfhe安装、测试与虚拟机备份    √
- 示例代码用途
- 构建用户应用程序    √
- 用户输入输出程序

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

### 客户端实现

#### 暂时设想1（舍弃）

1. 在`/home/luffy/桌面/openfhe/openfhe-development/src/pke/examples`下创建try.cpp文件
2. 终端执行make生成可执行程序（自动运行cmake生成构建系统）
3. 终端运行`bin/examples/pke/simple-integers-try`得到运算结果

#### 暂时设想2

构建CMakeLists.User.txt自行添加cmake指令单独执行，与源码分离

#### 测试流程（参考附录）

- 参考内容：[构建用户应用程序 — OpenFHE 文档 (openfhe-development.readthedocs.io)](https://openfhe-development.readthedocs.io/en/latest/sphinx_rsts/intro/building_user_applications.html)
- User文件夹与下属的文件夹都需要有CMakeLists.txt文件

#### 编写程序与示例解决问题

- [适合初学者！超详细的vscode的C++自定义头文件的配置！_vscode中c++无法正确导入自定义头文件-CSDN博客](https://blog.csdn.net/Lee_zj123/article/details/126868863)（缺少指定文件，此路不通）
- [示例 — OpenFHE 文档 (openfhe-development.readthedocs.io)](https://openfhe-development.readthedocs.io/en/latest/sphinx_rsts/intro/quickstart.html#pke-simd-fhe)  ==示例代码解决的问题==

### 使用库

1. 选择要使用的方案  BFVrns	BGVrns	CKKSrns

2. 创建CryptoContext（openfhe中的所有事情都是通过CryptoContext来完成的）

   > - 运行参数生成函数，或者运行
   >   - 确定晶格参数（环尺寸、模量大小）
   >   - 确定编码参数（明文模数）
   >   - 确定特定于方案的参数
   >
   > - 启用您想要使用的算法，例如，
   >   - Enable（ENCRYPTION） - 允许密钥生成和加密/解密
   >   - Enable（PRE） - 允许使用代理重新加密
   >   - Enable（SHE） - 启用 SHE 操作，例如 EvalAdd 和 EvalMult
   >   - Enable（MULTIPARTY） - 启用阈值 FHE 操作

3. 序列化和反序列化

   > 由 CryptoContext 创建的对象通常具有一种方法，该方法将对象转换为可以保存到字符串或磁盘文件中的谷物对象：`Serialize`

- **服务端生成的文件**：
  - `cryptocontext.txt`
  - `key_pub.txt`
  - `key_mult.txt`
  - `key_rot.txt`
  - `ciphertext1.txt`
  - `ciphertext2.txt`
- **客户端生成的文件**：
  - `ciphertextMult.txt`
  - `ciphertextAdd.txt`
  - `ciphertextRot.txt`
  - `ciphertextRotNegLocation.txt`
  - `ciphertextVectorFromClient.txt`
- **服务端读取的文件**：
  - `ciphertextMult.txt`
  - `ciphertextAdd.txt`
  - `ciphertextRot.txt`
  - `ciphertextRotNegLocation.txt`
  - `ciphertextVectorFromClient.txt`

### 示例程序

[openfhe-development/src/pke/examples/README.md 在 main ·openfheorg/openfhe-development (github.com)](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/README.md#generating-cryptocontext-using-gencryptocontext)

- [advanced-ckks-bootstrapping.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/advanced-ckks-bootstrapping.cpp)：一个示例，显示 CKKS 引导用于具有稀疏打包的密文
- [advanced-real-numbers.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/advanced-real-numbers.cpp)：展示了使用 CKKS 的近似同态加密的几个高级示例
- [advanced-real-numbers-128.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/advanced-real-numbers-128.cpp)：展示了使用高精度 CKKS 的近似同态加密的几个高级示例==无法使用==
- [ckks-noise-flooding.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/ckks-noise-flooding.cpp)：演示了在 CKKS 中使用实验性特性NOISE_FLOODING_DECRYPT模式，以增强安全性
- [depth-bfvrns.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/depth-bfvrns.cpp)：演示如何使用 BFVrns 方案进行基本同态加密

- [depth-bfvrns-behz.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/depth-bfvrns-behz.cpp)：演示如何使用 BEHZ BFV 变体进行基本同态加密
- [depth-bgvrns.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/depth-bgvrns.cpp)：演示如何使用 BGVrns 方案进行基本同态加密
- [iterative-ckks-bootstrapping.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/iterative-ckks-bootstrapping.cpp)：演示如何运行 CKKS 引导的多次迭代以提高精度
- [linearwsum-evaluation.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/linearwsum-evaluation.cpp)：演示如何使用 CKKS 评估线性加权和
- [function-evaluation.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/function-evaluation.cpp)：演示使用 CKKS 使用切比雪夫近似对非多项式函数进行求值
- [polynomial-evaluation.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/polynomial-evaluation.cpp)：演示使用 CKKS 对多项式（幂级数）的评估
- [pre-buffer.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/pre-buffer.cpp)：演示如何使用 OpenFHE 对二进制数据的打包向量进行加密、重新加密和解密
- [pre-hra-secure.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/pre-hra-secure.cpp)：显示基于 BGV 的 HRA 安全 PRE 示例
- [rotation.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/rotation.cpp)：演示了 EvalRotate 在不同方案中的使用
- [scheme-switching.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/scheme-switching.cpp)：演示了在 CKKS 和 FHEW 密文之间切换的几个用例
- [simple-ckks-bootstrapping.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-ckks-bootstrapping.cpp)：一个简单的例子，显示了CKKS引导一个完整的打包密文

> Input: (0.25, 0.5, 0.75, 1, 2, 3, 4, 5,  ... ); Estimated precision: 59 bits
>
> Initial number of levels remaining: 1
> Number of levels remaining after bootstrapping: 10
>
> Output after bootstrapping 
> 	(0.249995, 0.500002, 0.749997, 0.999999, 2, 3.00001, 4, 5,  ... ); Estimated precision: 18 bits

- [simple-integers.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-integers.cpp)：显示使用 BFVrns 的整数向量的同态加法、乘法和旋转的简单示例

> Plaintext #1: ( 10 2 3 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #2: ( 3 2 1 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #3: ( 1 2 5 2 5 6 7 8 9 10 11 12 ... )
>
> Results of homomorphic computations
> #1 + #2 + #3: ( 14 6 9 10 15 18 21 24 27 30 33 36 ... )
> #1 * #2 * #3: ( 30 8 15 32 125 216 343 512 729 1000 1331 1728 ... )
> Left rotation of #1 by 1: ( 2 3 4 5 6 7 8 9 10 11 12 ... )
> Left rotation of #1 by 2: ( 3 4 5 6 7 8 9 10 11 12 ... )
> Right rotation of #1 by 1: ( 0 10 2 3 4 5 6 7 8 9 10 11 ... )
> Right rotation of #1 by 2: ( 0 0 10 2 3 4 5 6 7 8 9 10 ... )

- [simple-integers-bgvrns.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-integers-bgvrns.cpp)：显示使用 BGVrns 的整数向量的同态加法、乘法和旋转的简单示例

> Plaintext #1: ( 1 2 3 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #2: ( 3 2 1 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #3: ( 1 2 5 2 5 6 7 8 9 10 11 12 ... )
>
> Results of homomorphic computations
> #1 + #2 + #3: ( 5 6 9 10 15 18 21 24 27 30 33 36 ... )
> #1 * #2 * #3: ( 3 8 15 32 125 216 343 512 729 1000 1331 1728 ... )
> Left rotation of #1 by 1: ( 2 3 4 5 6 7 8 9 10 11 12 ... )
> Left rotation of #1 by 2: ( 3 4 5 6 7 8 9 10 11 12 ... )
> Right rotation of #1 by 1: ( 0 1 2 3 4 5 6 7 8 9 10 11 ... )
> Right rotation of #1 by 2: ( 0 0 1 2 3 4 5 6 7 8 9 10 ... )

- [simple-integers-serial.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-integers-serial.cpp)：一个简单的例子，展示了一个原型的典型序列化/反序列化调用，该原型使用BFVrns计算整数向量的同态加法、乘法和旋转

> Plaintext #1: ( 1 2 3 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #2: ( 3 2 1 4 5 6 7 8 9 10 11 12 ... )
> Plaintext #3: ( 1 2 5 2 5 6 7 8 9 10 11 12 ... )
>
> Results of homomorphic computations
> #1 + #2 + #3: ( 5 6 9 10 15 18 21 24 27 30 33 36 ... )
> #1 * #2 * #3: ( 3 8 15 32 125 216 343 512 729 1000 1331 1728 ... )
> Left rotation of #1 by 1: ( 2 3 4 5 6 7 8 9 10 11 12 ... )
> Left rotation of #1 by 2: ( 3 4 5 6 7 8 9 10 11 12 ... )
> Right rotation of #1 by 1: ( 0 1 2 3 4 5 6 7 8 9 10 11 ... )
> Right rotation of #1 by 2: ( 0 0 1 2 3 4 5 6 7 8 9 10 ... )

- [simple-integers-serial-bgvrns.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-integers-serial-bgvrns.cpp)：一个简单的例子，展示了一个原型的典型序列化/反序列化调用，该原型使用BGVrns计算整数向量的同态加法、乘法和旋转

  > Plaintext #1: ( 1 2 3 4 5 6 7 8 9 10 11 12 ... )
  > Plaintext #2: ( 3 2 1 4 5 6 7 8 9 10 11 12 ... )
  > Plaintext #3: ( 1 2 5 2 5 6 7 8 9 10 11 12 ... )
  >
  > Results of homomorphic computations
  > #1 + #2 + #3: ( 5 6 9 10 15 18 21 24 27 30 33 36 ... )
  > #1 * #2 * #3: ( 3 8 15 32 125 216 343 512 729 1000 1331 1728 ... )
  > Left rotation of #1 by 1: ( 2 3 4 5 6 7 8 9 10 11 12 ... )
  > Left rotation of #1 by 2: ( 3 4 5 6 7 8 9 10 11 12 ... )
  > Right rotation of #1 by 1: ( 0 1 2 3 4 5 6 7 8 9 10 11 ... )
  > Right rotation of #1 by 2: ( 0 0 1 2 3 4 5 6 7 8 9 10 ... )

- [simple-real-numbers.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-real-numbers)：显示使用 CKKS 对实数向量进行同态加法、乘法和旋转的简单示例

  - 加法，减法，乘法，标量乘法，旋转

  - > Input x1: (0.25, 0.5, 0.75, 1, 2, 3, 4, 5,  ... ); Estimated precision: 50 bits
    >
    > Input x2: (5, 4, 3, 2, 1, 0.75, 0.5, 0.25,  ... ); Estimated precision: 50 bits
    >
    > Results of homomorphic computations: 
    > x1 = (0.25, 0.5, 0.75, 1, 2, 3, 4, 5,  ... ); Estimated precision: 43 bits
    > Estimated precision in bits: 43
    > x1 + x2 = (5.25, 4.5, 3.75, 3, 3, 3.75, 4.5, 5.25,  ... ); Estimated precision: 43 bits
    > Estimated precision in bits: 43
    > x1 - x2 = (-4.75, -3.5, -2.25, -1, 1, 2.25, 3.5, 4.75,  ... ); Estimated precision: 43 bits
    >
    > 4 * x1 = (1, 2, 3, 4, 8, 12, 16, 20,  ... ); Estimated precision: 41 bits
    >
    > x1 * x2 = (1.25, 2, 2.25, 2, 2, 2.25, 2, 1.25,  ... ); Estimated precision: 41 bits
    >
    >
    > In rotations, very small outputs (~10^-10 here) correspond to 0's:
    > x1 rotate by 1 = (0.5, 0.75, 1, 2, 3, 4, 5, 0.25,  ... ); Estimated precision: 43 bits
    >
    > x1 rotate by -2 = (4, 5, 0.25, 0.5, 0.75, 1, 2, 3,  ... ); Estimated precision: 43 bits

- [simple-real-numbers-serial.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/simple-real-numbers-serial.cpp)：一个简单的示例，展示了使用 CKKS 计算整数向量的同态加法、乘法和旋转的原型的典型序列化/反序列化调用

  - 服务端执行数据的输入与加密，客户端对加密后的数据进行序列化与反序列化并运算（包括向量相乘，相加，旋转）

  - > - `vec1 = {1.0, 2.0, 3.0, 4.0}`
    > - `vec2 = {12.5, 13.5, 14.5, 15.5}`
    > - (12.5, 27, 43.5, 62,  ... ); Estimated precision: 30 bits 
    > - (13.5, 15.5, 17.5, 19.5,  ... ); Estimated precision: 32 bits
    > - Displaying 5 elements of a 4-element vector to illustrate rotation 
    > - (2, 3, 4, -2.24326e-10, 1.65543e-10,  ... ); Estimated precision: 32 bits 
    > - (1.67455e-10, 1, 2, 3, 4,  ... ); Estimated precision: 32 bits

- [threshold-fhe.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/threshold-fhe.cpp)：显示 BGVrns、BFVrns 和 CKKSrns 中阈值 FHE 的几个示例

  - 三个明文向量的加，乘，本身求和

    > Original Plaintext:  
    >
    > ( 1 2 3 4 5 6 5 4 3 2 1 ... )
    >
    > ( 1 0 0 1 1 ... )
    >
    > ( 2 2 3 4 5 6 7 8 9 10 ... )  
    >
    > Resulting Fused Plaintext:  
    >
    > ( 4 4 6 9 11 12 12 12 12 12 1 ... )  
    >
    > Resulting Fused Plaintext after Multiplication of plaintexts 1 and 3:  
    >
    > ( 2 4 9 16 25 36 35 32 27 20 ... )  
    >
    > Fused result after summation of ciphertext 3: 
    >
    > ( 56 54 52 49 45 40 34 27 19 10 ... )

- [threshold-fhe-5p.cpp](https://github.com/openfheorg/openfhe-development/blob/main/src/pke/examples/threshold-fhe-5p.cpp)：显示 BFVrns 中具有 5 个参与方的阈值 FHE 示例

  >  Original Plaintext: 
  >
  >  ( 1 2 3 4 5 6 5 4 3 2 1 ... )
  >  ( 1 0 0 1 1 ... )
  >  ( 2 2 3 4 5 6 7 8 9 10 ... )
  >
  >  Resulting Fused Plaintext: 
  >
  >  ( 4 4 6 9 11 12 12 12 12 12 1 ... )
  >
  >
  >  Resulting Fused Plaintext after Multiplication of plaintexts 1 and 3: 
  >
  >  ( 1 32 243 1024 3125 7776 3125 1024 243 32 1 ... )
  >
  >
  >  Fused result after summation of ciphertext 3: 
  >
  >  ( 56 54 52 49 45 40 34 27 19 10 ... )

### 编写客户端（计算服务）与服务端（数据加密与结果解密）

==要先完成·测试流程（参考附录）的操作，后续说明都针对User文件夹==

├── build
│   ├── clientData
│   ├── CMakeFiles
│   │   ├── 3.28.3
│   │   │   └── CompilerIdCXX
│   │   │       └── tmp
│   │   └── pkgRedirects
│   ├── serverData
│   └── src
│       └── CMakeFiles
│           ├── CKKS-client.dir
│           ├── CKKS-server-pull.dir
│           ├── CKKS-server-push.dir
│           └── real-number.dir
└── src

1. build下新建serverData，clientData文件夹用于存储产生的加密数据、密钥等txt文件

2. 编写对应的客户端，服务端cpp程序

3. User/src 下的CMakeLists.txt增加以下内容，用于构建过程

   > add_executable(CKKS-server-push CKKS-server-push.cpp)
   > add_executable(CKKS-server-pull CKKS-server-pull.cpp)
   > add_executable(CKKS-client CKKS-client.cpp)

4. 编译运行CKKS-server-push，将serverData中==除了key_sec==之外的txt都传给客户端

5. 编译运行CKKS-client，产生的计算后的文件传给服务端

6. 编译运行CKKS-server-pull，得到最终结果

==如果文件夹改名，build下的系统产生的文件夹一定要删干净！！！==

## 注意事项

- 账户：luffy 密码：luffy123

- ctrl+alt鼠标退出虚拟机
- ctrl+alt+T打开终端
- ctrl+alt+n编译运行
- find -type f -print  查找目录下所有文件

## 疑问

- make和cmake是用来做什么的
- /usr/local/include/openfhe/pke/schemebase/base-fhe.h:41:10: fatal error: binfhecontext.h: 没有那个文件或目录，查找后确实没有该目录导致从cpp无法编译运行，但是库的安装与测试是通过的，why
- simple-integers-serial
  This program requres the subdirectory `demoData' to exist, otherwise you will get an error writing serializations.有的时候会出现该提示，但是删去文件夹后结果不变为什么，demodata是一个空文件夹==是在build下的demoData而不是大的文件夹下！！！把里面的文件复制到客户端就可以了==

# 附录

### VSCODE配置代码

#### tasks.json

```json
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


//增加fhe库后的配置
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
                "${fileDirname}/${fileBasenameNoExtension}",
                "-I",
                "/usr/local/include/openfhe",
                "-I",
                "/usr/local/include/openfhe/pke",
                "-I",
                "/usr/local/include/openfhe/core",
                "-I",
                "/usr/local/include/openfhe/cereal"
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

```json
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

#### settings.json

```json
{
    "files.associations": {
        "array": "cpp",
        "atomic": "cpp",
        "bit": "cpp",
        "*.tcc": "cpp",
        "cctype": "cpp",
        "charconv": "cpp",
        "chrono": "cpp",
        "clocale": "cpp",
        "cmath": "cpp",
        "compare": "cpp",
        "complex": "cpp",
        "concepts": "cpp",
        "condition_variable": "cpp",
        "cstdarg": "cpp",
        "cstddef": "cpp",
        "cstdint": "cpp",
        "cstdio": "cpp",
        "cstdlib": "cpp",
        "cstring": "cpp",
        "ctime": "cpp",
        "cwchar": "cpp",
        "cwctype": "cpp",
        "deque": "cpp",
        "map": "cpp",
        "set": "cpp",
        "string": "cpp",
        "unordered_map": "cpp",
        "unordered_set": "cpp",
        "vector": "cpp",
        "exception": "cpp",
        "algorithm": "cpp",
        "functional": "cpp",
        "iterator": "cpp",
        "memory": "cpp",
        "memory_resource": "cpp",
        "numeric": "cpp",
        "optional": "cpp",
        "random": "cpp",
        "ratio": "cpp",
        "string_view": "cpp",
        "system_error": "cpp",
        "tuple": "cpp",
        "type_traits": "cpp",
        "utility": "cpp",
        "format": "cpp",
        "fstream": "cpp",
        "initializer_list": "cpp",
        "iomanip": "cpp",
        "iosfwd": "cpp",
        "iostream": "cpp",
        "istream": "cpp",
        "limits": "cpp",
        "mutex": "cpp",
        "new": "cpp",
        "numbers": "cpp",
        "ostream": "cpp",
        "semaphore": "cpp",
        "span": "cpp",
        "sstream": "cpp",
        "stdexcept": "cpp",
        "stop_token": "cpp",
        "streambuf": "cpp",
        "thread": "cpp",
        "cinttypes": "cpp",
        "typeindex": "cpp",
        "typeinfo": "cpp",
        "variant": "cpp"
    }
}
```



## 测试流程-创建客户端

1. 创建User文件夹

2. 从openfhe-development文件夹下复制CMakeLists.User.txt并重命名为CMakeLists.txt，放于User下

3. 打开User下的CMakeLists.txt，添加指令，指定可执行文件的名称和源码（可以复制openfhe-development/src/pke/examples中的cpp文件进行验证，将复制的cpp文件同样放于User下）

   ```apl
   add_executable( fhe-demo simple-integers.cpp )
   ```

4. 在User下创建build文件夹（构建目录），并进入build目录

5. 运行`cmake ..`，build下会产生一个文件夹与多个文件

6. 运行`make`生成可执行文件，在build下会生成名称为`fhe-demo`的可执行文件

7. 返回User目录，执行`build/fhe-demo`即可得到结果==一定不可以在build下执行，会显示未找到命令==

8. 对于7，如果想要在build目录下执行文件，需要将路径添加到PATH变量中

   > 1. `nano ~/.bashrc`打开配置文件
   > 2. `export PATH=$PATH:/home/luffy/桌面/User/build`（build的完整路径）添加路径到PATH变量，按 `Ctrl+O` 保存更改，然后按 `Ctrl+X` 退出编辑器
   > 3. `source ~/.bashrc`让更改立即生效
   > 4. `echo $PATH`查看环境变量是否添加（重启后依然生效）

9. 在User下新建src，将源码分离。User下cmake文件增加`# 添加src子目录到构建过程 add_subdirectory(src)`,src文件夹下新增cmake文件，内容为`add_executable(fhe-demo simple-integers.cpp)`，运行后会在build下产生src文件夹保存可执行程序==注意此时PATH中只包含build，不能在src下运行可执行程序==

## 客户端，服务端代码

### server-push

```c++
#include <iomanip>
#include <tuple>
#include <unistd.h>

#include "openfhe.h"

// header files needed for serialization
#include "ciphertext-ser.h"
#include "cryptocontext-ser.h"
#include "key/key-ser.h"
#include "scheme/ckksrns/ckksrns-ser.h"

using namespace lbcrypto;

/////////////////////////////////////////////////////////////////
// NOTE:
// If running locally, you may want to replace the "hardcoded" DATAFOLDER with
// the DATAFOLDER location below which gets the current working directory
/////////////////////////////////////////////////////////////////
// char buff[1024];
// std::string DATAFOLDER = std::string(getcwd(buff, 1024));

// Save-Load locations for keys
const std::string DATAFOLDER = "serverData";
std::string ccLocation       = "/cryptocontext.txt";
std::string pubKeyLocation   = "/key_pub.txt";   // Pub key
std::string multKeyLocation  = "/key_mult.txt";  // relinearization key
std::string rotKeyLocation   = "/key_rot.txt";   // automorphism / rotation key
std::string secKeyLocation  = "/key_sec.txt";

// Save-load locations for RAW ciphertexts
std::string cipherOneLocation = "/ciphertext1.txt";
std::string cipherTwoLocation = "/ciphertext2.txt";

// Save-load locations for evaluated ciphertexts
std::string cipherMultLocation   = "/ciphertextMult.txt";
std::string cipherAddLocation    = "/ciphertextAdd.txt";
std::string cipherRotLocation    = "/ciphertextRot.txt";
std::string cipherRotNegLocation = "/ciphertextRotNegLocation.txt";
std::string clientVectorLocation = "/ciphertextVectorFromClient.txt";

/**
 * Demarcate - Visual separator between the sections of code
 * @param msg - string message that you want displayed between blocks of
 * characters
 */
void demarcate(const std::string& msg) {
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
    std::cout << msg << std::endl;
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
}

/**
 * serverSetupAndWrite
 *  - simulates a server at startup where we generate a cryptocontext and keys.
 *  - then, we generate some data (akin to loading raw data on an enclave)
 * before encrypting the data
 * @param multDepth - multiplication depth
 * @param scaleModSize - number of bits to use in the scale factor (not the
 * scale factor itself)
 * @param batchSize - batch size to use
 * @return Tuple<cryptoContext, keyPair>
 */
std::tuple<CryptoContext<DCRTPoly>, KeyPair<DCRTPoly>, int> serverSetupAndWrite(int multDepth, int scaleModSize,
                                                                                int batchSize) {
    CCParams<CryptoContextCKKSRNS> parameters;
    parameters.SetMultiplicativeDepth(multDepth);
    parameters.SetScalingModSize(scaleModSize);
    parameters.SetBatchSize(batchSize);

    CryptoContext<DCRTPoly> serverCC = GenCryptoContext(parameters);

    serverCC->Enable(PKE);
    serverCC->Enable(KEYSWITCH);
    serverCC->Enable(LEVELEDSHE);

    std::cout << "Cryptocontext generated" << std::endl;

    KeyPair<DCRTPoly> serverKP = serverCC->KeyGen();
    std::cout << "Keypair generated" << std::endl;

    serverCC->EvalMultKeyGen(serverKP.secretKey);
    std::cout << "Eval Mult Keys/ Relinearization keys have been generated" << std::endl;

    serverCC->EvalRotateKeyGen(serverKP.secretKey, {1, 2, -1, -2});
    std::cout << "Rotation keys generated" << std::endl;

    std::vector<std::complex<double>> vec1 = {12.0, 22.0, 32.0, 42.0};
    std::vector<std::complex<double>> vec2 = {12.5, 13.5, 14.5, 15.5};
    std::cout << "\nDisplaying first data vector: ";

    for (auto& v : vec1) {  
        std::cout << v << ',';
    }

    std::cout << '\n' << std::endl;

    Plaintext serverP1 = serverCC->MakeCKKSPackedPlaintext(vec1);
    Plaintext serverP2 = serverCC->MakeCKKSPackedPlaintext(vec2);

    std::cout << "Plaintext version of first vector: " << serverP1 << std::endl;

    std::cout << "Plaintexts have been generated from complex-double vectors" << std::endl;

    auto serverC1 = serverCC->Encrypt(serverKP.publicKey, serverP1);
    auto serverC2 = serverCC->Encrypt(serverKP.publicKey, serverP2);

    std::cout << "Ciphertexts have been generated from Plaintexts" << std::endl;

    /*
   * Part 2:
   * We serialize the following:
   *  Cryptocontext
   *  Public key
   *  relinearization (eval mult keys)
   *  rotation keys
   *  Some of the ciphertext
   *
   *  We serialize all of them to files
   */

    demarcate("Part 2: Data Serialization (server)");

    if (!Serial::SerializeToFile(DATAFOLDER + ccLocation, serverCC, SerType::BINARY)) {
        std::cerr << "Error writing serialization of the crypto context to "
                     "cryptocontext.txt"
                  << std::endl;
        std::exit(1);
    }

    std::cout << "Cryptocontext serialized" << std::endl;

    if (!Serial::SerializeToFile(DATAFOLDER + pubKeyLocation, serverKP.publicKey, SerType::BINARY)) {
        std::cerr << "Exception writing public key to pubkey.txt" << std::endl;
        std::exit(1);
    }
    std::cout << "Public key serialized" << std::endl;
    
    if (!Serial::SerializeToFile(DATAFOLDER + secKeyLocation, serverKP.secretKey, SerType::BINARY)) {
        std::cerr << "Exception writing secret key to seckey.txt" << std::endl;
        std::exit(1);
    }
    std::cout << "Secret key serialized" << std::endl;
    
    std::ofstream multKeyFile(DATAFOLDER + multKeyLocation, std::ios::out | std::ios::binary);
    if (multKeyFile.is_open()) {
        if (!serverCC->SerializeEvalMultKey(multKeyFile, SerType::BINARY)) {
            std::cerr << "Error writing eval mult keys" << std::endl;
            std::exit(1);
        }
        std::cout << "EvalMult/ relinearization keys have been serialized" << std::endl;
        multKeyFile.close();
    }
    else {
        std::cerr << "Error serializing EvalMult keys" << std::endl;
        std::exit(1);
    }

    std::ofstream rotationKeyFile(DATAFOLDER + rotKeyLocation, std::ios::out | std::ios::binary);
    if (rotationKeyFile.is_open()) {
        if (!serverCC->SerializeEvalAutomorphismKey(rotationKeyFile, SerType::BINARY)) {
            std::cerr << "Error writing rotation keys" << std::endl;
            std::exit(1);
        }
        std::cout << "Rotation keys have been serialized" << std::endl;
    }
    else {
        std::cerr << "Error serializing Rotation keys" << std::endl;
        std::exit(1);
    }

    if (!Serial::SerializeToFile(DATAFOLDER + cipherOneLocation, serverC1, SerType::BINARY)) {
        std::cerr << " Error writing ciphertext 1" << std::endl;
    }

    if (!Serial::SerializeToFile(DATAFOLDER + cipherTwoLocation, serverC2, SerType::BINARY)) {
        std::cerr << " Error writing ciphertext 2" << std::endl;
    }

    return std::make_tuple(serverCC, serverKP, vec1.size());
}
int main() {
    std::cout << "This program requres the subdirectory `" << DATAFOLDER << "' to exist, otherwise you will get "
              << "an error writing serializations." << std::endl;

    // Set main params
    const int multDepth    = 5;
    const int scaleModSize = 40;
    const usint batchSize  = 32;

    demarcate(
        "Part 1: Cryptocontext generation, key generation, data encryption "
        "(server)");
    auto tupleCryptoContext_KeyPair = serverSetupAndWrite(multDepth, scaleModSize, batchSize);
    const int vectorSizeIdx    = 2;
    int vectorSize                  = std::get<vectorSizeIdx>(tupleCryptoContext_KeyPair);
    // 文件路径，这里使用当前目录下的"number.txt"
    std::string filePath = DATAFOLDER+"/vectorSize.txt";
    // 使用 std::ofstream 打开文件，使用 std::ios::out 表示打开用于输出的文件
    std::ofstream outputFile(filePath);
    // 检查文件是否成功打开
    if (!outputFile.is_open()) {
        std::cerr << "无法打开文件：" << filePath << std::endl;
        return 1; // 如果文件无法打开，返回错误代码
    }
    // 将整数写入文件
    outputFile << vectorSize;
    // 关闭文件
    outputFile.close();
    std::cout << "vectorsize has wirtten." << filePath << std::endl;
}
```

### client

```c++
#include <iomanip>
#include <tuple>
#include <unistd.h>

#include "openfhe.h"

// header files needed for serialization
#include "ciphertext-ser.h"
#include "cryptocontext-ser.h"
#include "key/key-ser.h"
#include "scheme/ckksrns/ckksrns-ser.h"

using namespace lbcrypto;

/////////////////////////////////////////////////////////////////
// NOTE:
// If running locally, you may want to replace the "hardcoded" DATAFOLDER with
// the DATAFOLDER location below which gets the current working directory
/////////////////////////////////////////////////////////////////
// char buff[1024];
// std::string DATAFOLDER = std::string(getcwd(buff, 1024));

// Save-Load locations for keys
const std::string DATAFOLDER = "clientData";
std::string ccLocation       = "/cryptocontext.txt";
std::string pubKeyLocation   = "/key_pub.txt";   // Pub key
std::string multKeyLocation  = "/key_mult.txt";  // relinearization key
std::string rotKeyLocation   = "/key_rot.txt";   // automorphism / rotation key

// Save-load locations for RAW ciphertexts
std::string cipherOneLocation = "/ciphertext1.txt";
std::string cipherTwoLocation = "/ciphertext2.txt";

// Save-load locations for evaluated ciphertexts
std::string cipherMultLocation   = "/ciphertextMult.txt";
std::string cipherAddLocation    = "/ciphertextAdd.txt";
std::string cipherRotLocation    = "/ciphertextRot.txt";
std::string cipherRotNegLocation = "/ciphertextRotNegLocation.txt";
std::string clientVectorLocation = "/ciphertextVectorFromClient.txt";
/**
 * Demarcate - Visual separator between the sections of code
 * @param msg - string message that you want displayed between blocks of
 * characters
 */
void demarcate(const std::string& msg) {
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
    std::cout << msg << std::endl;
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
}
/**
 * clientProcess
 *  - deserialize data from a file which simulates receiving data from a server
 * after making a request
 *  - we then process the data by doing operations (multiplication, addition,
 * rotation, etc)
 *  - !! We also create an object and encrypt it in this function before sending
 * it off to the server to be decrypted
 */
void clientProcess() {
    CryptoContext<DCRTPoly> clientCC;
    clientCC->ClearEvalMultKeys();
    clientCC->ClearEvalAutomorphismKeys();
    lbcrypto::CryptoContextFactory<lbcrypto::DCRTPoly>::ReleaseAllContexts();
    if (!Serial::DeserializeFromFile(DATAFOLDER + ccLocation, clientCC, SerType::BINARY)) {
        std::cerr << "I cannot read serialized data from: " << DATAFOLDER << "/cryptocontext.txt" << std::endl;
        std::exit(1);
    }
    std::cout << "Client CC deserialized";

    KeyPair<DCRTPoly> clientKP;  // We do NOT have a secret key. The client
    // should not have access to this
    PublicKey<DCRTPoly> clientPublicKey;
    if (!Serial::DeserializeFromFile(DATAFOLDER + pubKeyLocation, clientPublicKey, SerType::BINARY)) {
        std::cerr << "I cannot read serialized data from: " << DATAFOLDER << "/cryptocontext.txt" << std::endl;
        std::exit(1);
    }
    std::cout << "Client KP deserialized" << '\n' << std::endl;

    std::ifstream multKeyIStream(DATAFOLDER + multKeyLocation, std::ios::in | std::ios::binary);
    if (!multKeyIStream.is_open()) {
        std::cerr << "Cannot read serialization from " << DATAFOLDER + multKeyLocation << std::endl;
        std::exit(1);
    }
    if (!clientCC->DeserializeEvalMultKey(multKeyIStream, SerType::BINARY)) {
        std::cerr << "Could not deserialize eval mult key file" << std::endl;
        std::exit(1);
    }

    std::cout << "Deserialized eval mult keys" << '\n' << std::endl;
    std::ifstream rotKeyIStream(DATAFOLDER + rotKeyLocation, std::ios::in | std::ios::binary);
    if (!rotKeyIStream.is_open()) {
        std::cerr << "Cannot read serialization from " << DATAFOLDER + multKeyLocation << std::endl;
        std::exit(1);
    }
    if (!clientCC->DeserializeEvalAutomorphismKey(rotKeyIStream, SerType::BINARY)) {
        std::cerr << "Could not deserialize eval rot key file" << std::endl;
        std::exit(1);
    }

    Ciphertext<DCRTPoly> clientC1;
    Ciphertext<DCRTPoly> clientC2;
    if (!Serial::DeserializeFromFile(DATAFOLDER + cipherOneLocation, clientC1, SerType::BINARY)) {
        std::cerr << "Cannot read serialization from " << DATAFOLDER + cipherOneLocation << std::endl;
        std::exit(1);
    }
    std::cout << "Deserialized ciphertext1" << '\n' << std::endl;

    if (!Serial::DeserializeFromFile(DATAFOLDER + cipherTwoLocation, clientC2, SerType::BINARY)) {
        std::cerr << "Cannot read serialization from " << DATAFOLDER + cipherTwoLocation << std::endl;
        std::exit(1);
    }

    std::cout << "Deserialized ciphertext1" << '\n' << std::endl;
    auto clientCiphertextMult   = clientCC->EvalMult(clientC1, clientC2);
    auto clientCiphertextAdd    = clientCC->EvalAdd(clientC1, clientC2);
    auto clientCiphertextRot    = clientCC->EvalRotate(clientC1, 2);
    auto clientCiphertextRotNeg = clientCC->EvalRotate(clientC1, -2);

    // Now, we want to simulate a client who is encrypting data for the server to
    // decrypt. E.g weights of a machine learning algorithm
    demarcate("Part 3.5: Client Serialization of data that has been operated on");

    std::vector<std::complex<double>> clientVector1 = {1.0, 2.0, 3.0, 4.0};
    auto clientPlaintext1                           = clientCC->MakeCKKSPackedPlaintext(clientVector1);
    auto clientInitiatedEncryption                  = clientCC->Encrypt(clientPublicKey, clientPlaintext1);
    Serial::SerializeToFile(DATAFOLDER + cipherMultLocation, clientCiphertextMult, SerType::BINARY);
    Serial::SerializeToFile(DATAFOLDER + cipherAddLocation, clientCiphertextAdd, SerType::BINARY);
    Serial::SerializeToFile(DATAFOLDER + cipherRotLocation, clientCiphertextRot, SerType::BINARY);
    Serial::SerializeToFile(DATAFOLDER + cipherRotNegLocation, clientCiphertextRotNeg, SerType::BINARY);
    Serial::SerializeToFile(DATAFOLDER + clientVectorLocation, clientInitiatedEncryption, SerType::BINARY);

    std::cout << "Serialized all ciphertexts from client" << '\n' << std::endl;
}
int main() {
    std::cout << "This program requres the subdirectory `" << DATAFOLDER << "' to exist, otherwise you will get "
              << "an error writing serializations." << std::endl;

    demarcate("Part 3: Client deserialize all data");
    clientProcess();
}
```

### server-pull

```c++
#include <iomanip>
#include <tuple>
#include <unistd.h>

#include "openfhe.h"

// header files needed for serialization
#include "ciphertext-ser.h"
#include "cryptocontext-ser.h"
#include "key/key-ser.h"
#include "scheme/ckksrns/ckksrns-ser.h"

using namespace lbcrypto;

/////////////////////////////////////////////////////////////////
// NOTE:
// If running locally, you may want to replace the "hardcoded" DATAFOLDER with
// the DATAFOLDER location below which gets the current working directory
/////////////////////////////////////////////////////////////////
// char buff[1024];
// std::string DATAFOLDER = std::string(getcwd(buff, 1024));

// Save-Load locations for keys
const std::string DATAFOLDER = "serverData";
std::string ccLocation       = "/cryptocontext.txt";
std::string pubKeyLocation   = "/key_pub.txt";   // Pub key
std::string secKeyLocation   = "/key_sec.txt";   // Sec key
std::string multKeyLocation  = "/key_mult.txt";  // relinearization key
std::string rotKeyLocation   = "/key_rot.txt";   // automorphism / rotation key
std::string vecSizeLocation   = "/vectorSize.txt"; 

// Save-load locations for RAW ciphertexts
std::string cipherOneLocation = "/ciphertext1.txt";
std::string cipherTwoLocation = "/ciphertext2.txt";

// Save-load locations for evaluated ciphertexts
std::string cipherMultLocation   = "/ciphertextMult.txt";
std::string cipherAddLocation    = "/ciphertextAdd.txt";
std::string cipherRotLocation    = "/ciphertextRot.txt";
std::string cipherRotNegLocation = "/ciphertextRotNegLocation.txt";
std::string clientVectorLocation = "/ciphertextVectorFromClient.txt";

/**
 * Demarcate - Visual separator between the sections of code
 * @param msg - string message that you want displayed between blocks of
 * characters
 */
void demarcate(const std::string& msg) {
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
    std::cout << msg << std::endl;
    std::cout << std::setw(50) << std::setfill('*') << '\n' << std::endl;
}
/**
 * serverVerification
 *  - deserialize data from the client.
 *  - Verify that the results are as we expect
 * @param cc cryptocontext that was previously generated
 * @param kp keypair that was previously generated
 * @param vectorSize vector size of the vectors supplied
 * @return
 *  5-tuple of the plaintexts of various operations
 */
std::tuple<Plaintext, Plaintext, Plaintext, Plaintext, Plaintext> serverVerification(CryptoContext<DCRTPoly>& cc,
                                                                                     KeyPair<DCRTPoly>& kp,
                                                                                     int vectorSize) {
    Ciphertext<DCRTPoly> serverCiphertextFromClient_Mult;
    Ciphertext<DCRTPoly> serverCiphertextFromClient_Add;
    Ciphertext<DCRTPoly> serverCiphertextFromClient_Rot;
    Ciphertext<DCRTPoly> serverCiphertextFromClient_RogNeg;
    Ciphertext<DCRTPoly> serverCiphertextFromClient_Vec;

    Serial::DeserializeFromFile(DATAFOLDER + cipherMultLocation, serverCiphertextFromClient_Mult, SerType::BINARY);
    Serial::DeserializeFromFile(DATAFOLDER + cipherAddLocation, serverCiphertextFromClient_Add, SerType::BINARY);
    Serial::DeserializeFromFile(DATAFOLDER + cipherRotLocation, serverCiphertextFromClient_Rot, SerType::BINARY);
    Serial::DeserializeFromFile(DATAFOLDER + cipherRotNegLocation, serverCiphertextFromClient_RogNeg, SerType::BINARY);
    Serial::DeserializeFromFile(DATAFOLDER + clientVectorLocation, serverCiphertextFromClient_Vec, SerType::BINARY);
    std::cout << "Deserialized all data from client on server" << '\n' << std::endl;

    demarcate("Part 5: Correctness verification");

    Plaintext serverPlaintextFromClient_Mult;
    Plaintext serverPlaintextFromClient_Add;
    Plaintext serverPlaintextFromClient_Rot;
    Plaintext serverPlaintextFromClient_RotNeg;
    Plaintext serverPlaintextFromClient_Vec;

    cc->Decrypt(kp.secretKey, serverCiphertextFromClient_Mult, &serverPlaintextFromClient_Mult);
    cc->Decrypt(kp.secretKey, serverCiphertextFromClient_Add, &serverPlaintextFromClient_Add);
    cc->Decrypt(kp.secretKey, serverCiphertextFromClient_Rot, &serverPlaintextFromClient_Rot);
    cc->Decrypt(kp.secretKey, serverCiphertextFromClient_RogNeg, &serverPlaintextFromClient_RotNeg);
    cc->Decrypt(kp.secretKey, serverCiphertextFromClient_Vec, &serverPlaintextFromClient_Vec);

    serverPlaintextFromClient_Mult->SetLength(vectorSize);
    serverPlaintextFromClient_Add->SetLength(vectorSize);
    serverPlaintextFromClient_Vec->SetLength(vectorSize);
    serverPlaintextFromClient_Rot->SetLength(vectorSize + 1);
    serverPlaintextFromClient_RotNeg->SetLength(vectorSize + 1);

    return std::make_tuple(serverPlaintextFromClient_Mult, serverPlaintextFromClient_Add, serverPlaintextFromClient_Vec,
                           serverPlaintextFromClient_Rot, serverPlaintextFromClient_RotNeg);
}
int main() {
    std::cout << "This program requres the subdirectory `" << DATAFOLDER << "' to exist, otherwise you will get "
              << "an error writing serializations." << std::endl;

    const int cipherMultResIdx   = 0;
    const int cipherAddResIdx    = 1;
    const int cipherVecResIdx    = 2;
    const int cipherRotResIdx    = 3;
    const int cipherRotNegResIdx = 4;

    demarcate("Part 4: Server deserialization of data from client. ");
    std::string vecfilePath = DATAFOLDER+vecSizeLocation;
    int vectorSize;
    // 使用 std::ifstream 打开文件，使用 std::ios::in 表示打开用于输入的文件
    std::ifstream inputFile(vecfilePath);
    // 检查文件是否成功打开
    if (!inputFile.is_open()) {
        std::cerr << "无法打开文件：" << vecfilePath << std::endl;
        return 1; // 如果文件无法打开，返回错误代码
    }
    // 从文件读取整数
    inputFile >> vectorSize;
    // 检查文件中是否成功读取了整数
    if (inputFile.fail()) {
        std::cerr << "从文件中读取整数失败。" << std::endl;
        inputFile.close();
        return 1;
    }
    // 关闭文件
    inputFile.close();
    CryptoContext<DCRTPoly> cc;
    cc->ClearEvalMultKeys();
    cc->ClearEvalAutomorphismKeys();
    lbcrypto::CryptoContextFactory<lbcrypto::DCRTPoly>::ReleaseAllContexts();
    if (!Serial::DeserializeFromFile(DATAFOLDER + ccLocation, cc, SerType::BINARY)) {
        std::cerr << "I cannot read serialized data from: " << DATAFOLDER << "/cryptocontext.txt" << std::endl;
        std::exit(1);
    }
    std::cout << "cc deserialized";
    
    KeyPair<DCRTPoly> clientKP;
    PublicKey<DCRTPoly> clientPublicKey;
    if (!Serial::DeserializeFromFile(DATAFOLDER + pubKeyLocation, clientPublicKey, SerType::BINARY)) {
        std::cerr << "I cannot read serialized data from: " << DATAFOLDER << "/pubKeyLocation.txt" << std::endl;
        std::exit(1);
    }
    clientKP.publicKey=clientPublicKey;
    PrivateKey<DCRTPoly> clientSecretKey;
    if (!Serial::DeserializeFromFile(DATAFOLDER + secKeyLocation, clientSecretKey, SerType::BINARY)) {
        std::cerr << "I cannot read serialized data from: " << DATAFOLDER << "/secKeyLocation.txt" << std::endl;
        std::exit(1);
    }
    clientKP.secretKey=clientSecretKey;
    
    
    
    auto tupleRes  = serverVerification(cc, clientKP, vectorSize);
    auto multRes   = std::get<cipherMultResIdx>(tupleRes);
    auto addRes    = std::get<cipherAddResIdx>(tupleRes);
    auto vecRes    = std::get<cipherVecResIdx>(tupleRes);
    auto rotRes    = std::get<cipherRotResIdx>(tupleRes);
    auto rotNegRes = std::get<cipherRotNegResIdx>(tupleRes);

    std::cout << multRes << std::endl; 
    std::cout << addRes << std::endl;   
    std::cout << vecRes << std::endl;   

    std::cout << "Displaying 5 elements of a 4-element vector to illustrate rotation" << '\n';
    std::cout << rotRes << std::endl;     // EXPECT: {2, 3, 4, noise, noise}
    std::cout << rotNegRes << std::endl;  // EXPECT: {noise, 1, 2, 3, 4}
}
```

