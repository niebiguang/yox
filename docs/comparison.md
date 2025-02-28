本文尽量做到客观评价...

## Vue

当你第一次看到 `Yox` 的示例，可能会觉得很像 `Vue`，是的，我们毫不掩饰这一点。

`Vue` 的组件 Options 结构非常简单易懂，如下：

```js
{
  data: function () {
    return {
      name: 'yox'
    }
  },
  filters: {
    formatDate: function () {

    }
  },
  methods: {
    greet: function () {

    }
  }
}
```

这种结构化的组件带来的好处不言而喻，它的约束性很强。

它通过专属字段（`data`、`filters`、`methods` 等）强约束了什么功能应该写在什么位置，作为对比，我们再提供一个约束不是那么强的例子：

```js
{
  data: function () {
    return {
      name: 'yox'
    }
  },
  formatDate: function () {

  },
  greet: function () {

  }
}
```

这里把 `filters` 和 `methods` 直接写到组件 Options 属性上，看起来结构更加简洁。

但是，当你看到 `formatDate` 时，你并不能一下子反应过来，它是一个过滤器，而是觉得它是一个 `method`，因此你可能在任何地方调用它。`Vue` 这种结构会让你产生一个概念约束：过滤器应该只用于渲染模板。

我们认为，强约束是有必要的，它有益于写出更规范的代码。

`Yox` 没有全盘照搬 `Vue`，它也存在一些设计缺陷，最典型的是 `mixins`，它使得功能可以随意组合，太过灵活会让人有时候不知道究竟发生了什么。

最后，Yox 的模板语法借鉴的是 `Ractive`，跟 `Vue` 没有太多关系。

我看到有不少人（包括我）吐槽过 `Vue` 的模板标记太多，这个问题对 `Yox` 来说不存在。

## React

三大框架，我最喜欢 `React`，它简单灵活，概念清晰，一旦学会，几乎可以脱离文档开发。

这是我认为框架应该追求的境界：做好一件事。

`Yox` 作为 MVVM 框架，把响应式的流程做到极致，这样开发者就会对它产生一个核心概念，修改数据会触发视图更新。其他的事情开发者都能自己做，框架不应干涉过多。

`Yox` 形似 `Vue`，神却更似 `React`，我希望 `Yox` 在保持简单的前提下，做到尽可能的好用。

最后，`Yox` 和 `React` 一样，推崇单向数据流。

## Angular

`TypeScipt` 集大成者，概念和标记双冠王，小弟不才，不敢玩。

> 没用过，没法比较。

## jQuery

既然跳过了 `Angular`，那就再补一个上古神器：`jQuery`。

`jQuery` 和 `Yox` 没什么可比性，下面说说如何在 `Yox` 中使用 `jQuery`。

在 `Yox` 中使用 `jQuery` 很简单，我们推崇组件有一个固定的根元素，因此如果你需要用一些 `jQuery` 插件，可以在生命周期钩子函数中进行初始化和销毁，如下：

```js
{
  afterMount: function () {
    // 在 afterMount 中初始化 jQuery 插件
    $(this.$el).xxx()
  },
  beforeDestroy: function () {
    // 销毁在 afterMount 中创建的 jQuery 插件
  }
}
```
