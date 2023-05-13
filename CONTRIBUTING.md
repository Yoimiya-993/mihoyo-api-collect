# 米哈游API收集

你好！这里是mihoyo-api-collect社区贡献指南。本文主要面向想向本仓库贡献文档的用户。

---

## 项目定义

米哈游API收集（mihoyo-api-collect，MhyAC）项目是一个仅用于学习与研究、社区开源、公益性质的，与[米哈游](https://www.mihoyo.com/)旗下应用与游戏的API（应用程序接口）文档，使用CC-BY-NC 4.0协议开源。它将无差别收集整理所有相关的接口。

## 基础

该项目始终使用[Markdown](https://markdown.com.cn/)格式进行书写。

文档索引按照业务类型及功能以**路径、文件**索引。

任何用户都可通过拉取请求（Pull Request）提供自己分析出的接口地址与其使用说明。

## 标题、文件夹与路径结构

### 标题

在[README.md](README.md)目录下的标题用于分类米哈游不同的应用、游戏的API。

### 文件夹

文件夹层级应当与[README.md](README.md)的目录一致，文档均存放于项目根路径的文件夹中，文件夹命名统一使用英文，如`原神`为`genshin_impact`，米游社为`hoyolab`。

2级、3级……文件夹应当存在其对应[README.md](README.md)目录的2级、3级……

### 文件

文档目录以**列表**形式在[README.md](README.md)中，使用缩进标识文档的层级，例如，`米游社`下有`用户`分类，其下又有例如`用户信息`、`用户游戏信息`等文档链接。文件名命名统一使用英文。

## 文档内容格式

注：文档格式可根据实际情况进行调整。

### 文档头部

文档的首行使用**1级标题**，描述这篇文档是属于哪一类别的。

标题下方为**文档目录**，与正文中的**2级标题**对应。该目录使用**列表**与缩进，每项使用**超链接**实现点击跳转到对应标题。

[例子](/hoyolab/user/game_account_info.md)：

```markdown
# 游戏账号信息

- [原神](#原神)
  - [获取玩家首页信息](#获取玩家首页信息)
  - [获取玩家角色信息](#获取玩家角色信息)

---

```

### 接口说明

文档可能需要说明多个接口，应该遵守同一格式，并依次排序在文档中。

接口说明分为以下几个部分：

- 标题：接口的简要说明（几个字）。
- 服务器标识（按情况标识）：米哈游的游戏一般有国服和国际服，若国服与国际服的请求接口不同，请进行标识“国服”或者“国际服”并使用粗体。一般国服接口在前。若没有这样的区分，则无需标注。
- 请求方式：接口的请求方式，GET、POST或Socket等。HTTP请求方式最好使用大写字母。使用斜体。
- 请求头验证（按情况标识）：一些接口需要验证请求头的信息，则需要标注“需要验证请求头”，置于引用块中并使用斜体。下一行需要标注请求头的信息，如`x-rpc-client_type`。见[鉴权](/other/authentication.md#请求头)以了解应该标注哪些请求头。若该接口需要验证额外的请求头，也需要标注。若不需要验证请求头，则无需标注。
- 鉴权（按情况标识）：一些接口需要登录账号，则需要标注“需要验证网页/应用Cookie”，置于引用块中并使用斜体。见[鉴权](/other/authentication.md#cookie)以了解Cookie的内容。若该接口需要验证额外的Cookie，也需要标注。若不需要验证Cookie，则无需标注。
- 接口网址（URL）：接口的完整URL，使用等宽字体。
- 备注（可选）：该接口使用的注意事项。

例子：

```markdown
## 获取玩家首页信息

**国服：**

_请求方式：GET_

> _需要验证请求头_
> 
> `x-rpc-client_type`：`5`
> 
> _需要验证网页Cookie_

`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/index`

```

### 请求参数

请求参数应该在[接口说明](#接口说明)下方。使用粗体。

使用**表格**对参数及其内容进行整理，需要填写POST请求体或URL参数的参数键、参数数据类型、参数填写内容、参数备注。

数据类型应使用JSON数据类型英文缩写：

- `bool`：布尔。
- `num`：数字。
- `str`：字符串。
- `arr`：数组。
- `obj`：对象（字典、集合）。

需要使用下面的格式：

```markdown
| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | --- |
| 参数 | JSON数据类型简写 | 参数应填写内容 | 参数备注 |
```

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | --- |
| 参数 | JSON数据类型简写 | 参数应填写内容 | 参数备注 |
| 参数2 | …… | …… | …… |
| …… | …… | …… | …… |


例子：

```markdown
**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role_id | num | 原神UID | |
| server | str | 服务器名称 | |
| param1 | num | 参数示例 | 可选 |
```

### 返回值

返回值应该在[请求参数](#请求参数)下方，使用粗体。

需要填写返回数据类型。

若返回类型为JSON数据，则填写`JSON返回`。
若返回类型为图片数据，则填写`<图片格式>返回`。
以此类推。



若返回数据类型为JSON数据，则按以下格式。

使用**表格**对JSON的各个数据及其内容进行整理，需要对返回JSON数据的所有值进行说明。

每个表格一般只描述一个对象或数组。

使用`→`符号（而不是`->`、`=>`等形式）来标注对象、数组的嵌套关系。

例子：

```markdown
`data`对象→`role`对象→`params`对象：
```

如果需要对一个数组进行说明，在其后再加入数组中的数据类型。

例子：

```markdown
`data`对象→`avatars`数组→对象：

<!-- 如果数组中有多个数据类型 -->
`data`对象→`biz`数组→数据：
```



每个字段应有：

- 字段（只有对象有，如果为数组则不需要该项。若数组按一定顺序放置数据，则替换该表头为“索引”）
- 类型（如果该数据在数组中，且该数组中的数据类型只有1种，则不需要该项）
- 内容描述
- 备注

数据类型应使用JSON数据类型英文缩写。



具体可查看例子：

```markdown
**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 用户游戏账号信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role | obj | 玩家基础信息 | |
| dict | obj | 描述 | |

`data`对象→`role`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 玩家名称 | |
| dested | arr | 数组中数据的类型不是数组和字典 | |
| dested_2 | arr | 数组中的对象 | |
| order_dested | arr | 顺序排列的数组，或数组中的每个数据不相同 | |

`data`对象→`role`对象→`dested`数组→数字：

| 内容 | 备注 |
| ---- | --- |
| 描述 | 备注 |

`data`对象→`role`对象→`dested_2`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| dested_data | str | 字符串 | |

`data`对象→`role`对象→`order_dested`数组→数据：

| 索引 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| 0 | str | 第1个数据 | |
| 1 | num | 第2个数据 | |


`data`对象→`dict`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| desc | str | | |
| title | str | | |
```





