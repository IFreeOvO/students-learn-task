# week02 笔记和作业


#### 为什么全局安装@vue/cli后会添加命令vue
因为决定命令名称的是package.json的bin 里面的配置，与包名无关

```json
// package.json
"bin": {
  "vue": "bin/vue.js"
}
```

#### 全局安装@vue-cli时发生了什么
安装后，包会被下载在全局的node_modules里，然后解析`package.json`的`bin`，接着在安装node的主目录的bin文件下创建一个软链接，指向实际执行的文件

#### 为什么vue指向一个js文件，我们却可以直接通过vue命令直接取执行它
执行vue时，它等价于执行指向软链接对应的实际文件，系统会根据文件首行的`#! /usr/bin/env node`，去环境变量中找node命令，最后通过node命令执行实际文件


## learn 指令用法
#### 创建一个包
> **lerna create \<name> [loc]**
>- name是包名，
>- loc是存放路径(**注意:路径必须是在learn.json里配置的。否则包会默认装在packages数组的第一个路径**)

在`utils`文件夹里创建一个包，例子：
```json
// lerna.json配置
{
  "packages": [
    "core/*",
    "commands/*",
    "models/*",
    "utils/*"
  ]
}
```

```
lerna create @if-cli-dev/get-npm-info utils
```


#### 给某个包添加依赖包
> **lerna add \<package> [loc] [@version] [--dev] [--exact]**
>- loc其他包`package.json`所在的路径
>- --dev 添加到devDependencies
>- --exact 安装准确版本，就是安装的包版本前面不带^, Eg: "^2.20.0" ➜ "2.20.0"

给`cli`包添加依赖包`lodash`，例子：

```
// 方式1
lerna add lodash core/cli/

// 方式2
lerna add lodash --scope=cli
```