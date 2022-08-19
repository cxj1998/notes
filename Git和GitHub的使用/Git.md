### 一、配置Git

#### 	1.配置用户信息

```
git config --global user.name "ithema"
```



```
git config --global user.email "ithema@itcast.cn"
```

#### 	2.Git的全局配置文件

```
C:\Users\PLA\.gitconfig
```

#### 	3.检查配置信息

##### 		查看所有的全局配置项

```
git config --list --global
```

##### 		查看指定的全局配置项

```
git config user.name
git config user.email
```

#### 	4.获取帮助信息

##### 		打开 git config 命令的帮助手册

```
git help config
```

##### 		查看简明版的手册

```
git config -h
```

### 二、获取git仓库

​	Git标准的工作流程是：**工作区**→**暂存区**→**Git仓库**

#### 	1.在现有目录中初始化仓库

```
git init
```

#### 	2.工作区中文件的4种状态

![1657375467125](E:\笔记\Git和GitHub的使用\assets\1657375467125.png)

**注意：**Git操作的终极结果：让工作区中的文件都处于“未**修改**”的状态

#### 	3.检查文件的状态

```
git status
```

#### 	4.以精简的方式显示文件状态

```
git status -s
git status --short
```

​		未跟踪文件前面有红色的？？标记

![1657375689182](E:\笔记\Git和GitHub的使用\assets\1657375689182.png)

#### 	5.跟踪新文件

```
git add 文件名称
```

​	文件在 Changes to be committed，说明已被跟踪，并处于暂存状态：

![1657375841732](E:\笔记\Git和GitHub的使用\assets\1657375841732.png)

------

![1657375848871](E:\笔记\Git和GitHub的使用\assets\1657375848871.png)

#### 	6.提交更新

```
git commit -m "新建了index.html文件"
```

​	提交成功：

![1657375942919](E:\笔记\Git和GitHub的使用\assets\1657375942919.png)

​	检查文件的状态：

![1657375976621](E:\笔记\Git和GitHub的使用\assets\1657375976621.png)

证明工作区中所有的文件都处于“**未修改**”的状态，**没有任何文件需要被提交**

#### 	7.对已提交的文件进行修改

![1657376216638](E:\笔记\Git和GitHub的使用\assets\1657376216638.png)

文件index.html出现在 **Changes not stages for commit** 这行下面，说明**已跟踪文件内容发生变化，但还没放到暂存区**（文件前面有**红色**的**M**标记）

#### 	8.暂存已修改的文件

![1657376424825](E:\笔记\Git和GitHub的使用\assets\1657376424825.png)

#### 	9.提交已暂存的文件

```
git commit -m "提交消息"
```

![1657376529364](E:\笔记\Git和GitHub的使用\assets\1657376529364.png)

#### 	10.撤销对文件的修改

​	把对工作区对应文件的修改，还原成 Git仓库中所保存的版本。

​	操作的结果：所有的**修改会丢失，且无法恢复！**

```
git checkout -- index.html
```

​	撤销操作的本质：用Git仓库中保存的文件，覆盖工作区指定的文件

#### 	11.向暂存区中一次性添加多个文件

```
git add .
```

#### 	12.取消暂存的文件

```
git reset HEAD 要移除的文件名称
```

#### 	13.跳过使用暂存区域

​	简化为：工作区→Git仓库

```
git commit -a -m "描述消息"
```

#### 	14.移除文件

##### 	①从Git 仓库和工作区中同时移除 index.js 文件

```
git rm -f index.js
```

##### 	②只从Git仓库中移除index.css，但保留工作区中的index.css文件

```
git rm --cached index.css
```

#### 	15.忽略文件

​	创建一个名为**.gitignore**的配置文件

​	.gitignore格式规范：

​	①以#开头的是注释

​	②以/结尾的是目录

​	③以/开头防止递归

​	④以！开头表示取反

​	⑤可以使用 **glob模式** 进行文件和文件夹的匹配（glob指简化了的正则表达式）

##### 		glob模式：

![1657377757009](E:\笔记\Git和GitHub的使用\assets\1657377757009.png)

##### 		.gitignore文件的例子

![1657377831546](E:\笔记\Git和GitHub的使用\assets\1657377831546.png)

#### 	16.查看提交历史

![1657378180869](E:\笔记\Git和GitHub的使用\assets\1657378180869.png)

#### 	17.回退到指定的版本

![1657378367992](E:\笔记\Git和GitHub的使用\assets\1657378367992.png)  