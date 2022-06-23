# 1. CPU的功能、组成、结构
## 1.1 功能
> - 指令控制——程序的顺序控制
>   - 取指令
>   - 分析指令
>   - 执行指令
> - 操作控制——产生和发送各操作信号
>   -  对指令操作码译码后产生控制信号
>   - 一条指令的功能往往由若干操作信号的组合来实现
> - 时间控制——维持各类操作的时序关系
>   - 各类操作有先有后
> - 数据加工——对数据进行算术逻辑运算
> - 中断处理
>   - 对计算机运行过程中出现的异常情况和特殊请求进行处理

## 1.2 组成
![picture 1](../assets/8b380a03dd7f29d2f8a755430f0697eaaf5459327de3ad1b60b2dd5380275cb3.png)  

## 1.3 CPU的结构
![picture 2](../assets/c0810755c58b0297618217d5a39342c844485993bb5ba5d7772e6cec95700359.png)  

![picture 3](../assets/bb88e8fa1899749fada70d7e8de314a2d8fc685d98027079e774183eca35a322.png)  

> - 程序状态条件寄存器（`PSW`）
>   - 每个信号由一个触发器保存，从而拼成一个寄存器
> - 地址寄存器（`AR`）
>   - 主要用于**解决**主存/外设和`CPU`之间的**速度差异**，使地址信息可以保持到主存/外设的读写操作完成为止
> - **数据缓冲寄存器**（`DR`）
>   - 暂时存放`CPU`与外界传送的数据
>   - 作为`CPU`和内存、外部设备之间信息传送的中转站
>   - 补偿`CPU`和内存、外围设备之间在操作速度上的差别
> - 程序计数器（`PC`）
>   - 顺序执行：` PC+1→PC`——计数功能
>   - 转移执行： `(指令OPR)→PC`——寄存功能


# 2. 指令执行过程

## 2.1 基本概念
![picture 4](../assets/8f76d1f26de111cbed0922c6ee66fb216723683ece1d3ac80cb97b4ac7fb17e4.png)  

![picture 7](../assets/2825b1f1f84528b993c99bacd3ca4f08cc223a682f0811cd9a37a3c80abba781.png)  


![picture 5](../assets/19574cc20bce88473cd4bfa823a8afc47375fc099ce061fa0c1870fedfe4755e.png)  

> - 比起取指令时候的访存，指令译码在`CPU`内部，十分快速，因此都划分为取指周期
>   - 展示的只是**必有**的**机器周期**
- 机器周期类别（指令周期的组成）
  - 一个基本的CPU周期包含4个时钟周期，对于某些`CPU`周期可以包含更多的时钟周期

![picture 8](../assets/18480630aee568f15f5184e5829b697ceed039f87fe8729740817cb1254a2a8a.png)  

![picture 11](../assets/45ae4250d1d9f0640949708a58b2f6b41776adc7dbc8b58259e9643eddf611a2.png)  

## 2.2 指令周期的数据流

- 取值周期数据流向

![picture 12](../assets/701bcb0655f6c1f0cd7d24d4e155a33e4e2546ad2a488c4eed1838c28b9fd38d.png)  

- 取值周期数据流向
  - `EA`：有效地址


![picture 13](../assets/bb49848165fa8301dca64de213c04cf45416cf0ecdc9e9ae52d17e2e3e6ad7bb.png)  

- 执行周期
  - 没有统一的数据流向
  
- 中断周期（略）


## 2.3 不同指令的指令周期

> - 寄存器-寄存器（`RR`）型指令：从寄存器中取操作数，把操作结果放到另一寄存器中，不需要访问内存存储器，因此速度快
> - 存储器—存储器（`SS`）型指令：执行此类指令，既要访问内存单元，又要访问寄存器
> - 寄存器-存储器（`RS`）型指令：执行此类指令，既要访问内存单元，又要访问寄存器

![picture 9](../assets/e0b95112f55f0c26a79b82b473672b22029b6d8725c4b03be03033c808fa5bf6.png) 
 ![picture 10](../assets/2c07d4b31d3da1a0680d6619e9d1851d26d18583e98bde5d02ec5e38a076e337.png)  

- `MOV R0 , R1`
  - 一条`RR型`指令，它需要**2**个`CPU`周期
  - 取指周期
    - `PC→ABUS→指令Cache` ，译码并启动
    - 指令`Cache → IR`
    - `PC→ PC+1`
    - `IR`中的操作码被译码或测试，`CPU`识别出是指令`MOV`
  - 执行指令
    - `R1→ALU`，`R1`中数据通过`ALU`传送
    - `ALU→ DBUS →DR→R0`，`ALU`输出，`DR`锁存，`R0`写


![picture 14](../assets/06d6d24775573fbbf951dcb2716dd3b2a0f55d3b3d16cfdf4c62eb69d1f00959.png)  

- `LAD R1 , 6`——直接访存指令
  - 一条`RS型`指令，它需要**3**个`CPU`周期
  - 取指周期
    - 类似`MOV`
  - 执行指令
    - 寻址
      - `IR→ DBUS→ AR`
    - `AR→ABUS→数据Cache` ，译码并启动
    - `数据Cache → DBUS → DR→R1`，`数据Cache`读，`DR`锁存，`R1`写


![picture 15](../assets/6df250caafe0f9e5fa4f4b59b3c20f2b19fbb55a8f761ed324521179728e0d68.png)  



- `ADD R1 , R2`
  - `RR型`指令，需要**2**个`CPU`周期
  - 取指周期
    - 类似`MOV`
  - 执行指令
    - `R1、R2→ALU`
    - `ALU`做加运算，将两数相加
    - `ALU→DBUS→DR→R2`，保存结果，`ALU`输出，`DR`锁存，`R2`写

- `STO R2 , (R3)`
  - `RS`型指令，需要**2**个`CPU`周期
  - 取指周期
    - 类似`MOV`
  - 执行指令
    - 间址
      - 根据`R3`中的地址寻址所要访问的存储单元
      - `R3→DBUS→AR`，发出地址启动`数据Cache`，`R3`读，`AR`锁存
    - `R2→DBUS→数据Cache`

- `JMP 101`
  - 无条件转移指令，改变程序的执行顺序
  - 取指周期（略）
  - 执行周期
    - `IR→DBUS→PC`


# 3. 数据通路

![picture 16](../assets/eab05340265b50a28f02fdf4c8a774f9c4a13763fdfa92ec60d24037493ded18.png)  



# 4. 控制器的功能与原理
## 4.1 基本概念
> - `CU`发出一个`微命令`，可完成对应的`微操作`
> - 每一个节拍其实可以**并行**完成**不冲突、相容的**的`微操作`

![picture 17](../assets/22af4d3656595edf3f82859085a4173c18be640db90e3ce15b66c6b88fa9ca06.png)  

> - 根据设计方法不同，操作控制器可分为
>   - 硬布线控制器 采用时序逻辑技术实现
>   - 微程序控制器 采用存储逻辑实现
>   - 前两种方式的结合

- `微操作`分类
  - 相容性`微操作`
    - 在同时或同一个`CPU`周期内可以并行执行的`微操作`
  - 相斥性`微操作`
    - 不能在同时或不能在同一个`CPU`周期内并行执行的`微操作`
## 4.2 硬布线控制器

- 简而言之就是纯硬件（电路）设计的控制器
![picture 19](../assets/2da6d428d9b6ea966cb13e362808629cadaa45dd2b6073f3c32638a9ecc5ab0a.png)  

![picture 20](../assets/69ff350ef5ea01beb6fc9439ea9601ea9e2b938714154a71c0d7083c2b271278.png)  

## 4.3 微程序控制器

### 4.3.1 设计思路
> - `微操作`序列之于指令，如同指令序列之于程序
> - `微指令`：完成几个`微操作`
>   - `微指令`是对`指令`执行步骤的描述
>     - `指令`是对程序执行步骤的描述
>   - `指令`是对`微指令`功能的**封装**
> - `微程序`：由`微指令`序列组成，**每一种指令对应一个微程序**
> - 一个`微命令`对应一根输出线
>   - `微命令`与`微操作`一一对应
> - 采用**存储程序**的思想，在出厂前就把所有指令的“**微程序**”存入“**控制器存储器**”中
  

![picture 23](../assets/ae93d6bda4b214bb78657fa926210684ff31a570d2b4a17ffa1749afa6460325.png) 

![picture 24](../assets/102dad64c2bf28f560cf7a050a8ee2369f53c99d81f53020a6670416fef9d11f.png)  


![picture 22](../assets/d9f2181b47be8289577649e5f1aa3558c989bb3b375faa20283800f43cabbae6.png)  
 


### 4.3.2 基本结构

![picture 26](../assets/381133f5add0b7f3f35b5f8983c2261c09f71365416da42ed3ca01733f6ba0da.png)  


![picture 27](../assets/9fbf8c94cc59f221d7e272584fdec3b6c86f68949d9306249c8073f57a68865e.png)  

![picture 28](../assets/f00562ada247050a855b2ce45eb6484583a2b14e6f8232eecdf7fe1bd3a9a2d4.png)  
![picture 29](../assets/f441e922b96c03461695048328ef2356bcf462deb68d54aff53440851ecee037.png)  
![picture 30](../assets/c7bfbe2f8101f09349268393139796c4b0c66eb31804d8c287fba70c37098825.png)  


### 4.3.3 微指令格式

 ![picture 4](../assets/c66ef79dec204fd34dfb232a867d5b899b0f51b131b1dff4fbcca556e49afa48.png)  


### 4.3.4 微指令编码
> 译码器：较少输入变为较多输出

#### 直接编码
![picture 5](../assets/75645fa001e816a88bc618b9f6d965966ad80a3c5b5c656f93638f70e8fd63b4.png)  

#### 字段直接编码
![picture 6](../assets/7ea500cb3aa7b55780eab97d940add7729a8116aac4fb8e11248b13eca47f334.png)  

![picture 7](../assets/eaabea915aa8aff7b7b0d1cc7fb58513cf934527575e4ca0a2b9ce31558903a0.png)  
![picture 8](../assets/553bb0567169152d013034cdc93ba5b7622d5370774d4247ce27bc4231f4a751.png)  
 

#### 字段间接编码

![picture 10](../assets/05a7b553902842033abc9fb810abf09a1badde6816e80bd4330769d679b5060a.png)  


### 4.3.5 微指令地址形成方式

> **计数器**、**多路转移**
![picture 11](../assets/8a1823e9db10636c195d1c25fb1e1456eaafafa99de11cd1bdb09bd3a81445c9.png)  

![picture 12](../assets/30c7ee1f721aed8e82df99c56fcdbe1b4e99f011ffcd7ccc8f5b12c531bdb8cc.png)  



## 4.4 对比

![picture 3](../assets/95e1f026277fde5cf4fe0cb0db13480ec4338a0ceb50a34afd11ede625cf3d1a.png)  




# 5. 流水线

> - `CISC`可以通过优化实现流水线
> - `RISC`必须要实现流水线
## 5.1 流水线分类

![picture 13](../assets/74e4bd87b23515c6f88f3b150caa8253201644a922f684c01178d3900e530206.png)  

![picture 14](../assets/f460c89048850694084fa85b6c91923242549cf776721533152730f6af2e1951.png)  

## 5.2 指令流水线
![picture 15](../assets/d9655964bb042bb1a958ac041ba1b2a208927584900eed03464ffc7db9bbdc60.png)  

## 5.3 性能指标

![picture 16](../assets/8d8d45750c7865b0846fe0c8bd56fc8723be7eb43f74c49106763c705a9ce616.png)  

![picture 18](../assets/8cbca5f1bd62014356e4cdaf8c4f197d7a1761681712c0a9c81571155078aed9.png)  

![picture 19](../assets/ad4387bb5cb0c45f220772c1c1f3c7bb4e43becdef7c4aa2cda97b568597cb6a.png)  


## 5.4 超标量流水线
- 具有2条以上的指令流水线
- 
![picture 17](../assets/734a272e30da3232b025fe4f396e5d8e00085778954802e5a872f345498f8c02.png)  
