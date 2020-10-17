
### 1. 确认安装ruby

- brew是ruby开发的，需要确认ruby是否已安装，默认是已经安装的。
- 查看ruby版本及是否按照：ruby --version
- 安装成功查询安装路径：which ruby
- 安装ruby指令如下

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
### 2. 安装brew
-  确认安装ruby后，再选择安装brew，并复制以下内容粘贴至git指令内：
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
-  brew 是MacOS上的包管理工具，可以简化 macOS 和 Linux 操作系统上软件的安装,首先安装[Homebrew](https://brew.sh/)

`注意：需要翻墙，外网不好下载的情况下选择如下方法（可直接选择国内镜像）`

3. 使用国内镜像
```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

1. 以下是可查询指令

- 查看brew版本及是否存在：brew --version
- 安装成功查询安装路径：which brew

### 3. 安装yarn

1. 运行指令
- 安装指令：npm install -g yarn
- 检查版本及检查是否安装：yarn --version

`注意：使用git指令还需要下载node.js`