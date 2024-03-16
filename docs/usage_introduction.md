---
id: intro
title: 使用概述
---

本章详细介绍几种页面对象的使用方法。

在 “入门指南》基本概念” 一节，我们简单介绍过几种页面对象，这里不再赘述。

## ✅️️ `SessionPage`

用于收发数据包的页面对象，只能收发数据包，不能控制浏览器。

### 📌 `SessionElement`

从`SessionPage`中获取的元素对象，可以从中读取元素信息。也可以之为基准获取周围或后代元素。

--- 

## ✅️️ `ChromiumPage`

用于控制浏览器的对象。除了控制一个页面，还能对浏览器整体进行操作，如调整窗口大小位置、管理文件下载、增删标签页等。

### 📌 `ChromiumTab`

浏览器标签页对象，功能与`ChromiumPage`相似。可以控制页面内部的功能，不能控制浏览器整体功能。

---

### 📌 `ChromiumFrame`

`<frame>`或`<iframe>`元素对象，既是页面对象，又有元素特性。可进行页面跳转、获取内部元素等操作。

---

### 📌 `ChromiumElement`

从上面几种浏览器页面对象中获取的元素对象，可进行交互，如点击、录入文本、拖动等。

---

### 📌 `ChromiumShadowElement`

shadow-root 对象，有元素特性，可在其中获取后代元素。

---

## ✅️️ `WebPage`

整合`SessionPage`和`ChromiumPage`两者功能的页面元素，拥有两者加起来的全部功能。运行时有 s 和 d 两种模式，能够在两种模式间同步登录信息。

### 📌 s 模式

s 模式功能与`SessionPage`一致，查找生成的元素是`SessionElement`对象。

---

### 📌 d 模式

d 模式功能与`ChromiumPage`一致，查找生成的元素是`ChromiumElement`对象。

---

## ✅️️ 配置对象

配置对象用于在页面对象创建时提供初始化信息，只在页面对象创建时生效，对象创建后再对其修改是没有效果的

### 📌 `SesssionOptions`

用于`SessionPage`和`WebPage` s 模式的配置对象。

---

### 📌 `ChromiumOptions`

用于`ChromiumOptions`和`WebPage` d 模式的配置对象。

---

## ✅️️ 关系图表

下图列出本库中要用到的各种对象的生成关系。

```
├─ SessionPage
|     └─ SessionElement
|           └─ SessionElement
├─ ChrmoiumPage
|     ├─ ChromiumTab
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     ├─ ChromiumFrame
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     ├─ ChromiumElement
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     └─ ChromiumShadowElement
|           └─ ChromiumElement
|           └─ SessionElement
├─ WebPage
|     ├─ ChromiumTab
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     ├─ ChromiumFrame
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     ├─ ChromiumElement
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     ├─ ChromiumShadowElement
|     |     └─ ChromiumElement
|     |     └─ SessionElement
|     └─ SessionElement
|           └─ SessionElement
├─ SessionOptions
└─ ChrmoiumOptions
```
