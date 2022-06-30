# 1. 进程的基本概念

## 1.1 进程的定义（不同角度）

> - 程序作用在一组数据上的一次执行过程（一次计算）
> - 操作系统中一个可独立调度和资源分配的基本单位
> - 可以与其他程序并发执行的程序的一次执行

## 1.2 进程的特征、与程序的区别
> - 动态性
>   - 进程由创建到消亡是有一定生命期的，在生命期间进程是一个活动实体
>   - 而程序是可以永久存放于某种介质上的有序指令集合，是一个静态实体
> - 并发性
>   - 在内存中的多个进程能在一段时间内同时运行
>   - 多个进程的程序可以并发执行,而程序是不能并发执行的
> - 独立性
>   - 进程是一个能够独立运行的基本单位，即只有进程才能被独立调度运行及独立获得资源
>   - 程序是不能作为调度运行和获得资源的基本单位的
> - 异步性
>   - 进程以各自独立的、不可预知的速度向前推进
> - 结构特征
>   - 进程控制块(`PCB`)、程序段、数据段

## 1.3 进程（实体）的组成

> 进程实体是进程的一次快照，进程是一次过程

> - 进程控制块`PCB`
>   - **进程存在的唯一标识**
> - 程序段
> - 数据段


![picture 12](../assets/aaafcefa310d0a6bf71d3edb960fe36ba8898059eab37f5e6567a121fda032af.png)  

![picture 13](../assets/3e89564806fb5807c801d540c6a9f8173fad76c5bc344522a1ebfec0d2c5f97d.png)  


## 1.4 进程状态
> - 不能由阻塞态直接转化为运行态
> - 不能由就绪态直接转为阻塞态

![picture 14](../assets/d5a5ffde0f69a47b77114be6d8f0bb073eb11fe1fa27558a9220b3e7a9efb3ea.png)  
![picture 15](../assets/346b85af06b5f922bd6691984959b6574ed583f5eac3fc46ff5d24c5e47891ef.png)  

# 2. 进程控制与原语
> - 用原语来实现进程控制，具有**原子性**，一气呵成(即操作时要**屏蔽中断**)
> - 如果不具有原子性，可能会导致某些关键数据结构信息不一致
> - 作业：在外存还没运行的程序

![picture 16](../assets/772ca811ec57ae34031ce2465ec1de54886f21a52a1aa7a6af01798fe0382505.png)  
![picture 17](../assets/7764d122eeece6294d3b8f3dc2413559fe62c9efc697ad1b504ed57d397e3765.png)  
## 2.1 创建原语
![picture 20](../assets/c217b95a0ce0706a7cc0ae16a6bf85987efd25c51879316b1566ee7383e86cd6.png)  


## 2.2 撤销原语
![picture 19](../assets/3a96b7fb04f51c421bf08dddca3577642a11728c7298aea4c44279f0c843cafe.png)  

## 2.3 阻塞原语和唤醒原语

![picture 21](../assets/39c911b651b08db66a863983b0679b88b4119d1091de5ec7355ac49aa56dacc3.png)  

## 2.3 切换原语
![picture 23](../assets/7869df9c9dfb792b2a1d2f9da196498eb80e93d5e6df4477d5a397f374765f8b.png)  


# 3. 进程同步与互斥
> - 进程同步————**解决异步**的问题，就是一种**制约关系**
> - **协调**进程之间的**相互制约关系**，达到**资源共享和进程协作**，**避免**进程之间的**冲突**
> - 临界资源：一段时间内只允许一个进程使用
> - 进入区、临界区、退出区、剩余区

![picture 24](../assets/a1c8574b5318eff18188b0bd8a90c72f8fe347a22f438acb3411eb686a00ff62.png)  

![picture 25](../assets/38da5ae85232ad15253265418f7d2741a625fa68e82ebef66eabf2de412c8565.png)  

## 3.1 进程互斥原则


1. 空闲让进：临界区空闲时，允许一个请求进入临界区的进程立即进入临界区
2. 忙则等待：临界区已有进程时，其余进程进入临界区必须等待
3. 有限等待：保证**不会饥饿**，要在**有限时间**内进入
4. 让权等待：若进程不能进入临界区，应立即释放处理机，**防止忙等待**

## 3.2 信号量机制

> 整形信号量不满足让权等待，因此人们提出记录型信号量

![picture 1](../assets/6d95c2415367b88e89bd78fbf894f3c411fa605ef95dfb404e6e08498cdbbd06.png)  

![picture 2](../assets/33235fd26231e06728503451d3a594150601961688eee3907df8248566adc910.png)  


## 3.3 利用信号量实现同步
> - P(S)——申请一个资源`mutex`，资源不够就阻塞等待
> - V(S)——释放一个资源`mutex`，若有进程在等待，唤醒一个进程
> - 不同的临界资源需要设置不同的互斥信号量`mutex`，初始值大于等于`1`
> - 在进入区P(`mutex`)——申请资源
> - 在退出区V(`mutex`)——释放资源

## 3.4 利用信号量实现同步
> 1. 分析在什么地方需要保证“**一前一后**”
> 2. 设置同步信号量`S`，初始值`0`
> 3. **前V后P**：在前操作之后执行`V(S)`，在后操作之前执行`P(S)`


![picture 3](../assets/8f9ace91656039c4b8264933dc6f7186ddc8e6983711bc27898e7e8197f9c4e1.png)  

![picture 4](../assets/c4741a9f7d6089a2b34e44eeadfc9f66fa33655642dc79239684f043bd7790e8.png)  

## 3.5 生产者与消费者问题
> - 实现互斥的P操作一定要在同步的P操作之后
> - V操作顺序可以交换，因为V操作不会导致进程阻塞
![picture 5](../assets/f48f63fea93a366b13619e7e289174047e90f089c2d05cbf9a56b8c7f4627a3f.png)  
![picture 6](../assets/de27b78cd4455c0a0b2179c6295b1c3f11fb6d8a5e9e937c3397fb46fedb2dfc.png)  
![picture 7](../assets/c387faecbe98284ad544137bb55de38d291a004cb2d859f0457148c403fc774f.png)  

## 3.6 多生产者多消费者问题
![picture 8](../assets/2379ca0f7761433e90a6cee7aa8c99688bdecaa4fbce8d6ed0e02f927c36ec0b.png)  

![picture 9](../assets/ae215592694318a1f095a39b1eab7b1a5d7ed7f4a02408ea06475afc7862c0e9.png)  

![picture 10](../assets/19bbd0b8977a1da059a2db91974e47fc3de6a87c8fd26e7cf8a3ed7871b34cee.png)  
![picture 11](../assets/8c6cb4962c1b8d29e3f5d16eec6aaef25717e7e66b2b4b03341b26a0649e1181.png)  

# 4. 线程
## 4.1 线程与进程
> - 进程作为一个独立运行的基本单位——只有进程可以被调度运行，只有进程才能拥有资源
> 
> - 为使进程的程序充分并发执行，同时能尽量减少系统的开销
>   - 分配、回收、切换 —— 时空开销
> - 进程**调度运行**和**拥有资源**这两个基本运行单位的属性分开，**让进程拥有资源**，而让一个**线程作为调度运行的基本单位**
> 
> - 在引入线程的操作系统中，将**进程**看作**资源集合与线程集合**的复合体

![picture 13](../assets/c9931f37bf1c5c9e0b98c259c363800f64403bfb575d2505d53a33fa9d3eb094.png)  

![picture 14](../assets/164cbf48f8ad2a9eeb05a8d6333b4a9da1f448ddbd0c689c885187658ddaa3e6.png)  

## 4.2 线程的类型

### a.用户级线程

> - 用户自己创建的**逻辑上的线程**
> - 多对一模型

![picture 15](../assets/135d427f2ab05105e8626f915f9c890544685ff9f5d0b92846811c0ef37fff2f.png)  

### b.内核级线程
> - 一对一模型
 ![picture 16](../assets/6f1f0de40e9e8f85d31fca708d147902433b3c748551d71f29a25509b73e4b04.png)  


### c.多对多模型

![picture 17](../assets/f6f682f0529a09ab07095dec325bb020ac3b1dfd3e041832fc537ab2367698d6.png)  


# 5. 进程调度

## 5.1 三个层次
![picture 1](../assets/054a172e3bcb357ca44fa628d7188fe9e640ee82db9cdca0602231b819532422.png)  


## 5.2 七状态模型（由中级调度扩充）

> - 挂起与阻塞的异同
>   - 同：都是暂时不能获得`CPU`服务
>   - 异：挂起的进程映像是放在外存，而阻塞的进程映像是在内存

![picture 2](../assets/42672ba161cfc903ad1f0263eb4a69e0a4951f872b1491aa26abe0261d7697ae.png)  

## 5.3 调度的时机与方式

### a.时机
![picture 3](../assets/5a6bc98dbafef78f8b1c1fe903547b86999d7aeba7affb8cccaa70ea73dddaa2.png)  
![picture 4](../assets/4be79eed8d15ff0b7c2ad32700da1d625577e011fcab48eb2407fbca3cbbba73.png)  \

### b.方式
![picture 5](../assets/1ae073124b094ad829df7e7cde21b6968c8a5e944531fa0e4b8ec35456d4a882.png)  

## 5.4 调度性能指标

![picture 6](../assets/1c6093de07e4602f1e00ee92cf3faba491fbd8ea99aec23d806877930d0eac3f.png)  



## 5.5 调度算法

### a. 先来先服务（`FCFS`）
![picture 8](../assets/46b337ac994fd5f48ecf47db7e5428d194fe525bace97d56ae302ebad02fc3e5.png)  

![picture 7](../assets/8eef963aff8ac50dcf09ec57c72383d111111b4fff4d11b7464a4548f62824eb.png)  

### b.短作业优先（`SJF`）与最短剩余时间优先（`SRTN`）
> 所有进程同时可运行时，**平均等待时间与平均周转时间最少**

![picture 12](../assets/5043a49ff5ac0fe2e4b049e8b2004441826657ac2d8cec5694f2fa8b79735c26.png)  


![picture 9](../assets/1054511575638a26f74dd0e49673dfd5812e18df444269f4205663ce900aaa40.png)  

![picture 10](../assets/1a657b8b56d779fd7549d2cec9d83c88aef156885b29bd27d1dfdbaccf52463f.png)  
![picture 13](../assets/f42ae8b99212b890adf8cd6f872280db1c229cfd8b412bf0fe1adf0b5eba31cd.png)  


### c.高响应比优先（`HRRN`）
![picture 14](../assets/151c795490b776f506457a4fbd17dd3b080af197c4eab8227ac9169b3d33b9e3.png)  

![picture 15](../assets/cbe2f040a3fbe96ef6effe411dcd0483bcd8ef3fd3ca504d7d1e87a101c326ca.png)  


### D.=======分割线=======总结=======


![picture 16](../assets/f2dbdf7c1edc336e2ba5e19400b536c6e85e16e8abe99829fc3450a672b2ae99.png)  


### e. 时间片轮转（`RR`）

> - **时间片太大，退化为先来先服务**
> - 时间片太小，进程切换频繁，一般让进程切换的开销占比不超1%

![picture 19](../assets/47ec79dd5ac10ffc6ca9360111df7605e8024d030fd980e366aaf3ee35399cf3.png)  


![picture 17](../assets/eb5fda9eeb6c9e7b05cf7ac23ad340e4d3c3ccd4c82dcefa154055c60288b1c1.png)  
![picture 18](../assets/e504a928ed28e433e0560e6e06d0a33430274db5985dfa4f5bab96cc31bdcad4.png)  


### f. 优先级
![picture 22](../assets/d0986aefdb6057eedff7b455641ea3d5a773fc64b1da77e7a6a640223e8c3d33.png)  

![picture 21](../assets/d1e4f1ea8c8f5ca80857a80dedeacf8c64086a2432f179abfaf270aeaebac6e8.png)  

![picture 23](../assets/a004526ad5af9ab794016028e6df88905f4995aecafd378b2139e2e1f92c2136.png)  

![picture 20](../assets/2c042eabc918ef097a449fd34d169a5a785687e290596babf8eaf8e869da50a2.png)  

### g. 多级反馈队列

![picture 24](../assets/0df13b3cc1f9df4359ac804cd6d83cce8b75e3959be927b07104e16c9f5da836.png)  
![picture 25](../assets/84708a9a70baac6bd45e576c923bbad7a719feb510a4fe023f91eea9b7a4d8ce.png)  

# 6. 进程通信

![picture 1](../assets/a77e985f5a43f2180e728aba5709a315ac68bf6af91f9b807d934cf10e582547.png)  

# 7. 死锁

## 7.1 概念

> - **并发环境下**，各进程因竞争资源而导致**互相等待对方手里的资源**，导致各进程都**阻塞**

## 7.2 死锁、饥饿、死循环的区别
> - 死锁：**各**进程都**等待对方资源**而阻塞，而无法向前推进，**阻塞态**
>   - 管理者`OS`的问题
> - 饥饿：**某**进程**长期得不到资源**而无法向前推进，**阻塞态**或**就绪态**
>   - 管理者`OS`的问题
> - 死循环：某进程**执行过程中一直跳不出某个循环**的现象，可以是**运行态**
>   - 代码、被管理者的问题

## 7.3 死锁条件
> - 互斥条件
>   - 一个资源在某一时刻只能分配给一个进程
> - 非剥夺条件
>   - 已分配给进程的资源只能被占有者自行释放
> - 请求与保持条件
>   - 进程在占用部分资源后，运行时还可以申请其余的资源，而且在申请其余资源时**并不释放已占用的资源**
> - 循环等待条件
>   - 系统中存在着一条由两个或两个以上的进程组成的循环链
>   - 但是**发生循环等待不一定死锁**，是**必要不充分**条件


## 7.4 死锁的处理策略
> - 预防死锁
>   - 破坏死锁产生的四个必要条件中的一个或几个
> - 避免死锁
>   - 通过某种算法防止系统进入不安全状态
> - 死锁的检测和解除
>   - 允许死锁发生，不过`OS`可以检测出死锁然后解除

### 7.4.1 静态策略：预防死锁

![picture 4](../assets/ac49f73c354122d68f4df2f84c053582e6d5d33a812b905e0451c791ffc26b59.png)  

![picture 3](../assets/ab0a44ba9134b99a11b210b9c525ed1e44b1b0d1e2182aa259a0dfac24c7e046.png)  
![picture 5](../assets/1dbefc3826eda4d4aef62971242f9a2b0e6654a7fe2a90c4a4bd19cf22faba88.png)  

### 7.4.2 动态策略：避免死锁

#### a. 安全序列
![picture 7](../assets/ab55e14dec8fedbc1427f1cfd5d135ac39dcb979918ee33762025b7495259879.png)  
![picture 8](../assets/a041c18de8ccc69ebe3f1989320fb5d24dda34ef1cf54352de570f515c6e3577.png)  

#### b. 银行家算法

![picture 9](../assets/d4a962edafaccedf84433694eb07cf4663e2ffd63cc810509729c3b9138d1a69.png)  
![picture 10](../assets/18129d7cfe2b9d3c6b6615db1ab6f893a1a2eb6e83e34fe5e82ad1c7d230e3af.png)  

![picture 11](../assets/ba5295ba4630e5e83d99bafc1c70445de001b8b4ef6fc1fb658afea796d1360c.png)  

![picture 12](../assets/e5fda8ce9a5139d220c6477126b4f17232f234fab59d092039acf906278aa07c.png)  


### 7.4.3 死锁的检测和解除
#### a.死锁的检测
![picture 13](../assets/b13c9f85e8c4e24753e037da959bfa0d2a61078e2ef0a38741962d471694bd01.png)  
![picture 14](../assets/45cfd4e61b8504d1bf4fcadd338582de0bfc8a757dff48bbdf564d8c96bc063d.png)  

#### b.死锁的解除

![picture 15](../assets/4aefa601a3857d66254d3760f4aa851663c46d1c8becddf19a0eb5b734e12c20.png)  
![picture 16](../assets/ecbbed2422b6aa8f47d0d24a56987d9b0805b7eee39acee6937ebcfde4fdaacb.png)  
