This is the contribute.md of our project. Great to have you here. Here are a few ways you can help make this project better!

## Team members

**Haoyang Chen**

**Zijian Hu**

## Learn & listen

This section includes ways to get started with your open source project. Include links to documentation and to different communication channels:

* Gitbook Website: [Website](advpetc.ml)

## Adding new features

This section includes advice on how to build new features for the project & what kind of process it includes.

* This is how we like people to add new features: creating pull request on develop branch, or fork this repo to your own.
* Here are some specifics on the coding style we prefer: all content are written by markdown.
* You should include the following tests: run on your local server and the styling meet previous content. no grammar or spelling mistakes.
* These are the updates we hope you make to the changelog:
    * New section(s) for OS
    * Add content for embedded-system.

### Instruction on how to set up local environments:

##### Requirements

Installing GitBook is easy and straightforward. Your system just needs to meet these two requirements:

* NodeJS (v4.0.0 and above is recommended)
* Windows, Linux, Unix, or Mac OS X

##### Install with NPM

The best way to install GitBook is via **NPM**. At the terminal prompt, simply run the following command to install GitBook:

```
$ npm install gitbook-cli -g
```

`gitbook-cli` is an utility to install and use multiple versions of GitBook on the same system. It will automatically install the required version of GitBook to build a book.

##### Create a book

GitBook can setup a boilerplate book:

```
$ gitbook init
```

If you wish to create the book into a new directory, you can do so by running `gitbook init ./directory`

Preview and serve your book using:

```
$ gitbook serve
```

Or build the static website using:

```
$ gitbook build
```

##### Install pre-releases

`gitbook-cli` makes it easy to download and install other versions of GitBook to test with your book:

```
$ gitbook fetch beta
```

Use `gitbook ls-remote` to list remote versions available for install.

##### Debugging

You can use the options `--log=debug` and `--debug` to get better error messages (with stack trace). For example:

```
$ gitbook build ./ --log=debug --debug
```


2. Then go to your cloned directory, enter command below:

```shell
$ npm install gitbook-cli -g
# serve
$ gitbook serve
```

Finally just go to localhost:4000(by default) to check your changes.



Don’t get discouraged! We estimate that the response time from the
maintainers is around: within 1 day

# Bug triage

This sections explains how bug triaging is done for your project. Help beginners by including examples to good bug reports and providing them questions they should look to answer.

* You can help us diagnose and fix existing bugs by asking and providing answers for the following:

  * Is the bug reproducible as explained?   
  * Is it reproducible in other environments (for instance, on different browsers or devices)?   
  * Are the steps to reproduce the bug clear? If not, can you describe how you might reproduce it?  
  * What tags should the bug have?  
  * Is this bug something you have run into? Would you appreciate it being looked into faster?  

* You can close fixed bugs by testing old tickets to see if they are still happening.

# Beta testing

This section explains if your project needs beta testing. Explain why early releases require heavy testing and how they can help with specially across browsers and on different hardware.

* For our project you can find the roadmap and features that require
testing from here:

# Your first bugfix
This section should help a person get started with their very first bug fix and thinking through the problem.

* If you have further questions, contact: [Email](mailto:chenhaoy@usc.edu)
