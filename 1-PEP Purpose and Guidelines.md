>  如果你为Python写了一篇PEP,这篇PEP成功的被Python指导委员会接受了,那么以后你在吹牛皮的时候你就可以说我主导了Python语言某个特性的设计工作.
>                                   							
>                                   					-- 跬蟒

我就问你主导Python语言特性设计牛不牛皮,今天我就写一篇文章告诉大家如何去为Python设计一篇PEP,并且整个PEP从一个想法到Python语言去实现它的这一套流程:

>  假设你已经是一个Python高手了,在使用Python给过程中你觉得Python语言在某方面还不够完善,你有一个不错的想法可以去改善Python这方面的不足,你打算把你的想法加入到Python语言里面,所以你打算写一篇PEP,为Python的发展献言建策,那首先需要做什么呢?

  1. 首先你要确保你的想法是个新的想法是个比较大的想法,是一个由必要去建立一个PEP的想法,也许你发现了Python的一些小问题,但是这些小问题如果提交一个小补丁就可以解决了,那就没必要提PEP 
  1. 当你确定自己的想法很牛B之后,你也不是马上就要提PEP,你首先要做的事情是引发社区的讨论,看看其他人怎么看,然后自己去实现一下这个想法看是否是可行的,并且发帖到 `python-list@python.org mailing list`或者到` python-ideas@python.org mailing list` 进行进一步的确定,看看大家对你的想法是否认同,如果你能让大多数人都认同,那你就有戏,在你发帖之前最好准备一份高质量的PEP草稿,这样的话才会更容易的被接受
  1. 总之就是先讨论,得到大家的认可,避免后期不必要的撕逼,然受自己也要做好准备,最好有个简单的实现,然后还有个高质量的PEP草稿

## 写PEP你不得不知道的几个Python社区角色

> PEP champion :  `PEP拥护者` 也就是PEP的发起人,也就是跟大家说我有个非常XXX的想法的人

> PEP author:  `PEP作者` 就是写PEP的人,PEP从一个想法到一篇PEP草稿,再到一篇拥有官方PEP编号的PEP文档,到后面PEP审核通过,PEP复审出现改动,PEP被接受这个过程中维护PEP文档的人就是PEP的作者,大部分PEP作者就是PEP拥护者本人

> PEP reviewer: 这个角色不是单指某一个人,一个PEP从想法到实现需要经过很多此review, 每一次参与review的人都可以被称作 PEP reviewer

> PEP editor: `PEP编辑者` 就是对PEP进行初步审核的人,审核通过的PEP进入到github上面的PEP仓库的master分支,进行下一轮的评审

> Python Core Developers: `Python核心开发人员` 就是开发Cpython解释器的那群人,都是大佬,都是大佬

>  Python's Steering Council: `Python指导委员会` 大佬中的大佬,从`Python核心开发人员`中选择出来的指导Python语言开发工作的一群人,对于PEP是否接受有着最终发言权


  PEP的工作流程是这样的:
  1. PEP champion 先有一个高质量的idear(经过讨论分析和理性验证)
  1. 你去github上面去fork PEP仓库
  1. 在仓库中创建一个 pep-9999.rst的文件去把你的PEP草稿粘贴进去
  1. 确定你的PEP的类型,PEP的状态设为草稿,PEP头部按照模板写一波
  1. 把你的pep-9999.rst push到PEP仓库
  1. 然后PEP editors 会去审核你的提交
  1. 如果审核通过,这个本来是草稿的PEP会拿到一个正规的PEP编号,如果没有审核通过那PEP editors 会打回去让 PEP author 去修改
  1. 如果PEP审核通过拿到了PEP编号 PEP editor 会把这个新提交的PEP合并到PEP仓库的 master 分支
  1. 如果你的PEP的类型是Standards Track类,那你提交的PEP还会被发送给Python-dev list 成员进行再次review, 确保你的新PEP没有坑
  1. 有些听起很不错的PEP在实现的时候其实是非常蛋疼的,没做的时候想的挺好,真正去实现的时候才知道是否靠谱,最好的情况时你在提交PEP的时候你手里就已经有一个这个PEP的原型实现了,所以如果你的PEP类型是Standards Track类型那你就不仅需要准备设计文档,你还需要准备一个参考实现,以此来避免一些不切实际的想法

当然凡事都有例外,有些Python的核心开发者是不会走这个流程的因为他们本身的权限比较大,他们有直接push内容到PEP仓库的权限,所以有时候他们会直接给自己的PEP分配一个PEP编号push进入PEP仓库的master分支,当然这并不意味着这个PEP就被接受了,他只是绕过了PEP editor的审批而已,PEP被接受和PEP通过审批是完全两码事儿,只有通过Python指导委员会的同意,PEP计划实现,才能叫做PEP被接受.


## 如果我写的PEP无法审核通过被拒怎么办?

  PEP被拒绝是很正常的事情,不要灰心,只要能够坚信自己的PEP是真正对Python有用的东西,真正好的idear,修改一下继续上就行了,但是被拒肯定是有原因的,最主要的原因就是下面几条:

  1. 该特性已经存在了
  1. 技术上不合理
  1. Python不需要去实现这样的特性,也就是说伪需求
  1. 无法进行后向兼容
  1. 不符合Python的设计哲学(Python设计哲学可以在Python交互解释器中输入import this获取)其实在PEP的审批阶段可以拿着自己的PEP idear去咨询Python指导委员会,因为PEP最终会不会被接受其实是由Python指导委员会所决定的,所以如果真的想要自己的PEP被接受,做好提前的沟通还是非常有必要的
  1. 奥对了还有一个蛋疼的要求,就是你的PEP草稿必须带着至少一名Python核心开发人员一起写,或者有一个Python核心开发人员指导你写,或者有一个经过Python指导委员会批准的非Python核心开发人员一起写,反正就是需要有一个能够被Python指导委员会所信任的人参与了你的PEP设计,如果没能满足这个条件 PEP editor有权直接驳回你的PEP草稿


## PEP的复审和决定机制

  一篇PEP是否最终被接受并且决定去实现是需要经过层层复审的,反正要经过很麻烦了一个流程,下面有个Python官方画的简单流程图:
![](https://cisco-test-images.oss-cn-shenzhen.aliyuncs.com/chrome_20_06_06_22_419_220.png)
  但是实际情况比较复杂,有时候不会按照这个流程图来,但是这个流程图给人们提供了一个比较清晰的PEP工作流的概览


## PEP格式和模板

  这年头写啥文档没个模板真不行,PEP也是文档,所以模板搞起来:

  1. 首先PEP是UTF-8编码的rst文件,首先你需要去指导rst文件的格式,如果rst的语法格式你已经会了,那你就可以阅读官方的`PEP 12--Sample reStructuredText PEP Template`,没错PEP12是介绍rst格式PEP模板的PEP(有点绕),为什么要用rst格式?官方给出的解释是 容易转成html进行在线发布和阅读
  1. 每一篇PEP必须有一个标准的PEP头部,如下所示,带* 号是可写可不写的,不带* 号的是必须要写的,记住写PEP头的时候,头的各个字段的顺序,必须按照下图的内容去写,先后顺序不能乱

![](https://cisco-test-images.oss-cn-shenzhen.aliyuncs.com/chrome_20_06_07_09_746_489.png)


写道这里就讲的差不多了,但是其实PEP的书写还有很多的内容比如:

> 1. 如何判断PEP是不是一个成功的PEP
> 1. PEP提交之后发现内容有bug怎么解决
> 1. PEP所有权以及所有权转移问题
> 1. PEP editor的详细职责和工作流
> 1. 等等问题,我就不写了,写不动了.....

想写PEP的可以先根据上面流程走一波,然后等到遇到问题的时候再去查资料吧.如果感觉本篇内容还不错,微信的朋友请点个在看,其他平台的朋友可以扫描下方的二维码关注我的公众号 `早睡蟒`更多优质原创无广告内容等你来看.



![](https://cisco-test-images.oss-cn-shenzhen.aliyuncs.com/test.png)




  

