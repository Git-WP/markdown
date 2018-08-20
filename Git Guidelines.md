### Git Guidelines 

---

[TOC]

#### 项目管理

- 企业级项目git的远程仓库一般是由 `master | test | dev` 三个分支构成
- 开发人员是在 `dev` 上开发
- 发布测试环境 或者 生产环境时, 合并到`test | master` 分支上



#### 开发人员操作步骤

1. git clone 把远程dev上的代码克隆到本地（origin/dev）
2. git checkout -b dev 在本地创建一个dev分支，在这个分支上修改代码
3. dev分支上add和commit代码
4. 切换到origin/dev分支上
5. git pull 把远程dev分支上的代码更新下来。因为在修改代码期间，或许有人提交了代码，需要把别人提交的代码更新下来，我们提交时才能保证不会覆盖掉别人的代码。
6. 切换到dev分支
7. 把origin/dev分支合并到dev分支，如果有冲突解决冲突。解决完冲突需要add和commit提交代码
8. 切换到origin/dev分支上
9. 把dev分支合并到origin/dev分支上
10. git push origin 把origin/dev分支提交到远程dev上



#### 常用命令

- git add filename	//提交到仓库

  git commit -m "descript"	//提交，并添加备注

  git status	//查看仓库状态

  git diff	//查看本地和仓库的不同		git diff HEAD -- filename

  git log	//历史记录

  git log --pretty=oneline

  git log --graph --pretty=oneline --abbrev-commit	//查看冲突合并详情

  git reset --hard HEAD^	//回退到上一个版本

  git reset --hard versionCode	//根据版本号到任意版本

  git reflog	//查看操作日志

​	git reset HEAD filename	//丢弃暂存区修改

​	git checkout -- filename //丢弃工作区修改（实际上是用版本库的版本替换工作区中的版本）

​	rm rilename	//删除工作区中的文件

​	git rm filename	//删除版本库中的文件，需要提交

​	git remote add origin git@github.com/GitNoHup/MyGitDemo.git	//关联远程库

​	git push -u origin master	//首次推送master分支的所有内容 -u 会把本地的master分支和远程的master分			支关联起来

​	git push origin master	//以后每次提交到远程库

​	git clone giturl //从远程库克隆一个本地库

​	git checkout -b dev	//创建并切换到dev分支，相当于下面两条命令

​	git branch dev	//创建dev分支

​	git checkout dev	//切换到dev分支

​	git branch	//查看分支

​	git merge dev	//把dev分支合并到当前分支上

​	git branch -d dev	//删除dev分支

​	git branch -D dev	//删除一个未被合并的分支

​	git stash	//存储当前工作现场

​	git stash list	//查看工作现场

​	git stash apply	//恢复工作现场	stash内容不删除，使用git stash drop删除stash内容

​	git stash pop	//恢复工作现场

​	git stash apply stash@{0}	//指定恢复某个工作现场

​	git remote	//查看远程仓库信息

​	git remote -v	//查看远程仓库详细信息

​	git push origin master	//推送指定分支到远程仓库

​	git pull //更新



#### 参考资料

[1]: https://blog.csdn.net/qq_35794202/article/details/80626074	"Git提交代码流程"

