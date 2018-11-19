title: "译React Mixins"
date: 2015-6-1 22:44:00
tags:
---

#译React Mixins
>翻译《React Mixins By Example》[原文](http://simblestudios.com/blog/development/react-mixins-by-example.html)
>

##做一个简单的Mixin

来开始创建一个app，因为一些原因我们总要设置默认的```name```属性在开发组件中。不要问为什么，这儿有个简单的方法

宁愿每次写一样的```getDefaultProps```方法，其实我们可以创建一个像这样的mixin

```
var DefaultNameMixin = {
    getDefaultProps: function () {
        return {name: "Skippy"};
    }
};
```

这没什么可说的，只是个简单的对象

##增加到React组件中
对于我们使用mixin，我们只要确定组件有``mixins```属性并且包含我们的mixin数组的值:

```
var ComponentOne = React.createClass({
    mixins: [DefaultNameMixin],
    render: function() {
        return <h2>Hello {this.props.name}</h2>;
    }
});

React.renderComponent(<ComponentOne />, document.body);

```

此处有个[JSFiddle例子](http://jsfiddle.net/veddermatic/qzh0ug5y/1/)。简单的mixin行为

##多次使用

正如你想象那样。我们可以include我们的mixin在任何组件中:

```
var ComponentTwo = React.createClass({
    mixins: [DefaultNameMixin],
    render: function () {
        return (
            <div>
                <h4>{this.props.name}</h4>
                <p>Favorite food: {this.props.food}</p>
            </div>
        );
    }
});
```

[JSFiddle example](http://jsfiddle.net/veddermatic/qzh0ug5y/2/) 我们用过的愚蠢组件~

##生命周期及方法
如果你使用mixin，则包含了[React生命周期方法](http://reactjs.cn/react/docs/component-specs.html)，别着急：你不需要“使用”，你仍然可以使用这些生命周期方法在你的组件中，而且也可以被调用到：

```
var DefaultNameMixin = {
    getDefaultProps: function () {
        return {name: "Skippy"};
    }
};

var ComponentTwo = React.createClass({
    mixins: [DefaultNameMixin],
    getDefaultProps: function () {
        return {food: "Pancakes"};
    },
    render: function () {
        return (
            <div>
                <h4>{this.props.name}</h4>
                <p>Favorite food: {this.props.food}</p>
            </div>
        );
    }
});

```
此处应有例子[JSFiddle example](http://jsfiddle.net/veddermatic/qzh0ug5y/3/)

两个``getDefalutProps``实例都将被调用，然后```default name```最终含有name属性的Skippy和food属性的favorite，任何[React生命周期](http://reactjs.cn/react/docs/component-specs.html)或者组件特征属性，复制在mixin中没有任何问题。  
除了以下情况：  
1. ``render``：含有超过1个以上的render方法将没有任何效果。React将会在你有两个render方法时提示如下：

```
Uncaught Error: Invariant Violation: ReactCompositeComponentInterface: 
You are attempting to define `render` on your component more than once. 
This conflict may be due to a mixin.
```

2.```displayName```:设置多次，这个将不会报错经过mixin方法，但是会覆盖掉，所以显示最终的值"wins".

这里值得指出的是```mixins```你可以定义多次，并且还可以引用其他mixins方法

```
var UselessMixin = {
    componentDidMount: function () {
      console.log("asdas");
    }
};

var LolMixin = {
   mixins: [UselessMixin]
};

var PantsOpinion = React.createClass({
   mixins: [LolMixin],
   render: function () {
       return (<p>I dislike pants</p>);
   }
});

React.renderComponent(<PantsOpinion />, document.body);
```
[JSFiddle example](http://jsfiddle.net/qzh0ug5y/17/)

当组件装载好，我们可以欢快的看到控制台log打印出"asdas".

3.多种Mixins
事实上我们```mixins```是一个数组，我们可以包含更多东西
再看下:

```
var DefaultNameMixin = {
    getDefaultProps: function () {
        return {name: "Lizie"};
    }
};

var DefaultFoodMixin = {
    getDefaultProps: function () {
        return {food: "Pancakes"};
    }
};

var ComponentTwo = React.createClass({
    mixins: [DefaultNameMixin, DefaultFoodMixin],
    render: function () {
        return (
            <div>
                <h4>{this.props.name}</h4>
                <p>Favorite food: {this.props.food}</p>
            </div>
        );
    }
});
```
[JSFiddle example](http://jsfiddle.net/veddermatic/92nwqss2/1/) 多种mixins

##Hi Man
当你用mixins方式时头疼的时候，我这儿有些小笔记。  
幸运的是，这个列表似乎挺少的、这儿有我的一些经验之谈

###Tips:设置相同的属性在Props或者State
当需要调用多个```getDefalutProps```时(```getIntialState等同```)  
并且设置了相同的属性或者状态时将会遇到一些麻烦，

```
// set the name prop here...
var DefaultNameMixin = {
    getDefaultProps: function () {
        return {name: "Skippy"};
    }
};

var ComponentTwo = React.createClass({
    mixins: [DefaultNameMixin],

    // ... and set the name prop here
    getDefaultProps: function () {
        return {
            food: "Pancakes",
            name: "Lizzie"
        };
    },
    render: function () {
        return (
            <div>
                <h4>{this.props.name}</h4>
                <p>Favorite food: {this.props.food}</p>
            </div>
        );
    }
});

```

console.log将会显示如下:  
```
Uncaught Error: Invariant Violation: mergeObjectsWithNoDuplicateKeys(): 
Tried to merge two objects with the same key: name
```
所以不能这样做滴，Okay？  
当我们使用相同状态和属性时将会报这种错，所以别这样~  
[JSFiddle example](http://jsfiddle.net/veddermatic/qzh0ug5y/4/) (瞅瞅例子)
###Tips:设置相同方法
在多个mixins个组件中创建了相同方法名时，一样会报错

```
var LogOnMountMixin = {
    componentDidMount: function () {
        console.log("mixin mount method");
        this.logBlah()
    },
    // add a logBlah method here...
    logBlah: function () {
        console.log("blah");
    }
};

var MoreLogOnMountMixin = {
    componentDidMount: function () {
        console.log("another mixin mount method");
    },
    // ... and again here.
    logBlah: function () {
        console.log("something other than blah");
    }
};
```
会生成如下信息:

```
Uncaught Error: Invariant Violation: ReactCompositeComponentInterface: 
You are attempting to define `logBlah` on your component more than once. 
This conflict may be due to a mixin.
```
###Tips:多种生命周期方法被调用的执行顺序
当我们的component和mixin都含有生命周期方法时，会发生什么呢

```
var LogOnMountMixin = {
    componentDidMount: function () {
        console.log("mixin mount method");
    }
};

var ComponentOne = React.createClass({
    mixins: [LogOnMountMixin],
    componentDidMount: function () {
        console.log("component one mount method");
    },
    render: function() {
        return <h2>Hello {this.props.name}</h2>;
    }
});
```
我们的mixin方法始终会先执行。我们可以看到console:

```
mixin mount method
component one mount method
```
当我们include多个mixin时，他们会从左到右执行

```
var LogOnMountMixin = {
    componentDidMount: function () {
        console.log("mixin mount method");
    }
};

var MoreLogOnMountMixin = {
    componentDidMount: function () {
        console.log("another mixin mount method");
    }
};
var ComponentOne = React.createClass({
    mixins: [MoreLogOnMountMixin, LogOnMountMixin],
    componentDidMount: function () {
        console.log("component one mount method");
    },
    ...

var ComponentTwo = React.createClass({
    mixins: [LogOnMountMixin, MoreLogOnMountMixin],
    componentDidMount: function () {
        console.log("component two mount method");
    },
    ...
```
控制台会如下

```
another mixin mount method
mixin mount method 
component one mount method

mixin mount method
another mixin mount method 
component two mount method

```

如果心情好的话，继续戳戳看[JSFiddle example](http://jsfiddle.net/qzh0ug5y/15/)

作为一个好的开发者，你不应该依靠顺序来执行，但是如果你非要这么做，看看我的笔记就好了。😃

##总结

当你用React开发app时候Mixins是个很简单高复用的东西   
It’s a Good Thing™.
