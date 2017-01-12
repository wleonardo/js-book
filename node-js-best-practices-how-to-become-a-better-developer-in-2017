#Node.js最佳实践--在2017如何成为一个更好的开发者

一年前，我们写了一篇文章[How to Become a Better Node.js Developer in 2016 ](https://blog.risingstack.com/how-to-become-a-better-node-js-developer-in-2016/)，这篇文章成功地获取了不错的反响，所以我想现在是时候回顾这个主题为2017年做准备了。

###2017年最好的Node.js实践

#### 使用ES2015

去年我们建议了你使用ES2015，当前现在的情况已经大有不同了

回到那个时候，Node.js v4是当时的稳定版本(LTS)，支持了ES2015中57%的功能。一年过去了，现在Node v6已经增长到支持ES2015中99%的功能了。

如果你现在在使用最新的LTS Node.js版本，你甚至可以不再需要babel就可以使用所有ES2015的特性。但是即使如此，在浏览器端你可能还是需要babel。

如果你需要关于Node.js版本对于ES2015支持情况的更多的信息，我推荐你可以查询[node.green](http://node.green/)

####使用Promises

在80年代第一次提出Promises的概念。现在多数现代编程语言已经支持这一特性了，使我们的编码变得更加简单。

想象一个如下的功能，它需要读取一个文件，然后解析它，然后打印出其中的name字段。如果使用回调，它可能是下面这个样子的：

```
fs.readFile('./package.json', 'utf-8', function (err, data) {  
  if (err) {
    return console.log(err)
  }

  try {
    JSON.parse(data)
  } catch (ex) {
    return console.log(ex)
  }
  console.log(data.name)
})
```

Promises可以使得这段代码变的更加有可读性：
```
fs.readFileAsync('./package.json').then(JSON.parse).then((data) => {  
  console.log(data.name)
})
.catch((e) => {
  console.error('error reading/parsing file', e)
})
```

当前，现在的`fs`的并没有一个返回一个Promise的`readFileAsync`api。为了做到这个，我们使用可以一个类似[promisifyAll](http://bluebirdjs.com/docs/api/promise.promisifyall.html)的模块。

####使用标准的JavaScript格式

当我们谈到代码风格的时候，一个公司有统一的代码风格是至关重要的。只有这样，当你需要改变你的项目的时候，你才可以高效的从零开始，而不用担心基础的架构不一样。

在RisingStack，我们在所有的项目中都使用了[JavaScript Standard Style](https://github.com/feross/standard)。

![](http://upload-images.jianshu.io/upload_images/2764259-080be7bedc3cb01a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用 Standard后，在你安装之后就可以直接使用，你不需要再做其他的事情，也不需要管理`.eslintrc`, `.jshintrc,` 或者 `.jscsrc`文件。具体的Standard的规则可以查看[Standard rules](http://standardjs.com/rules.html#javascript-standard-style)。

###使用docker---容器将在2017年被大量使用在生成环境

你可以把docker镜像当做部署的工具。docker容器可以将一个软件打包在一个完整的文件系统中，这个容器可以包含你在服务器上需要的一切，例如代码，运行环境，系统工具，系统程序库。

但是为什么我们需要开始使用容器呢?

* 容器可以使你的应用运行在一个隔离的环境中
* 作为一个安全工具，可以使你的代码更加的安全
* 轻量级的docker镜像
* 使得你的部署变得稳定
* 你可以在本地运行模拟线上的运行环境

你可以从[official getting started tutorial](https://docs.docker.com/engine/getstarted/)开始学习docker。另外也推荐[Kubernetes best practices](https://blog.risingstack.com/moving-node-js-from-paas-to-kubernetes-tutorial/) 

####监控你的项目

当你的应用发生错误的时候，第一个知道的人不应该是用户而应该是开发者。

最新的一个开源解决方案[Prometheus](https://prometheus.io/)可以帮助你实现项目的监控。Prometheus是一个基于SoundCloud的开源工具箱，它可以监控你的项目并报警。Prometheus唯一的缺点是你需要设置一些配置并且需要需要自己管理。

如果你在寻找一个开箱即用的解决方案，你也可以使用我们自己开发的[Trace by RisingStack](https://trace.risingstack.com/)

Trace可以帮助你做到以下的事情

* 报警
* 生产环境下的内存和cpu分析
* 分布式追踪和错误寻找
* 性能监控
* 保护你的npm包的安全


![](http://upload-images.jianshu.io/upload_images/2764259-82a2b67449ab54ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####在后台进程中使用消息服务

如果你使用http请求发送消息，当你的接收服务器宕机了，你所有的消息都会丢失。如果你的传输层支持持久化，类似使用消息队列来发送消息，你就不会有这个问题。

**你的接收服务器器宕机了，消息将会被保存下来，在服务重启后会继续发送，如果你的服务器未宕机但是发送了错误，消息会被重新发送一次，这样可以保证你的数据不会丢失。**

举个例子：你需要发送数千份邮件，在这个场景下，你只需要获取到一些类似邮件地址和用户的姓名等基础信息，后台就可以很轻松地将这些信息和邮件信息整合后发送出去。

这种方式最大的好处是，你可以你需要的时候横向扩展你的服务，而不会有邮件被丢失。如果你需要发送数百万的邮件，你可以用相同的方式来增加你的服务。

对于消息队列的选择有很多

* [RabbitMQ](https://www.rabbitmq.com/)
* [Kafka](https://kafka.apache.org/)
* [NSQ](http://nsq.io/)
* [AWS SQS](https://aws.amazon.com/sqs/)

####使用最新的LTS版本的Node.js

为了平衡稳定性和新特性，我推荐你使用最新的LTS版本的Node.js。当我写这篇文章的时候，最新的LTS版本是6.9.2。

你可以使用[nvm](https://github.com/creationix/nvm)来切换你的node版本，你只需要两个指令就可管理和切换你的node版本

```
nvm install 6.9.2 
nvm use 6.9.2
```

####使用语义化的版本管理

几个月前，我们进行了一个[Node.js开发者调查](https://blog.risingstack.com/node-js-developer-survey-results-2016/)，我们从中获取了开发者对于使用语义化版本的使用情况。

不幸的是，我们发现调查者只有71%的人在他们提交和使用模块时使用语义化的版本管理。**我们认为这个数字应该要更高 - 每一个都应该使用语义版本!**，因为不根据[semver规则](http://semver.org/lang/zh-CN/)来提交package，会很容易摧毁你的Node.js应用。


![](http://upload-images.jianshu.io/upload_images/2764259-23211e2ea8f4c975.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过版本号来管你的项目或者模块是至关重要的。你的用户应该要知道一个模块是否更新了，在使用新版本前他们要做什么。

这就是语义版本控制的来历。一个版本号应该要有**主版本号、副版本号、补丁版本号**，更新不同位置的版本号代表不同的意思：

* **主版本号**:表示更新会有不兼容的API
* **副版本号**:表示更新会有新的功能（不破坏现有的api）
* **补丁版本号**:表示更新是模块做了向后兼容的bug修复

npm是根据semver规则来安装依赖的，因此当你发布一个模块之前，请确认是否遵循了semver规则，否则你会破坏了其他使用了你的依赖的应用。

####保证你的应用安全

**保证你的用户数据的安全将是你2017年的头等大事。仅在2016年一年，因为缺少一些安全的措施就有[数百万的用户账户被泄漏](https://en.wikipedia.org/wiki/List_of_data_breaches)**。

你可以通过阅读我们的博客[Node.js Security Checklist](https://blog.risingstack.com/node-js-security-checklist/)来入门Node.js的安全，博客里包含了以下的话题：

* 安全的HTTP Headers
* 强制保护
* Session管理
* 不安全的依赖
* 数据验证

当你掌握了这些基础，你可以来观看我关于Node的互动讨论[Surviving Web Security with Node.js](https://www.youtube.com/watch?v=80LbyikAUqI)

#### 学习Serverless

Serverless started with the introduction of AWS Lambda. Since then it is growing fast, with a blooming open-source community.
In the next years, serverless will become a major factor for building new applications. If you'd like to stay on the edge, you should start learning it today.
One of the most popular solutions is the , which helps in deploying AWS Lambda functions.

Serverless是AWS Lambda第一个提出来的，之后它发展的很快，并建立了一个开源的社区。

接下来的一年，构建新应用时serverless会成为一个标准。如果你想要留在这个领域，你需要重现在开始就学习它。

[Serverless Framework](https://serverless.com/)是当前最流行的解决方案，在部署AWS Lambda functions可以帮助你。

####参加会议与聚会并发言

参加会议和聚会是一个很好地方式去了解和学习新的趋势，开发技巧和最佳实践。当日，这也是一个场合去认识更多新的人。

**To take it one step forward, I'd like to encourage you to speak at [one of these events](https://github.com/watson/conferences) as well!**
As public speaking is tough, and “imagine everyone's naked” is the worst advice, I'd recommend checking out [speaking.io](http://speaking.io/) for tips on public speaking!

**在此基础上，我也鼓励你在[一些会议](https://github.com/watson/conferences)上发言。**

在公共场合发言是一个不容易的事情，“imagine everyone's naked”是最坏的建议。我建议你可以去[speaking.io](http://speaking.io/)学习一些技巧。

####Become a better Node.js developer in 2017

[原文链接](http://www.zcfy.cc/article/node-js-best-practices-how-to-become-a-better-developer-in-2017-risingstack-2174.html)
