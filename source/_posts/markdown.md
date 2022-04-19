---
title: 简明手册
date: 2022-04-01 18:57:51
tags:
- HEXO
- markdown
categories: 
- HEXO
---
介绍hexo常用的命令以及markdown常用语法

<!--more-->
## hexo常用命令
```python
hexo new "postName"		#新建文章
hexo new page "pageName"#新建页面
hexo generate 			#生成静态页面至public目录
hexo server 			#开启预览访问端口
hexo deploy 			#部署到GitHub
hexo help  				#查看帮助
hexo version  			#查看Hexo的版本
hexo clean 				#清理public的内容
组合命令：
hexo s -g			 	#生成并本地预览
hexo d -g		 		#生成并上传
```

## 备份与自动部署

`hexo d`和`hexo d` 只是将生成的静态文件部署到了云端。

为了备份，将网站的源代码文件也推送到GitHub仓库备份。

`你的名字.github.io` 部署后，GitHub Pages 将默认使用你的 main 分支作为静态文件部署。所以我们最好新建一个 hexo 分支（命名无所谓）用来存储 Hexo 地源代码，master 分支则用来存储部署后的静态文件。
```py
git checkout -b hexo
```
这时便成功建立了一个 hexo 分支。（此后的工作都将在 hexo 分支下进行）
```python
git remote add origin https://github.com/你的用户名/你的名字.github.io
```
接下来准备提交，这几句命令将是你以后每次备份所需要输入。

```python
# 添加到缓存区
git add -A
git commit -m "这次做了什么更改，简单描述下即可"
# 推送至远程仓库
git push
# 第一次提交，你可能需设置一下默认提交分支
# git push --set-upstream origin hexo
```

每次推送都要输入这三条命令，你可能觉得有些麻烦。
那么你可以编写 bash 脚本。

譬如，在根目录下新建 `update.sh`。

```python
# 如果没有消息后缀，默认提交信息为 `:pencil: update content`
info=$1
if ["$info" = ""];
then info=":pencil: update content"
fi
git add -A
git commit -m "$info"
git push origin hexo
```

此后更新的话，只需要在终端执行 `sh update.sh` 即可。



## Hexo Markdown简明语法

### 斜体和粗体
使用``` * ```和``` ** ```表示斜体和粗体，格式如下：
```
*斜体*，**粗体**
```
效果如下：*斜体*，**粗体**
### 分级标题
使用 ``` === ```表示一级标题，使用``` --- ```表示二级标题，格式如下：
```
这是一个一级标题
===
这是一个二级标题
---
```
或者：使用``` # ```号（建议```#```后面跟一个空格）
```
# H1
## H2
### H3
#### H4
##### H5
###### H6
```
### 分割线
在单独的一行使用``` *** ```或者``` ___ ```表示分割线
```
part1
___ (三个下划线)
part2
```
效果如下：

part1
___
part2

### 删除线
使用``` ~~ ```表示删除线
（``` ~~ ```要紧跟文字不能空格）
```
~~我被划了吗？~~
```
~~我被划了吗？~~

### 超链接
#### 文字
插入文字超链接的格式如下 ：
```
[链接文字](链接地址 "链接标题")
eg:
hexo搭建时自动生成的[第一篇文章](https://jennycruise.github.io/2022/04/01/hello-world/ "helloworld")
```
hexo搭建时自动生成的[第一篇文章](https://jennycruise.github.io/2022/04/01/hello-world/ "helloworld")
#### 图片
插入图片超链接的格式如下：

```
![图片说明](图片链接 "图片标题")
eg:
![亮色模式背景](https://cdn.jsdelivr.net/gh/JennyCruise/mycdn/bg_light.jpg "bg_light")
```
eg:
![亮色模式背景](https://cdn.jsdelivr.net/gh/JennyCruise/mycdn/bg_light.jpg "bg_light")
#### 音频
插入音频，使用插件hexo-tag-aplayer，语法如下：
```
{% aplayer title author url [picture_url, narrow, autoplay, width:xx%, lrc:xxx] %}
```
详情参见：hexo-tag-aplayer [中文使用文档](https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md)
#### 视频
引用视频则直接插入iframe代码：
```
<script src="/js/youtube-autoresizer.js"></script>
<iframe width="640" height="360" src="https://www.youtube.com/embed/HfElOZSEqn4" frameborder="0" allowfullscreen></iframe>
```
### 注释
用``` \ ```表示注释，``` \ ```后面的文字解析为纯文本格式。
渲染效果：
```
\## 看我没有变成二级标题吧
```
\## 看我没有变成二级标题吧

### 引用
#### 普通引用
使用` > `表示文字引用：
(必须要在每行的开头)
```
> 野火烧不尽，
春风吹又生

遇到换行结束
```
eg：
> 野火烧不尽，
春风吹又生

遇到换行结束 
#### 嵌套引用
```
> 最外层引用
> > 第二层引用
> > > 可以嵌套很多层
```
> 最外层引用
> > 第二层引用
> > > 可以嵌套很多层
#### 引用嵌套列表
```
> - 这是引用里嵌套的一个列表
> - 还可以有子列表
> 	- 子列表
> 	- 子列表
```
> - 这是引用里嵌套的一个列表
> - 还可以有子列表
> 	- 子列表
> 	- 子列表
#### 引用嵌套代码
````
>     同样的，在前面加四个空格形成代码块


> ```
> 或者使用三个反引号形成代码块
> ```
````
>     同样的，在前面加四个空格形成代码块


> ```
> 或者使用三个反引号形成代码块
> ```
### 列表与表格
#### 无序列表
使用``` * ```, ``` + ```, ``` - ``` 来显示无序列表
(后面加空格)
```
+ 无序列表项 一
	- 子无序列表 一
	- 子无序列表 二
		* 子无序列表 三
+ 无序列表项 二
+ 无序列表项 三
```
效果展示：
+ 无序列表项 一
	- 子无序列表 一
	- 子无序列表 二
		* 子无序列表 三
+ 无序列表项 二
+ 无序列表项 三
#### 有序列表
使用数字和点表示有序列表：
(同样的，要加空格)
```
1. 有序列表项 一
	1. 子有序列表项 一
	2. 子有序列表项 二
	4. 故意标错，会自动排序
2. 有序列表项 二
3. 有序列表项 三
```
1. 有序列表项 一
	1. 子有序列表项 一
	2. 子有序列表项 二
	4. 故意标错，会自动排序
2. 有序列表项 二
3. 有序列表项 三
### 绘制表格
绘制表格格式如下：
` | ` 控制分列，
` - ` 控制分行，
` : ` 控制对齐方式。
    
示例：
```
| 这是标题 | 自动加粗 | 标题下指定对齐方式 | 不指定对齐方式 |
| :------- | --------: | :---: |---|
| ↑左对齐 | 右对齐↑  | ↑居中↑     |默认左对齐|
| 123456789    | ←空格不占位置   | 987654321 | 1 |
| 123456789| ←没有空格     | 987654321 | 0 |
```
效果展示：
| 这是标题 | 自动加粗 | 标题下指定对齐方式 | 不指定对齐方式 |
| :------- | --------: | :---: |---|
| ↑左对齐 | 右对齐↑  | ↑居中↑     |默认左对齐|
| 123456789    | ←空格不占位置   | 987654321 | 1 |
| 123456789| ←没有空格     | 987654321 | 0 |
### 代码块
#### 行内代码
使用``` ` ```符号
```
可以用 `一个`，
可以用 ``两个``，
也可以用 ```三个```，
总之就是要 ````成对````。
```
可以用 `一个`，
可以用 ``两个``，
也可以用 ```三个```，
总之就是要 ````成对````。
#### 多行代码
使用：``` ` ```符号
至少要三个连续的 ``` ` ```，数目要配对
````
```
#include<stdion.h>
int main
{
	cout<<"hello world!"<<endl;
	return 0;
}
```
````
```
#include<stdion.h>
int main
{
	cout<<"hello world!"<<endl;
	return 0;
}
```
#### 加强的代码块
````
```cpp
#include<stdion.h>
int main
{
	cout<<"hello world!"<<endl;
	return 0;
}
```
````
效果：
```cpp
#include<stdion.h>
int main
{
	cout<<"hello world!"<<endl;
	return 0;
}
```

***end***
