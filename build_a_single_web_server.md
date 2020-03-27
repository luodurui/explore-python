# 任务目标

从 0 开始使用 Python3 做一个 Web 服务器，当在浏览器中访问 http://localhost:8080 的时候可以在页面上看到 CODING！

# 本地环境

![本地环境](/Users/steven/Library/Application Support/typora-user-images/image-20200327164258380.png)

# 任务准备

## 环境检查

由于 Python 2 与 Python 3 之间差异较大，而 Mac 自带 Python 2.xx 版本。为了避免由于 Python 版本导致的问题，需要在开始前检本地的 Python 版本，具体步骤如下：

![查看 Python 版本](/Users/steven/Library/Application Support/typora-user-images/image-20200326165358851.png)

可看到 Python 版本为 2.7.16。此处我们决定安装 Python 3 来完成此次任务。

## 环境准备



### 1. 检查是否安装了 Python 3

```bash
python3
```



![检查 Python3](/Users/steven/Library/Application Support/typora-user-images/image-20200326170311408.png)

系统提示需要安装命令行开发者工具，点击` 安装 `

![安装命令行开发者工具](/Users/steven/Library/Application Support/typora-user-images/image-20200326170435487.png)

安装完成后再度在终端中输入` python3 `，系统提示已安装了版本为 3.7.3 的 Python。

###  2. 其他方法

下载安装 Python 也可通过 Mac 的包管理工具 [homebrew](https://brew.sh/index_zh-cn.html) 实现，可参考 [教程](https://www.cnblogs.com/meng1314-shuai/p/9031686.html) 进行下载安装。

# 任务思路

### 1. 搜索可用的框架

使用框架进行开发能够减少重复开发量，精简代码。使用关键字 “Python”，“web”及“framework”搜索可用的框架。

搜索到几种比较常见的框架： [Django](https://www.djangoproject.com/) 、 [Flask](https://dormousehole.readthedocs.io/en/latest/) 、 [Tornado](https://www.tornadoweb.org/en/stable/) 等等。

### 2. 框架选型

由于本任务的目标是让初学者快速搭建一个简单的 Web 应用，体验 Python 开发的感觉，故选用轻量的 Flask 来实现。

### 3. 通过 Flask 的文档快速开始编程。

# 实施步骤

### 1. 创建虚拟环境

建议在开发环境和生产环境下都是用虚拟环境来管理项目的依赖。随着你的 Python 项目越来越多，而项目之间往往需要不同的库，那么通过独立的虚拟环境进行开发就成了一个不错的选择。

Python 3 内置了用于创建虚拟环境的 [venv](https://docs.python.org/3/library/venv.html#module-venv) 模块，我们需要借助该模块创建虚拟环境。

创建一个项目文件夹 → 进入该文件夹 → 创建虚拟环境：

```bash
mkdir python_web
cd python_web
python3 -m venv venv
```

创建完成后，项目文件夹中会有一个 ` venv ` 文件夹：

![创建虚拟环境](/Users/steven/Library/Application Support/typora-user-images/image-20200326174620117.png)

### 2. 激活虚拟环境

正式工作前，激活相应的虚拟环境：

```bash
. venv/bin/activate
```

### 3. 安装 Flask

在已激活的虚拟环境中可以使用如下命令安装 Flask：

```bash
pip install Flask
```

![安装 Flask 报错](/Users/steven/Library/Application Support/typora-user-images/image-20200327102405141.png)

报错中提示 ` HTTPSConnectionPool: Read timed out ` ，应该是连接超时导致的下载失败。但超时的原因还看不出来。可能是 pip install 的超时时间过短、网络拥堵、wall等，导致超时时间内无法下载到任何数据。解决方法有两种：1.增加超时时间（不推荐）；2.更换源。

在终端中输入 ` pip --help ` 查看到默认超时时间为15s，可使用如下命令修改默认超时时间（不推荐）：

```bash
pip --default-timeout=600 install
```

![调整超时时间](/Users/steven/Library/Application Support/typora-user-images/image-20200327171632096.png)

另外，可通过更换源的方式改善下载情况。运行以下命令以使用腾讯云 pypi 软件源：

```bash
pip install -i https://mirrors.cloud.tencent.com/pypi/simple Flask
```

![更换源后下载](/Users/steven/Library/Application Support/typora-user-images/image-20200327125645103.png)

### 4. 开始编码

终端中使用 vim 创建一个名为 ` web_coding.py ` 的文件：

```
vim web_coding.py
```

源码如下：

```bash
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
		return 'CODING!'
```

### 5. 运行程序

导出 ` FLASH_APP ` 的环境变量，然后使用 flask 运行这个应用：

```
expert FLASK_APP=web_coding.py
flask run
```

![flask run](/Users/steven/Library/Application Support/typora-user-images/image-20200327130550410.png)

程序已经开始运行，浏览器访问：

![浏览器访问](/Users/steven/Library/Application Support/typora-user-images/image-20200327130703347.png)

### 6. 修改端口

而任务要求程序运行在 local:8080，我们则需要指定程序运行的端口：

```bash
^C%    //先把进程停掉
flask run -p 8080
```

![修改运行端口](/Users/steven/Library/Application Support/typora-user-images/image-20200327130935142.png)

浏览器中访问：

![更新端口后访问](/Users/steven/Library/Application Support/typora-user-images/image-20200327131208882.png)

反思

由于国内网络环境的复杂，下载包时常会导致超时。这时选择合适的源进行替换是个不错的方法。本次任务参考的源：

[腾讯软件源](http://mirrors.tencent.com/#/index)

[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)

