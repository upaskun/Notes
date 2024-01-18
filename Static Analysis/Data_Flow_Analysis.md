# 数据流分析

数据流分析： 研究数据如何在控制流图上流动


may analysis： 可能发生的要全部包含 (over approximation)

must analysis: 包含的一定要发生 (under approximation)

Over approximation->Safe-approximation

数据抽象，符号定义，从左到右依次是

正号、负号，0，unknow, undefine

<img width="92" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/9184325f-a2a3-4936-a9b4-6cb8c8557286">

不同类别的数据流分析，有不同的数据抽象策略

<img width="499" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/7bcf37e6-a3b0-4d04-8388-bc7a713c65d0">

<img width="499" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/284254e5-8c15-47aa-85f5-b41b0b4203c1">

每个program point都对应了程序状态中所有数据流的一个**抽象**

<img width="497" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/1a8c09f6-2c5a-4d7e-91d3-502b532f10ff">

通过data-flow分析，找到使每个申明的IN和OUT都满足safe-approximation的约束规则

## 应用

### 1. 可达性分析

定义

<img width="494" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/bdfceacd-644e-4c3c-b051-13909e1adc45">

v在p到q的路径中不能被重新定义

Safe-approximation从两个角度看
 
+ Transfer Function

  函数定义(可以正向也也可以反向)

  <img width="498" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/02a558c8-fe1d-47bf-94bb-355f45cc0e7c">

  定义
  
  <img width="266" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/2a75c532-0a6a-4fad-b3a2-d602c2b85c54">

  🌰

  <img width="412" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/015a2044-8f77-48e3-9c8f-71f19b8a6e52">

+ Control Flow

  函数定义

  <img width="500" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/a57f09a4-575d-427c-9316-6ddd59179be5">

  may analysis
  
  定义

  <img width="271" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/ea513217-4134-4e25-9c1b-3229f6336cdf">

Reaching Definitions Analysis算法

迭代算法

<img width="496" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/fb9da9be-60a1-4fa2-8fff-371b0b3f8d29">

停止的条件是没有任何BB的OUT发生变化

例子

<img width="494" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/24d5eee9-a011-4ca9-a10c-12fff88a8933">

当IN没有变化，OUT也就不会变化，反之亦然

### Live Variables Analysis(活跃变量分析)

#### 定义

变量v，从p点开始，在CFG中，存在至少一条路径使用了它(言外之意: v不应该在被使用前被重新定义)

<img width="501" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/4b2b5a97-df60-4fcb-8748-4d950f5802a8">

先use再define，IN\[B\] 就不为空

#### Transfer Function 

<img width="263" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/efa7e064-a65b-4814-9235-743935cb4b77">

#### 算法(后向)

<img width="501" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/00618d75-debe-4e21-8aa1-2167dc90cd47">

> 一般情况下may analysis初始化为空，must analysis初始化是all

🌰

<img width="501" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/42f4cb3e-6687-4403-be13-a2167370b0b5">

### Available Expressions Analysis(可行表达式分析) 

#### 定义

**Must Analysis**

如果表达式*x op y*对于程序点p来说满足下面两点
1. 所有以p为入口点的路径都经过*x op y*
2. 在*x op y*之后*x*和*y*都没有再被定义

#### Transfer Function

<img width="270" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/5966bbd0-dc8c-4f61-91c3-a3fb38a5f319">


Rule

<img width="492" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/06b03ee7-e880-4b2b-bd10-c270f1403617">

🌰

<img width="190" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/41d486d6-e07c-49e5-9058-2b26d26bf55d">

上面这个🌰满足。。。

#### 算法

<img width="501" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/b219977b-6eb8-403d-a30d-6aa93d3e9253">

🌰

<img width="501" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/300cdc1e-161f-41a9-aecd-a91afc82cba7">

## 基础


