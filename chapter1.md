# 查询语句和转变（Queries and Mutations）

在这一页里，你将会了解到如何在一个GraphQL服务器上查询。

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

在之前的例子里，我们只是查询英雄的名字对应 String 的回馈，但是 fields 也能指向对象。在这种情况里，你能给那个对象创建一个 fields 的 _sub-selection。GraphQL语句能遍历相关联的对象和它们的 fields，让客户端能够在一次请求中获取到多个相关数据_

