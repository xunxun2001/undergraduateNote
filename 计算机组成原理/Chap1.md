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
  - 半导体存储器
- 超大型集成电路
  - 微处理器出现
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
![picture 7](../assets/06dda3b1d1317a5faad6505d35ccc30b85641cc25117ab867c0b33fcd827d316.png)  

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

1. 取指令（记得`PC`+"1")
> `PC`——>`MAR`——>`M`（存储器）——>`MDR`——>`IR`

> `PC`+"1"
2. 分析指令（译码）
> `OP(IR)`——>`CU`
3. 执行指令
> `Ad(IR)`——>`MAR`——>`M`——>`MDR`——>`ACC`

## 2.6 多级层次结构
![picture 14](../assets/7d7be823641ab7ec8950136c838a2c1149bb255bcd5bd1a99862a7ecfa3c783f.png)  
![picture 15](../assets/3f4a6a6e8c461b574e0a331a4c430854ea6c93213c7206ad33ffec6e9b451709.png)  


# 1.3 计算机性能指标
![picture 16](../assets/b2a0551cde4c41fd8d44c210399462e707468f41128a9bac4f8fe7a915d42189.png)  


# 习题
## 题目
### 1.1
![picture 1](../assets/f1bd15668dfa87c8a71cf7d75b04c58b7379fc56c1003fe38b0886d7896e18c1.png)  
![picture 2](../assets/49e778abb836486a8a273c5645857a8f9096d10787608a0a9822cb39f6dbe273.png)  

### 1.2

## 答案


### 1.1
![picture 3](../assets/19f81dc2c31fab954545253f48e8f116647805b9ee7bd52338a713d104a74f92.png)  
![picture 4](../assets/267ceba88446207f1904f8cfaf70b629426e0193ed2c3e0e99f376d8302d8bf6.png)  

### 1.2
![picture 9](../assets/1e28dab20536b479296ebaf52440774e35ed71aad23a8616244f40a66efab40d.png)  


