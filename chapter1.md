# 查询语句和转变（Queries and Mutations）

在这一页里，你将会了解到如何在一个GraphQL服务器上查询。

### 

### Fields

最简单来说，GraphQL就是关于询问对象里特定的fields。让我们从看一个非常简单的语句和运行之后获得的结果开始：

```js
{
  hero {
    name
  }
}
```

```js
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```

你可以立即看见查询结果有完全一样的数据结构。这对于GraphQL来说是很有必要的，因为你总是得到你所想要的，而且服务器准确的知道客户端要求的fields是什么。

Field _name_ 返回一个 _String _类型，在这个情况下是星际争霸主角英雄的名字_“R2-D2”_。

> 对了，还有一件事 - 上面的语句是交互性（interactive）的。言下之意你可以按照你的喜好来获取新的结果。试着在查询语句里添加一个 _appearsIn_ field 到 _hero_ 对象里，然后看新的结果

在之前的例子里，我们只是查询英雄的名字对应 String 的回馈，但是 fields 也能指向对象。在这种情况里，你能给那个对象创建一个 fields 的 _sub-selection。GraphQL_语句能遍历相关联的对象和它们的 fields，让客户端能够在一次请求中获取到多个相关数据，而不是像传统的REST架构里需要反复请求多次。

```js
{
  hero {
    name
    # Queries can have comments!
    friends {
      name
    }
  }
}
```

```js
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "friends": [
        {
          "name": "Luke Skywalker"
        },
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        }
      ]
    }
  }
}
```

在这个例子中可以看到，_friends_ field 返回了一组数据单元。对于GraphQL语句来说，单数据元还是一个列表的数据元都是一样的，但是基于表达的数据模式我们知道最后会获得的是哪一个。

### 参数

如果我们只能遍历所有对象和它们的 fields，那么GraphQL 已经是最有用的数据接收语言。但当你增加给 fileds 传参数的能力，就更有意思了。

```js
{
  human(id: "1000") {
    name
    height
  }
}
```

```js
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}
```

在像REST这样的系统里，你只能在请求中传入单组参数 - 查询参数和URL部分。但是在GraphQL中，每一个field和嵌套对象都能获取它们自己的参数组，让GraphQL完全替代了多API接收的机制。你甚至可以将参数传入递进fields，得以一次性在服务器端完成数据传输，而不需要在每个客户端分开做。

```js
{
  human(id: "1000") {
    name
    height(unit: FOOT)
  }
}
```

```js
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 5.6430448
    }
  }
}
```

参数能够以多种类型呈现。在上面的例子中，我们使用了一种枚举（Enumeration）类型，它代表了有限选项集中的其中一个（在这种情况下，是长度单位，METER 或者 FOOT）。GraphQL 有一个默认类型组，但是GraphQL服务器也能声明它自己的自定义类型，只要它们能够被序列化到你的传输模型中就行。

[点击阅读更多关于GraphQL类型系统的信息。](http://graphql.org/learn/schema)

