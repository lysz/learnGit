﻿## 前言

* 相信大家在使用git进行团队开发的过程中，总会出现一些情况下需要去合并分支的操作，我也会经常出现这种情况，因为毕竟开发跟需求总是会有不同步的时候，所以难以在一条分支上解决很多问题，这时我们就需要进行新建分支进行测试性的开发，最后确定需求的时候再合并到主干上提交到生产环境！

* 使用git进行合并分支说难也不难，因为就使用一下那几个命令而已！但是不小心操作总会有一些难以预料的问题出现，所以这篇文档就介绍一下怎么用git进行合并分支操作！

* 最后说一下，这边文档是基于[这篇英语文档](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)然后集合我自己的理解和描述来通过小小的实际案例编写的，所以有些表达有误的地方建议你阅读原文！

## 开始

假如我们现在有个git仓库，我们现在工作在master分支上，我们加了一个文件index.html，内容如下：

```html
<!DOCTYPE html>
<html>
<head>
	<title>git branch merging demo</title>
</head>
<body>

</body>
</html>
```

然后我们新建一个分支，然后在index.html进行一些测试性的修改，命令如下：

```bash
   git checkout -b issue53
```

这条命令的结果在当前master分支的基础上新建一个分支issue53然后切换到issue53分支，此时issue53和master指针都指向同一个内容，如图所示：

![](../../images/13_1.png)

假设对index.html改动如下：

```html
	<!DOCTYPE html>
	<html>
	<head>
		<!--issue modifie-->
		<meta charset="utf-8"/>
		<title>git branch merging demo</title>
	</head>
	<body>

	</body>
	</html>
```

ok当我们做这样的改动之后，现在假设项目经理说我们的index.html有点问题急需修改，所以我们需要回到master分支进行开发，但是我们的issue53怎么办呢？因为这上面的功能是测试性的开发，还不确定能否合并到master上，所以我只能单独提交issue53分支，然后回到master分支，命令如下：

```bash
	git commit -a -m 'initial issue53 branch'
	git checkout master
```

ok，我们现在返回到master分支，再来查看各个分支指针指向情况，如图所示：

![](../../images/13_2.png)

因为此时我们在master分支上发现了bug，一般情况下我们都是在master分支的基础上新建一个修复bug的分支，等bug确认修复好之后再合并到master分支上，于是，我们新建一个分支hotfix，命令如下：

```bash
	git checkout -b hotfix
```

此时，对html改动如下：

```html
	<!DOCTYPE html>
	<!--hotfix modifie-->
	<html lang="Zh-cn">
	<head>
		<title>git branch merging demo</title>
	</head>
	<body>

	</body>
	</html>
```

然后我们提交到仓库，命令如下：

```bash
	git commit -a -m 'bug fixed'
```

到这个时候，我们再来看下各个分支指针指向情况：

![](../../images/13_3.png)

如何我们这个时候，可以确定我们所作的修复是正确的，那么就需要把hotfix分支上的修改合并到master分支上，
命令如下：

```bash
	git checkout master
	git merge hotfix
```

可以看到控制台结果如下：

![](../../images/13_4.png)

这里我们看到一个短语Fast-forward，什么情况下会出现这个短语呢？加入我们处理的两个的分支：其中一个分支可以在另外一个分支的历史版本中找到，那么就会出现Fast-forward！说白了就是其中一个分支是另外一个分支的子分支！看下原文给出的解释：

![](../../images/13_5.png)

所以在这种情况下合并，git只是会简单的改变一下master分支指针的指向而已，把它指向两个分支中最新的版本。此时各个分支指针的指向如下：

![](../../images/13_6.png)

到这一步，我们就可以删除hotfix分支了，因为我们已经不需要hotfix分支了，命令如下：

```bash
	 git branch -d hotfix
```

当我们的bug修复完成之后，我们就需要回到刚才中断开发的分支上，也就是issue53分支上，命令如下：

```bash
	git checkout issue53
```

我们在issue53分支上对index.html改动如下：

```html
<!DOCTYPE html>
<html>
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>

</body>
</html>
```

我们再来看一下分支指针指向情况：

![](../../images/13_7.png)

好，这个时候，假设项目经理决定在issue53分支上进行的测试性开发可以发布到正式版本上，所以我们就需要合并issue53分支到master分支上！命令如下：

```bash
	git checkout master
	git merge issue53
```

ok，我们看一下终端输出情况：

![](../../images/13_8.png)

我们可以看到已经没有Fast-forward短语了，那么git是怎么进行合并的呢？我们 先看一下原文是怎么进行叙述的：


![](../../images/13_9.png)

用一句话来解释就是：git进行了三方面的合并，一方面分别找到两个需要合并分支的的祖先，也就是说它找到它们相同的部分，然后再分别标记两个不同的分支，最后把这两个不同的部分进行合并，最后生成一个分支，也就是我们最终合并得到的master分支，此时我们再来看一下分支指针指向情况：

![](../../images/13_10.png)

我们可以看到当前master分支的父版本有两个分支，因为它是来自于两个部分！

到这一步你是不是以为合并分支是不是很简单呢！当然不是了，如果我们在两个子分支上更改了同一部分内容，那么我们进行合并的时候就会出现冲突，为了演示这个问题，我们现在在master分支的基础上建立两个分支dev1和dev2并同时修改同一部分内容，看下会出现什么情况。命令如下：

```bash
	git checkout -b dev1
	git checkout master
	git checkout -b dev2
```

在dev2分支上改动如下：

```html
<!DOCTYPE html>
<!--hotfix modifie-->
<html lang="Zh-cn">
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>
<div>dev2</div>
</body>
</html>
```

然后切换到dev1分支，命令如下：

```bash
  git checkout dev1
```

改动如下：

```html
<!DOCTYPE html>
<!--hotfix modifie-->
<html lang="Zh-cn">
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>
<div>dev1</div>
</body>
</html>
```
我们此时在dev1和dev2分支上更改了master分支的同一部分内容，我们先合并dev1分支到master，再合并dev2分支到master分支看会出现什么提示。命令如下：

```bash
	git checkout master
	git merge dev1
	git merge dev2
```

终端截图如下：

![](../../images/13_11.png)

我们可以看见有冲突了，并显示冲突就是index.html，于是我们打开index.html发现有这么一行数据，截图如下：

![](../../images/13_12.png)

这里显示了我们在合并的时候存在冲突的地方，我们根据需要更改成自己需要的内容然后再提交即可！这个时候可以

```bash
	git status
```
查看相关状态！

当我们把冲突解决完成之后，就可以使用如下命令成功合并了：

```bash
	git add .
	git commit -m 'submit'
```
最后我们再查看一下结果：

![](../../images/13_13.png)

### 内容补充

* 昨天因为有点事情先撤了，所以有部分该写的内容没来得及加上来，今天决定加上来。接着上文所写的内容，你肯定会想问：git什么时候合并两个分支的时候会出现冲突呢？以我的经验来看，如果你在合并分支的时候满足以下两个条件，肯定会出现冲突：1、合并的两个分支，并不存在所属关系，也就是说a分支并不是b分支的“子”分支，说白了，其中一个分支指向的内容并不是另外一个分支历史版本中的一个分支，如下图，master分支指向的是hotfix或issue53分支的上一次提交，所以这里我们可以理解成master分支是hotfix或issue53的“子”分支，因为它指向内容都可以在hotfix或issue53的历史提交版本中找到；2、你在合并的两个分支上改了同一部分内容。如何满足了中两个条件，那么合并分支的时候必定会产生冲突！

![](../../images/13_3.png)

* 其实从这点我们就可以知道，我们在平时开发的过程中，如果有新功能或者bug修复，我们不应该在主分支上修改，而是应该新建一个分支，等功能完善之后或者bug修复之后再合并过去，这样就不会出现冲突了，因为被合并的那个分支始终是“子”分支，还能保证主分支的干净稳定！


