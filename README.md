## Git
-----
> 在Windows上安装Git
安装完成后需要输入命令
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 创建版本库

1. 初始化一个Git仓库，使用`git init`命令。

2. 添加文件到Git仓库，分两步：

  * 第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；

  * 第二步，使用命令git commit，完成。


## 版本回退
 > `git status`命令可以让我们时刻掌握仓库当前的状态  
 > `git diff` 顾名思义就是查看difference，显示的格式正是Unix通用的diff格式  
 > `git log`命令显示从最近到最远的提交日志,可加 `--pretty=oneline` 命令  
 > `git reflog` 用来记录你的每一次命令：  
 > `git reset`
   * 要随时掌握工作区的状态，使用`git status`命令。
   * 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。  

1. `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`  
2. 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本  
3. 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本

#### 工作区 （*就是你在电脑里能看到的目录*）

#### 暂存区  
> 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。  
Git的版本库里存了很多东西，其中最重要的就是称为`stage`（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫 `HEAD`。  

添加版本库时  
第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；  
第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

## 撤销修改  
1. 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`  
2. 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。  
3. 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。  

## 删除文件
 > 命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

## 远程仓库
 1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：  
 `ssh-keygen -t rsa -C "youremail@example.com"`  
 > 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。  
 1. 登陆GitHub，打开“Account settings”，“SSH Keys”页面, 然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容.

## 添加远程库  
  * 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`

  * 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

  * 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

 > 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

## 从远程库克隆
  * 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。  
  * Git支持多种协议，包括`https`，但通过`ssh`支持的原生git协议速度最快。

## 分支管理     
### 创建与合并分支
  1. 首先，我们创建dev分支，然后切换到dev分支  
  `git checkout -b dev`  
  `git checkout` 命令加上 `-b` 参数表示创建并切换，相当于以下两条命令：  
  ```
  git branch dev  
  git checkout dev
  ```
  > 然后，用`git branch`命令查看当前分支：git branch命令会列出所有分支，当前分支前面会标一个`*`号。
  2. 然后，我们就可以在dev分支上正常提交，如提交readme.txt文件
  3. dev分支的工作完成，我们就可以切换回master分支:  
  ```
  git checkout master
  ```
  > 切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：
  4. 合并。把dev分支的工作成果合并到master分支上：
  ```
  git merge dev
  ```
  > `git merge`命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。  
  5. 合并后就可以删除dev分支：
  ```
  git branch -d dev
  ```
  > 删除后，使用 `git branch` 查看branch，就只剩下master分支了

> *因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。Git鼓励大量使用分支*    

* 查看分支：`git branch`  
* 切换分支：`git checkout <name>`  
* 创建+切换分支：`git checkout -b <name>`    
* 合并某分支到当前分支：`git merge <name>`   
* 删除分支：`git branch -d <name>`  
