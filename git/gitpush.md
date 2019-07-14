**小结**

1. 使用cd指令指定路径
2. pwd指令查看当前的目录
3. git init指令在当前目录下创建本地仓库
4. git add指令添加文件到仓库，git commit指令提交文件到仓库
5. git log查看log

> Get started by [creating a new file](https://github.com/YuanFeis/yfstudy/new/master) or [uploading an existing file](https://github.com/YuanFeis/yfstudy/upload). We recommend every repository include a [README](https://github.com/YuanFeis/yfstudy/new/master?readme=1), [LICENSE](https://github.com/YuanFeis/yfstudy/new/master?filename=LICENSE.md), and [.gitignore](https://github.com/YuanFeis/yfstudy/new/master?filename=.gitignore).
>
> ### …or create a new repository on the command line
>
> 
>
> ```
> echo "# yfstudy" >> README.md
> git init
> git add README.md
> git commit -m "first commit"
> git remote add origin git@github.com:YuanFeis/yfstudy.git
> git push -u origin master
> ```
>
> ### …or push an existing repository from the command line
>
> 
>
> ```
> git remote add origin git@github.com:YuanFeis/yfstudy.git
> git push -u origin master
> ```
>
> ### …or import code from another repository
>
> You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
>
> [Import code](https://github.com/YuanFeis/yfstudy/import)

今天提交git仓库的时候，遇到了如截图所示的问题，提示Your branch is up-to-date with 'origin/master'.





![img](https:////upload-images.jianshu.io/upload_images/7271374-610827abc6eb88a8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/486/format/webp)





查了些资料后，发现其根本原因是版本分支的问题

##### 这时候我们就需要新建一个分支

```
$ git branch newbranch  
```

##### 然后检查分支是否创建成功

```
$ git branch 
```

会有如下提示（前面的*代表的是当前你所在的工作分支）





![img](https:////upload-images.jianshu.io/upload_images/7271374-d2b41f107ddd92b1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/461/format/webp)



##### 然后切换到你的新分支

```
$ git checkout newbranch
```

如果不放心，还可以 $ git branch确认下

##### 然后将你的改动提交到新分支上

```
$ git add . 
$ git commit -m "18.03.01"
```

##### 然后`git status`检查是否成功



![img](https:////upload-images.jianshu.io/upload_images/7271374-e7db256c45e435f5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/476/format/webp)



##### 然后切换到主分支

```
$ git checkout master 
```

##### 然后将新分支提交的改动合并到主分支上

```
$ git merge newbranch  
```

##### 然后就可以push代码了

```
$ git push -u origin master
```

##### 最后还可以删除这个分支

```
$ git branch -D newbranch
```

# END