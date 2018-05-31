---
layout: post
title: angular、vue、react比较
date: 2018-03-25 22:31:30
categories: javascript
tags: [框架]
---
VUE 与其他常见前端框架对比，对比其他框架（转官方文档）
这个页面无疑是最难编写的，但我们认为它也是非常重要的。或许你曾遇到了一些问题并且已经用其他的框架解决了。你来这里的目的是看看 Vue 是否有更好的解决方案。这也是我们在此想要回答的。客观来说，作为核心团队成员，显然我们会更偏爱 Vue，认为对于某些问题来讲用 Vue 解决会更好。如果没有这点信念，我们也就不会整天为此忙活了。但是在此，我们想尽可能地公平和准确地来描述一切。其他的框架也有显著的优点，例如 React 庞大的生态系统，或者像是 Knockout 对浏览器的支持覆盖到了 IE6。我们会尝试着把这些内容全部列出来。

我们也希望得到你的帮助，来使文档保持最新状态，因为 JavaScript 的世界进步的太快。如果你注意到一个不准确或似乎不太正确的地方，请提交问题让我们知道。

**React**
React 和 Vue 有许多相似之处，它们都有：

## 使用 Virtual DOM
提供了响应式 (Reactive) 和组件化 (Composable) 的视图组件。
将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库。
由于有着众多的相似处，我们会用更多的时间在这一块进行比较。这里我们不只保证技术内容的准确性，同时也兼顾了平衡的考量。我们需要承认 React 比 Vue 更好的地方，比如更丰富的生态系统。

React 社区为我们准确进行平衡的考量提供了非常积极的帮助，特别感谢来自 React 团队的 Dan Abramov 。他非常慷慨的花费时间来贡献专业知识来帮助我们完善这篇文档。

## 运行时性能
React 和 Vue 都是非常快的，所以速度并不是在它们之中做选择的决定性因素。对于具体的数据表现，可以移步这个第三方 benchmark，它专注于渲染/更新非常简单的组件树的真实性能。

## 优化
在 React 应用中，当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树。

如要避免不必要的子组件的重渲染，你需要在所有可能的地方使用 PureComponent，或是手动实现 shouldComponentUpdate 方法。同时你可能会需要使用不可变的数据结构来使得你的组件更容易被优化。

然而，使用 PureComponent 和 shouldComponentUpdate 时，需要保证该组件的整个子树的渲染输出都是由该组件的 props 所决定的。如果不符合这个情况，那么此类优化就会导致难以察觉的渲染结果不一致。这使得 React 中的组件优化伴随着相当的心智负担。

在 Vue 应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染。你可以理解为每一个组件都已经自动获得了 shouldComponentUpdate，并且没有上述的子树问题限制。

Vue 的这个特点使得开发者不再需要考虑此类优化，从而能够更好地专注于应用本身。

## HTML & CSS
在 React 中，一切都是 JavaScript。不仅仅是 HTML 可以用 JSX 来表达，现在的潮流也越来越多地将 CSS 也纳入到 JavaScript 中来处理。这类方案有其优点，但也存在一些不是每个开发者都能接受的取舍。

Vue 的整体思想是拥抱经典的 Web 技术，并在其上进行扩展。我们下面会详细分析一下。

## JSX vs Templates
在 React 中，所有的组件的渲染功能都依靠 JSX。JSX 是使用 XML 语法编写 JavaScript 的一种语法糖。

JSX 说是手写的渲染函数有下面这些优势：

- 你可以使用完整的编程语言 JavaScript 功能来构建你的视图页面。比如你可以使用临时变量、JS 自带的流程控制、以及直接引用当前 JS 作用域中的值等等。

- 开发工具对 JSX 的支持相比于现有可用的其他 Vue 模板还是比较先进的 (比如，linting、类型检查、编辑器的自动完成)。

- 事实上 Vue 也提供了渲染函数，甚至支持 JSX。然而，我们默认推荐的还是模板。任何合乎规范的 HTML 都是合法的 Vue 模板，这也带来了一些特有的优势：

- 对于很多习惯了 HTML 的开发者来说，模板比起 JSX 读写起来更自然。这里当然有主观偏好的成分，但如果这种区别会导致开发效率的提升，那么它就有客观的价值存在。

- 基于 HTML 的模板使得将已有的应用逐步迁移到 Vue 更为容易。

- 这也使得设计师和新人开发者更容易理解和参与到项目中。

- 你甚至可以使用其他模板预处理器，比如 Pug 来书写 Vue 的模板。

有些开发者认为模板意味着需要学习额外的 DSL (Domain-Specific Language 领域特定语言) 才能进行开发——我们认为这种区别是比较肤浅的。首先，JSX 并不是免费的——它是基于 JS 之上的一套额外语法，因此也有它自己的学习成本。同时，正如同熟悉 JS 的人学习 JSX 会很容易一样，熟悉 HTML 的人学习 Vue 的模板语法也是很容易的。最后，DSL 的存在使得我们可以让开发者用更少的代码做更多的事，比如 v-on 的各种修饰符，在 JSX 中实现对应的功能会需要多得多的代码。

更抽象一点来看，我们可以把组件区分为两类：一类是偏视图表现的 (presentational)，一类则是偏逻辑的 (logical)。我们推荐在前者中使用模板，在后者中使用 JSX 或渲染函数。这两类组件的比例会根据应用类型的不同有所变化，但整体来说我们发现表现类的组件远远多于逻辑类组件。

## 组件作用域内的 CSS
除非你把组件分布在多个文件上 (例如 CSS Modules)，CSS 作用域在 React 中是通过 CSS-in-JS 的方案实现的 (比如 styled-components、glamorous 和 emotion)。这引入了一个新的面向组件的样式范例，它和普通的 CSS 撰写过程是有区别的。另外，虽然在构建时将 CSS 提取到一个单独的样式表是支持的，但 bundle 里通常还是需要一个运行时程序来让这些样式生效。当你能够利用 JavaScript 灵活处理样式的同时，也需要权衡 bundle 的尺寸和运行时的开销。

如果你是一个 CSS-in-JS 的爱好者，许多主流的 CSS-in-JS 库也都支持 Vue (比如 styled-components-vue 和 vue-emotion)。这里 React 和 Vue 主要的区别是，Vue 设置样式的默认方法是单文件组件里类似 style 的标签。

单文件组件让你可以在同一个文件里完全控制 CSS，将其作为组件代码的一部分。

```
<style scoped>
  @media (min-width: 250px) {
    .list-container:hover {
      background: orange;
    }
  }
</style>
```

这个可选 scoped 属性会自动添加一个唯一的属性 (比如 data-v-21e5b78) 为组件内 CSS 指定作用域，编译的时候 .list-container:hover 会被编译成类似.list-container[data-v-21e5b78]:hover。

最后，Vue 的单文件组件里的样式设置是非常灵活的。通过 vue-loader，你可以使用任意预处理器、后处理器，甚至深度集成 CSS Modules——全部都在 <style> 标签内。

## 规模
- 向上扩展
Vue 和 React 都提供了强大的路由来应对大型应用。React 社区在状态管理方面非常有创新精神 (比如 Flux、Redux)，而这些状态管理模式甚至 Redux 本身也可以非常容易的集成在 Vue 应用中。实际上，Vue 更进一步地采用了这种模式 (Vuex)，更加深入集成 Vue 的状态管理解决方案 Vuex 相信能为你带来更好的开发体验。

两者另一个重要差异是，Vue 的路由库和状态管理库都是由官方维护支持且与核心库同步更新的。React 则是选择把这些问题交给社区维护，因此创建了一个更分散的生态系统。但相对的，React 的生态系统相比 Vue 更加繁荣。

最后，Vue 提供了Vue-cli 脚手架，能让你非常容易地构建项目，包含了Webpack，Browserify，甚至 no build system。React 在这方面也提供了create-react-app，但是现在还存在一些局限性：

它不允许在项目生成时进行任何配置，而 Vue 支持 Yeoman-like 定制。
它只提供一个构建单页面应用的单一模板，而 Vue 提供了各种用途的模板。
它不能用用户自建的模板构建项目，而自建模板对企业环境下预先建立协议是特别有用的。
而要注意的是这些限制是故意设计的，这有它的优势。例如，如果你的项目需求非常简单，你就不需要自定义生成过程。你能把它作为一个依赖来更新。如果阅读更多关于不同的设计理念。

- 向下扩展
React 学习曲线陡峭，在你开始学 React 前，你需要知道 JSX 和 ES2015，因为许多示例用的是这些语法。你需要学习构建系统，虽然你在技术上可以用 Babel 来实时编译代码，但是这并不推荐用于生产环境。

就像 Vue 向上扩展好比 React 一样，Vue 向下扩展后就类似于 jQuery。你只要把如下标签放到页面就可以运行：

```
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

然后你就可以编写 Vue 代码并应用到生产中，你只要用 min 版 Vue 文件替换掉就不用担心其他的性能问题。

由于起步阶段不需学 JSX，ES2015 以及构建系统，所以开发者只需不到一天的时间阅读指南就可以建立简单的应用程序。

## 原生渲染
React Native 能使你用相同的组件模型编写有本地渲染能力的 APP (iOS 和 Android)。能同时跨多平台开发，对开发者是非常棒的。相应地，Vue 和 Weex 会进行官方合作，Weex 是阿里的跨平台用户界面开发框架，Weex 的 JavaScript 框架运行时用的就是 Vue。这意味着在 Weex 的帮助下，你使用 Vue 语法开发的组件不仅仅可以运行在浏览器端，还能被用于开发 iOS 和 Android 上的原生应用。

在现在，Weex 还在积极发展，成熟度也不能和 React Native 相抗衡。但是，Weex 的发展是由世界上最大的电子商务企业的需求在驱动，Vue 团队也会和 Weex 团队积极合作确保为开发者带来良好的开发体验。

另一个 Vue 的开发者们很快就会拥有的选项是 NativeScript，这是一个社区驱动的插件。

## MobX
Mobx 在 React 社区很流行，实际上在 Vue 也采用了几乎相同的反应系统。在有限程度上，React + Mobx 也可以被认为是更繁琐的 Vue，所以如果你习惯组合使用它们，那么选择 Vue 会更合理。

AngularJS (Angular 1)
Vue 的一些语法和 AngularJS 的很相似 (例如 v-if vs ng-if)。因为 AngularJS 是 Vue 早期开发的灵感来源。然而，AngularJS 中存在的许多问题，在 Vue 中已经得到解决。

## 复杂性
在 API 与设计两方面上 Vue.js 都比 AngularJS 简单得多，因此你可以快速地掌握它的全部特性并投入开发。

## 灵活性和模块化
Vue.js 是一个更加灵活开放的解决方案。它允许你以希望的方式组织应用程序，而不是在任何时候都必须遵循 AngularJS 制定的规则，这让 Vue 能适用于各种项目。我们知道把决定权交给你是非常必要的。
这也就是为什么我们提供 webpack template，让你可以用几分钟，去选择是否启用高级特性，比如热模块加载、linting、CSS 提取等等。

## 数据绑定
AngularJS 使用双向绑定，Vue 在不同组件间强制使用单向数据流。这使应用中的数据流更加清晰易懂。

## 指令与组件
在 Vue 中指令和组件分得更清晰。指令只封装 DOM 操作，而组件代表一个自给自足的独立单元——有自己的视图和数据逻辑。在 AngularJS 中两者有不少相混的地方。

## 运行时性能
Vue 有更好的性能，并且非常非常容易优化，因为它不使用脏检查。

在 AngularJS 中，当 watcher 越来越多时会变得越来越慢，因为作用域内的每一次变化，所有 watcher 都要重新计算。并且，如果一些 watcher 触发另一个更新，脏检查循环 (digest cycle) 可能要运行多次。AngularJS 用户常常要使用深奥的技术，以解决脏检查循环的问题。有时没有简单的办法来优化有大量 watcher 的作用域。

Vue 则根本没有这个问题，因为它使用基于依赖追踪的观察系统并且异步队列更新，所有的数据变化都是独立触发，除非它们之间有明确的依赖关系。

有意思的是，Angular 和 Vue 用相似的设计解决了一些 AngularJS 中存在的问题。

**Angular (原本的 Angular 2)**
我们将新的 Angular 独立开来讨论，因为它是一个和 AngularJS 完全不同的框架。例如：它具有优秀的组件系统，并且许多实现已经完全重写，API 也完全改变了。

## TypeScript
Angular 事实上必须用 TypeScript 来开发，因为它的文档和学习资源几乎全部是面向 TS 的。TS 有很多好处——静态类型检查在大规模的应用中非常有用，同时对于 Java 和 C# 背景的开发者也是非常提升开发效率的。

然而，并不是所有人都想用 TS——在中小型规模的项目中，引入 TS 可能并不会带来太多明显的优势。在这些情况下，用 Vue 会是更好的选择，因为在不用 TS 的情况下使用 Angular 会很有挑战性。

最后，虽然 Vue 和 TS 的整合可能不如 Angular 那么深入，我们也提供了官方的 类型声明 和组件装饰器，并且知道有大量用户在生产环境中使用 Vue + TS 的组合。我们也和微软的 TS / VSCode 团队进行着积极的合作，目标是为 Vue + TS 用户提供更好的类型检查和 IDE 开发体验。

## 运行时性能
这两个框架都很快，有非常类似的 benchmark 数据。你可以浏览具体的数据做更细粒度的对比，不过速度应该不是决定性的因素。

## 体积
在体积方面，最近的 Angular 版本中在使用了 AOT 和 tree-shaking 技术后使得最终的代码体积减小了许多。但即使如此，一个包含了 Vuex + Vue Router 的 Vue 项目 (gzip 之后 30kB) 相比使用了这些优化的 angular-cli 生成的默认项目尺寸 (~130kB) 还是要小得多。

## 灵活性
Vue 相比于 Angular 更加灵活，Vue 官方提供了构建工具来协助你构建项目，但它并不限制你去如何组织你的应用代码。有人可能喜欢有严格的代码组织规范，但也有开发者喜欢更灵活自由的方式。

## 学习曲线
要学习 Vue，你只需要有良好的 HTML 和 JavaScript 基础。有了这些基本的技能，你就可以非常快速地通过阅读 指南 投入开发。

Angular 的学习曲线是非常陡峭的——作为一个框架，它的 API 面积比起 Vue 要大得多，你也因此需要理解更多的概念才能开始有效率地工作。当然，Angular 本身的复杂度是因为它的设计目标就是只针对大型的复杂应用；但不可否认的是，这也使得它对于经验不甚丰富的开发者相当的不友好。

## Ember
Ember 是一个全能框架。它提供了大量的约定，一旦你熟悉了它们，开发会变得很高效。不过，这也意味着学习曲线较高，而且并不灵活。这意味着在框架和库 (加上一系列松散耦合的工具) 之间做权衡选择。后者会更自由，但是也要求你做更多架构上的决定。

也就是说，我们最好比较的是 Vue 内核和 Ember 的模板与数据模型层：

Vue 在普通 JavaScript 对象上建立响应，提供自动化的计算属性。在 Ember 中需要将所有东西放在 Ember 对象内，并且手工为计算属性声明依赖。

Vue 的模板语法可以用全功能的 JavaScript 表达式，而 Handlebars 的语法和帮助函数相比来说非常受限。

在性能上，Vue 比 Ember 好很多，即使是 Ember 2.x 的最新 Glimmer 引擎。Vue 能够自动批量更新，而 Ember 在性能敏感的场景时需要手动管理。

## Knockout
Knockout 是 MVVM 领域内的先驱，并且追踪依赖。它的响应系统和 Vue 也很相似。它在浏览器支持以及其他方面的表现也是让人印象深刻的。它最低能支持到 IE6，而 Vue 最低只能支持到 IE9。

随着时间的推移，Knockout 的发展已有所放缓，并且略显有点老旧了。比如，它的组件系统缺少完备的生命周期事件方法，尽管这些在现在是非常常见的。以及相比于 Vue 调用子组件的接口它的方法显得有点笨重。

如果你有兴趣研究，你还会发现二者在接口设计的理念上是不同的。这可以通过各自创建的simple Todo List 体现出来。或许有点主观，但是很多人认为 Vue 的 API 接口更简单结构更优雅。

## Polymer
Polymer 是另一个由谷歌赞助的项目，事实上也是 Vue 的一个灵感来源。Vue 的组件可以粗略的类比于 Polymer 的自定义元素，并且两者具有相似的开发风格。最大的不同之处在于，Polymer 是基于最新版的 Web Components 标准之上，并且需要重量级的 polyfills 来帮助工作 (性能下降)，浏览器本身并不支持这些功能。相比而言，Vue 在支持到 IE9 的情况下并不需要依赖 polyfills 来工作。

在 Polymer 1.0 版本中，为了弥补性能，团队非常有限的使用数据绑定系统。例如，在 Polymer 中唯一支持的表达式只有布尔值否定和单一的方法调用，它的 computed 方法的实现也并不是很灵活。

Polymer 自定义的元素是用 HTML 文件来创建的，这会限制使用 JavaScript/CSS (和被现代浏览器普遍支持的语言特性)。相比之下，Vue 的单文件组件允许你非常容易的使用 ES2015 和你想用的 CSS 预编译处理器。

在部署生产环境时，Polymer 建议使用 HTML Imports 加载所有资源。而这要求服务器和客户端都支持 Http 2.0 协议，并且浏览器实现了此标准。这是否可行就取决于你的目标用户和部署环境了。如果状况不佳，你必须用 Vulcanizer 工具来打包 Polymer 元素。而在这方面，Vue 可以结合异步组件的特性和 Webpack 的代码分割特性来实现懒加载 (lazy-loaded)。这同时确保了对旧浏览器的兼容且又能更快加载。

而 Vue 和 Web Component 标准进行深层次的整合也是完全可行的，比如使用 Custom Elements、Shadow DOM 的样式封装。然而在我们做出严肃的实现承诺之前，我们目前仍在等待相关标准成熟，进而再广泛应用于主流的浏览器中。

## Riot
Riot 3.0 提供了一个类似于基于组件的开发模型 (在 Riot 中称之为 Tag)，它提供了小巧精美的 API。Riot 和 Vue 在设计理念上可能有许多相似处。尽管相比 Riot ，Vue 要显得重一点，Vue 还是有很多显著优势的：

更好的性能。Riot 使用了 遍历 DOM 树 而不是虚拟 DOM，但实际上用的还是脏检查机制，因此和 AngularJS 患有相同的性能问题。
更多成熟工具的支持。Vue 提供官方支持 webpack 和 Browserify，而 Riot 是依靠社区来建立集成系统。


框架间的竞争并不是零和游戏。虽然解决的核心痛点有重合，但适用场景还是有区别。比如 React/Vue 这样以 view layer 为核心，可以灵活选择整体架构和工具链的框架，和 Angular 2 这样大而全一站到底的框架，各有各适合的场景。Vue 因为不需要构建也能直接用，也能用在一些比 React 更轻量的场景中。撇开场景，也有开发风格的偏好问题。有些人用 React 更有效率，有些人用 Vue 更有效率，而 C#/Java 生态圈一大群人会觉得 TypeScript 和 Angular 2 让他们更有效率。最理想的情况是大家都找到最符合自己场景需求和开发偏好的框架，所以我觉得多框架的并存是合理且有意义的，不太可能出现 Angular 2 火了就没人再用 React/Vue 的情况。

**技术角度**
    React 和 Angular 2 都有服务端渲染和原生渲染的功能（Angular 2 只是号称会有，具体啥时候会有，好不好用还不知道）。这两个东西在对此有需求的场景下，是很有吸引力的，但实际上对此有硬需求的场景占多少百分比则是个问题。比如服务端渲染的前提是前端渲染层得用 Node.js 交给『全栈』去做，原生渲染的多端代码复用率会因应用实际需求而变化，制约它们发挥的条件还是不少的，因此我个人乐观地认为这并不会影响 Vue 在整个市场中占有一席之地。另一方面，手淘已经押宝 Weex，也不排除哪天我会搞个 Vue 服务端渲染。

 **性能方面**
    这几个主流框架都应该可以轻松应付大部分常见场景的性能需求，区别在于可优化性和优化对于开发体验的影响。这一点上我觉得 Vue 可能是最简单的，加好 track-by 就 ok 了。React 需要 shouldComponentUpdate 或者全面 Immutable，Angular 2 需要手动指定 change detection strategy，都有一定程度的侵入性。但是从整体趋势上来说，浏览器和手机还会越变越快，框架本身的渲染性能在整个前端性能优化体系中，会渐渐淡化，更多的优化点还是在构建方式、缓存、图片加载、网络链路、HTTP/2 等方面。顺道说一句，Angular 2 压缩后的大小是 500 多 kb，在移动场景反正我是不敢用。
**开发体验**

这方面，我个人认为 Vue 是最容易上手，最具亲和度的。工具链方面最近刚发布了 vue-cli，1 分钟搞定 webpack 配置。Vue 组件格式只要你会 HTML/CSS/JS 就能写，你要用 coffeescript 或者 less/sass 也没问题。React 的 JSX 是道坎，但跨过去之后会有一定的生产力提升。社区工具丰富，但实在太多，配置工具麻烦。CSS in JS 也不是每个人的菜。Angular 2 目前上手配置也非常麻烦，官方正在写一个 cli，但体验如何要出来了才知道。它推荐的默认语言是 TypeScript，这个对于静态类型爱好者来说是个大优点，配合 WebStorm/VSCode 体验会很不错，但也不是所有人的菜。

**社区生态**
>React 是目前最成熟也最活跃的，但有一个问题就是过于频繁的方案迭代，几个月前的最佳实践可能明天就变过去式了，而 FB 官方对于最佳实践基本是采取让社区自行发展的态度，因此社区长期处于一个百家争鸣的状态，直到今年下半年才慢慢地开始合流到了 React + react-router + redux 的主流方案，并且这两天也开始讨论工具链的最佳实践。这些东西一旦稳定下来，会进一步巩固 React 的地位

>Vue 的社区固然比不上 React，但也不算太小。Gitter 聊天室里有 1300 来号人，国内听说也有几百人的 QQ 群，论坛上也还算有些活跃度。社区组件也在稳步发展：vuejs/awesome-vue · GitHub 当然比起 React 来说还是小巫见大巫，希望 2016 能更进一步。比起 React 来说，Vue 的一个好处就是提供了官方推荐的 Vue + vue-router + vuex + webpack + vue-loader 的全套方案，如果你不想三个月换一套，就跟着官方推荐走；如果自己有想法，那就自己整也没问题。

>Angular 2 的社区，目前来说基本没有，到现在连文档都没写完呢，也没法有什么生态。更伤的是 ng2 和 ng1 的生态是完全割裂的。2016 年能怎么发展，要看 Google 的社区运营做得如何，但不管怎么说 Google 的影响力在那边，群众基数还是很大的

>在中国还有另一个制约条件，那就是 IE8，这三个框架里面只有 React 支持 IE8


作者：尤雨溪
链接：https://www.zhihu.com/question/38989845/answer/79216477
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。