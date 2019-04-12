# 版本管理-Git

[https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)<br />Git是目前世界上最先进的分布式版本控制系统（没有之一）。<br /><br />
<a name="7055101b"></a>
# 安装Git 创建本地仓库和初始化仓库

安装Git...  

使用
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```
[]()<br /><br />现在总结一下今天学的两点内容：<br />创建一个文件夹<br />初始化一个Git仓库，使用`git init`命令。<br />添加文件到Git仓库，分两步：
1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
1. 使用命令`git commit -m <message>`，完成。

`git status`命令可以让我们时刻掌握仓库当前的状态<br />`git diff file`` `顾名思义就是查看difference查看修改内容

* 要随时掌握工作区的状态，使用`git status`命令。<br />
* 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。




<a name="0f4c97ef"></a>
# 时空机穿梭

<a name="da3751cd"></a>
### HEAD 版本切换
现在总结一下：

* `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，
* 使用命令`git reset --hard commit_id`。
* 回退当前版本的上一个版本 
* <br />
* 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。<br />
* 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

      `git reset --hard HEAD^`  回退上一个版本<br /> 查看日志：
```git
git log --graph --pretty=oneline --abbrev-commit
```


<a name="5fac8ba2"></a>
### 暂存区的了解，明白Git的操作是怎么回事儿

暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。<br />![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1554715490341-4f3e977b-54b4-4add-b399-fcce66b75b7b.png#align=left&display=inline&height=310&name=image.png&originHeight=310&originWidth=866&size=66395&status=done&width=866)<br /><br />第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；  stage<br />第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。 master /  other branch 
<a name="1e6f9405"></a>
### Git核心是跟踪 修改
现在，你又理解了Git是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

<a name="d9b77027"></a>
### 撤销工作区内容和暂存区内容

又到了小结时间。<br />场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。<br />场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，<br />第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。<br />场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。
<a name="53518c22"></a>
### 删除文件

命令`git rm <file>`用于删除版本库里的一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。<br />rm <file> 用于删除工作区的文件  ；  如果误删了，版本库里面还有呢，用<br />git checkout -- <file>  还原<br />`git checkout `其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”<br /><br />



<a name="44a6ae3f"></a>
# 远程仓库

<a name="bfe812f9"></a>
### 远程库- 注册GitHub 把本地关联到远程库
要关联一个远程库，<br />使用命令`git remote add origin git@server-name:path/repo-name.git`；<br />path是 GitHub账号名<br />关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；<br />此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；<br />分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

<a name="ffb10479"></a>
### 从远程仓库克隆到本地
使用命令 
```
git clone git@github.com:GitHub账户名/gitskills.git （文件名）
```
要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。<br />Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。<br />参数： --depth=1 <br />depth用于指定克隆深度，为1即表示只克隆最近一次commit.<br /><br />

<a name="5aa52869"></a>
# 分支管理

<a name="c439fe8e"></a>
### 创建切换分支  合并分支
Git鼓励大量使用分支：<br />查看本地分支：`git branch`<br />查看远程库分支：`git branch -r`  <br />查看本地 和 远程库分支：`git branch -a` <br />创建分支：`git branch <name>`<br />切换分支：`git checkout <name>`<br />创建+切换分支：`git checkout -b <name>`<br />合并某分支到当前分支：`git merge <name> ` 但会丢掉分支的信息<br />合并某分支到当前分支  带 --no-ff参数  和 -m “”添加合并信息的描述：<br />`git merge --no-ff -m "message" <name> ` 


删除分支：`git branch -d <name>`<br />删除远程库分支：`git push origin -d <name>`

从远程库拉取分支：`git pull`

从查看分支合并信息：`git log --graph`



<a name="d39e8dcc"></a>
### 分支合并冲突解决
当混帐无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。<br />解决冲突就是把Git的合并失败的文件手动编辑为我们希望的内容，再提交。<br />用`git log --graph`命令可以看到分支合并图产品。

<a name="82568b84"></a>
### 分支管理策略


![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1554776764298-7a98a6f1-8b6a-44b7-bac9-580ee0f544a9.png#align=left&display=inline&height=177&name=image.png&originHeight=177&originWidth=516&size=17409&status=done&width=516)<br />Git分支十分强大，在团队开发中应该充分应用。<br />合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。



![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/116060/1554776781354-c161b7bd-509a-42c6-bcdb-650e9b6d2961.png#align=left&display=inline&height=894&name=image.png&originHeight=1211&originWidth=1011&size=420208&status=done&width=746)



<a name="dd6986d0"></a>
### Bug分支
突然要修bug<br />先把正在开发的现场暂停保存一下<br />工作现场`git stash`一下,  修好后回来 git stash pop 回到工作现场


修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；<br />当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场。


<a name="5cf8f3fa"></a>
### 开发新功能，创建新的分支
开发一个新feature，最好新建一个分支；<br />如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。


<a name="b41555ef"></a>
### 多人协作 
* 查看远程库信息，使用`git remote -v`；<br />
* 本地新建的分支如果不推送到远程，对其他人就是不可见的；<br />
* 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；<br />
* 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；<br />
* 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；<br />
* 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

<a name="2ec512a4"></a>
# 标签管理

* 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；<br />
* 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；<br />
* 命令`git tag`可以查看所有标签。
<a name="a377eff7"></a>
### 操作标签 
* 命令`git push origin <tagname>`可以推送一个本地标签；<br />
* 命令`git push origin --tags`可以推送全部未推送过的本地标签；<br />
* 命令`git tag -d <tagname>`可以删除一个本地标签；<br />
* 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。<br />



