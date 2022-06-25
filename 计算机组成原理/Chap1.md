# 1.计算机系统发展

## 1.1 硬件发展

- 电子管时代
  - 第一台电子数字计算机
  - 机器语言
- 晶体管时代
  - 面向过程的语言：`FORTRAN`
  - OS雏形
- 中小规模集成电路
  - 元件集成在基片上
  - 分时操作系统
  - **半导体存储器**
- 超大型集成电路
  - **微处理器**出现
  - 并行、流水线、`Cache`、虚拟存储
  - 个人电脑`PC`萌芽，诞生了`Windows`、`MacOS`、`Linux`

## 1.2 软件发展

- 面向机器
  - 机器语言
  - 汇编语言
- 面向问题
  - `FORTRAN`、`PASCAL`、`C++`、`Java`

> 贝尔实验室：发明晶体管——>仙童半导体公司：发明集成电路——>`Intel`、`AMD`

# 2.计算机系统层次结构

- 硬件和软件在逻辑上是等效的

## 2.1 冯·诺依曼结构

- 早期冯诺依曼机
  ![picture 5](../assets/ae2f010fb4c1714a6cd31f93277dc39ef9bfb60f44942026e5468fc26e44967b.png)  
- 现代计算机
  ![picture 6](../assets/4688f96e88034e89e89acd7ed89be6e03c1c36648066c27aaaf726cbb6af1bf5.png)  
  
  > `I/O`操作尽可能的绕开`CPU`，实现`I/O设备`与存储器直接完成，从而**提高运行效率**
  > ![picture 7](../assets/06dda3b1d1317a5faad6505d35ccc30b85641cc25117ab867c0b33fcd827d316.png)  

> 辅存属于外设

![picture 8](../assets/1cf9ec7869813d5d3c81f2bb922902240658cdf4866d9150d5358cca5fde5dd0.png)  

## 2.2 主存基本组成

![picture 11](../assets/c6abd8eb479c0f1ff12c8484c5388b827a2784782770b4fc77e2eb6b703ddc62.png)  

- `MAR`位数：存储单元个数
- `MDR`位数：存储字长

## 2.3 运算器基本组成

![picture 12](../assets/2490f895a2fc66d9d2b52cc8551ec7151a021b4c51d1a2311a494c9131ed7adf.png)  

## 2.4 控制器基本组成

![picture 13](../assets/4d653bfdc55ce4f07921a0a4b02b036ae8ba36d4087a327dfe534bc067b43e2c.png)  

## 2.5 计算机工作流程

- 具体步骤
1. 程序、数据装入主存

2. 从程序起始地址运行

3. 程序首地址取出指令——>指令译码——>指令执行——>完成功能并计算下一条指令地址

4. 得到新的地址———>读出下一条指令

5. 直到程序结束
- 信息流程

> 1. 取指令（记得`PC`+"1")
> `PC`——>`MAR`——>`M`（存储器）——>`MDR`——>`IR`
> `PC`+"1"
> 2. 分析指令（译码）
> `OP(IR)`——>`CU`
> 3. 执行指令
> `Ad(IR)`——>`MAR`——>`M`——>`MDR`——>`ACC`

## 2.6 多级层次结构

![picture 14](../assets/7d7be823641ab7ec8950136c838a2c1149bb255bcd5bd1a99862a7ecfa3c783f.png)  
![picture 15](../assets/3f4a6a6e8c461b574e0a331a4c430854ea6c93213c7206ad33ffec6e9b451709.png)  

# 1.3 计算机性能指标

![picture 16](../assets/b2a0551cde4c41fd8d44c210399462e707468f41128a9bac4f8fe7a915d42189.png)  

# 习题


![picture 3](../assets/ba17f9cce5517d9187591f2431cfe35550dd1433023c781085b2bf334d823f28.png)  

![picture 5](../assets/7856ba97e1c9fc18fb030ffc420c865d90fba07609bc3bb6ec5faf96087316d0.png)  


![picture 1](../assets/e3da507ef7cef603de0e7462317da68d1962b17f92a9382eed475c3eaecc13e5.png)  

![picture 6](../assets/302fb68ec6ac247f9e61a688f8b326b1cb795cd1e39c2a6f734aa4565991bdcd.png)  

![picture 7](../assets/77bd0846d15f2d9dbf95cd6fa47cb62938f28b3eaf5d5f95b62e50085518a57f.png)  

![picture 8](../assets/019259d32a57029dff3bb0e0982bbb6b332b44aa823529e137f22e13d73644a1.png)  



![picture 9](../assets/e537ef6171d896770cacdb8a5ff553c1efcdfda0b5dcadebf3fb2f981d5bb965.png)  

![picture 13](../assets/02246b265f62fa78d7944918cb306a48854c35af74844d0924f28448712476b3.png)  


![picture 11](../assets/56010080fca801e2b87fa8715b3cc54b25d0c0c2bd7078f03ada45cb9c87d3e7.png)  
![picture 12](../assets/2ab0d84dd3e0cb72097dacb85ea007adea0f21740e4c8e92220a179f15beea7b.png)  




![picture 10](../assets/6ab650092cbe41804bd4c24205398cbc20dcd6535ac965cf0040cf78f310fef7.png)  

![picture 14](../assets/90a06e4c5897615aac5b4f6e28437285aa0208940a93355ef953b9c1b7b8edba.png)  

![picture 15](../assets/60af599fd6bbec84e0e28afd68aa4d8066ddca339869534daa95148607258d95.png)  

 - 存储系统：主存、辅存、Cache
 - 计算机硬件链接方式：总线

![picture 19](../assets/6c50b059439fbb2dbb61e240aea1dd7ade38c260ead2a01cbb3df898bba7ee47.png)  
