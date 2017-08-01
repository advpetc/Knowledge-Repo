# 机器学习部分

这部分主要是我自己琢磨的比较多，在数据方面做了一些数据清理的事情。因为是NLP公司，所以在处理分词上我还做了一些事情，后来居然发现了nltk的一个bug，现在已经提交了[issue](https://github.com/nltk/nltk_data/issues/85)，有兴趣的旁友可以看一下。在清理这部分公司用了自己的运行环境，主要使用一些自定义的schema来给不同类型的数据做测试。举一个例子：

```python
class General_Tokenizer(Rule_File_Shell):
    def __init__(self, **kwargs):  # delimiter should be singlself.exe, e char
        super(self.__class__, self).__init__()
        self.set_desc('File Shell cmd: general tokenizer (same as in Moses)', self)
        self.lang = 'en'
        if 'lang' in kwargs: self.lang = kwargs['lang']
        self.exe = os.path.join(os.path.dirname(os.path.abspath(sys.argv[0])), 'tokenizer', 'tokenizer.perl')

    def run(self, files):
        file = files[0]
        self.file_exist(file)
        cmd = r"chmod 755 %s; %s -l %s < %s > %s" % (self.exe, self.exe, self.lang, file, self.output)
        self.execute_cmd(cmd)
        return [self.output]
```

这里继承了运行的Rule_File_Shell，的对象，在这里直接跑就可以了。同时在tokenize的时候调用了一个perl的脚本来进行，脚本可以在[这里](https://github.com/moses-smt/mosesdecoder/blob/master/scripts/tokenizer/tokenizer.perl)看到。这部分的操作实际上十分简单，但是一个一定要有一个好的架构才可以把复杂的事情简单化。

最后讲一下ML的部分。我在初步学习了一下Tensorflow和Stanford231的课之后整理了一些资源和笔记，我认为ML不是一两句话可以说清楚的，跟何况自己也是刚刚入门，就先不发表自己的拙见。
* Computer Vision学习的路线可以参照Stanford231的课程，从环境setup开始一直到后面的KNN, Softmax, Linear Regression等等。
* 工具的使用也很重要，我建议使用google的Tensorflow来把自己的模型形象成一个可观的图，使用[TensorBoard](https://www.tensorflow.org/get_started/summaries_and_tensorboard)会十分有帮助。
* NLTK部分可以从[感知器](https://zybuluo.com/hanbingtao/note/433855)开始，然后学习[线性单元和梯度下降](https://zybuluo.com/hanbingtao/note/448086)，然后学习[神经网络和反向传播算法](https://zybuluo.com/hanbingtao/note/476663)，然后学习[卷积神经网络](https://zybuluo.com/hanbingtao/note/485480)，这四个其实是一个系列，讲的很清楚。还有一些神经系统相关，在这里也分享一下：
    * [RUN](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
    * [LSTM](http://www.jianshu.com/p/9dc9f41f0b29)
    * [GRU](https://arxiv.org/pdf/1406.1078v3.pdf)

总之在我看来要想做好ML首先要有足够的数据，然后配合一个强有力的cpu和gpu加速就可以做成想要的东西，这部分东西我还有很多要学习的地方。
