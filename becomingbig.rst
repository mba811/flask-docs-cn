.. _becomingbig:

聚沙成塔
============

你的应用变得越来越复杂？当你突然意识到 Flask 没有解决你应用的问题，
这里有一些解决的办法。

Flask 由 Werkzeug 和 Jinja2 驱动，两个被许多大型网站使用的库，并且 Flask
所做的全部就是把两个库放在一起。作为一个微框架， Flask 几乎不做组合现有
库的之外的事 —— 没有涉及太多的代码。这意味着对于大型应用，从 Flask 中获取
代码并放进一个应用内的新模块来扩展它
是容易的。

Flask 被设计为可以用多种方式来扩充或修改:

-   Flask 扩展。对大多数可重用功能，你可以创建扩展。 Flask 中到处都有大量的
    信号和回调函数用于扩展的挂钩。

-   子类。大多数功能可以通过创建一个 :class:`~flask.Flask` 类的子类来修改，
    或覆盖现有的方法来满足特定的需求。

-   分支。如果没有其它方法可以实现，你可以在要点利用 Flask 的代码作为
    基础，把它复制/粘贴到你的应用中，并修改它。 Flask 设计时考虑了这点，
    并使得这个行为异常简单。你只需要获取包并复制到你应用的代码中，然后
    给它重命名（比如 `framework` ）。然后你可以修改那里的代码。

为什么考虑分支？
---------------------

大多数 Flask 的代码是 Werkzeug 和 Jinja2 里的。这些库完成了大多数工作。
Flask 只是把它们粘合在一起。对于每个项目，会有一个底层框架受阻的点
（由于原始开发者的假设）这很自然，因为如果不是这样，框架会是一个非常
复杂的系统，并且学习曲线陡峭而导致用户的挫折。

不只是 Flask 。许多使用修补的或修改的版本的其它框架来消灭短板。这个
想法也在 Flask 的许可证中体现。如果你决定修改框架，你不需要做任何回馈。

分支的坏处是， Flask 扩展在大多数情况下无法正常工作，因为新框架的导入
名称不同。此外，集成上游是个复杂的过程，取决于更改的数量。因此，分支
应该是最后手段。

像专家一样扩大规模
-------------------

对许多 web 应用，代码的复杂程度比起为预期的用户或数据条目而扩大规模就不
是问题了。 Flask 自己扩大规模的限制只在于你的应用代码、你想用的数据存储
和 Python 解释器以及你运行的 web 服务器。

妥善地扩大规模意味着，比如当你有两倍数量的服务器，你会得到大约两倍的性能。
而糟糕的意味着，当你添加了一台新的服务器，应用不会有任何性能提升或根本不
支持第二台服务器。

在 Flask 中关于缩放只有一个限定因子，就是上下文局域代理。它们依赖于在
Flask 中定义为线程、进程或 greenlet 的上下文。如果你的服务器使用不基于
线程或 greenlet 的并行计算， Flask 不再能支持这些全局代理。然而大多数
服务器使用线程、 greenlet 或独立进程来实现并发，而这些方法在底层的
Werkzeug 库中有着良好的支持。


与社区对话
---------------------------

Flask 开发者对众乐乐很有兴趣，所以一旦你遇到了由 Flask 引起的麻烦，不要
犹豫，用邮件列表或 IRC 频道联系开发者。 Flask 和 Flask 扩展开发者为更大
型应用改进的最佳途径就是从用户获取反馈。
