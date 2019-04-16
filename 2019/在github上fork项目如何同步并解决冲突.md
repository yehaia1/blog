# 在github上fork项目如何同步并解决冲突

在github上有些项目我们可能会进行一些自己功能的添加但是提交PR后作者基于设计或者其他原因考虑没有通过，但是这个功能又是我们必须的。这时我们就想自己维护一份自己的版本，所以主仓库更新版本时我们就需要同步。

1. 首先，先克隆自己的fork后的远端仓库到本地

    ````powershell
    git clone https://github.com/your/projectname.git
    ````

2. 用`vscode`打开，并在`vscode`的终端进行操作

    ````powershell
    # 查看原有远程分支信息
    git remote -v
    # 添加源项目的远程分支并命名为upgrade，名称随意
    git remote add upgrade https://github.com/origin/projectname.git
    # 再次查看本地的远程分支信息，这时已经可以看到远程分支已经添加进去了
    git remote -v
    # 把upgrade的代码拉取到本地
    git fetch upgrade
    # 查看并选中dev（默认是选中master），或者其他你想合并的分支，只有一个master分支可以忽略
    git branch
    # *号就是选中的
    > * master
    > dev
    git checkout -b dev
    # 合并upgrade到我们自己的master分支
    git merge upgrade/master
    # 如果没有提示冲突，直接推送到github仓库，有冲突请继续往下看
    git push origin master
    ````

3. 处理冲突

    这时我们可以点开`vscode`的`Source Control`（源代码管理）就可以很方便的查看到冲突的文件，处理完冲突然后再次合并。

    ````powershell
    # 这时执行合并提示成功了
    git merge upgrade/master
    # 推送到github
    git push origin master
    ````

至此，大功告成。
