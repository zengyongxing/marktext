



# Package Mangement

在Node.js遵循模块化的设计：一个应用是一个Package。一个三方库也是一个Package。所有的内容都通过package.json描述，并可以上传到公共和私有的仓库中。

# 包结构

包可以压缩为zip或者tar.gz，但使用中都是目录形式。如下：

```
.
├── package.json						
├── bin							# 二进制文件的目录，用于全局安装
├── lib							# javascript代码
├── docs						# 文档
├── node_modules		# 安装后的三房库依赖
└── test						# 单元测试代码
```

# package.json

```
{
  "name": "test",				# 包名，需要发布的话，要在https://npmjs.org上唯一
  "version": "1.0.0",		# 版本号，形式为Major.Minior.Patch
  "description": "",
  "private": true,			# 不被发布到https://npmjs.org上
  "main": "index.js",		# 程序入口
  "scripts": {					# 脚本，可以通过npm run xxx 来执行的
    "test": "echo \"Error: no test specified\" && exit 1"
  },
    "dependencies": {		# 运行依赖，使用 npm install/yarn add 添加
  	"vue": "^2.5.2"			
	}，
	  "devDependencies": { # 开发依赖，使用npm install --save-dev/yarn add --dev 添加
	  "babel-core": "^6.22.1"
	},
	"engines": {					#  指定node.js版本
  "node": ">= 6.0.0",
  "npm": "1.0.0 || >=1.1.0 <1.2.0",	# 1.0.0 或者小于1.2.0大约1.1.0
  "yarn": "^0.13.0"
}
  "author": "user@email.com", # 在https://npmjs.org的用户名
  "license": "ISC"			# 许可证
}
```

# 依赖包的版本控制语法

在package.json中使用下面的语法控制可以更新的包的版本范围

`=`或者无符号: 仅接受指定的特定版本

`latest`: 使用可用的最新版本。 

`-`: 接受一定范围的版本。例如：`2.1.0 - 2.6.2`。

`~`: 接受补丁版本的修改。如果写入的是 `〜0.13.0`，则当运行 `npm update` 时，会更新到补丁版本：即 `0.13.1` 可以，但 `0.14.0` 不可以。

`^`: 只会执行不更改最左边非零数字的更新。 如果写入的是 `^0.13.0`，则当运行 `npm update` 时，可以更新到 `0.13.1`、`0.13.2` 等，但不能更新到 `0.14.0` 或更高版本。 如果写入的是 `^1.13.0`，则当运行 `npm update` 时，可以更新到 `1.13.1`、`1.14.0` 等，但不能更新到 `2.0.0` 或更高版本。

`>

``>=``

`<=`

`<`

`||`: 组合集合。例如 `< 2.1 || > 2.6`。

# 使用lock文件

开发过程中，或者三方库，使用package.json指定一个比较宽泛的范围。但是对于需要全局安装的应用，或者团队开发的应用，需要确定具体的版本。所以package-lock.json文件记录了具体使用的版本。

# NPM 仓库

默认的仓库是`registry.npmjs.com`，用户也可以自建仓库。或者使用国内镜像。

指定仓库的方式有两种，以修改为taobao的镜像为例：

1. 命令行

   `$npm configsetregistrty http://registry.npm.taobao.org`

2. 直接修改`~/.npmrc``

   `registry = http://registry.npm.taobao.org`

# NPM 用法

创建一个包

- `npm -v` 显示npm包管理器的当前版本
- `npm init` 向导方式创建package.json

全局包的操作

- `npm list -g` 列出系统中全局安装的所有模块
- `npm install -g module_name` 全局方式安装一个模块
- `npm remove -g module_name` 从系统的全局安装中移除已安装的模块
- `npm update -g module_name` 更新指定的全局安装模块的版本

项目包的操作

- `npm list` 列出项目中已安装的所有模块
- `npm install module_name –-save` 在项目中安装一个模块，并把此模块添加到项目配置文件`package.json`中，作为项目依赖
- `npm install module_name –-save-dev` 在项目中安装一个模块，并把此模块添加到项目配置文件`package.json`中，作为项目开发依赖（devDependency）
- `npm remove module_name –save` 从项目中移除已安装的模块，并从配置依赖中移除依赖关系
- `npm remove module_name –save-dev` 从项目中移除已安装的模块，并从配置依赖中移除开发依赖（`devDependency`）关系
- `npm update module_name` 更新指定的已安装模块的版本
- `npm install module_name` 在项目中安装一个模块
- `npm remove module_name` 从项目中移除已安装的模块

开源仓库管理

- `npm adduser username` 在npmjs.org创建一个账户
- `npm whoami` 显示你在npmjs.org上的账户详细信息
- `npm publish` 发布自己开发的模块到npmjs.org，要发布模块必须先有账户

# Yarn和NPM命令对比

|                NPM                 |           YARN            |                             說明                             |
| :--------------------------------: | :-----------------------: | :----------------------------------------------------------: |
|            npm install             |       yarn install        | 安裝 package.json中的依賴，<br>如果存在package.json.lock，优先使用 |
|    npm install –save [package]     |    yarn add [paakage]     |        安装包，并添加到package.json的dependencies字段        |
|  npm install –save-dev [package]   |  yarn add [paakage] –dev  |      安装包，并添加到package.json的devDependencies字段       |
|   npm uninstall –save [package]    |   yarn remove [package]   |                    移除dependencies某套件                    |
| npm uninstall –save-dev [package]  |   yarn remove [package]   |                  移除devDependencies某套件                   |
| rm -rf node_modules && npm install |       yarn upgrade        |                       更新node_modules                       |
|   npm install –global [package]    | yarn global add [package] |                     安裝全局可以执行的包                     |
|       npm install [package]        |           (N/A)           |                    Yarn不支援直接安裝套件                    |
|      npm uninstall [package]       |           (N/A)           |                 Yarn不支援直接安裝與移除套件                 |

