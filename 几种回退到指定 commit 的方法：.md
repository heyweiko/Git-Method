几种回退到指定 commit 的方法：

1. 使用 `git reset` (会丢弃目标 commit 之后的所有提交历史)：

```bash
# 硬重置 - 完全回退到指定commit，丢弃之后的所有更改
git reset --hard <commit_hash>

# 软重置 - 回退到指定commit，但保留更改在工作区
git reset --soft <commit_hash>
```

2. 使用 `git revert` (创建新的提交，保留历史记录)：
```bash
git revert --no-commit <commit_hash>..HEAD
git commit -m "Revert to <commit_hash>"
```

查看 commit 历史以获取 commit hash：

```bash
# 查看完整历史
git log

# 查看简洁历史
git log --oneline
```

具体建议：

1. 如果您想完全放弃某个 commit 之后的所有更改：
```bash
git reset --hard <commit_hash>
git push -f origin <branch_name>  # 强制推送到远程仓库
```

2. 如果您想保留更改但回到之前状态：
```bash
git reset --soft <commit_hash>
# 这样可以保留更改，您可以重新组织提交
```

3. 如果您想创建一个新的提交来撤销更改：
```bash
git revert --no-commit <commit_hash>..HEAD
git commit -m "Revert to previous state: <简短描述>"
```

注意事项：

- 使用 `--hard` 重置前请确保已备份重要更改

- 强制推送 (`push -f`) 要谨慎使用，可能会影响其他协作者
- 建议在执行重要操作前先创建分支备份：

```bash
git checkout -b backup_branch
```