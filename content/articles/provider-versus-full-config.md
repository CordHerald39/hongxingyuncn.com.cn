---
title: "节点集合不是完整配置：proxy-providers 导入位置与更新检查"
category: "tutorials"
label: "实用教程"
description: "区分仅节点列表、完整 Clash 配置与其他客户端格式，核对 provider 引用与策略组 use。"
date: "2026-10-04"
updated: "2026-10-04"
author: "红杏云中文资料编辑"
draft: false
---

## 先确认文件承担的角色

同样是 YAML 文件，有的包含完整配置，有的只是节点集合。完整配置可能包括入站、代理组和路由规则；provider 文件通常为代理集合提供节点。sing-box 配置又有自己的结构，不能把扩展名当作兼容证明。

## 看结构而非服务品牌

在本机查看脱敏副本的顶层键，确认服务方为目标客户端提供哪种格式。若仅有节点内容，不应期待它自动带来你的分流规则。不要把密码和订阅 URL 上传给格式识别或转换网站。

## 核对引用链

在支持 mihomo 的配置中，proxy-providers 定义集合，策略组使用 use 引用对应名称。集合名称、缓存路径应避免冲突，且最终规则需要指向存在的策略组。节点集合下载成功，只证明一段引用链成功。

~~~yaml
# 仅展示名称关系，不是一份可连接配置
proxy-groups:
  - name: 我的选择
    type: select
    use:
      - 我的节点集合
~~~

示例必须配合实际存在的 provider，不能单独导入后期待节点出现。

## 更新时分开检查

先确认 provider 获取成功，再查看集合内节点，最后确认策略组仍引用该集合。若节点变少，检查 filter 或 exclude-filter，不直接认定服务删除了节点。缓存旧内容与筛选结果也要分开判断。

不要为了修引用覆盖整份主配置；优先通过客户端支持的扩展方式修改，失败便回到旧配置。基础导入见[导入订阅](/tutorials/import-subscription/)。

## 原始资料

[mihomo proxy-providers](https://wiki.metacubex.one/en/config/proxy-providers/)和[代理组](https://wiki.metacubex.one/config/proxy-groups/)定义集合与引用；[sing-box 配置](https://sing-box.sagernet.org/configuration/)展示另一套格式。本文不保证红杏云提供上述全部输出格式。
