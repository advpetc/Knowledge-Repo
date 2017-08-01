## 网络前端开发

首先要说明的是前端不可能独立存在，如果没有后端提供数据处理是完全没有意义的。我做的是一个web app，目的是为了与人交互然后基于交互目的得到用户想看到的结果。前端在这个部分是直接面向用户的，所以很多时候并不是仅仅靠编程就可以，还要学会构建用户交互逻辑，这个部分更加重要。

**HTML, JS, jQuery**

前端主要的代码都是由这两部分构成的，html负责显示，js负责逻辑。比如要设计一个向上回到顶部的按钮：

```html
<a id="back-to-top" href="#" role="button">Top</a>
```

只用HTML是完全可以做到的，但是在用户看来这只是一个没有任何颜色，只有一行字Top的一个超链接，用户体验十分不好，于是我们添加这些：

```html
<a id="back-to-top" href="#" class="btn btn-primary btn-lg back-to-top pull-right" role="button" data-toggle="tooltip"
   data-placement="right"><span class="glyphicon glyphicon-chevron-up"></span></a>
```

这就变成了一个有颜色和字体的按钮，但是还是不够，我想让它在指定的位置出现而不是一直干扰用户的视线，于是我们就要给它添加一些逻辑：

```javascript
<script>
    $(document).ready(function () {
        $(window).scroll(function () {
            if ($(this).scrollTop() > 50) {
                $('#back-to-top').fadeIn();
            } else {
                $('#back-to-top').fadeOut();
            }


        });
        // scroll body to 0px on click
        $('#back-to-top').click(function () {
            $('#back-to-top').tooltip('hide');
            $('body,html').animate({
                scrollTop: 0
            }, 800);
            return false;
        });

        $('#back-to-top').tooltip('show');

    });

</script>
```

这里使用jQuery的原因由很多，其中就有它可以很好的调用一些函数例如*scroll*和*click*。在实际中我也更加倾向于使用jQuery，简单明了，填充了js本来没有的函数。这里干的事情就是在大于50px的时候显示这个按钮，反之消失，同时在点按的时候加了动画效果。

**一些资源分享**

* [Bootstrap](http://getbootstrap.com/)，现在已经出到第四个版本了，是很棒的基本前端控件的平台。可以本地现在源码，也可以直接用CDN，目前应该还没有被禁。
* [Bootsnipp](https://bootsnipp.com/)，这个是和Bootstrap一起使用的。假如在设计的时候没有好的想法可以从这里找别人写的snipp来模仿，非常有用。
* [jQuery](https://jquery.com/)，这个就不用多说了，我认为最有必要学习的一个前端的语言。下载支持源码也可以用CDN，官网上的google（疑似被墙）microsoft的都可以用。
* [Vue.js](https://vuejs.org/)，如果有时间的话可以用Vue代替js，也是个很好的选择。Vue自己是个js的框架，所以不要盲目使用，要结合自己的需求来做判断。Vue弱化了对js的要求，所以如果你对js不是很熟悉可以从Vue开始熟悉。
* [Material Design](https://getmdl.io/)，这个是Google强推的一个前端设计理念，现在开源了css和js，配合Bootstrap一起用可以提高自己的b格很多。同时也看到有人专门做了相辅相成的[MDB](https://mdbootstrap.com/)，如果懒得自己去设计可以参考这个，但是有部分控件是收费的。
