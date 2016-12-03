# OS X Odoo10 开发环境搭建

## 软件安装
### Homebrew
  ```
  # 安装
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  # 更新
  brew update
  ```
###  Python
  ```
  # 默认有安装python2.7，没卸载的话不用安装
  brew install python
  # 安装 pip
  sudo easy_install pip
  ```
###  PostgreSQL
  ```
  brew install postgres
  ```
### Git
  ```
  # 安装Xcode，自带git，或者
  brew install git
  ```

### Pycharm
  ```
  # 官网下载dmg文件安装
  # http://www.jetbrains.com/pycharm/
  ```

### 安装依赖
  ```
  # Pillow模块依赖
  brew install freetype jpeg libpng libtiff webp xz
  # odoo依赖，文件见附件
  pip install -r requirement.txt
  # 项目其他依赖
  pip install ipython, jpush
  # Node.js安装
  brew install node
  brew install npm
  npm install -g less less-plugin-clean-css

  ```
## 代码下载
  ```
  # 配置git
  git config --global user.name "your_name"
  git config --global user.email "your_email@runwise.cn"
  # 克隆代码
  git clone xxx
  ```
## 配置
### PostgreSQL
  ```
  # 自启动
  ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
  # 创建用户
  createuser user_name --createdb -P
  # 然后输入两次密码；createdb权限不能省。
  ```
### Odoo
  ```
  # 在项目根目录下新建 odoo.conf。
  # 主要配置db_user，db_password对应psql用户密码
  # 其他参数见附件odoo.conf。具体参数用法参考 Odoo Devement Cookbook
  ```

## 运行
  ```
  # terminal
  sudo chmod -R 777 project_name    # 修改项目权限
  cd project_name
  python setup.py install
  python setup/odoo -u upadte_module_name

  # pycharm
  # setup a configuration
  ```

## 问题
1. `Command psql not found`: 数据库配置错误
2. `Could not execute command lessc`：`virtualenv`惹的祸
