# Git 学习笔记

## 基本配置
    
### 目的

* 配置git，准备工作。

### 设置名字和邮箱

在使用git之前，需要先做一些配置。通过运行下面的命令，把你的名字和邮箱告诉git。

执行：

    git config --global user.name "AlexBai1991"
    git config --global user.email "baijinguo1991@163.com

### 设置换行符参数

对于Unix/Mac用户：

执行：

    git config --global core.autocrlf input
    git config --global core.safecrlf true

对于Windows用户：

执行：

    git config --global core.autocrlf true
    git config --global core.safecrlf true

## 创建一个本地项目

### 目的

* 学习如何从头创建一个git库。

### 创建一个"Hello Git"程序

首先我们需要在本地创建一个名叫"helloGit"的目录，然后添加一个名叫"helloGit.js"的文件。

    mkdir helloGit
    cd helloGit
    vim helloGit.js

"helloGit.js"添加内容如下:

    console.log("Hello Git!");

### 创建git库

现在我们有了一个包含"helloGit.js"文件的目录"helloGit"，用"git init"命令把这个目录初始化为git库。

    git init

### 将文件添加到git库

在上一步，我们已经成功的将"helloGit"目录初始化为库，现在用"git add"和"git commit"命令将"helloGit.js"文件添加到git库。

    git add helloGit.js
    git commit -m "添加helloGit.js新文件"

## 检查git库的状态

### 目的

* 学习如何检查git库的状态。

### 检查库状态

在"helloGit"git库中，可以使用"git status"命令查看该git库的状态。

    git status

输出：

    On branch master

    Initial commit

    Untracked files:
     (use "git add <file>..." to include in what will be committed)

       helloGit.js

    nothing added to commit but untracked files present (use "git add" to track)
    
这个命令报告git库里有未被跟踪的问价，请用"git add"命令添加它。后续将持续用"git status"命令来监控工作目录和git库之间的状态。

## 跟踪对文件的改动

### 目的

* 学习如何监控工作目录的状态。

### 更改helloGit.js文件

此时我们更改"helloGit.js"文件，在第二行添加如下内容：

    1. console.log("Hello Git!");
    2. console.log("Git is awsome!");

运行"git status"命令，输出：

    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   helloGit.js

    no changes added to commit (use "git add" and/or "git commit -a")

这里，我们发现"helloGit.js"文件被改动了，但是git还没有接受这些改动。此时我们可以选择通过"git add"命令把这些改动加入到git库中，也可以选择通过"git checkout"命令放弃这些改动。

### 加入这些改动

现在我们通过"git add"命令将上次我们的改动加入到git库中。

执行：

    git add helloGit.js
    git status

输出：

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        modified:   helloGit.js
    
直到现在，我们发现这些改动已经被加入到git库中，但是还没有被持久化的提交到git库中，还有待提交。此外，我们还可以通过"git reset"命令来取消对这些改动的跟踪。

### 提交这些改动

现在我们通过"git commit"命令提交对"helloGit.js"的改动。

执行：

    git commit -m "第一次修改helloGit.js文件"
    git status

输出：

    On branch master
    nothing to commit, working directory clean

现在，我们发现git库中是clean状态的，上次的提交已经生效。

## 改变，而不仅仅是文件

### 目的

* 学习git是根据改变在工作，而不是文件。

大部分源码控制系统都是根据文件在工作。如果你把一个文件加入到源码控制系统后，系统将跟踪这个时刻后文件的所有改动。

比起文件本身，git更关注的时改动而不是文件。当你执行"git add file"，你并不是让git把文件加入到库中，而是让git记录当前状态的文件，以便之后的提交。

### 第一次修改"helloGit.js文件"

这次我们修改"helloGit.js"文件，在第三行加入：

    1. console.log("Hello Git!");
    2. console.log("Git is awsome!");
    3. console.log("Github is good!");

接着，加入这次改动：

    git add helloGit.js

### 第二次修改"helloGit.js文件"

第二次修改该文件，在第四行中加入:

    1. console.log("Hello Git!");
    2. console.log("Git is awsome!");
    3. console.log("Github is good!");
    4. console.log("Gitlab is also good!");

现在，我们来查看此时git库的状态：

    git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        modified:   helloGit.js

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   helloGit.js


我们发现，第一次的修改处于有待提交git库状态，第二次的提交处于有待加入git库状态。现在，我们终于明白，git是跟踪的你的每一次的改动，而非文件！

## 查看提交历史

### 目的

* 学习如何查看git库的提交历史记录。

### 查看单行提交历史记录

我们可以通过很多参数精确控制"git log"命令的显示方式。

执行：

    git log --pretty=oneline

输出：

    dfcd1da9ff6b0328a97dc54f3330afe92404af85 第三次修改helloGit.js文件
    15dde970f6c652eadb112afd56720bb1e20fef8b 第二次修改helloGit.js文件
    b703c22187981cf9753cbfbeca6d1420beca6ee2 第一次修改helloGit.js文件
    f546278f9a7e9fd11fa3111b644abbf6921833cb 添加helloGit.js文件

### "git log"命令参数

有很多的选项可以指定哪些信息项显示在log里。

    1. git log --pretty=oneline --max-count=2
    2. git log --pretty=oneline --since='5 minutes ago'
    3. git log --pretty=oneline --until='5 minutes ago'
    4. git log --pretty=oneline --author=<your name>
    5. git log --pretty=oneline --all

输入：

    git log --all --pretty=format:"%h %cd %s (%an)" --since='7 days ago'

输出：

    dfcd1da Sun Jun 21 19:23:38 2015 +0800 第三次修改helloGit.js文件 (AlexBai1991)
    15dde97 Sun Jun 21 19:22:52 2015 +0800 第二次修改helloGit.js文件 (AlexBai1991)
    b703c22 Sun Jun 21 19:05:57 2015 +0800 第一次修改helloGit.js文件 (AlexBai1991)
    f546278 Sun Jun 21 18:48:45 2015 +0800 添加helloGit.js文件 (AlexBai1991)

输入：

    git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

输出：

    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (HEAD, master) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

说明：

    --pretty="..." 定义了输出格式。
    %h 代表提交的精简hash码
    %d 这个提交的一些修饰信息（比如，分支顶或者tag）
    %ad 作者提交的日期
    %s 提交时的注释
    %an 提交人的名字
    --graph 让git用字符图的方式显示提交树
    --date=short 显示简短的日期格式

## 设置常用git命令别名

### 目的

* 设置更容易记忆的git命令别名，提高git效率。

### 基本别名设置

"git status"， "git add"， "git commit"，和"git checkout"这些命令太常用了，缩写一下会很有帮助。

把下面的内容加到你$HOME目录下的.gitconfig文件。

    vim ~/.gitconfig
    [alias]
    co = checkout
    ci = commit
    st = status
    br = branch
    hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
    type = cat-file -t
    dump = cat-file -p

## 返回旧版本

### 目的

* 学习如何将之前的快照签入到工作目录。

### 退回指定旧版本

其实很容易就可以回到过去。命令checkout可以把库里任意时刻的快照拷贝到工作目录。

首先通过"git hist"命令查看此时git库的状态。

    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (HEAD, master) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

然后通过"git checkout hash"命令退回到指定旧版本。

    git checkout f546278
    Note: checking out 'f546278'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b new_branch_name

    HEAD is now at f546278... 添加helloGit.js文件

### 返回主分支最新版本

通过"git checkout"命令可以回到过去，那么当然也可以回到将来。

输入"git checkout master"命令，即可以返回到分支最新版本。

    git checkout master
    Previous HEAD position was 15dde97... 第二次修改helloGit.js文件
    Switched to branch 'master'

"master"是默认分支的名字。用名字签出一个分支，将会得到这个分支的最新版本。

## 给版本打标签

### 目的

* 学习如何提交一个命名标签，以便今后可以用标签来引用某个版本。

### 给当前master版本打标签

    git tag v1

给当前master分支打上"v1"的标签，之后就可以通过"v1"引用该版本了。

### 给之前版本打标签

让我们给当前版本之前的一个版本打上v1-beta的标签。首先我们需要签出上一个版本，除了去查找hash值，我们还可以使用"^"符号来表示v1的父版本。

    git checkout v1^
    Note: checking out 'v1^'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b new_branch_name

    HEAD is now at 15dde97... 第二次修改helloGit.js文件

现在我们给v1^版本打上标签。

    git tab v1-beta

### 通过标签来回切换版本

    git checkout v1 
    git checkout v1-beta

    git hist
    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (HEAD, tag: v1, master) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 (tag: v1-beta) [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

## 撤销已经提交的修改

### 目的

* 学习如何撤销一次已经提交到git库的修改。

### 撤销错误修改的版本

现在我修改"helloGit.js"文件，并加入了如下的错误信息：

    vim helloGit.js
    1. console.log("Hello Git!");
    2. console.log("Git is awsome!");
    3. console.log("Github is good!");
    4. console.log("Gitlab is also good!");
    5. add some wrong info.

然后加入到git库并提交到git库：

    git add helloGit.js
    git commit -m "错误修改helloGit.js文件"

现在该如何撤销这次错误的修改呢？

具体如下：

    git revert HEAD
    // 这是提交一个修改，这个修改移除了刚刚已经提交的错误修改

    * 5ec7dd9 2015-06-21 | Revert "错误修改helloGit.js文件" (HEAD, master) [AlexBai1991]
    * 3dfc1b8 2015-06-21 | 错误修改helloGit.js文件 [AlexBai1991]
    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (tag: v1) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 (tag: v1-beta) [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

现在我们的版本又回到了错误修改之前的版本，但是查看log历史记录，发现错误修改的提交历史仍然存在log历史中。

### 从分支中彻底删除错误修改版本记录

有时我们提交之后立刻意识到一些错误。有个"后悔"命令可以让这次错误的提交看起来完全没发生该多好。这个"后悔"命令甚至不会让这次错误提交显示在log历史记录里，就像完全没有这回事一样。

除了上面提到的"git revert"命令可以撤销错误修改的版本之外，还有"git reset命令"也能实现撤销错误修改。

具体操作：

    git tag wrongmodify

    git reset --hard hash(或者tag标签)
    // --hard 表示将当前工作目录更新到和新分支的最新版本一致

    git hist --all
    * 247c980 2015-06-21 | 错误修改啦 (tag: wrongmodify) [AlexBai1991]
    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (HEAD, tag: v1, master) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 (tag: v1-beta) [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

    git tag -d wrongmodify

    git hist --all
    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (HEAD, tag: v1, master) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 (tag: v1-beta) [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

至此，我们已经撤销了错误修改的版本，并且在log历史记录中也彻底删除了它。

## 修正提交

### 目的

* 学习如何修正已经完成的提交内容。

### 修改"helloGit.js"文件并提交

一次修改：

    git add helloGit.js
    git commit -m "修改电话"

二次修改：

    git add helloGit.js
    git commit --amend -m "修改电话和邮件"

查看历史：

    git hist
    // 发现一次修改和二次修改只在log历史记录中出现了一次

## 移动文件

### 目的

* 学习如何在git库内移动文件。

### 具体操作

首先，我们新建一个二级目录"tmpFolder"，并在二级目录下添加文件"zepto.js"

    cd helloGit
    mkdir tmpFolder
    cd tmpFolder
    vim zepto.js

然后，执行如下命令：

    git mv zepto.js ../
    git status

    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        renamed:    tmpFolder/zeoto.js -> zeoto.js

## 分支branch

### 目的

* 学习如何在git库中创建一个本地分支。

### 创建一个分支

    git checkout -b newBranch
    git status

    On branch newBranch
    nothing to commit, working directory clean

### 在新分支里做些更改

首先，在"tmpFolder/"增加"tmp.js"文件

    cd tmpFolder/
    vim tmp.js

```js
// 添加如下内容
;(function (win) {
    var test = function (arg) {
        console.log(arg);
    };
    win.tmp = {
        name: "tmpClass",
        test: test  
    };
})(window);
```

然后，提交这次修改：

    git add tmpFolder/tmp.js
    git ci -m "增加tmp.js"

    git status 
    * cbee482 2015-06-21 | 增加tmp.js (HEAD, newBranch) [AlexBai1991]
    * a3571a3 2015-06-21 | 移动文件 (master) [AlexBai1991]
    * 2cd9b17 2015-06-21 | 新建文件夹 [AlexBai1991]
    * dfcd1da 2015-06-21 | 第三次修改helloGit.js文件 (tag: v1) [AlexBai1991]
    * 15dde97 2015-06-21 | 第二次修改helloGit.js文件 (tag: v1-beta) [AlexBai1991]
    * b703c22 2015-06-21 | 第一次修改helloGit.js文件 [AlexBai1991]
    * f546278 2015-06-21 | 添加helloGit.js文件 [AlexBai1991]

### 切换分支

    git checkout master
    git checkout newBranch

### 在主分支里做些更改



