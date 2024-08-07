---
title: 创建智能脚本
sidebar_position: 3
---

# 创建自定义智能脚本

通过创建一个简单的 Hello 工作流了解 DevChat Workflow 的基本概念。

## 基本要求

在开始之前，需要安装DevChat插件:
- VSCode
- JetBrains IDE

## 创建自定义工作流

安装DevChat插件后，你的用户目录下会有`.chat/scripts`目录，这个目录用于DevChat Workflows相关管理，其中`custom`目录用于存放自定义工作流。

### 1. 创建并注册自定义命名空间`demo`

- 在`.chat/scripts/custom`目录下创建一个名为`demo`的目录。
- 在`.chat/scripts/custom`目录下创建`config.yml`文件，其内容如下：
```yaml
namespaces: 
  - demo
```

了解更多：[命名空间](../specs/namespace.md)


### 2. 在`demo`中创建`my_hello`的工作流

- 在`demo`目录下创建`my_hello`目录。
- 在`my_hello`目录下创建`command.yml`文件，其内容如下：
```yaml
description: Say hello to the world
steps:
  - run: echo "Hello World!"
  - run: echo "Have a nice day!"
```

了解更多：[工作流定义文件规范](../specs/command.md)

### 3. 运行`my_hello`工作流

打开DevChat聊天栏，输入`/my_hello`并发送。

![image](/img/quick-start-my_hello.jpeg)


## 总结

- 自定义工作流统一存放在`~/.chat/scripts/custom`目录下，通过命名空间进行管理，每个命名空间下可以有多个工作流。
- 每个工作流由一个包含`command.yml`的目录组成，目录名即为工作流名。`command.yml`为工作流的定义文件。
- 通过在 DevChat 聊天栏中发送以`/<workflow_name> `开头的消息触发工作流。

# 工作流开发指南

在[快速入门](../quick-start/create.md)中，我们创建了一个简单的DevChat Workflow。本文将展示更丰富的 DevChat Workflow 特性。


## 多层级 Workflow

工作流可随目录结构进行多层级扩展，用`.`连接各级目录组成子工作流的完整名称。

例如，对于如下`custom`目录结构：

```
custom
├── config.yml
└── demo
    ├── lang
    │   ├── command.yml
    │   ├── en
    │   │   ├── command.yml
    │   │   └── main.py
    │   ├── jp
    │   │   ├── command.yml
    │   │   └── main.py
    │   └── main.py
    └── my_hello
        └── command.yml
```
当`demo`被注册为命名空间后，4个`command.yml`文件分别对应4个工作流：
- `/lang`
- `/lang.en`
- `/lang.jp`
- `/my_hello`

`/lang.en` 和 `/lang.jp` 便是`lang`下的子工作流。

TODO: 引用example 

### 多层级 Workflow 的 workflow_python 环境共用

上级目录中`command.yml`里定义的`workflow_python`环境可在其子工作流中直接使用。子工作流也可另行定义自己单独的`workflow_python`环境。

但上级工作流无法使用子工作流中定义的`workflow_python`环境。`workflow_python`环境也不支持跨目录引用。


TODO: 引用example


## ChatMark: 在消息中进行用户交互的标记语法

语法介绍：
- [chatmark](https://github.com/devchat-ai/devchat-website/blob/main/docs/specs/chatmark.md)


### Python 封装

为了方便开发者在 Python 脚本中使用 ChatMark，我们提供了 ChatMark Python 封装。
- [ChatMark Python](https://github.com/devchat-ai/workflows/tree/scripts/lib/chatmark)
- [使用示例](https://github.com/devchat-ai/workflows/tree/scripts/lib/chatmark/chatmark_example)


## IDE Service Protocol：在工作流中与编辑器交互的协议

[IDE Service Protocol 介绍](https://merico.feishu.cn/wiki/A3LCwOUE8igbHRkhqE5cviJunyd)

TODO: 有些新接口没写到文档里，待补充


### Python 封装

为了方便开发者在 Python 脚本中使用 IDE Service，我们提供了IDE Service Python 封装。

- [IDE Service Python](https://github.com/devchat-ai/workflows/blob/scripts/lib/ide_service/service.py)
