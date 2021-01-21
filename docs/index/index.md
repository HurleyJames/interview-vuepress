# 序论 <Badge text="New"/>

::: callout 🍳 本章内容
欢迎来到 **Campus Recruitment Interview Experience** —— 这是根据自身校招经历总结的Android/Java技术方向求职者的「**校招面经**」。

前事不忘，后事之师。希望通过这份校招面经，能帮助更多的学子们，披荆斩棘，收获Offer大礼包！
:::

## 1. 文档简介

* 📚 本文档是面向Android/Java技术栈方向的校招应届求职者的面经总结，涵盖了Java编程语言、Android相关知识、数据结构、操作系统、算法（LeetCode）、数据库、计算机网络等基础知识。
* 🛠 本文档基于[VuePress]()开发，使用的是[vuepress-theme-book]()主题，基于Markdown来管理知识系统。
* 🙏 由于本人水平有限，本文档内容如有任何错误，欢迎提出[Issue]()或者进行`Pull Request`。本文档遵循[MIT]()协议，如果转载请注明出处。

## 2. 自我介绍

> 本人本科就读于NCHU的软件工程专业，硕士就读于[the University of Leeds]()的[Advanced Computer Science(AI)]()专业。虽然本人硕士期间从事的是AI方向，但毕业设计参与的是一个区块链端智能合约开发的项目，且学制较短没有拿出手的论文，所以选择没有尝试国内「灰飞烟灭」的算法岗。最终选择投递了很多互联网厂的移动端开发岗位，除此之外，还有各种大型国企、银行的软件开发工程师岗位。

## 3. 面经版块

* [Java]()：面试复习内容的Java部分。
* [Android]()：面试复习内容的Android部分。
* [操作系统]()：面试复习内容的操作系统部分。
* [计算机网络]()：面试复习内容的计算机网络部分。
* [算法（LeetCode）]()：面试复习内容的算法部分。因为国内大厂都喜欢考LeetCode上的题目，所以主要以LeetCode上的简单、中等难度题目为主。
* [数据库]()：面试复习内容的数据库部分。

## 4. 简历润色

> 一份好的简历对于招聘的简历筛选环节、面试环节都非常有帮助。如果一份简历过于简单或者平淡无奇，那么有可能无法通过大公司HR的筛选；如果一份简历过于炫技、或者过于吹捧自己的能力，那么在面试环节，面试官可能会因为你的简历抬高对你的要求，面试问题难度可能会更大，最终可能会得出「华而不实」的结论。所以，如果编写一份属于自己的好的简历，也同样是一个面试的重要pre部分。

在这里，最掐当的方式是「**准备多份不同的简历**」。针对不同类型的**公司**和**岗位**来投递相应的简历。岗位这里就不再多说，自然是根据投递的岗位，在自己的简历中突出自己的技能与岗位的相关度。下面主要详细叙述，针对不同的公司性质，如何准备不同的简历。

### 4.1. 互联网大中厂

就本人经验而言，互联网大中厂大多看重求职者的**基础知识**是否扎实。例如，下面是字节XX公司对于移动端开发岗位的需求：

![招聘要求](https://i.loli.net/2021/01/21/3dHzuDrPXZcxVKq.png)

我们可以发现，它并不在意求职者擅长哪门编程语言，只需要求职者的数据结构、操作系统、网络等知识扎实即可。所以，如果您投递移动端开发岗位，但您只有C++的编程经验，也并无大碍。因为大厂的业务、人员都很多，它们有足够的时间和空间来培养。您只要在简历中突出，您的数据结构、操作系统、网络等基础知识扎实即可。除此之外，最好在简历上有任何编程相关的**项目**、**实习经历**等，都属于加分项。

就本人参与面试的2020年秋招而言，除了大中厂的算法岗位竞争激烈之外，别的开发岗位都是急需人才。所以，只要您的学习背景是本科学历以上，专业符合计算机、软件工程等，就很有可能能够获得面试的机会。但是，切忌不要在简历中使用过多的吹捧自己的词语，比如不要随便使用「**精通**」两个字，不然可能会让面试官提出非常难的问题。

### 4.2. 互联网小厂/传统软件公司

对于一些互联网小厂（小于500人，甚至小于200人的团队），还有一些传统的软件公司，如X潮X软等，它们招聘的需要一般是看重的求职者具备的实战能力。例如，如果您会熟练使用到一些业界流行的主要框架，如Java开发工程师需要的Spring，Redis等，那么相对而言，你面试通过的概率会大一些。但这并不代表你不需要掌握基础知识，只是总体难度会比大厂相对简单一些，特别是在算法的考察方面，会更容易一些。

总而言之，编写一份能够突出您实战技能的简历，对于进入小厂工作十分有帮助。

### 4.3. 国企/银行

第三点与前两者又大有不同。如今，很多人找工作都紧盯着互联网公司投递，毕竟优渥的薪水的确十分令人羡慕。但是毕竟僧多粥少，并且互联网加班风气更甚，所以也有相对少部分人会选择另外一条道路——国企/银行。

既然是国企性质的单位，它对于技术的要求就会相对降低，因为国企不会使用太过于前沿的开源技术，一切保证安全稳定性为主。所以，对于应聘者的要求，只需要掌握基本的计算机基础知识，然后拥有不错的学历即可。

那么，在简历这关，我们就不能只关注于显示我们擅长的技术，例如学历、四六级英语证书、学生会经历都是面试国企的加分项。同时需要注意，简历应以简单质朴为主，不可太过于花哨；在个人评价这一块，也多介绍自己有关团队合作等一些优秀的品质，而不是只关注于擅长技术的方面。

### 4.4 简历网站

> 工欲善其事，必先利其器。

既然以上提到了要面对不同的公司和岗位，准备不同的简历，那么，使用合适的简历模板就至关重要。请尽量避免在淘宝上购买销量最多的简历模板，因为那样可能有太多人都是这样使用了，并且个人认为是太过于花哨而不实。所以，这里建议可以考虑以下的方案：



## 5. 书籍推荐

下面只是推荐有关于准备最开始提到的面试版块的复习书籍推荐：


## 6. 内推/面经网站

下面有一些常用的面试需要用到的网站，上面既会有一些求职者分享的面试经历，还要一些内部员工发布的内推帖子。通过使用内推码，可以让您的简历更加容易通过，直达面试官的电脑。