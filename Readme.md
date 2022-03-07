# 开发前准备

## 准备
### 一、人员角色安排与职责
- **产品负责人**
	- 资源管理（收集到的资源，分类管理）
		- 需求表
		- 测试账号 密码
	- 产品功能列表
	- 会议安排（计划会，评审会，反思会）
	- 决定发布时间和发布内容
	- 迭代任务
	- 工作排序
	- 审核原型，审核UI（合理性，缺漏，多余）
	- 推动项目进程 

	- *如果使用jira*
	   - 编写用户故事
	   - 确定用户故事优先级

- **设计**
	- 提供UI设计（页面设计，图标设计）
	- 上传至蓝湖或其他工具。
	- 切好的图标单独放一起。

- **开发团队**  
    *前端*
    - 技术选型
    - 技术评估
    - 估算时间  

    *后端*
    - 技术选型
    - 技术评估
    - 估算时间
    - 确定接口规则

- **运维**
	- 提供环境
		- dev环境
		- test环境
		- staging环境
		- production环境

### 二、版本（内容）更新
- **迭代版本：** x.0.0
- **功能版本：** 1.x.0
- **修复bug版本：** 1.0.x
- **每次版本更新内容，记录存档**

### 三、生命周期
**每次迭代：**  商业建模 --> 需求 --> 分析&设计 --> 开发实现 --> 测试 --> 部署
- 商业建模
	*
- 需求
	*
- 分析&设计
	*
- 开发实现
	*
- 测试
	*
- 部署
	*
	
## 团队容量计算  
  22天 – 2天（计划会1天，评审会/反思会1天）  
=20天 – 5天（假设有5天已经确认的培训/出差等）  
=15天 × (0.5 to 0.7) （修改Bug/额外任务占用30 to 50%）  
=7.5～10.5天   
  
  若团队有10人，则有效工作日有75～105人天。  
  一般刚成立或刚实践敏捷的团队，取最低值75人天。

----
## 管理
### 一、资源管理
- 项目资源
- 前端资源
- 后端资源

### 二、代码管理
#### git规范
- Git分支命名
    - master：主分支，负责记录上线版本的迭代，该分支代码与线上代码是完全一致的。
    - dev：开发分支，该分支记录相对稳定的版本，所有的feat分支和fix分支都从该分支创建。其它分支为短期分支，其完成功能开发之后需要删除
    - feat/*：特性（功能）分支，用于开发新的功能，不同的功能创建不同的功能分支，功能分支开发完成并自测通过之后，需要合并到 dev 分支，之后删除该分支。
    - fix/*：bug修复分支，用于修复不紧急的bug，普通bug均需要创建fix分支开发，开发完成自测没问题后合并到 dev 分支后，删除该分支。
    - release/*：发布分支，用于代码上线准备，该分支从dev分支创建，创建之后由测试同学发布到测试环境进行测试，测试过程中发现bug需要开发人员在该release分支上进行bug修复，所有bug修复完后，在上线之前，需要合并该release分支到master分支和dev分支。
    - hotfix/*：紧急bug修复分支，该分支只有在紧急情况下使用，从master分支创建，用于紧急修复线上bug，修复完成后，需要合并该分支到master分支以便上线，同时需要再合并到dev分支。 
- Commit Message格式  
type:subject
##### type指提交类型
- type:commit的类型
- feat: 新特性
- fix: 修改问题
- style: 代码格式修改
- test: 测试用例修改
- docs: 文档修改
- refactor: 代码重构
- misc: 其他修改，比如构建流程，依赖管理  
其他
- `perf` 优化/性能提升
- `revert` 撤销修改
- `docs` 文档/注释
- `chore` 依赖更新/脚手架配置修改等
- `workflow` 工作流改进
- `ci` 持续集成
- `types` 类型定义文件更改
- `wip` 开发中  
##### subject指提交描述  
对映内容是commit目的的简短描述，一般不超过50个字符

----
#### 前端开发规范

##### JS
- 变量  
命名方式：小驼峰  
命名规范：前缀名词
```js
// bad
let setCount = 10

// good
let maxCount = 10
```
- 常量  
命名方式：全部大写  
命名规范： 多个单词时使用分隔符`_`
```js
// bad
const serverErrorCode = {
  success: 200,
  repeat: 444 
}

// good
const SERVER_ERROR_CODE = {
  SUCCESS: 200,
  REPEAT: 444
}
```
- 函数  
命名方式： 小驼峰  
命名规范： 前缀动词
```js
// bad
function wordClass() {}

// good
function saveWordClass() {}
```
**常用动词：can、has、is、load、get、set**
- 类  
命名方式：大驼峰  
命名规范：前缀名词
```js
// bad
class person {}

// good
class Person {}
```
- 注释  
###### 单行
```js
// 单行注释，注意前面的空格
let maxCount = 123
```
###### 多行
```js
/**
 * 多行注释
 */
```
- 减少嵌套  
确定条件不允许时，尽早返回。经典使用场景：校验数据。
```js
// bad
if (condition1) {
  if (condition2) {
    ...
  }
}

// good
if (!condition1) return
if (!condition2) return
...
```
- 减少特定标记值  
使用常量进行自解释
```js
// bad
type: 1 // 1代表新增  2代表修改

// good
const MODIFY_TYPE = {
  ADD: 1,
  EDIT: 2
}
type: MODIFY_TYPE.ADD
```
- 表达式  
尽可能简洁表达式 
```js
// bad
if (name === ''){}
if (collection.length > 0){}
if (notTrue === false){}

// good
if (!name) {}
if (collection.length) {}
if (notTrue) {}
```
- 分支较多处理
对于相同变量或表达式的多值条件，用`switch`代替`if`。
```js
// bad
let type = typeof variable
if (type === 'object') {
  // ...
}
else if (type === 'number' || type === 'boolean' || type === 'string') {
  // ...
}

// good
switch (typeof variable) {
  case "object":
    // ...
    break;
  case "number":
  case "boolean":
  case "string":
    // ...
    break;
}
```
- 使用变量名自解释 `V1.1`
*逻辑复杂时*，建议使用变量名自解释，而不是晦涩难懂的简写。
```js
// bad
function(value) {
    return !helpers.req(value) || this.entity.entVocabularyEntries.filter(item => item.vocabularyEntryName === value).length < 2
}

// good
function(value) {
    let entVocabularyList = this.entity.entVocabularyEntries
    let repeatCount = entVocabularyList.filter(item => item.vocabularyEntryName === value).length
    return !helpers.req(value) || repeatCount < 2
}
```
- 使用函数名自解释 `V1.1`
*遵循单一职责*的基础上，可以把逻辑隐藏在函数中，同时使用准确的函数名自解释。
```js
// bad
if (modifyType === MODIFY_TYPE.ADD) {
    batchVariableAPI(data).then(() => {
        this.closeModal()
        this.$toast.show('添加变量成功')
    })
} else {
  updateVariableAPI(data).then(() => {
        this.closeModal()
        this.$toast.show('修改变量成功')
    })
}

// good
modifyType === MODIFY_TYPE.ADD ？ this._insertVariable(data) : this._updateVariable(data)

_insertVariable() {
    batchVariableAPI(data).then(() => this._successOperation('添加变量成功'))
}

_updateVariable() {
    updateVariableAPI(data).then(() => this._successOperation('修改变量成功'))
}

_successOperation(toastMsg) {
    this.closeModal()
    this.$toast.show(toastMsg)
}
```
###### ***其他规范***
使用prettier格式化工具以及eslint校验
- 格式自动化
- 4个缩进
- 全部单引号
- 方法if / else / for / while / function / switch / do / try / catch / finally 关键字后有一个空格
- 自动省略分号

**.prettierrc配置：**
```js
module.exports = {
    printWidth: 100, // 设置prettier单行输出（不折行）的（最大）长度

    tabWidth: 4, // 设置工具每一个水平缩进的空格数

    useTabs: false, // 使用tab（制表位）缩进而非空格

    semi: false, // 在语句末尾添加分号

    singleQuote: true, // 使用单引号而非双引号

    trailingComma: 'none', // 在任何可能的多行中输入尾逗号

    bracketSpacing: true, // 在对象字面量声明所使用的的花括号后（{）和前（}）输出空格

    arrowParens: 'avoid', // 为单行箭头函数的参数添加圆括号，参数个数为1时可以省略圆括号

    // parser: 'babylon', // 指定使用哪一种解析器

    jsxBracketSameLine: true, // 在多行JSX元素最后一行的末尾添加 > 而使 > 单独一行（不适用于自闭和元素）

    rangeStart: 0, // 只格式化某个文件的一部分

    rangeEnd: Infinity, // 只格式化某个文件的一部分

    filepath: 'none', // 指定文件的输入路径，这将被用于解析器参照

    requirePragma: false, // (v1.7.0+) Prettier可以严格按照按照文件顶部的一些特殊的注释格式化代码，这些注释称为“require pragma”(必须杂注)

    insertPragma: false, //  (v1.8.0+) Prettier可以在文件的顶部插入一个 @format的特殊注释，以表明改文件已经被Prettier格式化过了。

    proseWrap: 'preserve' // (v1.8.2+)
}
```
**.eslintrc.js规则：**
```js
module.exports = {
    root: true,
    env: {
        browser: true,
        node: true
    },
    extends: ['plugin:vue/essential'],
    parserOptions: {
        parser: 'babel-eslint'
    },
    plugins: ['vue'],
    // add your custom rules here
    rules: {
        'arrow-parens': 0, // allow paren-less arrow functions

        'generator-star-spacing': 0, // allow async-await

        'no-unused-vars': 'error', // disabled no ununsed var  `V1.1`

        'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off', // no use debugger in production

        'indent': [2, 4, { SwitchCase: 1 }], // 4 space for tab for perttier

        'space-before-function-paren': ['error', 'never'], // no space in function name for perttier
    }
}
```

##### CSS
- 分号  
每个属性声明后面都要加分号
- 命名
    1.不使用id选择器
    2.适用有意义的名词命名
    3.单词全部小写，名词超过1个时，使用`-`分隔符
- 属性声明顺序
原则：整体到局部，外部到内部，重要属性优先
```css
.element {
    display: block;
    float: left;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;
    margin: 0 100px;
    padding: 50px; // padding习惯写到margin后面
    width: 100px;
    height: 100px;
    border: 1px solid #e5e5e5; border-radius: 3px;
    font: normal 13px "Helvetica Neue", sans-serif;
    color: #333;
    text-align: center;
    line-height: 1.5;
    background-color: #f5f5f5;
    opacity: 1;
}
```
- 其他规范  
使用prettier格式化工具约束，推荐配置如下：
    - 格式自动化
    - 4个缩进
    - 全部单引号
    - 属性:后有空格
    - 颜色全部小写
    - 小数点前面0自动添加
```js
module.exports = {
    printWidth: 100, // 设置prettier单行输出（不折行）的（最大）长度

    tabWidth: 4, // 设置工具每一个水平缩进的空格数

    useTabs: false, // 使用tab（制表位）缩进而非空格

    semi: false, // 在语句末尾添加分号

    singleQuote: true, // 使用单引号而非双引号

    trailingComma: 'none', // 在任何可能的多行中输入尾逗号

    bracketSpacing: true, // 在对象字面量声明所使用的的花括号后（{）和前（}）输出空格

    arrowParens: 'avoid', // 为单行箭头函数的参数添加圆括号，参数个数为1时可以省略圆括号

    // parser: 'babylon', // 指定使用哪一种解析器

    jsxBracketSameLine: true, // 在多行JSX元素最后一行的末尾添加 > 而使 > 单独一行（不适用于自闭和元素）

    rangeStart: 0, // 只格式化某个文件的一部分

    rangeEnd: Infinity, // 只格式化某个文件的一部分

    filepath: 'none', // 指定文件的输入路径，这将被用于解析器参照

    requirePragma: false, // (v1.7.0+) Prettier可以严格按照按照文件顶部的一些特殊的注释格式化代码，这些注释称为“require pragma”(必须杂注)

    insertPragma: false, //  (v1.8.0+) Prettier可以在文件的顶部插入一个 @format的特殊注释，以表明改文件已经被Prettier格式化过了。

    proseWrap: 'preserve' // (v1.8.2+)
}
```

##### Vue规范
- 文件命名  
统一小写，多个单词作为文件名使用分隔符`-`
```js
// bad
EntityList.vue
entityList.vue

// good
entity-list.vue
```

- 紧密耦合的组件命名  
和父组件紧密耦合的子组件应该以父组件名作为前缀命名
```js
// bad
components/
|- todo-list.vue
|- todo-item.vue
└─ todo-button.vue

// good
components/
|- todo-list.vue
|- todo-list-item.vue
└─ todo-list-item-button.vue
```

- 自闭合组件  
在单文件组件中没有内容的组件应该是自闭合的
```js
<!-- bad -->
<u-input></u-input>

<!-- good -->
<u-input />
```

- 指令缩写  
用: 表示 v-bind: ，用@表示v-on
```js
<!-- bad -->
<input v-bind:value="value" v-on:input="onInput">

<!-- good -->
<input :value="value" @input="onInput">
```

- 组件数据  
组件的 data 必须是一个函数,并且建议在此不使用箭头函数
```vue
// bad
export default {
  data: () => ({
    foo: 'bar'
  })
}

// good
export default {
  data () {
    return {
      foo: 'bar'
    }
  }
}
```
- props命名  
小驼峰命名。内容尽量详细，至少有默认值
```vue
// bad
greeting-text: String

// good
greetingText: { type: String, default: ''}
```

- 组件属性顺序和分行规则  
顺序原则：重要属性放前面  
顺序依据：依次指令->props属性-> 事件->dom属性(class有标记作用，除外)  
分行规则：放在一行，重要内容较多时，可放置2～3行  
```vue
<!-- bad -->
<u-select
    class="select"
    size="s"
    @select="searchEntity($event, row)"
    @blur="searchEntity($event, row)"
    v-model="row.variableId"
    :list="variableList" />

<!-- good -->
<u-select v-model="row.variableId" :list="variableList" size="s"
    @select="searchEntity($event, row)" @blur="searchEntity($event, row)" class="select" />
```

- Vue API顺序  
```vue
export default {
    name: '',
    /*1. Vue扩展 */
    extends: '', // extends和mixins都扩展逻辑，需要重点放前面
    mixins: [],   
    components: {},
    /* 2. Vue数据 */
    props: {},
    model: { prop: '', event: '' }, // model 会使用到 props
    data () {
        return {}
    },
    computed: {},
    watch:{}, // watch 监控的是 props 和 data，有必要时监控computed
    /* 3. Vue资源 */
    filters: {},
    directives: {},
    /* 4. Vue生命周期 */
    created () {},
    mounted () {},
    destroy () {},
    /* 5. Vue方法 */
    methods: {}, // all the methods should be put here in the last
}
```

- Vue组件顶级标签顺序  
顺序保持一致，且标签之间留有空行。template第一层级下四个空格，script和style第一层级都不加空格  
```vue
<template>
    <div></div>
</template>

<script>
export default {}
</script>

<style>
.app {}
</style>
```

- import引入顺序 `V1.1`  
原则：同等类型的放一起，优先放mixins和components等UI资源。忌随意放置
```js
// bad
import { getAllEntityList, getVariableGroup } from '@/server/api'
import { helpers } from 'vuelidate/lib/validators'
import { getRepeatLine } from '@/utils/common'
import { CloseModalMixin, InvalidCheckMixin } from '@/components/common/mixins'
import VSearchSelect from '@/components/variable/v-search-select'
import EModifyModal from '@/components/entity/e-modify-modal'
import { MODIFY_MODAL_TYPE } from '@/utils/config'
import { botIdLoc, custIdLoc } from '@/utils/locs'

// good
import { CloseModalMixin, InvalidCheckMixin } from '@/components/common/mixins'
import VSearchSelect from '@/components/variable/v-search-select'
import EModifyModal from '@/components/entity/e-modify-modal'
import { getAllEntityList, getVariableGroup } from '@/server/api'
import { helpers } from 'vuelidate/lib/validators'
import { MODIFY_MODAL_TYPE } from '@/utils/config'
import { getRepeatLine } from '@/utils/common'
import { botIdLoc, custIdLoc } from '@/utils/locs'
```

- Vue 复杂data加注释/分组 `V1.1` 
 data数据是连接View和Modal的基础，当ViewModal复杂时，建议进行注释并分组。另外，当data过于复杂时应考虑优化重构。
```vue
// bad
data() {
    return {
        isOpenModal: false,
        list: [],
        groupList: [],
        searchParams: { groupId: '', searchParam: '', searchType: '' },
        pageParam: { currentPage: 1, pageSize: 50 },
        totalCount: 0,
        groupId: '',
        typeList: [],
        defaultType: 'paramName'
    }
}

// good
data() {
    return {
        variableList: [],
        groupList: [],
        typeList: [],

        /*
        * 查询参数
        * 组与组之间通过空行区分
        */
        searchParams: { groupId: '', searchParam: '', searchType: '', currentPage: 1, pageSize: 50 },
        totalCount: 0,
        defaultType: '',

        isOpenModal: false
    }
}
```

##### 推荐 Vue-Router 写法
使用路由懒加载，实现方式是结合Vue异步组件和Webpack代码分割功能。  
优点：
- 减小包体积，提高加载速度
- 当页面>20个时，组件定义需要拉到编辑器顶部才知道具体路径
```js
// bad
import IntentionList from '@/pages/intention/list'
import Variable from '@/pages/variable'
...

{
    path: '/intention/list',
    name: 'ilist',
    component: IntentionList
},
{
    path: '/variable',
    name: 'variable',
    component: Variable
}

// good
{
    path: '/intention/list',
    name: 'ilist',
    component: () => import('@/pages/intention/list')
},
{
    path: '/variable',
    name: 'variable',
    component: () => import('@/pages/variable')
}
```

##### 1.公用资源管理规范：  
- 公用资源管理，应备份记录在readme.md文件中
	- UI设计资源地址：（蓝湖的地址路径）
	- 测试账号，密码
	- 所用到的网络资源，例如：
		- 地图API  
			账号：   
			密码：  
			key：  
			sessert ID：  
			等
	- 部署：
		- 测试   
			IP：**  
			账号：**  
			密码：**  
			所在地址路径：**  
		- staging
		- production  
		- OSS  
			账号，密码，路径  
		**注**  （账号，密码 出于安全性考虑的话，可以由一个人保管，备注是谁：姓名）  

2.代码规范：  
- 工程目录规范
- 命名规范
	- 驼峰命名
	- 文件夹下 应 以index为入口（如：`test/index.js`）
	- 公用组件命名：需以开发人员的名字（或代号）作为前缀, 英文名+组件名（用图，功能）如：caro-button
	- 变量，文件夹，文件命名，可以使用英文，拼音（使用拼音者，需要全拼，太长的话，后面可以用首字母代替+注释）
- 编写规范
	- 以eslint为标准，根据个人偏好  
	**参考**  
	    - [前端JS规范](https://github.com/lq782655835/blogs/issues/24) ， [或https://lq782655835.github.io/blogs/team-standard/1.standard-ai-js.html](https://lq782655835.github.io/blogs/team-standard/1.standard-ai-js.html)
	    - [前端CSS规范](https://github.com/lq782655835/blogs/issues/25)
	    - [前端Vue规范](https://github.com/lq782655835/blogs/issues/26)
- 封装的组件或工具
	- 要么写测试用例，要么在readme.md文件中编写实例，方便其他人使用。
