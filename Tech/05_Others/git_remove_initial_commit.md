# Git 如何删除第一次 commit 内容

## 问题描述

通过 `git reset` 或者 `git rebase` 可以移除某次 `commit` 内容 或者 放弃 某个 `commit` 之前 / 之后的 `commit`，但是如果只想删除第一次的 `commit`，这两个命令是不行的。

## 解决方案

删除最初的 `commit` 内容，需要用到如下命令：`git update-ref -d HEAD`. It will delete the named reference `HEAD`, so it will reset (softly, you will not lose your work) ALL your commits of your current branch (this may delete every commit). 建议备份分支在执行该命令。

---

## References

- [How to remove the first commit in git?](https://stackoverflow.com/questions/10911317/how-to-remove-the-first-commit-in-git)

- [10.3 Git Internals - Git References](https://git-scm.com/book/tr/v2/Git-Internals-Git-References)

- [ORIG_HEAD, FETCH_HEAD, MERGE_HEAD etc](https://stackoverflow.com/questions/17595524/orig-head-fetch-head-merge-head-etc)

- [Git 内部原理之 Git 引用 ](https://jingsam.github.io/2018/10/12/git-reference.html)
