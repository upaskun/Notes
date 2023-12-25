# Intermediate Representation

## Compiler

源代码 -> 词法分析 -> 语法分析 -> 语义分析 -> IR

<img width="503" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/4b4465ee-d238-493d-957c-b9d53bd912f6">

静态分析的对象一般是IR
IR特点
+ 语言无关
+ 接近机器语言
+ **包含控制流信息**
<img width="497" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/9dc05294-9410-4756-8691-9f9746e24471">

### 3-Address Code(3AC)

3地址码是一种语言的中间表示形式，它的特点是一个等式的右边最多只有一个操作符。静态分析一般使用三地址码。

Method Signature： class name: return type(我是空格)method name(parameter1 type, parameter2 type,... )

<img width="499" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/1c7f54c2-3b6b-4d3e-8de6-100cd1b4d361">

### SSA（静态单一赋值）

每一个等式左边都会是一个新的变量，比如对于
> a = a + b

对于SSA来说是
> a1 = a + b

在SS中每个变量都只有一个定义

<img width="497" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/7e1a8013-a25b-43ca-be34-e7fc5f48d1ca">

对于存在分支的情况，SSA引入了φ函数

<img width="503" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/89a55083-bbf4-4f6a-bb3b-b0494a4fc52d">

SSA的优点, 将程序流信息间接嵌入到唯一的变量名中。（flow-insensitive速度更快，但是丢失一些信息，降低程序分析的精度）
SSA会引入很多变量，还涉及φ函数，并且如果要拿来用，还得再转一层，所以一般不会用SSA来进行分析。

## Control Flow Analysis

Control Flow Craph(CFG)
CFG的节点可以是单一的3AC，也可以（通常）是Basic Block(BB)

### BB的特点

只有唯一的入口和出口, 且需要是满足前面条件的最大指令集合

<img width="499" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/b60e6efa-9f7d-4e80-8d23-f2e18b16b48d">

### 构建CFG 

1. 确定BB 

<img width="503" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/61bb8e73-2d5a-45fd-847d-cdb9358e08ae">

2. 添边

<img width="503" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/c9c7d109-9631-4a47-bd63-244af85ccc57">

3. 添加Entry 和 Exit节点

<img width="504" alt="image" src="https://github.com/upaskun/Notes/assets/82031259/0f356b9f-8257-4cfb-8a6b-770f450639e1">

可能有很多边指向了Exit Node
