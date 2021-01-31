# week03 笔记和作业
### 脚手架core模块所涉及的工具库
* npmlog 打印日志
* fs-extra 基于fs封装的文件操作模块
* semver 用于版本比对
* colors 终端中打印不同颜色文字
* user-home 帮我们快速拿到用户的主目录
* dotenv 帮我们获取环境变量
* root-check 检查root账户

### require支持的文件类型
* .js -> 需要文件里又module.exports/exports
* .json -> require用JSON.parse来解析
* .node -> 通过process.dlopen打开c++插件解析
* 其他类型文件默认用js去解析

### npmlog使用
1. 我们可以用`log.addLevel('xxx',111, {xxx})`定制一个log
2. log等级可以用`log.level = xxx`控制, 设置完后凡是数字大于`xxx`的都可以在控制台打印出来。
   例如默认值`log.level = 'info'`, `info`的等级是2000,那么大于等于2000的命令都可以打印。但是`verbose`打印不了，因为`log.addLevel('verbose', 1000, {xxx})`它的值小于2000了
3. `log.heading = 'imooc'`可以给log加统一的前缀
4. `log.headingStyle = {fg: 'red'}`可以给log前缀改样式

### 如何切换root账号操作
在命令前面多加一个sudo
```
sudo 命令
```

### 如何检查是否是root账号操作
```js
process.geteuid() // 结果是0，则是root账号, 501是非root账号
```

### dotenv库注意事项
1. 主目录/.env 需要自己建立一个。默认是找命令执行时所在文件里的.env
2. .env里配置的变量会存一份到`process.env`里面