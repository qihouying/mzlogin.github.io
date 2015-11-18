---
layout: wiki
title: Git
categories: Git
description: Git 常用操作记录。
keywords: Git, 版本控制
---

| 功能                      | 命令                      |
|:--------------------------|:--------------------------|
| 添加文件/更改到暂存区     | git add filename          |
| 添加所有文件/更改到暂存区 | git add .                 |
| 提交                      | git commit -m msg         |
| 从远程仓库拉取最新代码    | git pull origin master    |
| 推送到远程仓库            | git push origin master    |
| 查看配置信息              | git config --list         |
| 查看文件列表              | git ls-files              |
| 比较工作区和暂存区        | git diff                  |
| 比较暂存区和版本库        | git diff --cached         |
| 比较工作区和版本库        | git diff HEAD             |
| 从暂存区移除文件          | git reset HEAD filename   |
| 查看本地远程仓库配置      | git remote -v             |
| 回滚                      | git reset --hard 提交SHA  |
| 强制推送到远程仓库        | git push -f origin master |
| 修改上次 commit           | git commit --amend        |

### Q&A

1. 如何解决gitk中文乱码，git ls-files 中文文件名乱码问题？

    在~/.gitconfig中添加如下内容

    ```
    [core]
        quotepath = false
    [gui]
        encoding = utf-8
    [i18n]
        commitencoding = utf-8 
    [svn]
        pathnameencoding = utf-8 
    ```

    参考 <http://zengrong.net/post/1249.htm>

2. 如何处理本地有更改需要从服务器合入新代码的情况？

    ```
    git stash
    git pull
    git stash pop
    ```

3. 如何合并 fork 的仓库的上游更新？

    ```
    git remote add upstream https://upstream-repo-url
    git fetch upstream
    git merge upstream/master
    ```

4. 如何通过 TortoiseSVN 带的 TortoiseMerge.exe 处理 git 产生的 conflict？
    * 将 TortoiseMerge.exe 所在路径添加到 `path` 环境变量。
    * 运行命令 `git config --global merge.tool tortoisemerge` 将 TortoiseMerge.exe 设置为默认的 merge tool。
    * 在产生 conflict 的目录运行 `git mergetool`，TortoiseMerge.exe 会跳出来供你 resolve conflict。

        > 也可以运行 `git mergetool -t vimdiff` 使用 `-t` 参数临时指定一个想要使用的 merge tool。

5. 不想跟踪的文件已经被提交了，如何不再跟踪而保留本地文件？

    `git rm --cached /path/to/file`，然后正常 add 和 commit 即可。
