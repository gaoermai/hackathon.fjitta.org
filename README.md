# 使用Pelican和Markdown的静态站点

## 安装方法

下面实践环境为Mac，打开终端执行：

```bash
$ sudo easy_install pip
$ sudo pip install virtualenv
$ virtualenv ~/virtualenvs/pelican
$ cd ~/virtualenvs/pelican
$ source bin/activate
(pelican) $ pip install pelican
(pelican) $ pip install Markdown
(pelican) $ pip install typogrify
```

至此，Pelican的基本环境已经安装完成。

## 使用帮助

### 初始化

参考[Pelican官方帮助](http://docs.getpelican.com/en/stable/index.html)，执行下面命令即可生成基本的站点。

```bash
$ mkdir -p ~/projects/yoursite
$ cd ~/projects/yoursite
$ pelican-quickstart
```

使用```pelican-quickstart```命令，可以快速生成站点所需的文件和目录。

### 本地测试

使用命令：

```bash
$ pelican # 生成静态页面
$ cd output
$ python -m SimpleHTTPServer
```

可以在浏览器中访问```http://127.0.0.1:8000/```看到新建的站点。

## 发布到生产环境

### 发布到GitHub

使用GitHub来部署静态站点，那么使用命令：

```bash
$ fab gh_pages
```

上面命令将自动执行以下步骤：

- 重新生成静态页面；
- 将output文件夹中的静态页面导入分支```gh_pages```；
- git pull到远端资源库。

使用时，如果需要设置自定义域名，需要在站点根目录下增加CNAME文件，内容为自定义的域名。利用Pelican添加静态资源的方法来设置CNAME：

步骤一：在```pelicanconf.py```增加配置项：

```
STATIC_PATHS = {'CNAME'}
```

步骤二：在```content```下增加文件```CNAME```，内容为自定义的域名。

按照上面步骤，在生成静态页面时会自动把CNAME文件放入到站点根目录下，GitHub会通过识别该文件的内容对域名进行自定义。

