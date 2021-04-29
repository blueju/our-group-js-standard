# our-group-js-code-standard

> 我们团队的 JavaScript 代码规范



TODO:

* [ ] 事件方法，匿名函数？手动绑定this？函数表达式？
* [ ] 注释使用 `/** xxx */`
* [ ] 属性接收字符串的，不需要使用{}包裹
* [ ] service里的方法以 api 开头
* [ ] 如果使用 class 组件，还要不要构造函数
* [ ] antd table column 写在 render 里
* [x] 不直接使用 export default 导出数据
* [x] 每个 React 组件都需要对其定制化命名
* [x] 渲染 DOM 的函数的命名以 render 开头
* [x] 提交代码需找至少一位同事审查并记录在 commit message 中
* [x] DOM 元素的 style 属性并不是都需要抽离，超过 3 个时才抽离
* [x] 引用的 CSS 变量名统一为 styles



# 前言

使用 Alloy Team 的 eslint config 对代码进行规范检查；

使用 Prettier 对代码进行格式检查；

最大化利用工具，对以上工具无法检查的部分，才使用人为约定的规范进行约束。



# 正文

## 1. 不直接使用 export default 导出数据

### 示范

> 错误示范

```javascript
export default [
  {
    name: "Tom",
  },
  {
    name: "Jerry",
  },
];
```

> 正确示范

```javascript
const nameList = [
  {
    name: "Tom",
  },
  {
    name: "Jerry",
  },
];

export default nameList;
```

### 原因

这么写，可以让 IDE 识别出该导出变量被哪些文件引用，方便追踪溯源。



## 2. 每个 React 组件都需要对其定制化命名

### 示范

> 错误示范

```
/** 登录组件 */
class Index extends React.Component {}

/** 注册组件 */
class Index extends React.Component {}
```

> 正确示范

```
/** 登录组件 */
class Login extends React.Component {}

/** 注册组件 */
class Register extends React.Component {}
```

### 原因

方便搜索组件，区分组件，定位错误。



## 3. 渲染 DOM 的函数的命名以 render 开头

### 示范

> 错误示范

```
/** 获取表单 */
getSearchForm(){}
```

> 正确示范

```
/** 获取表单 */
renderSearchForm(){}
```

### 原因

没为什么，参考自 render 函数的命名，与之保持一致风格。



## 4. 提交代码需找至少一位同事审查并记录在 commit message 中

### 示范

> 错误示范

```
git commit -m 'xxxx'
```

> 正确示范

```
git commit -m 'xxxx（审查人：蓝钜/喻鹏飞/...）'
```

### 原因

引入第三方约束及检查，也参考自本人在大公司实习时的规范。



## 5. DOM 元素的 style 属性并不是都需要抽离，超过 3 个时才抽离

### 示范

> 错误示范

```react
// index.less
.xxx{
  color: red;
}

// index.jsx
import styles from './index.less'

<div className={styles.xxx}></div>
```

> 正确示范

```react
import styles from './index.less'

<div style={{color:'red'}}></div>
```

### 原因

每个都抽离，反而更麻烦。



## 6. 引用的 CSS 变量名统一为 styles

### 示范

> 错误示范

```
// 不符合实际数量情况（复数）
import style from './index.less'
// 不符合小驼峰式命名
import Styles from './index.less'
```

> 正确示范

```
import styles from './index.less'
```

### 原因

参考自 umi 示例工程。



## 7. 不可擅自新增第三方依赖

### 示范

> 错误示范

```
无
```

> 正确示范

```
无
```

### 原因

避免滥用依赖的情况，也参考自本人在大公司实习时的规范；

如有需要，向前端组长咨询、讨论、对比、决定。



## 8. 目录结构
### 示范

> 错误示范

```
pages
 |-Aaaa
 |  |-index.jsx
 |  |-Ddd
 |  |  |-index.jsx
 |  |  |-Gggg
 |  |     |-index.jsx
 |  |     |-index.less
 |  |-Eee
 |  |-Ffff
 |-Bbbb
 |-Cccc
```

> 正确示范

```
pages
 |-Aaaa
 |  |-index.jsx
 |  |-components
 |     |-Aaaa
 |     |  |-index.jsx
 |     |  |-components
 |     |     |-Aaaa
 |     |     |-Bbbb
 |     |     |-Cccc
 |     |-Bbbb
 |     |-Cccc
 |-Bbbb
 |-Cccc
```

### 原因

避免滥用依赖的情况，也参考自本人在大公司实习时的规范；

如有需要，向前端组长咨询。



## 9. service 中的 api 方法命名以 api 开头

### 示范

> 错误示范

```react
// service.js
export function getTradeCodes() {}

// index.jsx
import React from 'react';
import { getTradeCodes } from './service

class TradeCode extends React.Component{
	// 是不是觉得为该函数取名为 getTradeCodes，则与 service 里的 getTradeCodes 重名了，
	// 但不取吧，又一时间想不到其他同样能表达“获取交易代码“的英文了
	getTradeCodes(){
		getTradeCodes().then(res=>{})
	}
	componentDidMount(){
		this.getTradeCodes()
	}
}
```

> 正确示范

```react
// service.js
export function apiGetTradeCodes() {}

// index.jsx
import React from 'react';
import { apiGetTradeCodes } from './service

class TradeCode extends React.Component{
	getTradeCodes(){
		apiGetTradeCodes().then(res=>{})
	}
	componentDidMount(){
		this.getTradeCodes()
	}
}
```

### 原因

针对 “ 在 service 定义 api 方法并在组件中使用 ” 这一必经流程，避免同一意思却命名不一致的经常性情况；

同时也方便区分 ” 组件方法 “ 与 ” api 方法 “ ；



## 10. 目录命名

### 示范

> 错误示范

```
tradeCode
```

> 正确示范

```
TradeCode
```

### 原因

暂无，统一即可，此项可再做仔细讨论。



## 11. 文件命名

### 示范

> 错误示范

```react
// tradeCode.jsx
import React from 'react';

class TradeCode extends React.Component{}
```

> 正确示范

```react
// TradeCode.jsx
import React from 'react';

class TradeCode extends React.Component{
```

### 原因

因为根据 React 规范，组件名必须大写，因此强烈建议文件名与组件命名报纸一致。



## 12. HTML标签内无数据时，使用自结束标签

### 示范

> 错误示范

```react
import React from 'react';
import { Input, Table } from 'antd';

class TradeCode extends React.Component{
	render(){
        return (
        	<>
                <Input value="username"></Input>
                <Table>
                    <Table.Column title="用户名" dataIndex="username"></Table.Column>
                <Table>
            </>
        )
    }
}
```

> 正确示范

```react
import React from 'react';
import { Input, Table } from 'antd';

class TradeCode extends React.Component{
	render(){
        return (
        	<>
            	<Input value="username"/>
                <Table>
                	<Table.Column title="用户名" dataIndex="username"/>
                <Table>
            </>
        )
    }
}
```

### 原因

HTML 规范，没啥好说的；

如果不按规范写，antd 也会报错误型警告；



## 13. 关于变量存放在哪里的问题

### 示范

> 错误示范

```react
无
```

> 正确示范

```react
// 正确示范一
export const data = []

// 正确示范二
class Login extends React.Component{
    this.data2 = []
}

// 正确示范三
class Login extends React.Component{
    this.state = {
        data3: []
    }
}
```

### 原因

1. 如果变量需要被其他组件共享，则放组件外定义，参考如上正确示范一；

2. 如果变量只是在组件内部被使用，且不需要频繁改变，则直接在组件内部定义，但不要 state 中，参考如上正确示范二：

3. 如果变量只是在组件内部被使用，且需要频繁改变，则放入 state 中，参考如上正确示范三；



## 13. 关于变量命名单词的拼写问题

### 示范

> 错误示范

```react
无
```

> 正确示范

```react
无
```

### 原因

宁愿变量名长一些，也不要擅自缩写成既不是接口属性的名称，也不是业界统一认同的名称，如：交易代码。

正确缩写：

- txnCode（接口属性是这么定义，如果有现成的，那就与它保持一致咯）
- tradeCode（按照中文直译的，完整，即使不认识，也可以通过翻译工具得知其意思）

错误缩写：

tsCode、tsElement、TSelement 等

