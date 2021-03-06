#目录结构

##起
虽然使用Linux系统已经有很长一段时间了，同时对Linux系统的目录结构有一些大致的理解，
但是显然不够成体系化，而了解Linux文件系统的目录结构是学好Linux的至关重要的一步，所以
这次对其做一个系统化梳理。

##承
已知Linux是类Unix的多用户操作系统，即：一台计算机在同一时间内可以有多个用户使用，多个用户共同享用系统的全部硬件和软件资源。因而为了多用户的互不干扰，甚至不同权限区分，Linux需要做一系列的设计。

所以，相较于Windows存在多个驱动器盘符，每个盘符形成多个树形并列的情形

Linux没有盘符这个概念，只有一个根目录，所有文件都在它（/）下面，每个用户都是在/home目录下面建立自己的文件夹，

##分部梳理

### '/'目录
Linux的系统由'/'根目录做起始，向下做树形发散。

所以：根目录是整个系统最重要的一个目录，因为不但所有的目录都是由根目录衍生出来的， 同时根目录也与开机/还原/系统修复等动作有关。 
由于系统开机时需要特定的开机软件、核心文件、开机所需程序、 函式库等等文件数据，若系统出现错误时，根目录也必须要包含有能够修复文件系统的程序才行。

[如图：可以看到根目录结构]()

[注]根据配色可以区分一些东西，当然这也是可以自行配置的
[如图：配色区分]()
	
	在本目录中有以下三种	
	蓝色：表示目录
	青色：表示链接
	绿底黑字：表征权限777 可读可写可执行
	[注]权限-rwx 读 写 执行 4 2 1


之后是由根目录下发的其他目录

### /bin

系统有很多放置执行档的目录，但/bin比较特殊。因为/bin放置的是在单人维护模式下还能够被操作的指令。在/bin底下的指令可以被root与一般帐号所使用，主要有：cat,chmod(修改权限), chown, date, mv, mkdir, cp, bash等等常用的指令。
[如图：配色区分]()
	
	在本目录中有以下三种	
	绿色：表示可执行文件，可执行的程序
	青色：表示链接
	红底白字：与绿色相比差在所有者的执行权限(文件可执行权限警告)

### /boot

主要放置开机会使用到的档案，包括Linux核心档案以及开机选单与开机所需设定档等等。Linux kernel常用的档名为：vmlinuz ，如果使用的是grub这个开机管理程序，则还会存在/boot/grub/这个目录。

[如图：配色区分]()
	
	在本目录中有以下两种	
	白色：普通，如文本文件，配置文件，源码文件等
	蓝色：仅一个grub引导目录

### /dev

在Linux系统上，任何装置与周边设备都是以档案的型态存在于这个目录当中。 只要通过存取这个目录下的某个档案，就等于存取某个装置。比要重要的档案有
	
	/dev/null,
	/dev/zero,
	/dev/tty , 
	/dev/lp*, 
	/dev/hd*, 
	/dev/sd*等等


[如图：配色区分]()
	
	在本目录中有以下四种	
	青色：链接文件
	蓝色：目录
	绿地黑字：满权限
	灰底黄字：设备文件(o:其他组没有权限)

### /etc
系统主要的设定档几乎都放置在这个目录内，例如人员的帐号密码档、各种服务的启始档等等。 一般来说，这个目录下的各档案属性是可以让一般使用者查阅的，但是只有root有权力修改。
	
	[注]/etc/X11/ 与X Window有关的各种设定档都在这里，
	尤其是xorg.conf或XF86Config这两个X Server的设定档。
	/home 这是系统预设的使用者家目录(home directory)。 
	在你新增一个一般使用者帐号时，预设的使用者家目录	都会规范到这里来。
	比较重要的是，
	家目录有两种代号：~ ：代表当前使用者的家目录，而 ~guest：则代表用户	名为guest的家目录。

[如图：发现]()
	
	一些系统安装之后，自行安装的应用程序被安装到这里
	如 vim zsh

### /lib

系统的函数库非常的多，而/lib放置的则是在开机时会用到的函数库，
以及在/bin或/sbin底下的指令会调用的函数库。

[如图：发现]()
	
	关于 这里的cpp链接调用到了 /etc的cpp程序
	而那里的cpp又指向 /usr/bin的cpp
	其后继续链接跳转 最后指向一个 可执行程序 x86...-cpp-7


### /mnt

 如果妳想要暂时挂载某些额外的装置，一般建议妳可以放置到这个目录中。在早些时候，这个目录的用途与/media相同了。 只是有了/media之后，这个目录就用来暂时挂载用了。

 [注]mediamedia 是媒体的英文，这个/media底下放置的就是可移除的装置。 包括软碟、光碟、DVD等等装置都暂时挂载于此。 

### /opt 
这个是给第三方软体放置的目录 。 
另外，如果想要自行安装额外的软件(非原本的distribution提供的)，
那么也能够将你的软体安装到这里来。 
不过，以前的Linux系统中，我们还是习惯放置在/usr/local目录下。

### /root 
系统管理员(root)的家目录。 
之所以放在这里，是因为如果进入单人维护模式而仅挂载根目录时，
该目录就能够拥有root的家目录，所以我们会希望root的家目录与根目录放置在同一个分区中。

### /tmp 
这是让一般使用者或者是正在执行的程序暂时放置档案的地方。
这个目录是任何人都能够存取的，所以你需要定期的清理一下。
当然，重要资料不可放置在此目录啊。 
因为FHS甚至建议在开机时，应该要将/tmp下的资料都删除。