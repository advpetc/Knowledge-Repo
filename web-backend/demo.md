## 网络后端开发

把js放到前端去说的一个原因是我用的Django框架，是一个很容易上手的python框架。后端我主要用python完成，所以只是在迫不得已的情况下才会在前端加一些js的代码。在之前的post里也简单介绍过Django框架，现在再次感受到它的强大，举个例子：

如果你想在本地跑你的app：

```shell
$ ./manage.py runserver
```

默认在127.0.0.1:8000，假如想在同个局域网给朋友showoff，只要在runserver后添加你的ip地址和对应的端口就可以了：

```shell
$ ./manage.py runserver YOUR_IP_ADDRESS:PORT
```

假如你要更改自己的model，只要在改完之后使用如下指令：

```shell
$ ./manage.py migrate
$ ./manage.py makemigrations
```
不再需要一个一个检查model和之前有什么区别，因为Django已经帮你比较好了，你只要按照流程更改就可以了，如果运气好直接migrate就不会用问题了。

Django的setting.py文件相当于你的config文件，尤其的重要，部署的时候添加机器的ip到ALLOWED_DOMAIN，再设置好数据库就可以了在server上跑了（当然你要先把环境用docker设好）。Django支持的数据库真的是一大把，小学生级别的设置，很多时候填用户名和密码就可以了，剩下Django都帮你设置好了。不过在迁移数据库的时候（尤其从sqlite到postgresql）Django是把文件dump出来然后再写入，所以难免由很多migrations的问题要解决，关于迁移数据库做了一个简单的总结：

```shell
$ python manage.py migrate --database=postgresql --run-syncdb
//python manage.py dumpdata --all --indent=4 -e auth.user -e admin.logentry -e sessions -e=contenttypes  > imtx.json
//python manage.py dumpdata > dump.json
$ python manage.py loaddata imtx.json --database=postgresql
```

里面comment掉的是dump的两个方法，第一个是去除了一些不必要的auth，session的行，第二个是直接dump，我觉得既没有意义也总是出现migrations conflict的问题，第一个就当作一个不错的snipp记录下来吧。

用python写后端确实轻松一些，但是还是有很多要注意的情况，比如处理url等，这些在Django的官方教程中其实都可以看到，我在这里就不重复了。

**一些资源分享**

* [Django](djangoproject.com)，官方给了一个很详细的教程，做的是一个投票系统，MVC框架在看完这个教程之后就基本了解了。
* [Node.js](https://nodejs.org/en/)，这次实习我自己没有用node，不过看到别人用的时候感觉很酷，尤其是移步进程的部分非常值得学习，可以提升网页速度，这里稍微提一下debug的工具[node-inspector](https://github.com/node-inspector/node-inspector)，用`$ npm install -g node-inspector`就安装好了。
* 关于数据库我整理了一个从备份postgres数据库的脚本，在[Gist](https://gist.github.com/advpetc/9ec48862fa2f64ed5505cb39c47a56ec)上分享。里面需要了解以下CronTab的知识。
* [Postgres](https://www.postgresql.org/)，这个数据库由有很多支持的第三方客户端，我比较喜欢的是在Mac上的[Posgres.app](http://postgresapp.com/)，一键式的启动，不过在具体操作的时候还是用的JetBrain的[DataGrip](https://www.jetbrains.com/datagrip/)，这里顺便提一下JetBrain免费提供学生使用，所以如果是学生强推直接升级的professional版，我用的PyCharm在升级之后发现可以直接调用数据库，非常酸爽。
