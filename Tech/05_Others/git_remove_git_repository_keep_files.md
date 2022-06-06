# 如何删除 git 仓库但是保留所有代码文件

如果向 删除 git 仓库，可以直接删除 当前 repository 里面 `.git` 目录中的所有文件即可。但是需要注意的是，这个操作只会保留当前 checkout 出来的文件，历史版本中提交的内容都会被删除。所以，需要 checkout 需要的分支 和对应的 commit。之后再进行删除即可。

---

## References

- [Remove Git repository, but keep all files](https://stackoverflow.com/questions/22796285/remove-git-repository-but-keep-all-files)
