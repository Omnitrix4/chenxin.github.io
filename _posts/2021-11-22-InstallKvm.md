---
title: 安装kvm
tags: TeXt
toc:
  selectors: "h1,h2,h3,h4,h5"
image: 
  src: /chenxin.github.io
    

# Mathjax
mathjax: true
mathjax_autoNumber: true

# Mermaid
mermaid: true

# Chart
chart: true
typora-root-url: ..\chenxin.github.io\images
---







## 1.准备工作

因为我们需要在Linux下安装win10，而win10又需要比较大的内存和硬盘空间，所以需要我们的的内存和硬盘都要比较大，还需要有网络连接。

- 先安装好linux，我使用的版本是CentOS 7

- 内存建议3G起步，并且需要**勾选虚拟化引擎**

  ![image-20211121221252313](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256710.png)

  

- 在linux中安装win10,硬盘需要45G，如果够了就不需要再增加。因为我刚开始设置不够，所以加装了一块硬盘，加装后要记得去在linux上挂载

  ![image-20211121233453791](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256183.png)

  



### 增加硬盘并挂载

（如果硬盘大于45G，可以不用看这

Linux与Win系统在增加硬盘是有区别，当win插入一块新硬盘时，**我的电脑**会自动多一块如：U盘E之类的，而linux需要我们手动去挂载硬盘。



**1.**

![image-20211121221558251](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256941.png)

**2.**



![image-20211121221608307](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256202.png)



**3.**

![image-20211121221623286](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256501.png)

**4.**

![image-20211121221639029](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256803.png)



#### 挂载新硬盘

1.**查看磁盘占用情况**,此时并没有发现刚刚新增加的硬盘

```
df -h
```

![image-20211121234500736](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256505.png)

2.查找已经安装并且未格式化的磁盘,使用命令 fdisk -l 列出所有的磁盘

```
fdisk -l
```

![image-20211121234959450](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256675.png)

发现此时sdb还没有挂载和格式化



3.**格式化磁盘**

**3.1**

```
fdisk /dev/sdb
```

image-20211121235309267



**3.2** 再以此输入n,p

![image-20211121235409569](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271256872.png)

**3.3** 分区号这些都默认

![image-20211121235451873](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257045.png)

**3.4** 输入p，可以看到默认为sdb1

![image-20211121235757971](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257069.png)



**3.5** 再输入w，写入操作

![image-20211121235537881](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257080.png)



3.6输入命令 

```
mkfs.ext4 /dev/sdb1
```

 将sdb1分区设为 ext4 的文件系统格式。

![image-20211122000043172](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257839.png)



**4.挂载硬盘**

先创建一个新的目录，命名为data1，存放在data1中的数据实际上就是存放在新的硬盘上

![image-20211122000247489](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257086.png)

再挂载

```
 mount /dev/sdb1 /data1
```

![image-20211122000438810](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257422.png)

通过df -h 查看是否挂载成功

![image-20211122000520229](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257903.png)



**5.开机自动挂载**

通过

```
vim /etc/fstab
```

命令，进行编辑![image-20211122000744544](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257781.png)

先输入 **i**   切换成编辑模式 ，再末尾增加

```
/dev/sdb1 /data1 defaults 0 0
```

![image-20211122000943906](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257932.png)

再按Esc 输入`:wq`退出



通过`cat /etc/fstab` 进行查看

![image-20211122001245689](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257096.png)

**挂载新硬盘完毕**



## 2.安装KVM



==1.检查自己的centOS是否支持虚拟化==

加53**端口**

如果不支持的话，将这些打钩

![image-20211121220631534](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257147.png)



==2.查看是否加载KVM模块==

```
lsmod | grep kvm
```

![image-20211121231207487](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257425.png)

如果出现上述，说明已加载。

- 如果没有KVM模块，执行下面的语句

- ```
  modprobe kvm
  modprobe kvm-intel
  lsmod | grep kvm
  ```

  

==3.安装安装libvirt，virt-manage及kvm==

```
yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python python-virtinstlibvirt-client virt-install virt-viewer
```

出现下列消息，说明成功安装

![image-20211121231333989](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257886.png)



==4.使用virt-manager安装Win10==

输入命令

```
virt-manager
```

出现下图，说明安装virt-manager安装成功

![image-20211121231552054](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257333.png)





## 3.使用virt-manager安装win10

### 1.下载win10

推荐使用主机在[官网](https://www.microsoft.com/zh-cn/software-download/windows10ISO) 下载iso(如果是win电脑会出现让你更新，而不是下载iso，可以F12，然后切换成手机模式，再去下载)，然后再拖入linux桌面

有百度云会员也可以使用这个链接：https://pan.baidu.com/s/1N02korB0h9KUhuHnGBSseA 
提取码：qotj 





### 安装win10

`virt-manager`

![image-20211122002644609](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271257576.png)



![image-20211122002731369](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258117.png)



![image-20211122003007401](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258056.png)







![image-20211122003218677](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258158.png)



![image-20211122003235769](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258757.png)



### CPU建议最最低2G，不然真的卡死



### 给win10配置硬盘

![image-20211122003426842](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258066.png)

因为默认只剩下10GB，肯定不够，所以使用添加的前面第二块硬盘

![image-20211122003534151](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258087.png)



![image-20211122003546303](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258333.png)



![image-20211122003638984](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258994.png)

![image-20211122003656918](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258951.png)

![image-20211122003716582](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258783.png)



![image-20211122003730275](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258964.png)



![image-20211122003745110](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258235.png)



![image-20211122003801165](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271258077.png)



![image-20211122003823617](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271259182.png)



最后完成不出意外的话应该能行



下载







因为文件直接拖入linux桌面会损失，所以可以**在linux上下载**，或者**使用共享文件夹**

![image-20211122130323877](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300217.png)



### 创建共享文件夹

我的win10iso放在D盘的IDm下载里面

![image-20211122121440506](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300090.png)



![image-20211122121407466](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300972.png)



![image-20211122121351693](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300616.png)



![image-20211122121421027](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300414.png)



#### 运行linux系统

1.输入命令 `vmware-hgfsclient`

![image-20211122124951729](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300006.png)

出现上述共享目录设置成功

2.创建目录 ，并挂载

`mkdir /sharewin`

![image-20211122125205067](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300420.png)



3.在命令行输入下列命令 手动挂载

`vmhgfs-fuse .host:/IDM下载 /sharewin`

![image-20211122125325370](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300994.png)

可以看到 打开/sharewin文件夹，已经可以看到D盘下的文件

4.永久挂载 输入命令``vim /etc/fstab`

在插入：

`.host:/IDM下载 /sharewin fuse.vmhgfs-fuse allow_other,defaults 0 0`

![image-20211122125532198](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271300822.png)



5.再输入`mount -a` 是挂载立即生效



![image-20211122125636330](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271301901.png)

如果出现上述说明成功



### 移动iso

因为直接使用/sharewin文件夹下的iso安装会报错，并没有找到解决方法，所以将/sharewin下的win10移动到 linux目录下有比较大的空间的目录（我放在\data1文件夹下）

1.输入`mv win.iso /data1`，（iso的名字太长了，我重命名了

![image-20211122130013850](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271301918.png)

2.接下来只要在linux目录下找到iso就可以安装了

![image-20211122130244668](https://gitee.com/chenxinnnn/learn_images/raw/master/img/202111271301156.png)

