This is the knowledge base shared by known people. If you find this useful, please star us on [Github](https://github.com/advpetc/Knowledge-Repo)

## Instruction for how to contribute

**Set up**

This easiest and recommended way to contribute is by forking this repo to your own space. However, if you want to have long term contributions please contact with [me](chenhaoy@usc.edu) for adding you to collaborators list.

In theory, you won't be required to serve Gitbook on your own computer, but if you want to check your own work instantly, please follow the steps below:

1. First make sure you have `npm` and `node` installed by checking `npm -v`, if it's not being installed, please do this:

```shell
# first install Homebrew
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# install node
$ brew install node
# check installation
$ node -v
v8.1.2
$ npm -v
5.3.0
```

2. Then go to your cloned directory, enter command below:

```shell
$ npm install gitbook-cli -g
# serve
$ gitbook serve
```

3. Finally just go to localhost:4000(by default) to check your changes.

**Pull Request Rules**

Please do not push to master branch directly, every time you want to make contributions please make pull request, or the main branch will be all in mess.
