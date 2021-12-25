# odoo 深圳市耀影科技有限公司 https://www.yaoying.vip
Odoo 社区驱动直接transifex，中文人工校对翻译，汉语本地化项目。
**项目QQ群：52123458**
---------------------------------------

## 概述
本项目启动，提交PR后，会推送到transifex，您也可以到官方的TX项目直接更新。
下载本项目直接覆盖ODOO目录，即可更新.
项目分支名对应ODOO版本，仅针对社区版本


## 如何贡献 odoo 翻译
odoo 官方翻译主要通过 transifex.com ，由于 transifex 上的使用方便和审核效率问题，我们同时也建立了这个仓库，力争更快更精确的实现 odoo 中文化。

## odoo 翻译生效说明
此 repo 是人工合并，人工 push 到 tx
然后 odoo 官方定期同步 tx 上的翻译，一般是一周。故传递到 odoo社区版时，更新会有所延迟。

### 方法一：通过我们的 github 贡献翻译
仓库地址：https://github.com/yaoyingkeji/odoo
更新提交：使用 git PR(pull request)，参考 https://www.jianshu.com/p/d921828bf623
建议：在此 repo 上提 issue

### 方法二：通过 transifex.com
1. 注册登录
http://www.transifex.com 
2. 加入 odoo 中国团队
https://www.transifex.com/odoo/teams/
3. 参与 odoo 翻译
总览： https://www.transifex.com/odoo/public/
模块翻译： 找到对应版本并找到相关模块。点进去可以po下载与上传：
也可以在线进行翻译

## 获取最新 .po 文件，更新后发布至 transifex
### 1. deepin V20.3 安装 tx 客户端
#### 1.安装pyenv Python虚拟环境
```
#安装依赖
sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev git
#克隆pyenv
git clone https://github.com/pyenv/pyenv.git ~/.pyenv

#安装构建，也许失败，可以忽略它
cd ~/.pyenv && src/configure && make -C src

#设置SHELL环境变量
sed -Ei -e '/^([^#]|$)/ {a \
export PYENV_ROOT="$HOME/.pyenv"
a \
export PATH="$PYENV_ROOT/bin:$PATH"
a \
' -e ':a' -e '$!{n;ba};}' ~/.bashrc
echo 'eval "$(pyenv init --path)"' >>~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc

#退出SHELL
exec "$SHELL"

#安装Python环境
pyenv install 3.9.9  #安装Python3.9.9，同时会安装对用的pip3

# 克隆pyenv-virtualenv
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv

#添加到~/.bashrc 环境变量
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

#退出"$SHELL" 
exec "$SHELL" 

#创建虚拟空间基于Python环境3.9.9版本的虚拟空间名为“tx"
pyenv virtualenv 3.9.9 tx 

#添加自动激活虚拟空间
echo "tx" >> $HOME/.pyenv/versions/3.9.9/envs/tx/.python-version

#安装pip
sudo apt-get install python-pip

#安装transifex-client
sudo pip install transifex-client

#检查版本
tx --version

#激活tx虚拟环境。每次需要在哪个目录使用tx时候，需要先激活tx虚拟环境
pyenv activate tx
```

2. 获取最新 .po 文件

```
#取最新的 po，新建一个文件夹，初始化tx
tx init
#提示输入 transifex 的token 
#在用户设置中https://www.transifex.com/user/settings/api/ 生成一个token拷贝进来，然后关闭即可
#会自动在主目录下产生一个tx配置文件”.transifexrc “，详细参见TX官方文档
#当前文件夹下自动创建一个”.tx"目录，和“config” 配置文件

#获取中文本地化文件zh_CN
#把odoo 对应版本项目下的“.tx/config"拷贝道当前文件夹，执行如下命令
tx pull -l zh_CN

#推送最新翻译文件到transifex，参考 https://docs.transifex.com/transifex-github-integrations/github-tx-client
tx push -t

```