# 工作流程

1. 一般有 master分支，dev分支，还有各个小组成员的分支  
    master分支和dev分支需要与远程仓库同步，而成员分支是各自玩自己的，只要时不时的向dev分支push自己的工作就可以了。

2. 从远程仓库 clone  
    ```git clone https://...```   
    clone之后默认只能看到 master 分支，可以用命令```git branch```查看。然后要转移到 dev 分支用命令```git checkout -b dev origin/dev```，这之后会将本地 dev 分支和远程 origin/dev 分支关联起来。

3. 从 dev 上分出一个分支来工作  
    ```git checkout -b lab```

4. 在 lab 分支上工作完后和本地 dev 合并  
    ```git checkout dev```  
    ```git merge --no-ff lab```

5. 将 dev 分支推送到远程仓库  
    ```git push origin dev```   

6. 之后再工作时可以先从远程拉取 dev 分支，接着工作  
    ```git pull dev```