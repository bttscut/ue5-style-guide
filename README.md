# [Gamemakin](https://gamemak.in) UE4 Style Guide() {

*最合理的UE4规范*

灵感来源于Airbnb的JS规范 [Airbnb Javascript Style Guide](https://github.com/airbnb/javascript).


## 关于本工程的声明

当前工程的地址为 https://github.com/thejinchao/ue5-style-guide. 原英文工程地址为 https://github.com/Allar/ue5-style-guide. 缺省分支名已经改为 `main`.

## 关于Linter和规范的文档

更多关于Linter和工程规范的文档可以参考[这个页面](https://ue4-style-guide.readthedocs.io/en/latest/)

## 讨论该规范

Gamemakin LLC 有一个公开的讨论板块，地址是 http://discord.gamemak.in ，其中还包含了#linter聊天区，如果你有关于本套规范或者插件的任何想法，欢迎来讨论。

## 链接到本文档

本文的任何章节都有数字超链接地址，你可以直接通过本文的短地址 http://ue-cn.style 再加上章节编号，直接链接到本文的任意位置。
例如，如果你想把本文的第一节发送给其他人，在地址后面加上`#0.1`即可，也就是使用地址 http://ue-cn.style#0.1

## 目录
- [重要术语](#important-terminology)
  - [关卡/地图](#terms-level-map)
  - [标识符](#terms-identifiers)
  - [大小写](#terms-cases)
  - [变量 / 属性](#terms-var-prop)
    - [属性](#terms-property)
    - [变量](#terms-variable)
- [0. 原则](#0)
  - [0.1 如果你的项目已经存在现有规范，那么请继续遵守规范](#0.1)
  - [0.2 不管团队中有多少人，工程中所有的数据结构、资源、代码风格应该统一，如同是同一个人的作品](#0.2)
  - [0.3 真正的好朋友不会让对方写烂代码](#0.3)
  - [0.4 谨慎加入没有规范的团队](#0.4)
  - [0.5 请遵守法律条款](#0.5)
- [00. 需要强制执行的全局规范](#00)
  - [00.1 禁止使用的字符](#00.1)
    - [标识符](#identifiers)
- [1. 资源命名约定](#anc)
  - [1.1 基本命名规则 - `Prefix_BaseAssetName_Variant_Suffix`](#base-asset-name)
    - [1.1 范例](#1.1-examples)
  - [1.2 资源类型表](#asset-name-modifiers)
    - [1.2.1 通用类型(Most Common)](#anc-common)
    - [1.2.2 动作(Animations)](#anc-animations)
    - [1.2.3 人工智能(Artificial Intelligence)](#anc-ai)
    - [1.2.4 蓝图(Blueprints)](#anc-bp)
    - [1.2.5 材质(Materials)](#anc-materials)
    - [1.2.6 纹理(Textures)](#anc-textures)
      - [1.2.6.1 多重纹理(Texture Packing)](#anc-textures-packing)
    - [1.2.7 杂项(Miscellaneous)](#anc-misc)
    - [1.2.8 Paper 2D](#anc-paper2d)
    - [1.2.9 物理(Physics)](#anc-physics)
    - [1.2.10 声音(Sounds)](#anc-sounds)
    - [1.2.11 界面(User Interface)](#anc-ui)
    - [1.2.12 特效(Effects)](#anc-effects)
- [2. Content的目录结构](#structure)
  - [2e1 目录结构示例](#2e1)
  - [2.1 文件夹命名](#structure-folder-names)
    - [2.1.1 使用PascalCase大小写规范](#2.1.1)
    - [2.1.2 不要使用空格](#2.1.2)
    - [2.1.3 不要使用奇怪的符号 ](#2.1.3)
  - [2.2 使用一个顶级目录来保存所有工程资源 ](#structure-top-level)
    - [2.2.1 避免全局资源](#2.2.1)
    - [2.2.2 减少资源迁移时的冲突](#2.2.2)
      - [2.2.2e1 举例：基础材质的麻烦](#2.2.2e1)
    - [2.2.3 范例，模板以及商场中的资源都是安全没有风险的](#2.2.3)
    - [2.2.4 使得DLC、子工程、以及补丁包容易维护](#2.2.4)
  - [2.3 使用开发者目录做本地测试](#structure-developers)
  - [2.4 所有场景<sup>*</sup> 文件应该保存在一个名为'Maps'的目录中 ](#structure-maps)
  - [2.5 使用`Core`目录存储系统蓝图资源以及其他系统资源 ](#structure-core)
  - [2.6 不要创建名为`Assets` 或者 `AssetTypes`的目录](#structure-assettypes)
    - [2.6.1 创建一个名为`Assets`的目录是多余的](#2.6.1)
    - [2.6.2 创建名为`Meshes`、 `Textures`或者`Materials`的目录是多余的](#2.6.2)
  - [2.7 超大资源要有自己的目录结构 ](#structure-large-sets)
  - [2.8 材质库`MaterialLibrary`](#structure-material-library)
  - [2.9 避免空目录存在](#structure-no-empty-folders)
- [3. 蓝图(Blueprint)](#bp)
  - [3.1 编译(Compiling)](#bp-compiling)
  - [3.2 变量(Variables)](#bp-vars)
    - [3.2.1 命名(Naming)](#bp-var-naming)
      - [3.2.1.1 使用名词](#bp-var-naming-nouns)
      - [3.2.1.2 PascalCase](#bp-var-naming-case)
        - [3.2.1.2e 范例](#3.2.1.2e)
      - [3.2.1.3 布尔变量 `b` 前缀](#bp-var-bool-prefix)
      - [3.2.1.4 布尔类型变量命名规则](#bp-var-bool-names)
        - [3.2.1.4.1 需要包含独立信息](#3.2.1.4.1)
        - [3.2.1.4.2 避免表达复杂状态](#3.2.1.4.2)
      - [3.2.1.5 考虑上下文](#bp-vars-naming-context)
        - [3.2.1.5e 范例](#3.2.1.5e)
      - [3.2.1.6 __不要__ 在变量中包含变量类型名称](#bp-vars-naming-atomic)
      - [3.2.1.7 非原生类型的变量，需要包含变量类型名](#bp-vars-naming-complex)
      - [3.2.1.8 数组](#bp-vars-naming-arrays)
    - [3.2.2 可编辑变量](#bp-vars-editable)
      - [3.2.2.1 Tooltips](#bp-vars-editable-tooltips)
      - [3.2.2.2 滑动条(Slider)以及取值范围](#bp-vars-editable-ranges)
    - [3.2.3 分类](#bp-vars-categories)
    - [3.2.4 变量的访问权限](#bp-vars-access)
      - [3.2.4.1 私有变量](#bp-vars-access-private)
    - [3.2.5 高级显示](#bp-vars-advanced)
    - [3.2.6 Transient变量](#bp-vars-transient)
    - [3.2.8 Config变量](#bp-vars-config)
  - [3.3 函数、事件以及事件派发器](#bp-functions)
    - [3.3.1 函数命名](#bp-funcs-naming)
      - [3.3.1.1 所有函数的命名都应该是动词](#bp-funcs-naming-verbs)
      - [3.3.1.2 属性的状态变化响应函数应该命名为`OnRep_Variable`](#bp-funcs-naming-onrep)
      - [3.3.1.3 返回布尔变量的信息查询函数应该是问询函数](#bp-funcs-naming-bool)
      - [3.3.1.4 E事件的响应函数和派发函数都应该以`On`开头](#bp-funcs-naming-eventhandlers)
      - [3.3.1.5 远程调用函数应该用目标作为前缀](#bp-funcs-naming-rpcs)
    - [3.3.2 所有函数都应该有返回节点](#bp-funcs-return)
    - [3.3.3 蓝图函数中节点数不应该超过50个](#bp-graphs-funcs-node-limit)
    - [3.3.4 所有Public函数都应该有功能描述](#bp-graphs-funcs-description)
    - [3.3.5 插件中自定义的可以在蓝图中调用的函数都应该放在以插件名命名的类别中](#bp-graphs-funcs-plugin-category)
  - [3.4 蓝图节点](#bp-graphs)
    - [3.4.1 不要画‘意面’](#bp-graphs-spaghetti)
    - [3.4.2 保持连线对齐，而不是节点](#bp-graphs-align-wires)
    - [3.4.3 白色的可执行线优先级最高](#bp-graphs-exec-first-class)
    - [3.4.4 节点应该有合理的注释](#bp-graphs-block-comments)
    - [3.4.5 蓝图中需要在适当的地方处理类型转换错误](#bp-graphs-cast-error-handling)
    - [3.4.6 避免出现空悬节点和死节点](#bp-graphs-dangling-nodes)
- [4. 静态模型](#4)
  - [4.1 静态模型的UVs](#s-uvs)
    - [4.1.1 静态模型需要包含UV](#s-uvs-no-missing)
    - [4.1.2 静态模型的UV须要避免互相覆盖](#s-uvs-no-overlapping)
  - [4.2 正确的设置LOD](#s-lods)
  - [4.3 不带插槽的模块化的模型需要严格对齐网格](#s-modular-snapping)
  - [4.4 所有模型需要有碰撞体](#s-collision)
  - [4.5 所有模型资源需要正确的缩放系数](#s-scaled)
- [5. Niagara](#Niagara)
  - [5.1 永远不要有空格](#ng-rules)
- [6. 关卡/ 地图](#levels)
  - [6.1 解决掉错误和警告](#levels-no-errors-or-warnings)
  - [6.2 记得构建光照](#levels-lighting-should-be-built)
  - [6.3 不要让玩家看到Z Fighting](#levels-no-visible-z-fighting)
  - [6.4 商城需要遵守的规范](#levels-mp-rules)
    - [6.4.1 预览场景](#levels-mp-rules-overview)
    - [6.4.2 演示场景](#levels-mp-rules-demo)
- [7. 纹理](#textures)
  - [7.1 纹理大小需要是2的幂](#textures-dimensions)
  - [7.2 纹理图案密度应该保持一致](#textures-density)
  - [7.3 纹理大小不要超过8192](#textures-max-size)
  - [7.4 正确对纹理进行分组](#textures-group)

## 重要术语

<a name="terms-level-map"></a>
##### 关卡/地图

“map”(地图)这个词通常也会被称为“level”(关卡)，两者的含义是等同的，在[这里](https://en.wikipedia.org/wiki/Level_(video_gaming)) 可以查看这个词的历史

<a name="terms-identifiers"></a>
##### 标识符(Identifier)

“标识符”(`Identifier`)是指所有类似于“名称”或起到“名称”作用的东西。 例如，资源的名称，或材质的名称，蓝图属性、变量名或文件夹名，或数据表行名称等......

<a name="terms-cases"></a>
##### 大小写(Case)

对于大小写的规范有数种，以下是几种常见的几种

> ###### 大驼峰式(PascalCase)
>
> 每个单词的首字母都是大写，单词之间没有其他字符，例如 ：`DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
>
> ###### 小驼峰式(camelCase)
>
> 第一个单词的首字母小写，后面的单词的首字母大写，例如：`desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### 蛇式(Snake_case)
>
> 单词之间用下划线链接，单词的首字母可以大写也可以小写，例如：`desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

<a name="terms-var-prop"></a>
##### 变量/属性(Variables / Properties)

'变量'和'属性'两个词在很多情况下是可以互相通用的。但如果他们同时出现在一个环境时，含义有一些不同：

<a name="terms-property"></a>
###### 属性(Property)
'属性'通常定义在一个类的内部。例如，如果一个类`BP_Barrel`有一个内部成员`bExploded`，那么`bExploded`可以是做是`BP_Barrel`的一个属性

当'属性'用在类的内部时，通常用来获取已经定义好的数据

<a name="terms-variable"></a>
###### 变量(Variable)
'变量'通常用在给函数传递参数，或者用在函数内的局部变量

当'变量'用在类的内部时，通常是用来定义什么或者用来保存某些数据的。

<a name="0"></a>
## 0. 基本原则

以下改编自[idomatic.js代码规范](https://github.com/rwaldron/idiomatic.js/).

<a name="0.1"></a>
### 0.1 如果你的项目已经存在现有规范，那么请继续遵守规范

如果你工作的项目或你的团队已经有一套自己的规范，那么请尊重它。如果现有规范和本套规范发生冲突，请继续遵守原规范.

好的项目规范应该是不断进步的，当你发现有好的更改可以适合所有用户时，你应该建议去更改现有规范.

> #### "对规范优劣的争论是没有意义的，有规范你就该去遵守。"
> [_Rebecca Murphey_](https://rmurphey.com)

<a name="0.2"></a>
### 0.2 不管团队中有多少人，工程中所有的数据结构、资源、代码风格应该统一，如同是同一个人的作品

把资源从一个工程迁移到另一个工程不应该产生新的学习成本，所有资源应该符合项目规范，消除不必要的歧义和不确定性.

遵守规范可以促进对于项目的生产和维护效率，因为团队成员不用去考虑规范问题，只需要去遵守。本套规范根据诸多优秀经验编写，遵守它意味着可以少走很多弯路.

<a name="0.3"></a>
### 0.3 真正的好朋友不会让对方写烂代码

如果你发现同事不遵守规范，该去纠正他们.

当在团队中工作时，或者在社区提问时(例如[Unreal Slackers](http://join.unrealslackers.org/)) ，你会发现如果大家都遵守同一套规范会容易的多，没有人愿意在面对一堆乱糟糟的蓝图或者莫名其妙的代码时帮你解决问题.

如果你要帮助的人使用另一套不同但很健全的规范，你应该去适应它，如果他们没有遵守任何规范，那么带他们来这儿.

<a name="0.4"></a>
### 0.4 谨慎加入没有规范的团队

当你要加入一个新的UE团队时，你应该首先问他们有没有项目规范，如果没有的话，你该怀疑他们是否有能力像一个真正的团队那样工作.

<a name="0.5"></a>
### 0.5 请遵守法律条款

Gamemakin 团队不是专业的律师，但请不要在项目中涉及违反法律的行为，包括但不限于：

* 请勿传播您无权传播的内容.
* 不得侵犯他人的版权或商标.
* 请勿窃取工程资产.
* 遵守资产的许可协议，例如当需要注明资产原创作者时，一定要注明.

<a name="00"></a>
## 00. 需要强制执行的全局规范

@TODO: Make this section 1 and update this document accordingly. Or maybe we don't?

<a name="00.1"></a>
### 00.1 禁止使用的字符

<a name="identifiers-1"></a>
#### 标识符

对于标识符类型的命名，除非必要，**绝对不要**使用以下字符:

* 空格或者其他类似的空白字符
* 反斜杠 `\`
* 各种符号，例如 `#!@$%`
* 任何Unicode字符集

标识符应该只包含以下字符（用正则表达式表示就是`[A-Za-z0-9_]+`)

* ABCDEFGHIJKLMNOPQRSTUVWXYZ
* abcdefghijklmnopqrstuvwxyz
* 1234567890
* _ (下划线)

这样做的原因是，尽可能确保跨平台和工具链的兼容性。并有也有助于防止那些不是你控制的程序处理你的工程资产时，因为这些程序中的字符处理错误而导致的意外故障。

<a name="anc"></a>
<a name="1"></a>
## 1. 资源命名约定

对于资源的命名的规范应该像法律一样被遵守。一个项目如果有好的命名规范，那么在资源管理、查找、解析、维护时，都会有极大的便利性。

大多数资源的命名都应该有前缀，前缀一般是资源类型的缩写，然后使用下划线和资源名链接。

<a name="base-asset-name"></a>
<a name="1.1"></a>
### 1.1 基本命名规则 - `Prefix_BaseAssetName_Variant_Suffix`

所有资源都应该有一个 _BaseAssetName_ (基本资源名)。所谓基本资源名表明该资源在逻辑关系上属于那种资源，任何属于该逻辑组的资源都应该遵守同样的命名规范 `Prefix_BaseAssetName_Variant_Suffix`.

时刻谨记这个命名规范`Prefix_BaseAssetName_Variant_Suffix`，只要遵守它，大部分情况下都可以让命名规范。下面是详细的解释.

`Prefix`(前缀) 和 `Suffix`(后缀)由资源类型确定，请参照下面的[资源类型表](#asset-name-modifiers).

`BaseAssetName`(基本资源名)应该使用简短而便于识别的词汇，例如，如果你有一个角色名字叫做Bob，那么所有和Bob相关的资源的`BaseAssetName`都应该叫做`Bob`.

`Varient`(扩展名)用来保证资源的唯一性，同样，扩展名也应该是简短而容易理解的短词，以说明该资源在所属的资源逻辑组中的子集。例如，如果Bob有多套皮肤，那么这些皮肤资源都应该使用Bob作为基本资源名同时包含扩展名，例如'Evil'类型的皮肤资源，名字应该是`Bob_Evil`，而Retro类型的皮肤应该是用`Bob_Retro`.

一般来说，如果仅仅是为了保证资源的唯一性，`Varient`可以使用从`01`开始的两位数字来表示。例如，如果你要制作一堆环境中使用的石头资源，那么他们应该命名为`Rock_01`, `Rock_02`, `Rock_03`等等。除非特殊需要，不要让数字超过三位数，如果你真的需要超过100个的资源序列，那么你应该考虑使用多个基础资源名.

基于你所制作的资源扩展属性，你可以把多个扩展名串联起来。例如，如果你在制作一套地板所使用的资源，那么你的资源除了使用`Flooring`作为基本名，扩展名可以使用多个，例如`Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

<a name="1.1-examples"></a>
#### 1.1 范例

##### 1.1e1 Bob

| 资源类型                | 资源名                                                     |
| ----------------------- | ---------------------------------------------------------- |
| Skeletal Mesh           | SK_Bob                                                     |
| Material                | M_Bob                                                      |
| Texture (Diffuse/Albedo)| T_Bob_D                                                    |
| Texture (Normal)        | T_Bob_N                                                    |
| Texture (Evil Diffuse)  | T_Bob_Evil_D                                               |

##### 1.1e2 Rocks

| 资源类型                | 资源名                                                     |
| ----------------------- | ---------------------------------------------------------- |
| Static Mesh (01)        | S_Rock_01                                                  |
| Static Mesh (02)        | S_Rock_02                                                  |
| Static Mesh (03)        | S_Rock_03                                                  |
| Material                | M_Rock                                                     |
| Material Instance (Snow)| MI_Rock_Snow                                               |

<a name="asset-name-modifiers"></a>
<a name="1.2"></a>
### 1.2 资源类型表

当给一个资源命名的时候，请参照以下表格来决定在[基本命名](#base-asset-name)中所使用的前缀和后缀

<a name="anc-common"></a>
<a name="1.2.1"></a>
#### 1.2.1 通用类型(Most Common)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Level / Map             |            |            | [所有地图应该放在Maps目录下](#2.4) |
| Level (持久关卡)        |            | _P         |                                  |
| Level (音效关卡)        |            | _Audio     |                                  |
| Level (光照)            |            | _Lighting  |                                  |
| Level (几何体)          |            | _Geo       |                                  |
| Level (Gameplay)        |            | _Gameplay  |                                  |
| Blueprint               | BP_        |            |                                  |
| Material                | M_         |            |                                  |
| Static Mesh             | S_         |            | 很多人使用 SM_. 但我们建议用 S_. |
| Skeletal Mesh           | SK_        |            |                                  |
| Texture                 | T_         | _?         | 参照[纹理](#anc-textures)        |
| Particle System         | PS_        |            |                                  |
| Widget Blueprint        | WBP_       |            |                                  |

<a name="anc-animations"></a>
<a name="1.2.2"></a>
#### 1.2.2 动作(Animations)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Aim Offset              | AO_        |            |                                  |
| Aim Offset 1D           | AO_        |            |                                  |
| Animation Blueprint     | ABP_       |            |                                  |
| Animation Composite     | AC_        |            |                                  |
| Animation Montage       | AM_        |            |                                  |
| Animation Sequence      | A_         |            |                                  |
| Blend Space             | BS_        |            |                                  |
| Blend Space 1D          | BS_        |            |                                  |
| Level Sequence          | LS_        |            |                                  |
| Morph Target            | MT_        |            |                                  |
| Paper Flipbook          | PFB_       |            |                                  |
| Rig                     | Rig_       |            |                                  |
| Skeletal Mesh           | SK_        |            |                                  |
| Skeleton                | SKEL_      |            |                                  |

<a name="anc-ai"></a>
<a name="1.2.3"></a>
### 1.2.3 人工智能(Artificial Intelligence)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI Controller           | AIC_       |            |                                  |
| Behavior Tree           | BT_        |            |                                  |
| Blackboard              | BB_        |            |                                  |
| Decorator               | BTDecorator_ |          |                                  |
| Service                 | BTService_ |            |                                  |
| Task                    | BTTask_    |            |                                  |
| Environment Query       | EQS_       |            |                                  |
| EnvQueryContext         | EQS_       | Context    |                                  |

<a name="anc-bp"></a>
<a name="1.2.4"></a>
### 1.2.4 蓝图(Blueprints)

| 资源类型                      | 前缀       | 后缀       | 备注                             |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Blueprint                     | BP_        |            |                                  |
| Blueprint Component           | BP_        | Component  | 例如 BP_InventoryComponent       |
| Blueprint Function Library    | BPFL_      |            |                                  |
| Blueprint Interface           | BPI_       |            |                                  |
| Blueprint Macro Library       | BPML_      |            | 可能的话尽量不要使用蓝图宏.      |
| Enumeration                   | E          |            | 没有下划线.                      |
| Structure                     | F or S     |            | 没有下划线.                      |
| Tutorial Blueprint            | TBP_       |            |                                  |
| Widget Blueprint              | WBP_       |            |                                  |

<a name="anc-materials"></a>
<a name="1.2.5"></a>
### 1.2.5 材质(Materials)

| 资源类型                      | 前缀       | 后缀       | 备注                             |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Material                      | M_         |            |                                  |
| Material (Post Process)       | PP_        |            |                                  |
| Material Function             | MF_        |            |                                  |
| Material Instance             | MI_        |            |                                  |
| Material Parameter Collection | MPC_       |            |                                  |
| Subsurface Profile            | SP_        |            |                                  |
| Physical Materials            | PM_        |            |                                  |
| Decal                         | M_, MI_    | _Decal     |                                  |

<a name="anc-textures"></a>
<a name="1.2.6"></a>
### 1.2.6 纹理(Textures)

| 资源类型                      | 前缀       | 后缀       | 备注                             |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Texture                       | T_         |            |                                  |
| Texture (Diffuse/Albedo/Base Color)| T_    | _D         |                                  |
| Texture (Normal)              | T_         | _N         |                                  |
| Texture (Roughness)           | T_         | _R         |                                  |
| Texture (Alpha/Opacity)       | T_         | _A         |                                  |
| Texture (Ambient Occlusion)   | T_         | _O         |                                  |
| Texture (Bump)                | T_         | _B         |                                  |
| Texture (Emissive)            | T_         | _E         |                                  |
| Texture (Mask)                | T_         | _M         |                                  |
| Texture (Specular)            | T_         | _S         |                                  |
| Texture (Metallic)            | T_         | _M         |                                  |
| Texture (Packed)              | T_         | _*         | 参照下面的[多重纹理](#anc-textures-packing). |
| Texture Cube                  | TC_        |            |                                  |
| Media Texture                 | MT_        |            |                                  |
| Render Target                 | RT_        |            |                                  |
| Cube Render Target            | RTC_       |            |                                  |
| Texture Light Profile         | TLP        |            |                                  |

<a name="anc-textures-packing"></a>
<a name="1.2.6.1"></a>
#### 1.2.6.1 多重纹理(Texture Packing)
把多张纹理存于一个纹理文件中是很常见的方法，比如通常可以把自发光(Emissive), 粗糙度(Roughness), 环境光(Ambient Occlusion)以RGB通道的形式保存在纹理中，然后在文件的后缀中，注明这些信息，例如`_EGO`

> 一般来说，在纹理的Diffuse信息中附带Alpha/Opacity信息是很常见的，这时在`_D`后缀中可以加入`A`也可以不用加

不推荐同时把RGBA四个通道的信息保存在一张纹理中，这是由于带有Alpha通道的纹理要比不带的占用更多的资源，除非Alpha信息是以蒙版(Mask)的形式保存在Diffuse/Albedo通道中。


<a name="anc-misc"></a>
<a name="1.2.7"></a>
### 1.2.7 杂项(Miscellaneous)

| 资源类型                   | 前缀       | 后缀       | 备注                             |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| Animated Vector Field      | VFA_       |            |                                  |
| Camera Anim                | CA_        |            |                                  |
| Color Curve                | Curve_     | _Color     |                                  |
| Curve Table                | Curve_     | _Table     |                                  |
| Data Asset                 | *_         |            | 前缀取决于何种类型资源.          |
| Data Table                 | DT_        |            |                                  |
| Float Curve                | Curve_     | _Float     |                                  |
| Foliage Type               | FT_        |            |                                  |
| Force Feedback Effect      | FFE_       |            |                                  |
| Landscape Grass Type       | LG_        |            |                                  |
| Landscape Layer            | LL_        |            |                                  |
| Matinee Data               | Matinee_   |            |                                  |
| Media Player               | MP_        |            |                                  |
| File Media Source          | FMS_       |            |                                  |
| Object Library             | OL_        |            |                                  |
| Redirector                 |            |            | (暂时空缺，尽快解决).            |
| Sprite Sheet               | SS_        |            |                                  |
| Static Vector Field        | VF_        |            |                                  |
| Substance Graph Instance   | SGI_       |            |                                  |
| Substance Instance Factory | SIF_       |            |                                  |
| Touch Interface Setup      | TI_        |            |                                  |
| Vector Curve               | Curve_     | _Vector    |                                  |

<a name="anc-paper2d"></a>
<a name="1.2.8"></a>
### 1.2.8 Paper 2D

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          | PFB_       |            |                                  |
| Sprite                  | SPR_       |            |                                  |
| Sprite Atlas Group      | SPRG_      |            |                                  |
| Tile Map                | TM_        |            |                                  |
| Tile Set                | TS_        |            |                                  |

<a name="anc-physics"></a>
<a name="1.2.9"></a>
### 1.2.9 物理(Physics)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Physical Material       | PM_        |            |                                  |
| Physics Asset           | PHYS_      |            |                                  |
| Destructible Mesh       | DM_        |            |                                  |

<a name="anc-sounds"></a>
<a name="1.2.10"></a>
### 1.2.10 声音(Sounds)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          | DV_        |            |                                  |
| Dialogue Wave           | DW_        |            |                                  |
| Media Sound Wave        | MSW_       |            |                                  |
| Reverb Effect           | Reverb_    |            |                                  |
| Sound Attenuation       | ATT_       |            |                                  |
| Sound Class             |            |            | 没有前缀和后缀，这些资源应该放在SoundClasses目录中 |
| Sound Concurrency       |            | _SC        | 在SoundClass之后命名             |
| Sound Cue               | A_         | _Cue       |                                  |
| Sound Mix               | Mix_       |            |                                  |
| Sound Wave              | A_         |            |                                  |

<a name="anc-ui"></a>
<a name="1.2.11"></a>
### 1.2.11 界面(User Interface)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    | Font_      |            |                                  |
| Slate Brush             | Brush_     |            |                                  |
| Slate Widget Style      | Style_     |            |                                  |
| Widget Blueprint        | WBP_       |            |                                  |

<a name="anc-effects"></a>
<a name="1.2.12"></a>
### 1.2.12 特效(Effects)

| 资源类型                | 前缀       | 后缀       | 备注                             |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Particle System         | PS_        |            |                                  |
| Material (Post Process) | PP_        |            |                                  |

**[⬆ 返回](#table-of-contents)**

<a name="2"></a>
<a name="structure"></a>
## 2. Content Directory Structure

Equally important as asset names, the directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

There are multiple ways to lay out the content of a UE4 project. In this style, we will be using a structure that relies more on filtering and search abilities of the Content Browser for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

> If you are using the prefix [naming convention](#1.2) above, using folders to contain assets of similar types such as `Meshes`, `Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix as well as able to be filtered in the content browser.

<a name="2e1"><a>
### 2e1 Example Project Content Structure
<pre>
|-- Content
    |-- <a href="#2.2">GenericShooter</a>
        |-- Art
        |   |-- Industrial
        |   |   |-- Ambient
        |   |   |-- Machinery
        |   |   |-- Pipes
        |   |-- Nature
        |   |   |-- Ambient
        |   |   |-- Foliage
        |   |   |-- Rocks
        |   |   |-- Trees
        |   |-- Office
        |-- Characters
        |   |-- Bob
        |   |-- Common
        |   |   |-- <a href="#2.7">Animations</a>
        |   |   |-- Audio
        |   |-- Jack
        |   |-- Steve
        |   |-- <a href="#2.1.3">Zoe</a>
        |-- <a href="#2.5">Core</a>
        |   |-- Characters
        |   |-- Engine
        |   |-- <a href="#2.1.2">GameModes</a>
        |   |-- Interactables
        |   |-- Pickups
        |   |-- Weapons
        |-- Effects
        |   |-- Electrical
        |   |-- Fire
        |   |-- Weather
        |-- <a href="#2.4">Maps</a>
        |   |-- Campaign1
        |   |-- Campaign2
        |-- <a href="#2.8">MaterialLibrary</a>
        |   |-- Debug
        |   |-- Metal
        |   |-- Paint
        |   |-- Utility
        |   |-- Weathering
        |-- Placeables
        |   |-- Pickups
        |-- Weapons
            |-- Common
            |-- Pistols
            |   |-- DesertEagle
            |   |-- RocketPistol
            |-- Rifles
</pre>

The reasons for this structure are listed in the following sub-sections.

<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 Folder Names

These are common rules for naming any folder in the content structure.

<a name="2.1.1"></a>
#### 2.1.1 Always Use PascalCase[<sup>*</sup>](#terms-cases)

PascalCase refers to starting a name with a capital letter and then instead of using spaces, every following word also starts with a capital letter. For example, `DesertEagle`, `RocketPistol`, and `ASeriesOfWords`.

See [Cases](#terms-cases).

<a name="2.1.2"></a>
#### 2.1.2 Never Use Spaces

Re-enforcing [2.1.1](#2.1.1), never use spaces. Spaces can cause various engineering tools and batch processes to fail. Ideally, your project's root also contains no spaces and is located somewhere such as `D:\Project` instead of `C:\Users\My Name\My Documents\Unreal Projects`.

<a name="2.1.3"></a>
#### 2.1.3 Never Use Unicode Characters And Other Symbols

If one of your game characters is named 'Zoë', its folder name should be `Zoe`. Unicode characters can be worse than [Spaces](#2.1.2) for engineering tool and some parts of UE4 don't support Unicode characters in paths either.

Related to this, if your project has [unexplained issues](https://answers.unrealengine.com/questions/101207/undefined.html) and your computer's user name has a Unicode character (i.e. your name is `Zoë`), any project located in your `My Documents` folder will suffer from this issue. Often simply moving your project to something like `D:\Project` will fix these mysterious issues.

Using other characters outside `a-z`, `A-Z`, and `0-9` such as `@`, `-`, `_`, `,`, `*`, and `#` can also lead to unexpected and hard to track issues on other platforms, source control, and weaker engineering tools.

<a name="2.2"></a>
<a name="structure-top-level"><a>
### 2.2 Use A Top Level Folder For Project Specific Assets

All of a project's assets should exist in a folder named after the project. For example, if your project is named 'Generic Shooter', _all_ of it's content should exist in `Content/GenericShooter`.

> The `Developers` folder is not for assets that your project relies on and therefore is not project specific. See [Developer Folders](#2.3) for details about this.

There are multiple reasons for this approach.

<a name="2.2.1"></a>
#### 2.2.1 No Global Assets

Often in code style guides it is written that you should not pollute the global namespace and this follows the same principle. When assets are allowed to exist outside of a project folder, it often becomes much harder to enforce a strict structure layout as assets not in a folder encourages the bad behavior of not having to organize assets.

Every asset should have a purpose, otherwise it does not belong in a project. If an asset is an experimental test and shouldn't be used by the project it should be put in a [`Developer`](#2.3) folder.

<a name="2.2.2"></a>
#### 2.2.2 Reduce Migration Conflicts

When working on multiple projects it is common for a team to copy assets from one project to another if they have made something useful for both. When this occurs, the easiest way to perform the copy is to use the Content Browser's Migrate functionality as it will copy over not just the selected asset but all of its dependencies.

These dependencies are what can easily get you into trouble. If two project's assets do not have a top level folder and they happen to have similarly named or already previously migrated assets, a new migration can accidentally wipe any changes to the existing assets.

This is also the primary reason why Epic's Marketplace staff enforces the same policy for submitted assets.

After a migration, safe merging of assets can be done using the 'Replace References' tool in the content browser with the added clarity of assets not belonging to a project's top level folder are clearly pending a merge. Once assets are merged and fully migrated, there shouldn't be another top level folder in your Content tree. This method is _100%_ guaranteed to make any migrations that occur completely safe.

<a name="2.2.2e1"></a>
##### 2.2.2e1 Master Material Example

For example, say you created a master material in one project that you would like to use in another project so you migrated that asset over. If this asset is not in a top level folder, it may have a name like `Content/MaterialLibrary/M_Master`. If the target project doesn't have a master material already, this should work without issue.

As work on one or both projects progress, their respective master materials may change to be tailored for their specific projects due to the course of normal development.

The issue comes when, for example, an artist for one project created a nice generic modular set of static meshes and someone wants to include that set of static meshes in the second project. If the artist who created the assets used material instances based on `Content/MaterialLibrary/M_Master` as they're instructed to, when a migration is performed there is a great chance of conflict for the previously migrated `Content/MaterialLibrary/M_Master` asset.

This issue can be hard to predict and hard to account for. The person migrating the static meshes may not be the same person who is familiar with the development of both project's master material, and they may not be even aware that the static meshes in question rely on material instances which then rely on the master material. The Migrate tool requires the entire chain of dependencies to work however, and so it will be forced to grab `Content/MaterialLibrary/M_Master` when it copies these assets to the other project and it will overwrite the existing asset.

It is at this point where if the master materials for both projects are incompatible in _any way_, you risk breaking possibly the entire material library for a project as well as any other dependencies that may have already been migrated, simply because assets were not stored in a top level folder. The simple migration of static meshes now becomes a very ugly task.

<a name="2.2.3"></a>
#### 2.2.3 Samples, Templates, and Marketplace Content Are Risk-Free

An extension to [2.2.2](#2.2.2), if a team member decides to add sample content, template files, or assets they bought from the marketplace, it is guaranteed, as long your project's top-level folder is uniquely named,that these new assets will not interfere with your project.

You can not trust marketplace content to fully conform to the [top level folder rule](#2.2). There exists many assets that have the majority of their content in a top level folder but also have possibly modified Epic sample content as well as level files polluting the global `Content` folder.

When adhering to [2.2](#2.2), the worst marketplace conflict you can have is if two marketplace assets both have the same Epic sample content. If all your assets are in a project specific folder, including sample content you may have moved into your folder, your project will never break.

<a name="2.2.4"></a>
#### 2.2.4 DLC, Sub-Projects, and Patches Are Easily Maintained

If your project plans to release DLC or has multiple sub-projects associated with it that may either be migrated out or simply not cooked in a build, assets relating to these projects should have their own separate top level content folder. This make cooking DLC separate from main project content far easier. Sub-projects can also be migrated in and out with minimal effort. If you need to change a material of an asset or add some very specific asset override behavior in a patch, you can easily put these changes in a patch folder and work safely without the chance of breaking the core project.

<a name="2.3"></a>
<a name="structure-developers"></a>
### 2.3 Use Developers Folder For Local Testing

During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control server. Not all teams require use of Developer folders, but ones that do use them often run into a common problem with assets submitted to source control.

It is very easy for a team member to accidentally use assets that are not ready for use, which will cause issues once those assets are removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they could be subject to incredible change and/or removal. This causes massive amounts of re-working for everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never have had a reason to use them and the whole issue would never happen. The Content Browser has specific View Options that will hide Developer folders (they are hidden by default) making it impossible to accidentally use Developer assets under normal use.

Once the assets are ready for use, an artist simply has to move the assets into the project specific folder and fix up redirectors. This is essentially 'promoting' the assets from experimental to production.

<a name="2.4"></a>
<a name="structure-maps"></a>
### 2.4 All Map[<sup>*</sup>](#terms-level-map) Files Belong In A Folder Called Maps

Map files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `/Content/Project/Maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `Maps`, such as `Maps/Campaign1/` or `Maps/Arenas`, but the most important thing here is that they all exist within `/Content/Project/Maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well as QA processes.

<a name="2.5"></a>
<a name="structure-core"></a>
### 2.5 Use A `Core` Folder For Critical Blueprints And Other Assets

Use `/Content/Project/Core` folder for assets that are absolutely fundamental to a project's workings. For example, base `GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`, and related Blueprints should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the `Core` folder. Following good code structure style, designers should be making their gameplay tweaks in child classes that expose functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `Core/Pickups` that defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as `/Content/Project/Placeables/Pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not touch `Core/Pickups` as they may unintentionally break pickups project-wide.

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 Do Not Create Folders Called `Assets` or `AssetTypes`

<a name="2.6.1"></a>
#### 2.6.1 Creating a folder named `Assets` is redundant

All assets are assets.

<a name="2.6.2"></a>
#### 2.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant

All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `S_` prefix for a static mesh is only two characters, whereas `Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 Very Large Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [2.6](#2.6).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#2.8).

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary`

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Content/Project/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="2.9"></a>
<a name="structure-no-empty-folders"></a>
### 2.9 No Empty Folders

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:
1. Be sure you're using source control.
1. Immediately run Fix Up Redirectors on your project.
1. Navigate to the folder on-disk and delete the assets inside.
1. Close the editor.
1. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
1. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
1. Ensure the folder is now gone.
1. Submit changes to source control.

**[⬆ Back to Top](#table-of-contents)**


<a name="3"></a>
<a name="bp"></a>
## 3. Blueprints

This section will focus on Blueprint classes and their internals. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Remember: Blueprinting badly bears blunders, beware! (Phrase by [KorkuVeren](http://github.com/KorkuVeren))

<a name="3.1"></a>
<a name="bp-compiling"></a>
### 3.1 Compiling

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken blueprints to source control. If you must store them on source control, shelve them instead.

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures, and frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

<a name="3.2"></a>
<a name="bp-vars"></a>
### 3.2 Variables

The words `variable` and `property` may be used interchangeably.

<a name="3.2.1"></a>
<a name="bp-var-naming"></a>
#### 3.2.1 Naming

<a name="3.2.1.1"></a>
<a name="bp-var-naming-nouns"></a>
##### 3.2.1.1 Nouns

All non-boolean variable names must be clear, unambiguous, and descriptive nouns.

<a name="3.2.1.2"></a>
<a name="bp-var-naming-case"></a>
##### 3.2.1.2 PascalCase

All non-boolean variables should be in the form of [PascalCase](#terms-cases).

<a name="3.2.1.2e"></a>
###### 3.2.1.2e Examples

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

<a name="3.2.1.3"></a>
<a name="bp-var-bool-prefix"></a>
##### 3.2.1.3 Boolean `b` Prefix

All booleans should be named in PascalCase but prefixed with a lowercase `b`.

Example: Use `bDead` and `bEvil`, **not** `Dead` and `Evil`.

UE4 Blueprint editors know not to include the `b` in user-friendly displays of the variable.

<a name="3.2.1.4"></a>
<a name="bp-var-bool-names"></a>
##### 3.2.1.4 Boolean Names

<a name="3.2.1.4.1"></a>
###### 3.2.1.4.1 General And Independent State Information

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase the variable as a question, such as `Is`. This is reserved for functions.

Example: Use `bDead` and `bHostile` **not** `bIsDead` and `bIsHostile`.

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

<a name="3.2.1.4.2"></a>
###### 3.2.1.4.2 Complex States

Do not to use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `EWeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined state names.

<a name="3.2.1.5"></a>
<a name="bp-vars-naming-context"></a>
##### 3.2.1.5 Considered Context

All variable names must not be redundant with their context as all variable references in Blueprint will always have context.

<a name="3.2.1.5e"></a>
###### 3.2.1.5e Examples

Consider a Blueprint called `BP_PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `BP_PlayerCharacter` it belongs to because it is `BP_PlayerCharacter` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

<a name="3.2.1.6"></a>
<a name="bp-vars-naming-atomic"></a>
##### 3.2.1.6 Do _Not_ Include Atomic Type Names

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats, and enumerations.

Strings and vectors are considered atomic in terms of style when working with Blueprints, however they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do _not_ consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of a string of characters is `String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted _and_ when using a name without a variable type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may potentially read as an Array of a variable type named `Post`.

<a name="3.2.1.7"></a>
<a name="bp-vars-naming-complex"></a>
##### 3.2.1.7 Do Include Non-Atomic Type Names

Non-atomic or complex variables are variables that represent data as a collection of atomic variables. Structs, Classes, Interfaces, and primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic variable type is a list of variables, Arrays do not change the 'atomicness' of a variable type.

These variables should include their type name while still considering their context.

If a class owns an instance of a complex variable, i.e. if a `BP_PlayerCharacter` owns a `BP_Hat`, it should be stored as the variable type as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex variable represents, you should use a noun along with the variable type.

Example: If a `BP_Turret` has the ability to target a `BP_PlayerCharacter`, it should store its target as `TargetPlayer` as when in the context of `BP_Turret` it should be clear that it is a reference to another complex variable type that it does not own.


<a name="3.2.1.8"></a>
<a name="bp-vars-naming-arrays"></a>
##### 3.2.1.8 Arrays

Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.


<a name="3.2.2"></a>
<a name="bp-vars-editable"></a>
#### 3.2.2 Editable Variables

All variables that are safe to change the value of in order to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should _not_ be marked as editable, unless for engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

<a name="3.2.2.1"></a>
<a name="bp-vars-editable-tooltips"></a>
##### 3.2.2.1 Tooltips

All `Editable` variables, including those marked editable just so they can be marked as `Expose On Spawn`, should have a description in their `Tooltip` fields that explains how changing this value affects the behavior of the blueprint.

<a name="3.2.2.2"></a>
<a name="bp-vars-editable-ranges"></a>
##### 3.2.2.2 Slider And Value Ranges

All `Editable` variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A blueprint that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

<a name="3.2.3"></a>
<a name="bp-vars-categories"></a>
#### 3.2.3 Categories

If a class has only a small number of variables, categories are not required.

If a class has a moderate amount of variables (5-10), all `Editable` variables should have a non-default category assigned. A common category is `Config`.

If a class has a large amount of variables, all `Editable` variables should be categorized into sub-categories using the category `Config` as the base category. Non-editable variables should be categorized into descriptive categories describing their usage.

> You can define sub-categories by using the pipe character `|`, i.e. `Config | Animations`.

Example: A weapon class set of variables might be organized as:

    |-- Config
    |    |-- Animations
    |    |-- Effects
    |    |-- Audio
    |    |-- Recoil
    |    |-- Timings
    |-- Animations
    |-- State
    |-- Visuals

<a name="3.2.4"></a>
<a name="bp-vars-access"></a>
#### 3.2.4 Variable Access Level

In C++, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

Blueprints do not have a defined concept of protected access currently.

Treat `Editable` variables as public variables. Treat non-editable variables as protected variables.

<a name="3.2.4.1"></a>
<a name="bp-vars-access-private"></a>
##### 3.2.4.1 Private Variables

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

<a name="3.2.5"></a>
<a name="bp-vars-advanced"></a>
#### 3.2.5 Advanced Display

If a variable should be editable but often untouched, mark it as `Advanced Display`. This makes the variable hidden unless the advanced display arrow is clicked.

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

<a name="3.2.6"></a>
<a name="bp-vars-transient"></a>
#### 3.2.6 Transient Variables

Transient variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is useful for references to other objects and actors who's value isn't known until run-time. This prevents the editor from ever saving a reference to it, and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

<a name="3.2.7"></a>
<a name="bp-vars-config"></a>
#### 3.2.8 Config Variables

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

<a name="3.3"></a>
<a name="bp-functions"></a>
### 3.3 Functions, Events, and Event Dispatchers

This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

<a name="3.3.1"></a>
<a name="bp-funcs-naming"></a>
#### 3.3.1 Function Naming

The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="3.3.1.1"></a>
<a name="bp-funcs-naming-verbs"></a>
#### 3.3.1.1 All Functions Should Be Verbs

All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions, event handlers, and event dispatchers are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

<a name="3.3.1.2"></a>
<a name="bp-funcs-naming-onrep"></a>
#### 3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor. If you are writing a C++ `OnRep` function however, it should also follow this convention when exposing it to Blueprints.

<a name="3.3.1.3"></a>
<a name="bp-funcs-naming-bool"></a>
#### 3.3.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#bp-funcs-naming-verbs).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

<a name="3.3.1.4"></a>
<a name="bp-funcs-naming-eventhandlers"></a>
#### 3.3.1.4 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#bp-funcs-naming-verbs). The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

<a name="3.3.1.5"></a>
<a name="bp-funcs-naming-rpcs"></a>
#### 3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be prefixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the prefix, follow all other rules regarding function naming.

Good examples:

* `ServerFireWeapon`
* `ClientNotifyDeath`
* `MulticastSpawnTracerEffect`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.


<a name="3.3.2"></a>
<a name="bp-funcs-return"></a>
#### 3.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

<a name="3.3.3"></a>
<a name="bp-graphs-funcs-node-limit"></a>
#### 3.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="3.3.4"></a>
<a name="bp-graphs-funcs-description"></a>
#### 3.3.4 All Public Functions Should Have A Description

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specificer of Public should have its description filled out.

<a name="3.3.5"></a>
<a name="bp-graphs-funcs-plugin-category"></a>
#### 3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

<a name="3.4"></a>
<a name="bp-graphs"></a>
### 3.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

<a name="3.4.1"></a>
<a name="bp-graphs-spaghetti"></a>
#### 3.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

<a name="3.4.2"></a>
<a name="bp-graphs-align-wires"></a>
#### 3.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

<a name="3.4.3"></a>
<a name="bp-graphs-exec-first-class"></a>
#### 3.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

<a name="3.4.4"></a>
<a name="bp-graphs-block-comments"></a>
#### 3.4.4 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and  description should suffice.

<a name="3.4.5"></a>
<a name="bp-graphs-cast-error-handling"></a>
#### 3.4.5 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

<a name="3.4.6"></a>
<a name="bp-graphs-dangling-nodes"></a>
#### 3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.

**[⬆ Back to Top](#table-of-contents)**


<a name="4"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 4. Static Meshes

This section will focus on Static Mesh assets and their internals.

<a name="4.1"></a>
<a name="s-uvs"></a>
### 4.1 Static Mesh UVs

If Linter is reporting bad UVs and you can't seem to track it down, open the resulting `.log` file in your project's `Saved/Logs` folder for exact details as to why it's failing. I am hoping to include these messages in the Lint report in the future.

<a name="4.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 4.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="4.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="4.2"></a>
<a name="s-lods"></a>
### 4.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="4.3"></a>
<a name="s-modular-snapping"></a>
### 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="4.4"></a>
<a name="s-collision"></a>
### 4.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="4.5"></a>
<a name="s-scaled"></a>
### 4.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**


<a name="5"></a>
<a name="Niagara"></a>
<a name="ng"></a>
## 5. Niagara

This section will focus on Niagara assets and their internals.

<a name="5.1"></a>
<a name="ng-rules"></a>
### 5.1 No Spaces, Ever

As mentioned in [00.1 Forbidden Identifiers](#00), spaces and all white space characters are forbidden in identifiers. This is especially true for Niagara systems as it makes working with things significantly harder if not impossible when working with HLSL or other means of scripting within Niagara and trying to reference an identifier.

(Original Contribution by [@dunenkoff](https://github.com/Allar/ue5-style-guide/issues/58))


**[⬆ Back to Top](#table-of-contents)**


<a name="6"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 6. Levels / Maps

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

<a name="6.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 6.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

Please note: Linter is even more strict on this than the editor is currently, and will catch load errors that the editor will resolve on its own.

<a name="6.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 6.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="6.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 6.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

<a name="6.4"></a>
<a name="levels-mp-rules"></a>
### 6.4 Marketplace Specific Rules

If a project is to be sold on the UE4 Marketplace, it must follow these rules.

<a name="6.4.1"></a>
<a name="levels-mp-rules-overview"></a>
#### 6.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

This overview map, if it is visualizing assets, should be set up according to [Epic's guidelines](http://help.epicgames.com/customer/en/portal/articles/2592186-marketplace-submission-guidelines-preparing-your-assets#Required%20Levels%20and%20Maps).

For example, `InteractionComponent_Overview`.

<a name="6.4.2"></a>
<a name="levels-mp-rules-demo"></a>
#### 6.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**


<a name="7"></a>
<a name="textures"></a>
## 7. Textures

This section will focus on Texture assets and their internals.

<a name="7.1"></a>
<a name="textures-dimensions"></a>
### 7.1 Dimensions Are Powers of 2

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="7.2"></a>
<a name="textures-density"></a>
### 7.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="7.3"></a>
<a name="textures-max-size"></a>
### 7.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="7.4"></a>
<a name="textures-group"></a>
### 7.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**


## Major Contributors

* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [billymcguffin](https://github.com/billymcguffin)
* [akenatsu](https://github.com/akenatsu)

## License

Copyright (c) 2016 Gamemakin LLC

See [LICENSE](/LICENSE)

**[⬆ Back to Top](#table-of-contents)**


## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
