# 1. 存储器的分类
## 1.1 层次分类

![picture 2](../assets/e3ee0b01baac75df9aec2ccb55393bbb0bee2c8b15674ad2531b7a9bcb78cd16.png)  
- 辅存：**不可以**与`CPU`直接交互
- 主存：**可以**和`CPU`直接交互，也可以和`Cache`、辅存交换数据

## 1.2 介质分类
> - 磁表面存储器：磁盘、磁带
> - 半导体存储器：`MOS`管——主存、`Cache`
> - 光存储器：光盘

## 1.3 存储方式分类
> - 顺序存储器（`SAM`）——磁带
>   - 存取时间和存储单元的物理位置**有关**
> - 随机存储器（`RAM`）——半导体存储
>   - 存取时间和存储单元的物理位置**无关**
>   - 分为`静态RAM`（`SRAM`）和`动态RAM`（`DRAM`）
>       - `SRAM`：主要用于构成`Cache`，由`MOS`电路构成的**双稳触发器**保存二进制信息
>       - `DRAM`：主要用于构成主存，由`MOS`电路中的**栅极电容**保存二进制信息；
> - 半顺序存储器（`DAM`）——磁盘
>   - 存取时间**部分地依赖于**存储单元的物理位置
>       - 先直接选取信息所在区域
>       - 然后按顺序存储
> 


## 1.4 存储内容分类
> - 随机存储器（`RAM`）、只读存储器（`ROM`）
>   - 相同点
>       - 随机读取
>       - 半导体存储器
>   - 不同点
>       - RAM 随机存取，读写方便————ROM 只能读不能写
>       - RAM 用于主存、Cache————ROM 用于主存和`CPU`，存储固定不变的程序，如控制存储器`CM`

## 1.5 信息保存行
> - 易失性存储
>   - `RAM`
>   - 断电后，无法保持信息
> - 非易失性存储
>   - 只读存储器`ROM`
>       - 只读不能写
>    - 可编程序的只读存储器`PROM`
>      - 一次性写入
>    - 可擦可编程序的只读存储器`EPROM`
>       - 可多次写入、读出
>   - 可电擦可编程序只读存储器`E2PROM`
>     - 可多次读出但写入次数有限
>   - 快擦除读写存储器`Flash Memory`
>     - 重复写入、读出

# 2. 存储容量的扩展

![picture 7](../assets/9bf58b72b5a6b79f617bd9d99a9c9a577850ba4235711490f0e647fcd2245bed.png)  


## 2.1 连接原理
- 多块主存的存储芯片与`CPU`连接
   - 控制总线
   - 数据总线
   - 地址总线

## 2.2 位扩展（位扩并）
![picture 20](../assets/a6077193fff4d1014cf871d17d12fe25699d7ea562109ad90907c6970689708e.png)  

## 2.3 字扩展——存储芯片地址分配和片选（字扩串）

![picture 21](../assets/cd60f7398922afe4f219f97f1e9396a64305bdf187b1e97ca0bea2199464a1f1.png)  


![picture 23](../assets/4fa75d16f3c41ea7a5ae5d36fc13fa80dc7b05a92a1335ddb03d5faf73a333bf.png)  

![picture 22](../assets/3679b56e7385919b84459b716b14e882ecb7ce67549d0fcd000fa6f60f873b5d.png)  

## 2.4 字位同时扩展

![picture 24](../assets/1ec7014013d6d473e7a63e50d4ea8d2c837aa1e485d73a4fbde9bc104a37ced0.png)  



# 3. Cache

## 3.1 基本原理
![picture 1](../assets/8f5d55fa52d242f692dabd72385079244ce558731b29b998b61e9bf195c8d1a1.png)  

![picture 2](../assets/db406dc8f50e62208cd8204634b889b162bc74df25dcc38f45d0923e69d09170.png)  


## 3.2 `Cache`映射


![picture 3](../assets/8f101fc6c2465bb243552365b510345ef356d75e154785d3d779a1c0351e6b5d.png)  

![picture 8](../assets/4b2fb8a2592247e9f1b67972127b5c9def66f218733b5f34318047d2a0cc2122.png)  


## 3.3 `Cache`替换算法

- 直接映射不需要考虑替换算法

![picture 6](../assets/6bcd65fb1dade7b51bc6e4fda3d3fb70ba050b340347f970e35dda8ec79cd612.png)  

![picture 7](../assets/90abb8a4d5a979b3f3bb8c16851bfc6e49c3cc6059ac8f3fe1fd4812932f9047.png)  


![picture 8](../assets/2df373176f421e9d28a60ee183e1539983ef810beea057626f5bd7c823d6843d.png)  

![picture 9](../assets/a0d3dd9fa0002b1ab6d1c8fb16ec996b1ab2094c6ece235184fbcfe35af7455b.png)  

![picture 10](../assets/adb8ea0c761d78dd44a9c99a01bae81834531c6d05aa0284bd1e63da3f6918ef.png)  


## 3.4 Cache写策略——数据一致性问题

 ![picture 12](../assets/ef90ceaa17c1dfebcd17f918e5499d3db19131e7bd78575c09f264f6e112e35a.png)  



# 4. 补充概念

## 4.1 虚拟存储的概念

![picture 1](../assets/226797fede2c8a0a8cc7bd7a465e88ff31ab7c6a988598e15393a04f358396e1.png)  

![picture 2](../assets/acbe1467dd8df88985d328a3680e9722d2bbfc7b144dec46f104814e3d77c451.png)  



## 4.2 大端和小端
>-  **Little**-Endian就是**低位字节排放在内存的低地址端**，高位字节排放在内存的高地址端。
>-  **Big**-Endian就是**高位字节排放在内存的低地址端**，低位字节排放在内存的高地址端。

## 4.3 DRAM刷新方法

![picture 3](../assets/86b5e12d1d2a64888b8c3438c25da9520bce25aa96ca51954ce598ffa6f803db.png)  

- 用了行列地址

![picture 4](../assets/6d2b1084e9b8eb357e9f6178299123bab95c5d6f8be3416329424a9f99f1280b.png)  


## 4.4 RAM读写周期

![picture 5](../assets/8343556ab4e65072630155972283568470eb5a2b6fb26b2db4f7d12108f13cb3.png)  


## 4.5 存储器性能指标

![picture 6](../assets/290cd86e9815f7b39e9659b3ff7d2d023ea250bbe41208e6848688bea3d2953f.png)  

## 4.6 多模块存储器（空间并行）与存储周期

- 存储周期
  - 存储器连续启动两次独立的访问操作所需的最小间隔时间
  - `存取周期=存取时间+复原时间`

- 多模块存储器（空间并行）
![picture 32](../assets/25f85b1f1907f6c8a116eeac35822326a35620d1d43a87c8bc1428485a88e708.png)  


# 习题

![picture 4](../assets/a6576ab7bf0dea7dce91d99384b511f83fbb50bd097c5cb63a6daaf763b8b4d0.png)  

![picture 5](../assets/1d16a9210067ea161c66f7295896b68b9d376841b30b883ae500ed8dfa2a16e0.png)  

![picture 6](../assets/49c9902a08f672e968ea500403b510e9ef7be2752644f275d8ff4999e5c643d7.png)  

![picture 7](../assets/b165122ea5a820e44e2cdb4577f28e0276414cadc9f841b963d7e6989c31091b.png)  

![picture 9](../assets/52916e1179527fb329b5cd2975c96b3b50317dcf61fa75660ea88861e0392ce5.png)  

![picture 14](../assets/656a6fdc188c1375f8926c29d9262101a4cdde57715e105a1538d88c9ed3316f.png)  
![picture 12](../assets/cb08fa198b41d17cb7e5f997424ef306e52e3fc4e195513e9a57481f5e85da13.png)  
![picture 13](../assets/9621236816a67a9bf633f25e063b6341c4bcd23ab8ab6d55dfc27bb5218a40f2.png)  


![picture 15](../assets/0a705afa08d44da043a2a6714d6a4a68da41bfec621ca669ea729eb3fdfeafcd.png)  
![picture 16](../assets/1b8927dad397c3cfc4695dc3ca0ca0230c4557177b03c1a4dc8aed42e7e43e94.png)  
![picture 17](../assets/18ec1aae0e6b35e2d361dacbfc567e945ae2af5eaf6017c11e7bb230c210fac0.png)  


![picture 1](../assets/ca30605ec09433aed974f741de9d15927e5031a96701a855838f2b666d167d57.png)  
![picture 2](../assets/45dad248c60626748982cb1f628b04e564d75cb9e65a509db06fde797d457c7a.png) 


![picture 3](../assets/0d927580c9261e4aa514737a713641e2e423ec188be22413c82c07ca978ed1d2.png)  

![picture 4](../assets/764965c727c51e45fc377078f860cc73f6e95798f6c5500c89dc3658f5473a88.png)  
![picture 5](../assets/9b6000a8e09a3d54f2c8606f95183ac70101284d539b6735a0de7ba7c02f552a.png)  


> - **微程序===指令>>>微指令>>>multiple 微命令 === 微操作**