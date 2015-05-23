# 关于 #
EasySNS 是由EasySNS Team基于Code Igniter开发的SNS平台,在09年4月以BSD协议发布开源版本.
该协议允许用户在保留版权的前提下任意修改,分发和用于商业.

# 注意 #
由于easysns.com域名过期导致后台自定义模块不可用,请手工更新以下代码修复该问题:

修改 \application\libraries\Service.php

第7行
> $this->url\_base = 'http://alpha.easysns.com/service/';

修改为
> $this->url\_base = 'http://dhbus.com/service/';


即可.

目前SVN中的代码已经做了同步更新.

# Staff #
**产品设计 Easychen**

**代码实现 十月**

**部分插件开发 小北**

# 功能简介 #

**突破SNS界限,融合内容,社区和商务,提供一站式体验**

**完全本地化的组件,您的数据完全由您控制**

**智能组件生成向导, 不懂技术也能轻松创建想要的组件**

# 特色功能 #

EasySNS最核心的功能,是解决目前SNS中存在的两大问题.

1 封闭式SNS的围墙问题.
2 用户不能获得自己想要的SNS应用的问题.

第一个 - 封闭式SNS的围墙问题

目前大多数SNS都是封闭式的,用户不注册和登录完全不知道里边的内容.这就是围墙.
EasySNS通过widgets来解决这个问题.

用过msn space的应该都比较熟悉基于widgets的自定义页面,EasySNS的App包含了一个Widgets目录,而网站的首页可以通过简单的拖拽操作将原来深藏在APP里边的信息显示到首页上.

![http://photo.hainei.com/b0/01/5s/k711293.jpg](http://photo.hainei.com/b0/01/5s/k711293.jpg)

拖拽布局

![http://photo.hainei.com/b0/01/5s/kf11034.jpg](http://photo.hainei.com/b0/01/5s/kf11034.jpg)

考虑到一个首页不一定够用,我们添加了页面导航和页面管理,可以创建任意多个页面并指定起布局和属性,通过这部分功能,已经可以轻松搭建一个网站的骨架了.

![http://photo.hainei.com/b0/01/5s/kk11257.jpg](http://photo.hainei.com/b0/01/5s/kk11257.jpg)

围墙的问题到此就基本解决了.

第二个问题  - 用户不能获得自己想要的SNS应用的问题.


应用雷同是小型SNS遇到的最大的问题,一百个SNS,都是公模出来的,再装上一样的应用.这很难发挥出自己的特色.而开发应用本身却又是一件很麻烦的事情.

机器当然不可能取代程序员,我们显然不可能完美的解决这个问题.但是EasySNS可以通过在线代码生成技术来提升在分享领域应用创建的速度和质量.

程序后台,我们提供了”自定义”栏目,在这里,你可以轻松创建一个分享类型的应用.比如电影,比如图书,比如游戏…

![http://photo.hainei.com/b0/01/5s/kp11548.jpg](http://photo.hainei.com/b0/01/5s/kp11548.jpg)

设置组件基本属性

![http://photo.hainei.com/b0/01/5s/l111294.jpg](http://photo.hainei.com/b0/01/5s/l111294.jpg)

设置组件数据字段

![http://photo.hainei.com/b0/01/5s/l419966.jpg](http://photo.hainei.com/b0/01/5s/l419966.jpg)

调整生成页面的布局

![http://photo.hainei.com/b0/01/5s/l519742.jpg](http://photo.hainei.com/b0/01/5s/l519742.jpg)

最终生成应用效果

![http://photo.hainei.com/b0/01/5s/l719743.jpg](http://photo.hainei.com/b0/01/5s/l719743.jpg)

由于代码都是生成为独立的App,即使有地方不符合需求,也可以直接修改app中的代码进行调整.比起从头开发来,要快太多.

# About #
Easysns is an open source social networking platform that based on Code Igniter framework and developed by webmagik team.
This project has only Chinese version now .

# Features #
**news feed**

**personal message**

**forum**

**shopcart**

**plugin wizard**
