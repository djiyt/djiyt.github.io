---
layout: post
title: 单元测试
date: 2020-1-11
tag: 学习笔记
---
# 单元测试
单元测试是对程序中的单个子程序、子程序或过程进行测试的过程，也就是说，一开始并不是对整个程序进行测试，而是首先将注意力集中在程序的较小模块的测试上面。这样做的动机有三个。首先，由于模块测试的注意力一开始集中在程序的较小单元上，因此它是一种管理组合的测试元素的手段。其次，模块测试减轻了调试（准确定位并纠正某个已知错误的过程）的难度，这是因为一旦某个错误被发现出来，我们就知道它在哪个具体的模块中。第三，模块测试通过为我们提供同时测试多个模块的可能，将并行工程引入软件测试中。
## 测试用例设计
在为模块测试设计测试用例时，需要使用两种类型的信息：模块的规格说明和模块的源代码。规格说明一般都规定了模块的输入和输出参数以及模块的功能。
模块测试总体上是面向白盒测试的。其中一个原因是如果对大一点的软件进行测试，例如一个完整的程序（其实是后续的测试过程中所针对的对象），白盒测试不容易展开。第二个原因是，后续的测试过程着眼于发现其他类型的错误（举例来说，这些错误不一定与程序的逻辑结构有关，比如程序未能满足其用户需求）。因此，模块测试的测试用例的设计过程如下：使用一种或多种白盒测试方法分析模块的逻辑结构，然后使用黑盒测试方法对照模块的规格说明以补充测试用例。
无论采用哪种逻辑覆盖方法，第一步都是要列举程序中所有的条件判断。

### 1、语句覆盖
语句覆盖，顾名思义就是针对代码语句。所有的“语句”都要覆盖一遍，它的含义是我们设计出来的测试用例要保证程序中的每一个语句至少被执行一次。通常语句覆盖被认为是“最弱的覆盖”，原因是它仅仅考虑对代码中的执行语句进行覆盖而没有考虑各种条件和分支，因此在实际运用中语句覆盖很难发现代码中的问题。举个非常简单的例子：

public int foo(int a,int b)

{

return a/b;

}

这是一个求两数之商的函数。如果我们设计如下的测试用例：

TestCase: a = 2, b = 1

这时候我们会发现，该函数的代码覆盖率达到了100%，并且设计的case可以顺利通过测试。但是显然该函数有一个很明显的bug：当 b=0 时，会抛出异常。

### 2、判断覆盖
判定覆盖也被成为分支覆盖(Branch Coverage)，也就是说设计的测试用例要保证让被测试程序中的每一个分支都至少执行一次。判定覆盖比语句覆盖强一些，能发现一些语句覆盖无法发现的问题。但是往往一些判定条件都是由多个逻辑条件组合而成的，进行分支判断时相当于对整个组合的最终结果进行判断，这样就会忽略每个条件的取值情况，导致遗漏部分测试路径。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101220255554.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM4NjUwNDcw,size_16,color_FFFFFF,t_70)

### 3、条件覆盖
条件覆盖于分支覆盖不同，条件覆盖要求所设计的测试用例能使每个判定中的每一个条件都获得可能的取值，即每个条件至少有一次真值、有一次假值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101220311654.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM4NjUwNDcw,size_16,color_FFFFFF,t_70)

通常而言条件覆盖比判定覆盖强，因为条件覆盖使得判定中的每一个条件都取到了不同的结果，这一点判定覆盖则无法保证。但条件覆盖也有缺陷，因为它只能保证每个条件都取到了不同结果，但没有考虑到判定结果，因此有时候条件覆盖并不能保证判定覆盖。
### 4、MCDC覆盖
MC/DC首先要求实现条件覆盖、判定覆盖，在此基础上，对于每一个条件C，要求存在符合以下条件的两次计算：
 1. 条件C所在判定内的所有条件，除条件C外，其他条件的取值完全相同；
 2. 条件C的取值相反；
 3. 判定的计算结果相反;

核心意思是每个条件都要独立影响判定结果。为什么说“两次计算”，而不是“两个用例”呢？当循环中有判定时，一个用例下同一判定可能被计算多次，每次的条件值和判定值也可能不同，因此，一个用例就可能完成循环中判定MC/DC。

MC/DC是条件组合覆盖的子集。条件组合覆盖要求覆盖判定中所有条件取值的所有可能组合，需要大量的测试用例，实用性较差。MC/DC具有条件组合覆盖的优势，同时大幅减少用例数。满足MC/DC的用例数下界为条件数+1，上界为条件数的两倍，例如，判定中有三个条件，条件组合覆盖需要8个用例，而MC/DC需要的用例数为4至6个。如果判定中条件很多，用例数的差别将非常大，例如，判定中有10个条件，条件组合覆盖需要1024个用例，而MC/DC只需要11至20个用例。
### 5、判定条件覆盖（Decision/Condition Coverage）
判定条件覆盖，说白了就是我们设计的测试用例可以使得判断中每个条件所有的可能取值至少执行一次（条件覆盖），同时每个判断本身所有的结果也要至少执行一次（判定覆盖）。不难发现判定条件覆盖同时满足判定覆盖和条件覆盖，弥补了两者各自的不足，但是判定条件覆盖并未考虑条件的组合情况。
![+](https://img-blog.csdnimg.cn/20200101220339194.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM4NjUwNDcw,size_16,color_FFFFFF,t_70)
### 6、组合覆盖（Branch Condition Combination Coverage）
组合覆盖也叫做条件组合覆盖。意思是说我们设计的测试用例应该使得每个判定中的各个条件的各种可能组合都至少出现一次。显然，满足条件组合覆盖的测试用例一定是满足判定覆盖、条件覆盖和判定条件覆盖的。条件组合覆盖能够同时满足判定、条件和判定条件覆盖，覆盖度较高，但是组合覆盖的测试用例数量相对来说也是比较多的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101220516931.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM4NjUwNDcw,size_16,color_FFFFFF,t_70)
### 7、路径覆盖
路径覆盖，意思是说我们设计的测试用例可以覆盖程序中所有可能的执行路径。这种覆盖方法可以对程序进行彻底的测试用例覆盖，比前面讲的五种方法覆盖度都要高。那么这种方法是不是就一定最好呢？当然不能讲得这么绝对，它的缺点也是显而易见的：由于需要对所有可能的路径全部进行覆盖，那么我们需要设计数量非常巨大的而且较为复杂的测试用例，用例数量将呈现指数级的增长。所以理论上来讲路径覆盖是最彻底的测试用例覆盖，但实际上很多时候路径覆盖的可操作性不强。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101220535432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM4NjUwNDcw,size_16,color_FFFFFF,t_70)

 ###   单元测试方法总结
在实际的操作中，要正确使用白盒测试的代码覆盖方法，就要从代码分析和代码调研入手，根据调研的结果，可以选择上述方法中的某一种，或者好几种方法的结合，设计出高效的测试用例，尽可能全面地覆盖到代码中的每一个逻辑路径。
|是否引用了当前入口点无关的形参|——|
|常数是否以实参形式传递过|——|
### （3）代码走查
走查和代码检查很相似，但是进行的规格和使用的错误发现技术稍有不同，走查实施的过程中，走查人员对程序进行模拟，一步步演示程序是如何处理相关数据的，在模拟程序的过程中，每个走查组的成员在自己的脑海中也进行着程序逻辑的模拟，这样一来能够高效的发现程序中的错误，并且可以精确的定位这些错误。
### （4）同行评审
同行评审是一种通过作者同行来确认缺陷和需要变更区域的检查方法，它涉及的范围比较广，主要分为管理评审，技术评审，文档评审和过程评审等，简而言之，同行评审的对象并不只是程序，而是软件生命周期中可能产生的各类产品，同时，同行评审的技术和方法从非正式的到最严谨的都各不相同，在评审过程中，应该先了解评审经常出现的问题有哪些，然后采取相对应的对策进行解决。
