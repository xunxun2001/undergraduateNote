# 1. 程序的装入与链接

## 1.1 创建步骤

![picture 16](../assets/09e8ab086b1b7e3e4ee3c10849fdacf07abf5fe0a83b61b32bee3fd2ab16ba59.png)  


## 1.2 链接的类型

![picture 17](../assets/55bdf417dcc939fdd753bd41ccf9e37cb6988002286ad8cee339371164b72cc9.png)  


## 1.3 装入模式(地址转换)

![picture 13](../assets/c9d62d91e9f28d8e83d0514f43abae89314158aaed12d044e7a8fa317b8efe43.png)  


![picture 11](../assets/cae095bc2165ff17ac06b532e24239c91fa20763dee62c28f3776ee2b4e70668.png)  
![picture 12](../assets/00884aa5e08c5ec4daa1f691018f656a8c9d1dbc0583fc4e26f5d68f03e5aacf.png)  
![picture 14](../assets/29f62391b21b7350987b5d7f55048590618e46c30213c23990b640ce54186bc9.png)  


# 2. 内存管理的概念 + 内存保护、扩充

>   - **内存管理**
>     - 内存分配和内存回收
>     - 内存保护
>       - 确保每道用户程序都只在自己的内存空间内运行，彼此互不干扰
>       - 方法①：设置一对**上下限寄存器**
>       - 方法②：**重定位寄存器**（又称**基址寄存器**）与**界地址寄存器**（又称**限长寄存器**）进行越界检查
>           - 重定位寄存器：`起始物理地址`
>           - 界地址寄存器：`最大逻辑地址`
>     - 地址映射
>       - 将地址空间中的**逻辑地址**转换为内存空间中与之对应的**物理地址**（见1.3）
>     - 内存扩充
>       - 从逻辑上去扩充内存容量，使用户所感觉到的内存容量比实际内存容量大得多  
>       - 方法①（用于早期`OS`）：**覆盖技术**——将程序分为多个段，常用的段常驻内存，不常用的段在需要时调入内存
>           - 内存中分一个**固定区**和若干个**覆盖区**
>           - 常用的段放在**固定区**，运行结束才会调出
>           - 不常用的段放在**覆盖区**，需要时调入内存，用不到时调出内存
>           - 按照逻辑结构，让不可能被同时访问的程序共享一个覆盖区
>       -  方法②：**交换技术**
>           - 把处于等待状态（或在CPU调度原则下被剥夺运行权利）的进程从内存移到辅存，把内存空间腾出来，这一过程又叫**换出**
>           - 把准备好竞争CPU运行的进程从辅存移到内存，这一过程又称为**换入**
>           - 外存的什么位置保存？什么时候交换？换出哪些进程？
>       -  方法③：**虚拟存储技术**

![picture 1](../assets/7cb093340cc4da99bbd41849de92b003ea5c3ba88910e3daa808bb0e16394f49.png)  


![picture 2](../assets/2ee4fcbc10e20419bc14d86e054468a698b8b6bdd5c2bb65d5d2441fe4af8d40.png)  
![picture 3](../assets/ad1eb87691531697d00865cbd6a806928dd4cfd7cf1afd552b9ff6926c45bba9.png)  

![picture 4](../assets/331600b4e70e104f6ab68a23a5a468f10e7626e4ab1c0c3de61af4e5555d8fc7.png)  

# 3. 内存分配

## 3.1 连续分配

### 3.1.1 单一连续分配

![picture 6](../assets/0347dec175407297ca431bab4915dc7e7aea6b747a3930dddc0817e66c9b3454.png)  



### 3.1.2 固定分区分配

![picture 7](../assets/9918bf9c61acf72b66ec83199d92587df1ac48a1f800ec3ceb87a03f7a4e4096.png)  
![picture 8](../assets/940dfb15ef72daa237412f215a5dea08928a8d93a9353647b41e861228b89cd5.png)  

### 3.1.3 动态分区分配
> - 不会预先将内存划分
> - 在进程装入内存时，根据进程的大小动态的建立分区，并使分区的大小正好适合进程的需要
> - 没有内部碎片，**但是有外部碎片**
>   - **内部碎片**：分配给某进程的内存区域中，有些部分没有用上
>   - **外部碎片**：内存中的某些空闲分区因**太小而难以利用**
>  - **克服**外部碎片可以通过**紧凑(compaction)**技术来解决，就是操作系统不时地对进程进行移动和整理。但是这需要**动态重定位**的支持，且相对费时
> - 系统要用怎样的数据架构记录内存的使用情况？
> - 当很多个空闲分区都满足需求时，选择哪个分区进行分配？
> - 如何进行分区的分配和回收





#### a. 系统要用怎样的数据架构记录内存的使用情况？
![picture 9](../assets/8de7cf3d7c12e76c64a940016d9e94077e51cdfd9983e7ab104412c79397e88e.png)  


#### b. 当很多个空闲分区都满足需求时，选择哪个分区进行分配？（动态分区分配算法）
![picture 20](../assets/3f849c556e8882f2f06c3dd170292f06b9d1d6271e960a6547b0666fdaf96580.png)  

##### 首次适应算法
> 空闲分区：地址递增排列

![picture 15](../assets/2eca22968ab8525dc4dbbf77e4cd2cf6cd3405df09e63af5861a040b362e942d.png)  

##### 最佳适应算法

> 空闲分区：容量递增排列

![picture 17](../assets/82ce8ecf2ede712bd4e23396065e0ed494acb9d49b67c987437ef53e43683ed7.png)



##### 最差适配算法——最坏适配
> 空闲分区：容量递减排列

![picture 18](../assets/a629fc7e0020d5753572364d33a55c375f0c693ef7cc3536a5df2380ebdabcaa.png)  


##### 循环首次适应算法
> 空闲分区：地址递增排列
> 
> 循环链表

![picture 19](../assets/bcc089c6425cc48bd8295650d23b1581579cb253b67f1acc007ef9174e33e2df.png)  



#### c. 如何进行分区的分配和回收？

![picture 10](../assets/db09e69f3f9cb198460a6f12d0fd049b623fa703ef32697ac0e1a7e969044f3b.png)  
![picture 12](../assets/a567185c80061a6bdf336f1c4272a4428ef92682bed06216d95e7b9641b326f2.png)  

![picture 13](../assets/1a18c3cc562f967213035d37665ccefd26c181c2d07a4673a6fe842eea454c36.png)  
![picture 14](../assets/c36554829bfebdf907c0f75c19d0c3fbed5de705547bfa4ea53487936c264435.png)  



## 3.2 离散分配

### 3.2.1 分页存储

> 与固定分区技术很像，但是其分页相对于分区又很小，分页管理**不会产生外部碎片**，产生的**内部碎片也非常的小**


![picture 1](../assets/e233e5b0e253cb79d958d68e5046183f2818cf736086235fcb4ce36628537fa3.png)  
![picture 2](../assets/edaf3c9f9328ae2b2d181261964b27781108bb62b7edb12540a9530585b390c4.png)  

#### a. 每一个页表项占多少Byte

![picture 3](../assets/7814d197e6ebd25d7c5d629d11688ae63a85c45336724f4f4523774d8f1d28d8.png)  

> - 而页号不需要占存储空间——>因为页表项是连续存放，页号可以是隐含的（类比数组）

![picture 4](../assets/4dd0e4f53701e2bef25c6494f9f0d283463f206a7310ebd940a7e9aa9efc6591.png)  
![picture 5](../assets/807aa3762185a05989688b3e4c9fa091818d8d4274eac61bad100aa498f5f7d4.png)  

#### b. 如何实现地址的转换

> - K位“页内偏移量”<——————>一个页面大小2**k个内存单元
> - M位“页号”<——————>一个进程最多允许2**m个页面

![picture 6](../assets/f075620e14389db91d616f8534e65e05eeebd2672bc745830c3e0142488d7f31.png)  
![picture 7](../assets/6fbf7cd2da4e13e3658e857d17f02f341fbcb2bcf3d0e95c168281a2e5a8e245.png)  
![picture 8](../assets/cc5022108f9f03670a84cbd8d9a4e8ac48628798afa0d6a1749ee47a78aeccea.png)  
![picture 9](../assets/198bf0c2aee58c9f58d7c0aae978d83920a80e9c797d3bf71fd4d5facee09ce9.png)  

#### c. 地址映射机构

![picture 10](../assets/b9c04fe5ba7f49411e88700cc712e144e087bd9b1d9217aa23150c39c19d42e1.png)  
![picture 11](../assets/b24d66f15975fffedce925c0c14ba1bfd39f75b594c1dffb5d9375d40a28d4dc.png)  
