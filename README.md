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
