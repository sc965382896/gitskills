* fetch   
Git中的fetch命令是将远程分支的最新内容拉到了本地，但不立即将远程分支的变更合并到本地分支上。当我们执行完fetch命令后，在执行git branch命令会发现此时后本
地多了一个FETCH_HEAD的分支。当我们检查完成后在checkout回本地分支执行merge命令进行合并。合并后如果出现冲突则需要我们手动解决冲突，然后在commit一次。

* pull    
pull相当于fetch和merge两步操作。
