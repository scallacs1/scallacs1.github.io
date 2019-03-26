# 菜鸡日常 #
---
## 问题描述 ##
得空准备清理一下电脑空间，删掉了几个软件后，竟然有非常顽固的文件夹残余删不掉，很烦，照常用软件直接给粉碎了得了，重启之后辣鸡文件夹竟然还在，大概给设置了开机启动。
最后只能手动清理了。
## 正文 ##
样图如下
![avatar](https://github.com/scallacs1/scallacs1.github.io/tree/master/img/delete_folder/the_bad_exe.PNG)
在其他应用中打开，那只能在kill该应用的进程后再删除文件了。
任务管理器里的服务排的密密麻麻，看的我头皮发麻。
![avatar](https://github.com/scallacs1/scallacs1.github.io/tree/master/img/delete_folder/jincheng.PNG)
换个方式解决。打开**cmd**输入命令：**tasklist**列出进行中的进程清单。可以把该清单转成一个txt文档便于查找相关信息。**tasklist >e:/list.txt**即可在E盘生成一个文档包含所有进程信息
然后。按照相关的PID结束进程
![avatar](https://github.com/scallacs1/scallacs1.github.io/tree/master/img/delete_folder/notlill.PNG)
因为关联问题，还干不掉它。是个多进程守护型！！！
按Error返回的PID号查询了相关应用名，发现其中六个PID对应了同样的应用名。


这是怎样一堆流氓程序啊！！！换成**ntsd**都关不掉它
百度了一下，还真有不少人遇见过相同的情况

----
一堆资料查找分析后，最后选择找到对应的程序软件，在其属性窗口打开“安全”面板，点击“编辑”选项，在弹出的“组或用户名”列表中“拒绝”列勾选所有项目，重启系统，使用system权限删除相关文件。
