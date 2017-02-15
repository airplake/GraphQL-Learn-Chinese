# GraphQL介绍

> 在这一系列的文章中我们将学习GraphQL是怎样工作的。想要通过文档知道如何打造GraphQL服务？这里有一些库可以帮助你在很多不同语言里实现GraphQL。

GraphQL是一种支持API的查询语言，同时也是根据你的数据自定义类型（type）系统的服务端热执行查询。GraphQL并没有绑定任何数据库或内存引擎，而是完全基于你现有的代码和数据。

一个GraphQL服务是通过定义类型（type）和type上的fields, 然后给每一个type里的fields提供函数来创建的。比如，一个GraphQL服务要告诉我们谁是已登陆的用户（我自己）以及用户的名字可能会是这样的：

```js
type Query {
  me: User
}

type User {
  id: ID
  name: String
}
```

对应每一个type里的field的函数：

```js
function Query_me(request) {
  return request.auth.user;
}

function User_name(user) {
  return user.getName();
}
```

当一个GraphQL服务正在运行时（通常在一个web服务的URL上），可以通过发送GraphQL语句来进行验证和执行。一个收到的查询语句会首先被检查以保证它被指向被定义的types和fields，然后运行提供的函数来执行结果。

比如这个语句：

```js
{
  me {
    name
  }
}
```

能够生成以下JSON结果：

```js
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

学习更多关于GraphQL - 查询语句，类型系统，GraphQL服务如何工作，以及用GraphQL来解决一般问题的最佳实践 - 这些就是这个部分所写的内容。

