[![Build Status](https://travis-ci.org/alibaba/jarslink.svg?branch=master)](https://travis-ci.org/alibaba/jarslink)
[![Coverage Status](https://coveralls.io/repos/github/alibaba/jarslink/badge.svg?branch=master)](https://coveralls.io/github/alibaba/jarslink?branch=master)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.alicp.jetcache/jetcache-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.alicp.jetcache/jetcache-parent/)
[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)


JarsLink (原名Titan) 是一个基于JAVA的模块化开发框架，它提供在运行时动态加载模块（一个JAR包）、卸载模块和模块间调用的API。

# 需求背景

- 应用拆分的多或少都有问题。多则维护成本高，每次发布一堆应用。少则拆分成本高，无用功能很难下线。
- 故障不隔离。当一个系统由多人同时参与开发时，修改A功能，可能会影响B功能，引发故障。
- 多分支开发引发冲突。多分支开发完之后合并会产生冲突。
- 牵一发动全身。一处核心代码的改动，或一个基础Jar的升级需要回归整个系统。
- 升级和迁移成本高。中间件升级每个应用都有升级成本。


# 模块化开发的好处

![](http://ifeve.com/wp-content/uploads/2017/08/Snip20170806_31.png)

- 可插拔，一个应用由多个模块组成，应用里的模块可拆和合，模块可快速在多个系统中迁移和部署。
- 模块化开发，模块之间互相隔离，实现故障隔离。
- 一个模块一个分支，不会引发代码冲突。
- 在模块中增加或修改功能，只会影响当前模块，不会影响整个应用。
- 动态部署，在运行时把模块部署到应用中，快速修复故障，提高发布效率。
- 多版本部署，可以在运行时同时部署某个模块的新旧版本，进行AB TEST。
- 减少资源消耗，通过部署模块的方式减少应用数量和机器数量。

# JarsLink的应用场景

- 微服务集成测试, 目前一个微服务是一个FAT JAR,如果有几十个微服务,则需要启动很多进程,DEBUG端口会很多,使用JarsLink框架合并FAT JAR,再路由请求到其他JAR,就可以只启动一个进程进行DEBUG测试。
- 数据管理中心，数据采集的数据源多，而且每种数据源都需要对接和开发，通过模块化开发，实现一个数据源使用一个模块进行对接。
- 指标计算系统，每个TOPIC一个模块，把消息转发到模块中进行消息处理。
- 后台管理系统，几乎每个系统都有后台开发的需求，新建应用则应用数多，维护成本高，引入模块化开发，一个二级域一个模块来开发后台功能。

目前蚂蚁金服微贷事业部几个系统和几十个模块已经使用JarsLink框架。

# JarsLink的特性

## 隔离性

- 类隔离：框架为每个模块的Class使用单独的ClassLoader来加载，每个模块可以依赖同一种框架的不同的版本。
- 实例隔离：框架为每个模块创建了一个独立的Spring上下文，来加载模块中的BEAN，实例化失败不会影响其他模块。
- 资源隔离：后续会支持模块之间的资源隔离，每个模块使用独立的CPU和内存资源。

## 动态性

- 动态发布：模块能在运行时动态加载到系统中，实现不需要重启和发布系统新增功能。支持突破双亲委派机制，在运行时加载父加载器已经加载过的类，实现模块升级依赖包不需要系统发布。
- 动态卸载：模块能在运行时被动态卸载干净，实现快速下线不需要功能。

## 易用性

提供了通用灵活的API让系统和模块进行交互。

# 文档

- [如何使用](https://github.com/alibaba/taitan/wiki/如何使用)
- [实现原理](https://github.com/alibaba/taitan/wiki/实现原理)
- [应用场景](https://github.com/alibaba/taitan/wiki/应用场景)
- [高级特性](https://github.com/alibaba/taitan/wiki/高级特性)


# 下载

- [1.5.0.20171107版本](http://ifeve.com/wp-content/uploads/2018/02/jarslink.zip)
- [更多版本](https://oss.sonatype.org/#nexus-search;quick~com.alipay.jarslink)


# *License*

JarsLink is released under the [Apache 2.0 license](https://github.com/alibaba/jarslink/blob/master/LICENSE).

```
Copyright 1999-2017 Alibaba Group Holding Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at following link.

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```