# Git Rebase操作
## git graph操作
1. 可以在git graph上先操作rebase，然后执行
    git push --force

## 命令行操作
1. git checkout A;git fetch origin B;git rebase origin/B
2. 解决冲突
3. git rebase --continue（如需取消rebase：git rebase --abort）