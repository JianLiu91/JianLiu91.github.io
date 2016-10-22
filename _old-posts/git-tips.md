title: Git tips
date: 2016-01-05 15:30:47
tags:
---

[Git](https://zh.wikipedia.org/wiki/Git) 由大名鼎鼎的 Linus Torvalds 开发，本来是他自娱自乐，用于管理自己开发的 Linux 内核的版本控制工作，但是一不留神，现今成为了家喻户晓的版本控制工具。

> I'm an egotistical bastard, and I name all my projects after myself. First Linux, now git.

其优势主要在于:

* 轻量
* 分布式
* 便于团队合作

如果你是一个严肃的，职业化的coder，那么你可能会用到这个方便，但是有时候却比较莫名其妙的工具。

![image](/img/git.png)

![image](https://imgs.xkcd.com/comics/git.png)

本文的目的是通过一个小团队合作的栗子具体阐述 Git 的"开发流程"，一些用法可能会略显死板，解决方案也并不完美，仅仅旨在提供一个可行的解决思路。同时结合具体例子说明了团队中各个角色应该熟悉的 Git 命令。

### 应用场景

典型应用场景: Leader, 高富帅，白富美，单身狗，四个人共同负责开发维护一个项目。其中，高与白共同开发一个模块，单身狗独自负责一个模块（你懂的），项目进度统一由Leader掌控和对外发布。

下面分角色来阐述每一个角色应该承担的工作，以及用哪些命令来完成这些操作。

#### Leader

Leader 需要做的工作有两个：
* 代码的对外发布
* code review 和 code merge (团队成员之间相互也应该进行 code review)

简单说，Leader 需要保证如下两条线中的 master 线的完美推进。

![image](http://image.beekka.com/blog/201207/bg2012070504.png)

Leader流程伪代码如下:

```
    git checkout -b develop          // 建立一个新的 develop 分支，并且切换到这一分支
    git push origin develop          // 把 develop 分支提交到代码托管服务器
    git checkout master              // 切换回主分支
                                     
    // 以上为初始化阶段，仅仅需要做一次    
    
    while (True) {                            // 直到项目做完那天啊~ - -
    
        // 等待团队成员提交代码， 时间取决于团队开发速度
        
        git fetch origin                      // 把远程的代码拿回本地，一定不要用git  pull!!!!!!
        git checkout origin/develop           // 切换到拿到的远程 develop 分支，注意不要合并
        git log                               // 查看团队成员的 commit 记录，code review等等
                                            
        // 。。。
                                            
        if (代码没有问题，并且测试通过，可以发布新的版本) {
            git checkout master               // 切换到master分支
            git merge --no-ff origin/develop  // 合并分支，一般不会(不应该)有冲突
            
                // 填写 commit 信息， 如下格式，可以参考 [我](http://www.zhihu.com/question/21209619)
            
                // 功能汇总:
                // (空行）
                // 1. 文件功能完成 (by xxx)
                // 2. 硬件功能完成 (by yyy)
                // 3. 软件功能完成 (by zzz)
       
            git tag                           // 打上新的标签
            git push origin master            // 发布
            
        } else {
            代码中的bug反馈给团队成员，勒令其修改
            或者还不到发布时机，继续喝茶等待其他关键代码被提交  
        }
    }
```

有几点需要注意(但是不一定正确)：

1. Leader 不需要把 origin/develop 和本地的 develop 分支合并，只需要 checkout 到 origin/develop 即可以查看只读代码。
2. 不要用`git pull`, git pull 会依次执行 `git fetch` 和 `git merge`, `git merge`有个比较烦人的属性是它会默认执行 fast forword，则会把待合并分支的全部 commit 在待合并分支上重新弄一遍，会让提交的分支结构图变得很乱（参见第一副图的项目分支图)
3. 使用`git merge --no-ff`。 `--no-ff` 参数会让提交记录变得干净（并不会把待合并分支的 commit 信息加入进来)：

![image](http://i.stack.imgur.com/GGkZc.png)

至此，Leader 负责的部分结束。


#### 单身狗

单身狗自己负责一个模块，自给自足，简单粗暴。但是为了保证提交记录的干净，方便日后的 trace 以及回退操作，需要熟悉如下以下几个 Git 命令， 结合其工作流程总结伪代码如下:

```
   git fetch origin
   git checkout --track origin/develop     // 建立一个本地 develop 追踪远程 develop
   
   git checkout -b myfeature               // 新建自己的分支，并且切换到自己的分支上，准备开发
                                           // 严格说，对自己负责的没一个模块（功能），都需要建立一个分支。
   // 以上为初始化操作， 只需要执行一次
   
   while (true) {                          // ...
   
        // 开发 function 1
        git commit -am 'add function 1'    // 这里的 commit 信息是给自己看的
        
        // 开发 function 2
        git commit -am 'add function 2'    // 这里的 commit 信息是给自己看的，
        
        // 如果 commit 之后又修改了代码，同时不想再次增加新的 commit 信息，可以用 --amend
        // git commit -a --amend           // 这个命令是追加修改，同时修改上一次的 commit 信息
        
        // 当觉得功能开发完成了，需要合并到 develop 分支，同时提交到远程服务器
        
        git checkout develop               // 切换到开发分支，准备合并和提交
        git fetch origin                   // 注意这里不要用pull!!!!!!
        git merge --no-ff origin/develop   // 此时，处在 develop 分支上， 与远程分支的 develop 合并，不会（不应该）有冲突
        
        
        git merge --no-ff myfeature
        
            // 这里可能会产生冲突，按照提示冲突的文件对每个文件进行修改
        // git status                  // 这时候会看到每一个冲突文件都是 [M] (modified) 状态
        // git commit -a               // 解决冲突完成        
                
                
        // 填写 commit log, 格式参考[我](http://www.zhihu.com/question/21209619)
        
        // 完成了文件管理功能
        //
        // 1. 文件新建功能
        // 2. 文件删除功能
        // 3. 文件重命名功能
        // 4. 文件查看功能
        
        
        git push origin develop            // 把 develop 分支推送到服务器
        
        git checkout myfeature             // 切换回自己的分支, 继续准备开发工作。。。
        git merger --no-ff develop         // 如果有必要的话，需要和 develop 分支再次合并
        
        }
    }
```


#### 高 & 白

对于多人负责的模块，不要把代码直接 push 到 develop 上，而是应该建立新的分支来进行合并，这样可以尽可能的避免其他人的打扰。 - -

在合作之前，需要首先建立合作分支，并且提交到远程代码托管服务器，伪代码:

```
       git fetch origin
       git checkout --track origin/develop     // 建立一个本地 develop 追踪远程 develop
   
       git checkout -b teamfeature             // 建立一个用于协作的分支
       git push origin teamfeature             // 把此分支发布到代码管理器上
       
       // 以上只需要做一次，目的是建立协同的分支
       
```

高和白的开发伪代码:

```
    git fetch origin
    git checkout --track teamfeature          // 建立本地的 teamfeature 分支来追踪远程分支
    git checkout teamfeature                  // 切换到开发分支
    
    while (True) {
        git fetch origin                      // 把远程代码拉到本地
        git merge --no-ff origin/teamfeature  // 这里主要是为了把合作同伴写的代码合并进来
        
        // 这里可能会有冲突，参照一般的解决冲突方案，这里的 commit 信息可以随意一些
        
        // add some useful function
        git commit -am 'some useful function'  // 提交 commit 信息
        
        git push origin teamfeature            // 把远程分支提交到代码管理器上，方便同伴的查看
        
   }
```

当共同的任务开发完成之后，高和白还需要把合作的结晶合并到 develop 分支，并且删除远程的合作分支。

伪代码如下:

```
    git fetch origin                           // 把远程的代码拉到本地
    git checkout develop                           
    git merge --no-ff origin/develop           // 此时，处在 develop 分支上， 与远程分支的 develop 合并，不会(不应该)有冲突

    git merge --no-ff teamfeature              // 把合作的分支合并到 develop 分支上，主要使用 --no-ff 参数
        
        // 这里可能会产生冲突，修改冲突的文件
        // git status 查看没有冲突之后
        // git commit -a                       // 解决冲突完成        
                
                
        // 填写 commit log, 格式参考
        
        // 完成了文件管理功能
        // (空行)
        // 1. 文件新建功能
        // 2. 文件删除功能
        // 3. 文件重命名功能
        // 4. 文件查看功能
        
        
     git push origin develop                   // 把 develop 分支推送到服务器
       
     git push origin --delete teamfeature      // 删除远程分支
```

#### Tips

* 使用重命名机制让命令变短，[链接](https://git-scm.com/book/tr/v2/Git-Basics-Git-Aliases)
    `git config --global alias.co checkout`，然后可以执行`git co`代替`git checkout`操作.
* 关闭 merge 的 ff 操作,`git config merge.ff false`, 这样直接使用 merge 就可以了。[链接](http://stackoverflow.com/questions/10234369/git-merge-without-fast-forward-by-default)


以上, 如果严格按照代码提交机制来提交的化，那么最后 develop 这条分支就会是一条简单的直线图。每个人会保存两条直线，分别是 develop, myfeature。并且提交记录会非常之清晰，方便功能回退，代码调试工作等等。

如果遇到问题，参照漫画中提到的最简单而有效的方案解决。。。。(^^)
   
