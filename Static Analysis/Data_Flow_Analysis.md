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

