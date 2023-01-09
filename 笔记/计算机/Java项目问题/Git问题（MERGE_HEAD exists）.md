拉取代码报错（Couldn't merge origin/master: You have not concluded your merge (MERGE_HEAD exists).） 
造成原因：本地合并其他分支代码的时候，在merge代码后未提交就失手revert了本地代码。 解决方式： 进行以下两步操作后直接重新拉取代码。这个方式中止了以上的合并，需要重新操作。 
```java
git merge --abort 
git reset --merge
```