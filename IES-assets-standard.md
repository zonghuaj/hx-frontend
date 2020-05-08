 Technology Asset 前端工程规范（v2.0.1）


UI/UX 规范

UI/UX 规范遵循  Technology Asset 资产项目设计规范。详情在 Teams 中  Technology Asset > General  Channel 的文件夹 UI-Mockup > Guideline 下。



 Technology Asset 资产项目设计规范


技术规范


命名规范


项目名称

项目仓库名称使用项目英文名，并使用“-”分割单词，后缀加入"-frontend"。 例如：“Service Catalog”项目的仓库名称为“service-catalog-frontend”。


文件名

项目下文件名使用小写字母, 并使用“-“分割单词。 例如：app-router.module.ts


类名

使用 ES6 Class 时， 类名使用大驼峰式命名规则。 例如：“user service” 类名为 “UserService”


变量名

变量使用小驼峰式命名规则。 例如：“user name” 变量名为 “userName”


代码风格


Angular 项目

遵循 Angular 代码风格


tslint

使用 Angular CLI 创建项目时生成的默认 tslint 规则。


方案选择

框架统一选用基于  Angular 7 + Material + NgRx 封装的 CDS Framework 框架。

CDS Framework 一下技术方案：


UI：CDS components (Material base) + Bootstrap 4 Grid System

Javascript 框架： Angular 7

数据流管理： NgRx

打包：ng cli

测试：jasmine + karma




依赖管理

包管理有限使用 Accenture DevOps 提供的 NPM 服务。

服务地址：https://nexus.atcdevops.accenture.com/nexus/repository/npm-all/


项目配置

在项目根目录添加 .npmrc 文件，并放入以下内容：

registry=https://nexus.atcdevops.accenture.com/nexus/repository/npm-all/
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/

版本管理

依赖包版本使用^前缀，不锁末位小版本。保证项目可以自动更新修复。例如：

// bad
"@cds/framework":'1.0.0',
// good
"@cds/framework":'^1.0.0',


优先使用 "@cds/xx" 包中的 "peerDependencies" 版本。

“@cds/xxx” 依赖 Angular + NgRx + Material 封装， 如项目中版本与 "@cds/xxx" 依赖邦本有冲突，有引发接口不兼容问题。


Javascript


优先使用 Typescript

优先使用 Typescript 语法， 遗留项目可继续使用 Javascript 。


优先使用 esm

优先使用 esm 方式加载和导出 module 。

例如：

import { Inject } from '@angular/core'

export default {a, b}
禁止 esm 与 cjs 混写

例如：


import { Inject } from '@angular/core'

module.exports = {a,b}

避免污染 window

默认不应该向 window 对象上添加变量。在 window 上添加变量会引起全局污染，并使代码不易阅读和理解。

如需要污染 window 变量，需要向团队内技术负责人说明原因，并在设置和引用变量的代码处添加详细使用注释。


CSS


优先使用 sass

优先使用 sass 语法，统一 CSS 语言。 Less 不推荐使用，遗留项目可继续使用。


默认使用 css module

项目默认开启 css module 避免 css 命名冲突。


CDS Framework

项目框架默认使用 CDS Framework。 框架内已集成 Angular 7 + CDS Components + NgRx， 并针对不同场景提供定制模版。


应用架构原则

前端应用应遵循如下原则：


分离 UI 层， 业务层 ， 数据层


UI容器与数据绑定容器分离
状态（数据）集中管理，且不可变。
使用 Flux 模型管理数据。三大前端框架均有相应实现。



使用 action, reducer, selector, effect 方式管理状态更新与绑定

应用状态管理使用 Flux 模型。 使用 action 和 dispatch 方式触发 reducer 更新 state。 这种方式可以让状态更新可追溯，且可回放。配合浏览器 dev 插件，可以清晰看到应用状态如何变化。此方式在复杂应用和庞大系统时优秀的扩展能力。


符合 AOT 语法规范

Angular 项目生产环境必须使用 AOT 模式构建的发布包。 AOT（预先编译）可以压缩发布包体积，并提高项目的运行效率，减少白屏时间。

AOT 要求项目中元数据遵循 Javascript 子集，具体约束参考 Angular 官方文档-元数据的限制


测试


单测

单元测试使用与文件名同名的 .spec.ts 结尾。


集成测试

集成测试用例统一放在项目的 e2e 文件夹下。


工程管控规范


版本管理

版本管理遵循语义化版本规则。

版本格式：主版本号.次版本号.修订号，版本号递增规则如下：


主版本号：当你做了不兼容的 API 修改。
次版本号：当你做了向下兼容的功能性新增。
修订号：当你做了向下兼容的问题修正。



Git 仓库管理

项目版本管理遵循 Gitflow 模式。


主分支（ master ）永远不做直接代码提交，只从开发分支（ dev ） merge
新功能分支使用 feature/xxx 语义化分支名称
线上问题修复使用 hotfix/xxx 语义化分支
集成测试阶段将新功能分支，或修复分支 merge 到开发分支（dev/x.y.z），发布到测试环境。
发布时将开发分支的对应 commit 打 'release/x.y.z' 标签，发布到生产环境并 merge 到  master 分支



发布管理

前端发布使用 DevOps 平台发布。
