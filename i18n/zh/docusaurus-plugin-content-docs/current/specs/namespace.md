---
slug: /namespace
description: 组织智能脚本和命令的目录
sidebar_position: 1
---

# 命名空间

命名空间是`custom`目录下的子目录，用于将工作流分组，以便更好地管理和组织自定义工作流。

## `config.yml` 配置

### `namespaces`字段

命名空间注册列表，列表中的每个元素为一个命名空间名。

命名空间需要显式注册后才会被启用，列表顺序为命名空间的优先级顺序。当多个命名空间下存在同名工作流时，只会执行优先级最高的命名空间下的工作流。

例如，以下配置文件中，`demo`命名空间的优先级高于`team_a`命名空间。如果`demo`和`team_a`下都存在`hello`工作流，则`/hello`只会触发`demo`命名空间下的`hello`工作流。
```yaml
namespaces: 
  - demo
  - team_a
```

#### 自定义命名空间与默认命名空间的优先顺序
DevChat Workflow Engine中有两个默认命名空间`merico`和`community`，它们与自定义命名空间的优先顺序从高到低为：
- 所已注册的自定义命名空间
- `merico`
- `community`
