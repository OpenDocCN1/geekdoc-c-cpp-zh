

# Web 应用开发指南：Ember.js 指南

![](img/00001.jpeg)

## 免责声明

尽管已尽一切努力验证书中提供的信息，但作者对书中包含的错误、遗漏或对主题内容的相反解释不承担任何责任。书中提供的信息仅供教育和娱乐之用。读者对其自己的行为负责，作者对使用这些信息而产生的任何实际或感知的责任或损害不承担任何责任。

书中使用的商标均未获得任何许可，且商标的出版未获得商标所有者的许可或支持。书中的所有商标和品牌仅用于说明目的，其所有权归所有人，与本文无关联。

## 引言

对 Web 应用的需求正在增加。`Ember JS` 是一种可以辅助开发此类应用的 JavaScript。该框架很容易学习，特别是对于 JavaScript 专家来说。然而，即使你完全不擅长 JavaScript，也不担心，因为书中的解释对你来说非常容易。通过这种 JavaScript，你可以创建具有高度交互性界面的 Web 应用，你的用户一定会喜欢你的应用。

## 第 1 章 控制器（Controllers）

控制器非常像组件，人们认为这些未来将由组件取代。

在大多数当前应用中，控制器并不经常使用。当使用它们时，它们承担以下职责：

1. 用于根据当前使用的路由维护状态。
2. 当用户操作从组件传递到路由时，它们必须经过控制器。

我们需要通过使用路由来演示这一点，这可以帮助我们显示博客文章。

模板将绑定到模板中的以下属性：

```html
<h1>{{model.title}}</h1>
<h2>by {{model.author}}</h2>
<div class="intro">
  {{model.intro}}
</div>
<hr>
<div class="body">
  {{model.body}}
</div>
```

如上面的示例所示，我们没有特定的属性或操作需要显示。

假设我们需要添加一个功能，允许用户切换正文部分的显示。为了实现这一点，我们将代码修改为如下：

```html
<h1>{{model.title}}</h1>
<h2>by {{model.author}}</h2>
<div class='intro'>
  {{model.intro}}
</div>
<hr>
{{#if isExpanded}}
  <button {{action "toggleBody"}}>隐藏正文</button>
  <div class="body">
    {{model.body}}
  </div>
{{else}}
  <button {{action "toggleBody"}}>显示正文</button>
{{/if}}
```

在我们的控制器的“actions”钩子中，我们可以定义操作的内容，就像我们在组件中做的那样。如下面的代码所示：

```javascript
export default Ember.Controller.extend({
  actions: {
    toggleBody() {
      this.toggleProperty('isExpanded');
    }
  }
});
```

### 控制器之间的依赖管理

有时，当我们嵌套资源时，我们通常需要在两个控制器之间建立连接。考虑下面的路由器：

```javascript
Router.map(function() {
  this.route('post', { path: '/p/:post_id' }, function() {
    this.route('comments', { path: '/comments' });
  });
});
```

在访问 URL `/posts/1/comments` 时，模型 `post` 将加载到 `PostController` 的模型中。然而，与之相关的某些信息可能会显示在 `comments` 的模板中。

为了实现这一点，我们必须将 `pController` 注入到 `CommentsController` 中。如下：

```javascript
export default Ember.Controller.extend({
  pController: Ember.inject.controller('post')
});
```

我们的注释将能够访问 `PController`，它是一个只读别名，可用于从控制器中读取模型。考虑下面的代码：

```javascript
export default Ember.Controller.extend({
  pController: Ember.inject.controller('post'),
  post: Ember.computed('pController')
});
```

考虑下面的代码：

```html
<h1>{{post.title}} 的评论</h1>
<ul>
  {{each model as |comment}}
    <li>{{comment.text}}</li>
  {{/each}}
</ul>
```

## 第 2 章 模型（Models）

构建 Web 应用的方法之一是实现与数据高度耦合的组件。考虑你正在创建一个博客的情况。以下代码演示了这一点：

```html
<h1>{{post.title}} 的评论</h1>
<ul>
  {{each model as |comment}}
    <li>{{comment.text}}</li>
{{/each}}
</ul>
```

注意，应用是由组件组成的。你可能希望将所有草稿显示在另一个页面上。这可能需要将旧代码复制到组件中：

```javascript
export default Ember.Component.extend({
  willRender() {
    $.getJSON('/myDrafts').then(data => {
      this.set('drafts', data);
    });
  }
});
```

按钮的 `.hbs` 文件如下：

```html
{{#link-to 'drafts' tagName="button"}}
草稿 ({{drafts.length}})
{{/link-to}}
```

通过上述操作，应用将发出两次独立的请求。

在 Ember 数据中，模型的表示是使用模型的子类完成的，它定义了呈现给数据的属性和行为。通过模型可以定义服务器提供的数据类型。考虑下面名为 `human` 的模型示例：

```javascript
export default DS.Model.extend({
  fName: DS.attr('string'),
  birthday: DS.attr('date')
});
```

模型还可以描述自身与其他模型之间的关系。考虑下面的示例，它展示了如何这样做：

```javascript
export default DS.Model.extend({
  lItems: DS.hasMany('line-item')
});
```

上面的代码是用于订单的。`line.js` 的代码如下：

```javascript
export default DS.Model.extend({
  order: DS.belongsTo('order')
});
```

你需要注意的是，模型本身没有数据，但它们用于定义特定实例（称为“记录”）属性和行为。

### 创建记录（Creating Records）

当你需要创建记录时，只需在 store 上调用 `createRecord()` 方法。考虑下面的代码：

```javascript
store.createRecord('post', {
  title: 'Ember 是一个很棒的框架',
  body: 'Lorem ipsum'
});
```

存储的对象可以通过 `this.store` 用于控制器和路由器。

### 更新记录（Updating Records）

可以通过设置需要更改的属性来修改 Ember JS 数据记录。如下代码所示：

```javascript
this.store.findRecord('human', 1).then(function(myfunction) {
  // ...一旦记录被加载
});
```

```javascript
myfunction.set('fName', "John");

});
```

所有 Ember.js 的便利方法始终可用于修改属性。操作方法如下：

```javascript
human.incrementProperty('age'); // 生日快乐！
```

### 持久化记录

在 Ember JS 中，记录是基于实例进行持久化的。当你对任何 `DS.Model` 实例调用 `save()` 方法时，将发送一个网络请求。

默认情况下，EmberJS 中新创建的记录将被提交（post）到 Ember data 中的类型 URL。如下代码所示：

```javascript
var p = store.createRecord('post', {
  title: 'Ember is Great',
  body: 'Lorem ipsum'
});

p.save(); // => POST to '/posts'
```

后端已存在的记录将通过 HTTP `PATCH` 动词进行更新。代码所示：

```javascript
store.findRecord('post', 1).then(function(p) {
  p.get('title'); // => "Ember JS is Great"
  p.set('title', 'New post');
  p.save(); // => PATCH to '/posts/1'
});
```

考虑以下代码：

```javascript
human.get('isAdmin');            //=> false
human.get('hasDirtyAttributes'); //=> false
human.set('isAdmin', true);
human.get('hasDirtyAttributes'); //=> true
human.changedAttributes();      //=> { isAdmin: [false, true] }
```

可以通过检查记录的属性 `hasDirtyAttributes` 来判断待处理记录是否包含某些尚未保存的更改。

在上述位置，你可以通过调用 `save()` 方法来保存更改，或者直接将其回滚。考虑以下代码：

```javascript
human.get('hasDirtyAttributes'); //=> true
human.changedAttributes();      //=> { isAdmin: [false, true] }
human.rollbackAttributes();

human.get('hasDirtyAttributes'); //=> false
human.get('isAdmin');            //=> false
human.changedAttributes();      //=> {}
```

### 处理验证错误

如果你尝试保存时，后端服务器返回了验证错误，那么你的模型的 `errors` 属性将包含这些错误。错误的显示方式如下所示：

```handlebars
{{#each p.errors.title as |err|}}
  <div class="error">{{err.message}}</div
{{/each}}

{{#each p.errors.body as |err|}}
  <div class="error">{{err.message}}</div
{{/each}}
```

### Promises

`save()` 方法将返回一个 promise，这使得我们易于处理成功或失败的情况。考虑下面的常用模式：

```javascript
var p = store.createRecord('post', {
  title: 'Ember is Great',
  body: 'Lorem ipsum'
});
var self = this;

function transitionToPost(p) {
  self.transitionToRoute('posts.show', p);
}

function failure(reason) {
  // 处理错误
}

p.save().then(transitionToPost).catch(failure);
// => POST to '/posts'
// => transitioning to posts.show route
```

### 删除记录

记录的删除方式与创建记录相同。可以在 `DS.Model` 实例上调用 `deleteRecord()` 方法。这会将记录标记为 `isDeleted`。随后应该调用 `save()` 方法来保存记录的删除操作。考虑以下代码：

```javascript
store.findRecord('post', 1).then(function(p) {
  p.deleteRecord();
  p.get('isDeleted'); // => true
  p.save(); // => DELETE to /posts/1
});

// 或者

store.findRecord('post', 2).then(function(post) {
  p.destroyRecord(); // => DELETE to /posts/2
});
```

### 关系

Ember 拥有几个内置关系，定义了模型之间的相互关系。

### 一对一

如果你需要在两个模型之间声明这种类型的关系，请使用以下代码：

这里是文件 `myuser.js` 的代码：

```javascript
export default DS.Model.extend({
  profile: DS.belongsTo('profile')
});
```

`profile.js` 文件应如下：

```javascript
export default DS.Model.extend({
  user: DS.belongsTo('myuser')
});
```

### 一对多关系

这种类型的关系可以在两个模型之间如下声明：

考虑文件 `myposts.js` 的代码：

```javascript
export default DS.Model.extend({
  comments: DS.hasMany('comment')
});
```

这里应该是文件 `ourcomments.js` 的代码：

```javascript
export default DS.Model.extend({
  post: DS.belongsTo('p')
});
```

### 显式反向

Ember JS 会尽力发现组件之间存在的关系类型。有时，你可能对同一种类型有不同的关系。

考虑以下代码：

```javascript
export default DS.Model.extend({
  first: DS.belongsTo('post'),
  second: DS.belongsTo('post')
});
```

这里是文件 `mypost.js` 的代码：

```javascript
export default DS.Model.extend({
  comments: DS.hasMany('comment')
});
```

### 自射关系

为了定义反射关系，你应该已经拥有反向关系。如果没有反向关系，可以将其设置为 `null`。示例所示：

```javascript
export default DS.Model.extend({
  parent: DS.belongsTo('folder')
});
```

### 创建记录

假设我们有两个模型 `myposts` 和 `comments`。它们的关系如下：

`myposts.js` 的代码：

```javascript
export default DS.Model.extend({
  comments: DS.hasMany('comment')
});
```

`comment.js` 文件如下：

```javascript
export default DS.Model.extend({
  post: DS.belongsTo('post')
});
```

要移除一个 `belongsTo` 关系，我们只需要将其设置为 `null`。这将从 `hasMany` 关系的一侧将其移除。考虑下面的代码，它最清楚地说明了这一点：

```javascript
let comm = this.store.peekRecord('comment', 1);

comm.set('post', null);

comm.save();
```

记录也可以从 `hasMany` 关系中移除。考虑下面的代码，它很好地展示了如何实现这一点：

```javascript
let p = this.store.peekRecord('post', 1);

let comm = this.store.peekRecord('comment', 1);

p.get('comments').removeObject(comm);

p.save();
```

### 关系作为承诺（Promises）

每当你处理关系时，最好始终记住这些关系将返回 promise。假设我们要处理一个文章的异步评论，我们应该等待直到我们的 promise 被完成（fulfilled）。考虑下面的代码：

```javascript
let p = this.store.peekRecord('post', 1);

p.get('comments').then((comments) => {
  // 我们现在可以处理这些评论了
});
```

同样的情况也适用于 `hasMany` 关系，如下所示：




```javascript
let comm = this.store.peekRecord('comment', 1);

comm.get('post').then((p) => {
  // 文章将在这里可用
});
```

Handlebars 模板会自动更新，以反映已解析的 promise。文章中可以显示评论列表，如下所示：

```html
<ul>
  {{#each p.comments as |comm|}}
    <li{{comm.id}}</li>
  {{/each}}
</ul>
```

### 将记录推入数据存储器（Store）

Store 可以被看作一个缓存，其中包含了应用已加载的所有记录。

要将记录推入 store，你只需要调用 `push()` 方法。考虑这样一种情况：在应用首次启动后，我们需要先将某些数据预加载到 store 中。这可以通过 `route:application` 轻松地完成。考虑下面的代码：

```javascript
export default DS.Model.extend({
  title: DS.attr(),
  artist: DS.attr(),
  songCount: DS.attr()
});
```

考虑接下来这段代码：

```javascript
export default Ember.Route.extend({
  model() {
    this.store.push({
      data: [{
        id: 1,
        type: 'album',
        attributes: {
          title: 'Very Few Moving Parts',
          artist: 'John Joel',
          songCount: 5
        },
        relationships: {}
      }, {
        id: 2,
        type: 'album',
        attributes: {
          title: 'Our God is Great all the time',
          artist: 'Steve John',
          songCount: 3
        },
        relationships: {}
      }]
    });
  }
});
```

如果数据在推入 store 之前需要通过模型的默认序列化器（serializer）进行归一化处理，可以使用 `story.pushPayload()` 方法。下面的代码展示这一点：

```javascript
export default DS.RestSerializer.extend({
  normalize(typeHash, hash) {
    hash['songCount'] = hash['song_count']
    delete hash['song_count']
    return this._super(typeHash, hash);
  }
})
```

接下来的代码应该如下所示：

```javascript
export default Ember.Route.extend({
  model() {
    this.store.pushPayload({
      albums: [
        {
          id: 1,
          title: 'Very Fever Moving Parts',
          artist: 'John Joel',
          song_count: 5
        },
        {
          id: 2,
          title: 'Our God is Great all the time',
          artist: 'Steve John',
          song_count: 2
        }
      ]
    });
  }
});
```

在处理复杂的端点（endpoints）时，`push()` 方法非常重要。你的应用可能有一个端点，负责执行某些逻辑并创建几条记录。下面的代码演示了这一点：

```javascript
export default Ember.Route.extend({
  actions: {
    confirm: function(d) {
      $.ajax({
        data: d,
        method: 'POST',
        url: 'process-payment'
      }).then((digInventory) => {
        this.store.pushPayload(digInventory);
        this.transitionTo('Thanks');
      });
    }
  }
});
```

### 处理元数据（Metadata）

除了从 store 返回的记录外，还需要处理某种形式的元数据。元数据只是与某些模型或类型关联而非记录的数据。

分页是元数据的一种的一种常用方式。考虑一个有很多文章的博客，它们无法一次性显示。可以像下面所示进行查询：

```javascript
let res = this.store.query('post', {
  limit: 10,
  offset: 0
});
```

为了获取不同页的数据，可以以 10 为步长更改 `offset`。问题在于知道你有多少页数据。为了获取不同页的数据，我们可以以 10 为步长设置 `offset`。对于服务器来说，它需要将记录的总数作为元数据返回。

每个序列化器期望的元数据返回方式不同。考虑下面的代码：

```json
{
  "post": {
    "id": 1,
    "title": "Ember is easy to learn for beginners",
    "comments": ["1", "2"],
    "links": {
      "user": "/posts/ember"
    }
  },
  "meta": {
    "total": 100
  }
}
```

无论使用哪种序列化器，元数据都会从响应中提取。要读取它，可以使用 `.get('meta')`。这可以应用于 `store.query()` 调用的结果上。这里是代码：

```javascript
store.query('post').then((res) => {
  let metad = res.get('meta');
})
```

如果我们有一个 `belongsTo` 关系，可以这样操作：

```javascript
let p = this.store.peekRecord('post', 1);
p.get('author').then((author) => {
  let metad = author.get('meta');
});
```

在 `hasMany` 关系上，可以这样操作：

```javascript
let p = this.store.peekRecord('post', 1);
p.get('comments').then((comments) => {
  let metad = comments.get('meta');
});
```

### 适配器（Adapters）的自定义

在 Ember Data 中，适配器负责确定数据如何持久化到 store，例如 RESTful API 的格式和请求头。

对于具有某些规则的端点，可以定义 `adapter:application`。它的优先级高于默认适配器，但会被特定模型的适配器覆盖。下面的代码展示了这一点：

```javascript
export default DS.JSONAPIAdapter.extend({
  // 此处定义应用配置
});
```

默认情况下，Ember Data 自带多个内置适配器。如果你需要创建自定义适配器，可以以这些为起点。一个很好的例子是，当你运行命令 `ember generate adapter post` 时，会创建如下文件：

```javascript
export default DS.JSONAPIAdapter.extend({
  namespace: 'api/v1'
});
```

#### URL 约定

`JSONAPIAdapter` 适配器在根据模型类型确定用于通信的 URL 时非常有用。考虑下面通过 ID 请求文章的示例：

```javascript
store.find('post', 1).then(function(p) {
});
```

#### 复数形式自定义

有时，你可能需要在生成路由 URL 时处理模型名称的复数形式。可以使用 Ember 反射（reflector）来实现此目的。这是一个用于在单数和复数形式之间转换单词的库。对于不可数或不规则的复数，可以使用 `Ember.Inflector.inflector()`。可以像下面所示轻松完成：

```javascript
// 设置 Ember.Inflector
import './models/custom-inflector-rules';
```

接下来的代码如下：

```javascript
import Inflector from 'ember-inflector';

const inflect = Inflector.inflector;

inflect.irregular('formula', 'formulae');

inflect.uncountable('advice');

// 符合 Ember Inspector 导出的预期
export default {};
```

```javascript
export default DS.JSONAPIAdapter.extend({
  namespace: 'api/1'
});
```

这就是实现方法。

### 宿主机自定义（Host Customizations）

适配器默认指向当前域名。如果你需要指定新域名，只需在新的适配器上设置 `host` 属性即可。下面的代码很好地展示了如何实现：

```javascript
export default DS.JSONAPIAdapter.extend({
  host: 'https://api.sample.com'
});
```

就是这样。

### 路径自定义（Path Customizations）

可以像下面的代码所示，重写 `pathForType` 方法：

```javascript
export default DS.JSONAPIAdapter.extend({
  pathForType: function(type) {
    return Ember.String.underscore(type);
  }
});
```

在上述情况下，我们不需要将模型名称变为复数形式，并且需要使用下线命名（underscore）而不是驼命名法（camelCase）。

### 请求头自定义（Headers Customizations）

某些 API 需要 HTTP 请求头，一个很好的例子是需要提供 API 密钥时。可以将任意请求头作为 `JSONAPIAdapter` 头对象上的键值对进行设置，Ember data 将在我们的每个 Ajax 请求中发送。考虑下面的代码：

```javascript
export default DS.JSONAPIAdapter.extend({
  headers: {
    'API_KEY': 'secret key',
    'ANOTHER_HEADER': 'A header value'
  }
});
```

人们还可以将 `headers` 作为计算属性，以支持动态请求头。考虑下面的示例，请求头将根据会 服务通过计算属性生成。以下是该示例的代码：

```javascript
export default DS.JSONAPIAdapter.extend({
  session: Ember.inject.service('session'),
  headers: Ember.computed('session.authToken', function() {
    return {
      'API_KEY': this.get('session.authToken'),
      'ANOTHER_HEADER': 'A header value'
    };
  })
});
```

在某些情况下，动态请求头可能来自 Ember 观察者系统之外的对象数据。还可以使用 `volatile` 函数将属性设置为非缓存模式，这将导致每次请求都重新计算请求头。如下代码所示：

```javascript
export default DS.JSONAPIAdapter.extend({
  headers: Ember.computed(function() {
    return {
      'API_KEY': Ember.get(document.cookie.match(/apiKey\=([^;]*)/), '1'),
      'ANOTHER_HEADER': 'A header value'
    };
  }).volatile()
});
```

### 编写适配器（Authoring Adapters）

`defaultSerializer` 属性将用于指定适配器使用的序列化器。这仅在没有指定 `serializer:application` 或特定模型的适配器时才使用。在任何应用程序中指定 `serializer:application` 都非常简单。考虑下面的示例展示了如何实现：

```javascript
export default DS.JSONAPIAdapter.extend({
  defaultSerializer: '-default'
});
```

### 自定义序列化器（Customizing Serializers）

在 Ember data 中，序列化器用于格式化发送到后端存储以及从后端存储接收的数据。默认设置是 Ember data 将使用 JSON API 格式进行数据序列化。

#### JSON API 文档（JSON API Document）

考虑我们请求的如下响应：

```json
{
  "data": {
    "type": "people",
    "id": "567",
    "attributes": {
      "first-name": "John",
      "last-name": "Joel"
    }
  }
}
```

在上述示例中，我们得到了对 `/people/567` 请求的响应。包含多个记录的响应可以在 `data` 属性中包含一个数组，如下：

```json
{
  "data": [{
    "type": "people",
    "id": "567",
    "attributes": {
      "first-name": "John",
      "last-name": "Joel"
    }
  }, {
    "type": "people",
    "id": "345",
    "attributes": {
      "first-name": "Mercy",
      "last-name": "Donald"
    }
  }]
}
```

#### 侧载数据（Sideloaded Data）

这类数据不属于主请求的一部分，但具有一些关联关系，这些关系应该被添加到 `included` 键下的数组中。考虑下面的代码：

```json
{
  "data": {
    "type": "blogs",
    "id": "1",
    "attributes": {
      "title": "I really like and blogging!"
    },
    "links": {
      "self": "http://mysite.com/blogs/1"
    },
    "relationships": {
      "comments": {
        "data": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  },
  "included": [{
    "type": "comments",
    "id": "5",
    "attributes": {
      "body": "First!"
    },
    "links": {
      "self": "http://mysite.com/comments/5"
    }
  }, {
    "type": "comments",
    "id": "12",
    "attributes": {
      "body": "Ember is easy"
    },
    "links": {
      "self": "http://mysite.com/comments/12"
    }
  }]
}
```

#### 自定义序列化器（Serializers）

在 Ember data 中，序列化器用于格式化发送到后端存储以及从后端存储接收的数据。默认设置是 Ember data 将使用 JSON API 格式进行数据序列化。

（注：由于原文文本在此处存在部分重复和逻辑断层，译文已根据技术上下文进行了整理，保留了核心意图。）



如果你需要跟踪`store`中包含的唯一记录，Ember Data 期望负载（payload）中的每条记录都应该有一个唯一的`id`属性。对于特定类型的每条记录，`id`也应该是唯一的。如果后端使用了不同的键而不是`id`，可以使用序列化器的主键（primary key）属性，以便在数据的序列化和反序列化过程中正确地转换`id`。下面的代码所示：

```javascript
export default DS.JSONSerializer.extend({
  primaryKey: '_id'
});
```

### 属性名称

Ember Data 的惯例是将特定模型上的属性名称转换为驼峰命名法（camelize）。考虑下面的示例：

```javascript
export default DS.Model.extend({
  fName: DS.attr('string'),
  lName:  DS.attr('string'),
  isPersonOfTheYear: DS.attr('boolean')
});
```

`JSONAPISerializer`期望服务器返回的文档负载中的属性是短横线命名法（dasherized）的。下面的代码所示：

```json
{
  "data": {
    "id": "44",
    "type": "people",
    "attributes": {
      "first-name": "John",
      "last-name": "Joel",
      "is-person-of-the-year": true
    }
  }
}
```

如果服务器返回的属性使用了非常不同的惯例，可以使用序列化器的`keyForAttribute()`方法将模型中的属性名转换为 JSON 负载中的键。考虑下面的代码：

```javascript
export default DS.JSONAPISerializer.extend({
  keyForAttribute: function(attribute) {
    return Ember.String.underscore(attribute);
  }
});
```

可以使用自定义的序列化器来映射不规则的键。`attrs`对象可以用于在`DS`中不同属性名之间建立简单的映射。考虑样例代码：

```javascript
export default DS.Model.extend({
  lName: DS.attr('string')
});
```

我们所做的是为我们的模型创建了一个自定义序列化器，然后覆盖了`attrs`属性。接下来的代码应该如下：

```javascript
export default DS.JSONAPISerializer.extend({
  attrs: {
    lName: 'lastNameOfPerson'
  }
});
```

### 关系

`id`属性应该用于引用其他记录。考虑你的模型具有如下所示的`hasMany`关系的情况：

```javascript
export default DS.Model.extend({
  comments: DS.hasMany('comment', { async: true })
});
```

JSON 应该将关系编码为类型和 ID 的数组。下面的代码所示：

```json
{
  "data": {
    "type": "posts",
    "id": "1",
    "relationships": {
      "comments": {
        "data": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  }
}
```

考虑你有一个如下所示模型的情况：

```javascript
export default DS.Model.extend({
  origPost: DS.belongsTo('post')
});
```

该关系应该被 JSON 编码为另一个记录中的一个 ID。下面的代码所示：

```json
{
  "data": {
    "type": "comment",
    "id": "1",
    "relationships": {
      "original-post": {
        "data": { "type": "post", "id": "5" },
      }
    }
  }
}
```

如果需要这些命名惯例，可以通过`keyForRelationship`方法来覆盖它们。下面的代码演示了这一点：

```javascript
export default DS.JSONAPISerializer.extend({
  keyForRelationship: function(key, relship) {
    return key + 'Ids';
  }
});
```

### 自定义转换

在某些情况下，内置类型（如`string`、`Boolean`等）可能不足以实现我们需要。一个很好的例子是服务器给出了非标准的日期格式。在 Ember Data 中，我们可能注册了作为属性的新 JSON 转换。下面的代码最好描述了这一点：

```javascript
export default DS.Transform.extend({
  serialize: function(val) {
    return [value.get('a'), value.get('b')];
  },
  deserialize: function(val) {
    return Ember.Object.create({ a: value[0], b: value[1] });
  }
});
```

接下来的代码应该是：

```javascript
export default DS.Model.extend({
  position: DS.attr('coordinate-point')
});
```

从 API 接收到`coordinatePoint`后，期望是一个如下数组：

```json
{
  "cursor": {
    "position": [5, 9]
  }
}
```

一旦加载到模型实例，它将像所示所示：

```javascript
var c = store.findRecord('cursor', 1);
c.get('position.x'); // 5
c.get('position.y'); // 9
```

一旦位置被修改并保存，它将通过转换中的`serialize`函数传递并以数组的形式呈现。在应用中使用`JSONSerializer`必须定义`serializer`。下面的代码显示了如何这样做：

```javascript
export default DS.JSONSerializer.extend({
  // ...
});
```

在某些请求的情况下，期望的结果应该有一个记录。响应应该是与下面类似的 JSON：

```json
{
  "id": "1",
  "title": "Ember is easy to Learn",
  "tag": "rails",
  "comments": ["1", "2"]
}
```

为了给出零或多个记录，期望的结果应该是如下的 JSON 数组：

```json
[{
  "id": "1",
  "title": "Ember is easy to Learn",
  "tag": "ember",
  "comments": ["1", "2"]
}, {
  "id": "2",
  "title": "When I was young, I aspired to become an athlete!",
  "tag": "w3c",
  "comments": ["3"]
}]
```

### EmbeddedRecordMixin

在 Ember Data 中，我们鼓励侧加载（sideload）关系，但有时在处理旧 API 时，可能需要处理嵌入其他记录中的 JSON。`EmbeddedRecordsMixin`的创建是为了解决这个问题。设置嵌入记录，只需在扩展序列化器包含该`mixin`，然后对嵌入关系进行配置。考虑模型`post`有如下所示`author`记录的情况：

```json
{
  "id": "1",
  "title": "Ember is easy to Learn",
  "tag": "ember",
  "authors": [
    {
      "id": "2",
      "name": "Mark"
    }
  ]
}
```

关系将如下所示定义：

```javascript
export default DS.JSONSerializer.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
    authors: {
      serialize: 'records',
      deserialize: 'records'
    }
  }
});
```

如果你自己定义并需要序列化和反序列化嵌入关系，可以使用简写选项`{ embedded: 'always' }`。考虑与下面类似的示例：

```javascript
export default DS.JSONSerializer.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
    authors: { embedded: 'always' }
  }
});
```

考虑你需要在提取 JSON 负载的过程中读取嵌入记录，但在序列化记录时只需要包含关系的`id`。这可以通过使用`serialize: 'ids'`选项轻松实现。要跳过关系的序列化，可以使用`serialize: false`选项。下面的代码演示了如何这样做：

```javascript
export default DS.JSONSerializer.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
    author: {
      serialize: false,
      deserialize: 'records'
    },
    comments: {
      deserialize: 'records',
      serialize: 'ids'
    }
  }
});
```

#### EmbeddedRecordsMixin 默认值

如果你不需要为特定关系覆盖`attrs`属性，以下是`EmbeddedRecordsMixin`的行为：

- `BelongsTo`：`{ serialize: 'id', deserialize: 'id' }`
- `HasMany`：`{ serialize: false, deserialize: 'ids' }`

### 编写序列化器

对于那些需要创建序列化器的人，我们建议从`JSONAPISerializer`或`JSONSerializer`开始，然后扩展其中之一以匹配我们的需求。然而，如果负载（payload）与这些序列化器之一不同，请考虑你获得了如下“posts”模型：

```javascript
export default DS.Model.extend({
  title: DS.attr('string'),
  tag: DS.attr('string'),
  comments: hasMany('comment', { async: false }),
  relatedPosts: hasMany('blogs')
});
```

此时`store.push`将接受一个如下结构的对象：

```json
{
  data: {
    id: "1",
    type: 'post',
    attributes: {
      title: "Ember is easy to Learn",
      tag: "ember",
    },
    relationships: {
      comments: {
        data: [{ id: "1", type: 'comment' },
               { id: "2", type: 'comment' }],
      },
      relatedPosts: {
        data: {
          related: "/api/v1/blogs/1/related-posts/"
        }
      }
    }
  }
}
```

为了使每个序列化的记录都能转换为 Ember Data 记录，必须遵循上述格式。

# 第 3 章：应用关注

## 依赖注入

这种技术在 EmberJS 中用于对象的声明、实例化以及它们之间的依赖。应用程序和应用实例将在 Ember 的依赖注入（DI）实现中发挥作用。

### 工厂注册（Factory Registrations）

工厂可以用于表示应用的一部分，例如模板、路由或自定义类。这的一个很好的例子是索引模板，它通过键“template:index”进行注册。请注意，工厂注册必须在应用程序内部或应用实例初始化器中完成，但前者更为常见。考虑下文给示例，它展示了应用初始化器如何使用键“logger:main”注册一个“logger”工厂：

```javascript
export function initialize(app) {
  var Logger = Ember.Object.extend({
    log(n) {
      console.log(n);
    }
  });
  app.register('logger:main', Logger);
}

export default {
  name: 'logger',
  initialize: initialize
};
```

### 注册实例化对象（Registering Instantiated Objects）

默认设置是 Ember 会在查找后尝试实例化已注册的工厂。在特定类的实例化对象的注册过程中，你必须使用选项`instantiate: false`，以便避免它在查找期间被重复实例化。在下文的示例中，`logger`是 JavaScript 中的一个对象，在查找期间应原样返回。以下是代码：

```javascript
export function initialize(app) {
  var logger = {
    log(n) {
      console.log(n);
    }
  };
  app.register('logger:main', logger, { instantiate: false });
}

export default {
  name: 'logger',
  initialize: initialize
};
```

### 单例与非单例（Singletons vs. Non-Singletons）

在 Ember Data 中，注册被视为单例。这意味着在查找后必须创建一个实例，并且同一个实例将在后续查找中被缓存并返回。在下文的示例中，“message”类将被注册为非单例：

```javascript
export function initialize(app) {
  var Msge = Ember.Object.extend({
    text: ''
  });
  app.register('notification:message', Msge, { singleton: false });
}

export default {
  name: 'notification',
  initialize: initialize
};
```

### 工厂注入（Factory Injections）

一旦完成工厂注册，我们可以在需要时对其进行注入。工厂的注入可以在整个类型的工厂中进行。考虑下文的示例：

```javascript
export function initialize(app) {
  var Logger = Ember.Object.extend({
    log(n) {
      console.log(n);
    }
  });
  app.register('logger:main', Logger);
  app.inject('route', 'logger', 'logger:main');
}

export default {
  name: 'logger',
  initialize: initialize
};
```

由于这种类型注入，类型为“route”的工厂将使用已注入的`logger`进行实例化。`logger`值将从名为“logger:main”的工厂中获取。考虑下文的示例，它展示了如何通过注入的`logger`访问应用：

```javascript
export default Ember.Route.extend({
  activate() {
    // 属性 logger 被注入到所有路由中
    this.get('logger').log('Entered your route!');
  }
});
```

使用全键时，可以像如下所示对全键进行注入：

`app.inject('route:index', 'logger', 'logger:main');`

### 现有的注入（Ad Hoc Injections）

依赖注入通过`Ember.inject`直接在 Ember 类上声明。目前，该属性支持服务和控制器的注入。考虑下文的代码，它展示了如何将服务“shopping-cart”作为`cart`属性注入到组件“cart-contents”中。以下是相应的代码：



```javascript
export default Ember.Component.extend({
  cart: Ember.inject.service('shopping-cart')
});
```

如果你需要注入一个与属性名称相似的服务，只需留空服务的名称即可。下文的代码演示了这一点：

```javascript
export default Ember.Component.extend({
  shoppingCart: Ember.inject.service()
});
```

实例初始化器通常接收应用实例作为参数，这为我们提供了查找已注册工厂实例的机会。考虑下文的代码：

```javascript
export function initialize(appInstance) {
  let logger = appInstance.lookup('logger:main');
  logger.log('Hello from an instance initializer!');
}

export default {
  name: 'logger',
  initialize: initialize
};
```

我们也可以从工厂集中获取应用程序的实例。考虑下文的示例，它根据歌曲的 `audioType` 使用不同的音频服务播放歌曲。以下是代码：

```javascript
import Ember from 'ember';
const {
  Component,
  computed,
  getOwner
} = Ember;

// 使用方法：
// {{play-audio song=song}}

export default Component.extend({
  audioService: computed('song.audioType', function() {
    let appInstance = getOwner(this);
    let audioType = this.get('song.audioType');
    return appInstance.lookup(`service:${audioType}`);
  }),
  click() {
    let p = this.get('audioService');
    p.play(this.get('mysong.file'));
  }
});
```

## 初始化器（Initializers）

这些为我们提供了在启动过程中配置应用的机会。存在两种类型的初始化器：应用实例初始化器和应用初始化器。

应用初始化器在启动过程中执行，它们为我们提供了应用中配置依赖注入的方法。另一种类型的初始化器在加载应用实例期间配置。它们为我们提供了配置应用初始状态以及设置局部于应用实例的方法。

### 应用初始化器（Application Initializers）

应用初始化器使用 Ember CLI 的初始化器生成器创建。下文的命令演示了这一点：

`ember generate initializer shopping-cart`

我们可以自定义“shopping-cart”初始化器，将属性“cart”注入到应用中的所有路由中。下文的代码演示了这一点：

```javascript
export function initialize(app) {
  app.inject('route', 'cart', 'service:shopping-cart');
}

export default {
  name: 'shopping-cart',
  initialize: initialize
};
```

### 应用实例初始化器（Application Instance Initializers）

这些可以使用 Ember CLI 的“instance-initializer”生成器创建。如下文所示：

`ember generate instance-initializer logger`

考虑下文的代码，它展示了如何实现一些简单的日志记录，用以指示实例已经启动。如下文所示：

```javascript
export function initialize(appInstance) {
  let logger = appInstance.lookup('logger:main');
  logger.log('Hello from an instance initializer!');
}
```

```javascript
logger.log('Hi from our instance initializer!');

}

export default {
  name: 'logger',
  initialize: initialize
};
```

## 指定初始化器顺序

如果你需要控制初始化器的运行顺序，可以使用“before”和“after”选项。请考虑下面的代码：

```javascript
export function initialize(app) {
  // ...在此处添加你的代码 ...
};

export default {
  name: 'configReader',
  before: 'websocketInit',
  initialize: initialize
};
```

接下来的代码应该如下：

```javascript
export function initialize(application) {
  // ... 在此处添加你的代码...
};

export default {
  name: 'websocketInit',
  after: 'configReader',
  initialize: initialize
};
```

## 服务（Services）

`Ember.service` 属性是 Ember 中的一个对象，可以在应用程序的不同部分使用并可用。以下是服务使用的领域：

- `Geolocation`（地理位置）。
- `User/session authentication`（用户/会话认证）。
- `Web Sockets`（网络套）。
- 无法放入 Ember Data 的服务器后端 API 调用。
- `Third-party APIs`（第三方 API）。
- 服务器发送事件或通知 `Logging`（日志记录）。

## 服务的定义

Ember CLI 中的 `service` 生成器可用于生成服务。考虑以下用于创建“shoppingCart”（购物车）服务的命令：

```bash
ember generate service shopping-cart
```

服务必须继承基类 `Ember.Service`。下方的代码所示：

```javascript
export default Ember.Service.extend({
});
```

像 Ember 中的对象一样，服务必须经过初始化，并且它应该有自己的方法和属性。考虑下面的购物车服务，它最好地演示了这是如何工作的：

```javascript
export default Ember.Service.extend({
  items: null,
  init() {
    this._super(args);
    this.set('items', []);
  },
  add(item) {
    this.get('items').pushObject(item);
  },
  remove(item) {
    this.get('items').removeObject(item);
  },
  empty() {
    this.get('items').setObjects([]);
  }
});
```

## 访问服务

为了访问服务，可以通过函数 `Ember.inject.service` 将其注入到任何由容器解析的对象中，例如另一个服务或一个组件。该函数有两种使用方法：你可以选择不带参数地调用它，或者将你的服务的注册名称传递给它。

在不传递参数的情况下，服务必须根据其变量键名加载。要不带参数加载购物车服务，请如下所示：

```javascript
export default Ember.Component.extend({
  // 加载文件 /app/services/shopping-cart.js 中的服务
  shoppingCart: Ember.inject.service()
});
```

另一种方法涉及使用服务的名称作为参数。下方的代码所示：

```javascript
export default Ember.Component.extend({
  // 加载文件 /app/services/shopping-cart.js 中的我们的服务
  cart: Ember.inject.service('shopping-cart')
});
```

通过上述代码，购物车服务将被注入到我们的组件中，然后通过 `cart` 属性可用。被注入的属性是懒加载的，这意味着在没有显式调用该属性，不会对服务进行实例化。这意味着必须使用 `get` 函数来访问特定组件的服务，否则你将得到 undefined 错误。

加载后，服务将一直持续到服务退出。

考虑下面的代码：

```javascript
export default Ember.Component.extend({
  cart: Ember.inject.service('shopping-cart'),
  actions: {
    remove(item) {
      this.get('cart').remove(item);
    }
  }
});
```

在上述代码中，我们将 `remove` 添加到了 `cart-contacts` 组件中。一旦注入到组件中，服务将在模板中使用。注意下面的代码中用于从购物车获取数据的 `cart`：

```html
<ul>
  {{#each cart.items as |item|}}
    <li>
      {{item.name}}
      <button {{action "remove" item}}>移除</button>
    </li>
  {{/each}}
</ul>
```

## 运行循环（Run Loop）

Ember 大多数的内部机制以及我们为应用程序编写的代码都发生在运行循环中。运行循环用于以更高效、有效的方式对工作进行批处理和排序。

```html
<div id="foo"></</div>
<div id="bar"></</div>
<div id="baz"></</div>
```

该框架具有许多我们可以利用的特性来增强我们的应用程序。

在 Ember JS 中，控制器（controllers）非常重要，大多数人会将它们与组件（components）混淆。很快，人们认为控制器将被组件所取代。控制器的目的是控制状态，而这取决于当前使用的路由类型。在将信息从组件传递到路由时，也会使用控制器，因为信息必须经过它。此外，控制器之间也需要建立依赖关系。

当我们需要嵌套资源时，通常会遇到这种情况。我们必须想出一种机制，在控制器之间建立连接。了解如何在 Ember JS 中创建自定义转换（custom transformations）对你很有帮助，因为现有的数据类型可能无法满足你的需求。Ember JS 中提供的自定义转换可以在这方面提供帮助。我希望这本书能够帮助你理解如何在 Ember JS 中构建应用程序。祝你学习愉快！
