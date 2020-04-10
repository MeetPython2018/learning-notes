# learning-notes
### 使用git进行版本控制

- git init                     将当前目录变成git可以管理的本地仓库
- git add fileName             将该文件添加到暂存区中
- git commit -m 'Tips'         将文件提交到仓库中
- git status                   查看是否还有文件未提交
- git diff fileName            查看文件前后的变化
- git fetch origin             从主分支拉下最新版本
- git merge origin/master      将本地最新版本合并到主分支
- git push -u origin master    第一次远程提交时
- git push                     后续版本迭代是提交远程仓库
### 版本回退

- git log                      查看历史纪录
- git log –pretty=oneline      以一行显示历史纪录
- git reset  --hard HEAD^      回退到上一个版本
- git reset  --hard HEAD^^     回退到上上一个版本
- git reset  --hard HEAD~n     回退到前n个版本
- git reflog                   获取版本号
- git reset  --hard 6fcfc89    以版本号恢复被回退的版本
### 本地仓库与远程仓库实现同步

- ssh-keygen -t rsa -C "youremail@example.com"    生成密钥文件
- git remote -v                                   查看现有的远程仓库
- git remote rm repositoryName                    移除这个远程仓库
- git pull --rebase origin                        拉取远程仓库的文件

