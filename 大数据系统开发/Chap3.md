# Spark的设计与运行原理

## 1. Spark概述

- Apache软件基金会最重要的三大分布式计算系统开源项目
  - `Hadoop`
  - `Spark`
  - `Storm`
- 主要特点
  - 运行模式多样
  - 运行速度快
  - 容易使用
  - 通用性好
- `Hadoop`存在如下一些缺点
  - 表达能力有限
  - 磁盘`IO`开销大
  - 延迟高
    - 任务之间的衔接涉及IO开销
    - 在前一个任务执行完成之前，其他任务就无法开始，难以胜任复杂、多阶段的计算任务 
- `Spark`的优点
  - 计算模式也属于`MapReduce`，但**不局限于**`Map和Reduce`操作，还提供了多种数据集操作类型，编程模型比`Hadoop MapReduce`**更灵活**
  - 提供了**内存计算**，可将**中间结果**放到内存中，对于**迭代运算效率更高**
  - 基于`DAG`的任务调度执行机制，要优于`Hadoop MapReduce`的**迭代执行机制**
    - `RDD`：是`Resilient Distributed Dataset`（**弹性分布式数据集**）
      - **分布式内存**的一个**抽象概念**，提供了一种高度受限的**共享内存模型**
    - `DAG`：是`Directed Acyclic Graph`（**有向无环图**）的简称
      - 反映`RDD`之间的**依赖关系**
   - `Spark`用**1/10**的计算资源，获得了比`Hadoop`快**3**倍的速度


![picture 1](../assets/e7325c9be7f91094f161358cec4136f85f860b7e7545c8c9ff58e70dea9e2d26.png)  




## 2. Spark生态
- 应用场景


![picture 2](../assets/e818ddeeead752c832a437054de80be1407a2f15340e51c3eb9fabebac687302.png)  

## 3. Spark运行架构

- `RDD`：`Spark`**最核心的数据抽象**

### 3.1 基本概念
>  - `Executor`：是运行在工作节点（`WorkerNode`）的一个进程，负责运行`Task`
>  - 应用（`Application`）：用户编写的`Spark`应用程序
>  - 任务（ `Task` ）：运行在`Executor`上的工作单元 
>  - 作业（ `Job` ）：一个作业包含多个`RDD`及作用于相应`RDD`上的各种操作
>  - 阶段（ `Stage` ）：是作业的基本调度单位
>    - 一个作业会分为多组任务，每组任务被称为阶段
>    - 代表了一组**关联的、相互之间没有**`Shuffle`依赖关系的任务组成的**任务子集**

### 3.2 基本架构

![picture 3](../assets/d2bf2cbbb687743aac432deaec5f4d5775122a9610caa79bfc96e504b4eebadc.png)  

![picture 4](../assets/3a2ebfe3b70bcb869606398e8480a6b503cdfe90c27dbd32006158d727a92e5b.png)  

![picture 5](../assets/f504c2f3a4a6d9436328a8a625e9647e8a47c07df3dd1bc8944cc979a71ecb49.png)  

![picture 6](../assets/42c195189bcedb816b689e44496a4b5a174d29bdfa36830355af94d4ad247f5a.png)  

![picture 7](../assets/6933c2aeebbdf2d750e9e551f7694c6abf25af47adb7fd7baa842033490542ce.png)  


### 3.3 基本运行流程（总结于3.4.5）

- 首先由`Driver`创建一个`SparkContext`，进行资源的申请、任务的分配和监控

![picture 8](../assets/5a927ca93be18f3f6d44483240555aacecb5f2804e77ee39bfe0e2ebf8b3b334.png)  

- 资源管理器为`Executor`分配资源，并启动Executor进程

![picture 9](../assets/489cd86a78c13a0ba8e0873bc1fdc9d7dc566a291014aac7b15c6750789efe5d.png)  

- `SparkContext`根据`RDD`的依赖关系构建`DAG`图
  - `DAG`图提交给`DAGScheduler`解析成`Stage`，然后把一个个`TaskSet`提交给底层调度器TaskScheduler处理
  - `Executor`向`SparkContext`申请`Task`，`Task Scheduler`将`Task`发放给`Executor`运行，并提供应用程序代码

![picture 10](../assets/6963152427a3f32cc3e7d93414a217b1997d702517a390cbb58caa6779753a78.png)  

- `Task`在`Executor`上运行，把执行结果反馈给`TaskScheduler`，然后反馈给`DAGScheduler`，运行完毕后写入数据并释放所有资源 

![picture 11](../assets/98a915e354916774660ff81b6691e0e077d0b0c8997f7768bb58a0c157289348.png)  


### 3.4 RDD原理

#### 3.4.1 RDD设计背景

- Hadoop无法很好处理
  - 迭代
  - 反复读写工作子集
- Hadoop开销
  - 磁盘IO
  - 序列化与反序列化
![picture 12](../assets/15ec8d2f31f8bfbc2496e1ed05149a0b1acc52fd2507efbd30c4441aff8359d9.png)  

![picture 13](../assets/7c2712ba22a79eca0eafa2ab97ab98fcc8dffff127db1efe0d75514213414702.png)  

![picture 14](../assets/d4f2a7487122a796d4a73ae314a9dd1a022f322429211e42a452431053d541a2.png)  


#### 3.4.2 RDD概念
> - 一个`RDD`就是一个分布式对象集合，本质上是一个**只读**的**分区**记录集合
>   - 分区是因为数据集太大单个内存放不下
>   - 只读：高度受限的共享内存模型，**不能直接修改**
>     - 基于稳定的物理存储中的数据集创建`RDD`
>     - 通过在其他`RDD`上执行确定的转换操作（如join和group by）而创建得到新的`RDD`
>   - 一个`RDD`的不同分区可以被保存到集群中不同的节点上
>     - 从而可以在集群中的不同节点上进行并行计算
> - `RDD`提供了一组丰富的操作以支持常见的数据运算，分为“动作”（`Action`）和“转换”（`Transformation`）两种类型
>   - 只有`Action`发生计算，`Transformation`记录转化生成`DAG`
>     - `惰性调用机制`
>   - **粗粒度**，相当于没有`SQL`中的`Where`语句，无脑all in
>     - 因此也不适用网页爬虫


![picture 15](../assets/69631e702ac1f936ba5491a782d4ba13df18565ed1eb60b6b4f69d125ea172b8.png)  


![picture 19](../assets/337f09881df598bf453da286e52f8c696c714c766517106ff0ed58c256502273.png)  

> - 血缘关系`Lineage`——`DAG`**拓扑排序**的结果
>   - 可以**恢复数据**（寻亲）
>       - 无需回滚
>       - 重算过程在不同节点之间并行
>   - **流水线优化**（不需要保存中间结果）
>       - 避免了不必要的IO磁盘开销
>       - 存放的数据可以是`Java`对象，避免了**不必要的对象序列化和反序列化**


#### 3.4.3 RDD依赖关系

> - 是划分不同阶段的依据

![picture 20](../assets/eab0e3c76d51cd3598363fb50287bb26cfce9bf81ad2fc86ccbe043014df173c.png)  


> - 只要发生了shuffle的地方就是宽依赖

![picture 21](../assets/d6e36acb68aa9a9f789aa3c213031171a5df39b17d2b3175b4564824ac32c894.png)  

> - 窄依赖

![picture 22](../assets/16d68664982d7bbcb65bce97eb3b7df4f061e703579df8d7698659f92eeb34d9.png)  


> - 宽依赖

![picture 23](../assets/08240ffd21fd5b0ddb880d92ffdb09ec73db7f01cdaf48d07a8490c3dbe02c0a.png)  

![picture 24](../assets/f04103534efca5ed691a8302fc65eed74586e9e2a0c30158acb8aaa66bc383a9.png)  


#### 3.4.4 RDD阶段划分

- 窄依赖就断开，宽依赖就不断
- 窄依赖对于作业的流水线优化很有利，宽依赖无法优化
  - 逻辑上，每个RDD 操作都是一个`fork/join`（一种用于并行执行任务的框架），把计算`fork` 到每个`RDD` 分区，完成计算后对各个分区得到的结果进行`join` 操作，然后`fork/join`下一个`RDD` 操作



![picture 26](../assets/4cc627eacf5daf853db42530f1bfb4c6c454a9c87d9be9eb201bed23bc211309.png)  

![picture 27](../assets/d368fc6e709caf22ba6b397937e3aa65cfad4264befd2fe003f5946da1b053e7.png)  

![picture 28](../assets/c7d334399a75856a38f3b3fa706b5472e9629f3ea6ea4cbbc2dc7499f5f2a7ca.png)  

- 流水线优化
  - 不发生无意义的等待
    - 只要发生shuffle就一定会写磁盘
  - 具体方法
    - 在`DAG`中进行**反向解析**，**遇到宽依赖就断开**
    - 遇到窄依赖就把当前的`RDD`加入到`Stage`中
    - 将窄依赖尽量划分在同一个`Stage`中，可以实现流水线计算




![picture 29](../assets/cd1f528b3a43f0c4c6513952e8b2fc917d5321c0a944b9a20f0e766e147b610c.png)  

> - 被分成三个`Stage`，在`Stage2`中，从`map`到`union`都是窄依赖，这两步操作可以形成一个流水线操作

![picture 30](../assets/4f21be0b1382856e78c691e448a22c12ccecb2f41a417ce13cdab9d72265be79.png)  


#### 3.4.5 RDD运行过程
> 1. 创建`RDD`对象；
> 2. `SparkContext`负责计算`RDD`之间的依赖关系，构建`DAG`；
> 3. `DAGScheduler`负责把`DAG`图分解成多个`Stage`，每个`Stage`中包含了多个`Task`，每个`Task`会被`TaskScheduler`分发给各个`WorkerNode`上的`Executor`去执行

![picture 31](../assets/b1d45c2278e904abc65c684d981ab3666a877e114d31e1c54b25809ca8d9800c.png)  


## 4. Spark部署与应用方式

- `Standalone`，自带
- `Spark on Mesos`，和`Spark`有血缘关系，更好支持`Mesos`
- `Spark on YARN`，`Hadoop`集群
