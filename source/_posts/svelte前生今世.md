---
title: svelte前生今世
date: 2018-11-19 16:45:25
tags: svelte
---


#### introduction
![](/img/svelte/1.png)

---

#### catalogue

- Feature
- Source code
- Application
- Optimize

---

#### feature

- component
- lifectyle
- scoped styles
- custom-elements

---

#### hello world


```
{#if isVisible}
	<div class="todo {todo.done ? 'done': ''}" on:click="set({ count: count + 1 })">
		{todo.description}
	</div>
{/if}
```
---


#### hello world


```
<script>
	export default {
		computed: {
			// `todo` is a component property, `$filter` is
			// a store property
			isVisible: ({ todo, $filter }) => {
				if ($filter === 'all') return true;
				if ($filter === 'done') return todo.done;
				if ($filter === 'pending') return !todo.done;
			}
		},
		data() {
			return {
				count: 0
			};
		},
		methods: {
			onScroll() {

			}
		},
		oncreate() {},
		destroy() {}
	};
</script>
```

---

#### 编译

##### 词法分析 => 语法分析

---

####  递归下降
BNF范式：四则运算规则如下，<非终结符>
```
<expr> ::= <expr> + <term>
         | <expr> - <term>
         | <term>

<term> ::= <term> * <factor>
         | <term> / <factor>
         | <factor>

<factor> ::= ( <expr> )
           | Num
```
---


####  递归下降

举个🌰   
9 * (4 + 2) 进行语法分析

#### 递归下降
```
1. <expr> => <expr>
2.           => <term>        * <factor>
3.              => <factor>     |
4.                 => Num (9)   |
5.                              => ( <expr> )
6.                                   => <expr>           + <term>
7.                                      => <term>          |
8.                                         => <factor>     |
9.                                            => Num (4)   |
10.                                                        => <factor>
11.                                                           => Num (2)

```
---

#### 递归下降

例1需要消除左递归，不然就是死循环

```
<expr> ::= <term> <expr_tail>
<expr_tail> ::= + <term> <expr_tail>
              | - <term> <expr_tail>
              | <empty>

<term> ::= <factor> <term_tail>
<term_tail> ::= * <factor> <term_tail>
              | / <factor> <term_tail>
              | <empty>

<factor> ::= ( <expr> )
           | Num
```
---

#### 递归下降-js实现
---

####  Source code

####  一个svelte-component怎么产生的？

---

# Source code

1.parse文件

2.验证文件

3.生成代码

---

# Source code

1.parse文件

![logo](/img/svelte/2.png)

---


# Source code

- component生成顺序

 - createComment
 - add_css
 - 根据parse得到的bind、event-handlers、refs相关绑定在context
 - prototype指向methods

---

#### optimize

1.借鉴vue-property-decorator

```
//before
const { params } = this.get();

//after
get params () {
    return this.params;
}
```

---

#### optimize

```
//before
this.set({
    a: 1
});

//after
this.a = 1;
```

---

#### optimize

- methods和data的this已隔离开，操作很不便

- event-binding不支持func，必须func()

- 子组件不支持透传className

- defineProperty、list performance

---


#### optimize

- 不支持watch，在generator中dispatchObservers做钩子

- style不支持Object

- refs中绑定addEventListener很多，需要removeEventListener

---

####  Thanks
