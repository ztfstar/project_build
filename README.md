# project_build
前端轻量化部署脚手架，支持测试、线上等多环境部署，支持环境配置扩展，配置好后仅需一条命令即可完成整个部署流程。

## 安装
全局安装project_build
```
npm i project_build -g
```
查看版本，表示安装成功。

![安装project_build](./imgs/安装deploy.png)

## 使用
### 1.初始化部署模板
```
deploy init
```

![初始化](./imgs/初始化.png)

### 2.配置部署环境
部署配置文件位于deploy文件夹下的`deploy.config.js`,
一般包含`dev`（测试环境）和`prod`（线上环境）两个配置，再有多余的环境配置形式与之类似，只有一个环境的可以删除另一个多余的配置（比如只有`prod`线上环境，请删除`dev`测试环境配置）。

具体配置信息请参考配置文件注释：
```
module.exports = {
  privateKey: '', // 本地私钥地址，位置一般在C:/Users/xxx/.ssh/id_rsa，非必填，有私钥则配置
  passphrase: '', // 本地私钥密码，非必填，有私钥则配置
  projectName: 'hivue', // 项目名称
  dev: { // 测试环境
    name: '测试环境',
    script: "npm run build-dev", // 测试环境打包脚本
    host: '10.240.176.99', // 开发服务器地址
    port: 22, // ssh port，一般默认22
    username: 'root', // 登录服务器用户名
    password: '123456', // 登录服务器密码
    distPath: 'dist',  // 本地打包dist目录
    webDir: '/var/www/html/dev/hivue',  // // 测试环境服务器地址
  },
  prod: {  // 线上环境
    name: '线上环境',
    script: "npm run build", // 线上环境打包脚本
    host: '10.240.176.99', // 开发服务器地址
    port: 22, // ssh port，一般默认22
    username: 'root', // 登录服务器用户名
    password: '123456', // 登录服务器密码
    distPath: 'dist',  // 本地打包dist目录
    webDir: '/var/www/html/prod/hivue' // 线上环境web目录
  }
  // 再还有多余的环境按照这个格式写即可
}
```

### 3.查看部署命令
配置好`deploy.config.js`，运行
```
deploy --help
```
查看部署命令

![部署命令](./imgs/部署命令.png)

### 4.测试环境部署
测试环境部署采用的时`dev`的配置
```
deploy dev
```
先有一个确认，确认后进入部署流程，完成6步操作后，部署成功！！！

![测试环境部署](./imgs/测试环境部署.png)

### 5.线上环境部署
线上环境部署采用的时`prod`的配置
```
deploy prod
```
部署流程和测试环境相同：

![线上环境部署](./imgs/线上环境部署.png)

感谢大家支持，欢迎star，O(∩_∩)O。
