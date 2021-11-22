---
title: 安装kvm
tags: TeXt
toc:
  selectors: "h1,h2,h3,h4,h5"
image: /chenxin.github.io
    
typora-root-url: ..
# Mathjax
mathjax: true
mathjax_autoNumber: true

# Mermaid
mermaid: true

# Chart
chart: true

---







---
typora-copy-images-to: ..\GithubLib\GitHubPage\chenxin.github.io\images
---

## 1.准备工作

因为我们需要在Linux下安装win10，而win10又需要比较大的内存和硬盘空间，所以需要我们的的内存和硬盘都要比较大，还需要有网络连接。

- 先安装好linux，我使用的版本是CentOS 7

- 内存建议3G起步，并且需要**勾选虚拟化引擎**

  ![image-20211121221252313](/chenxin.github.io/images/image-20211121221252313-1637572459679.png)

  

- 在linux中安装win10,硬盘需要45G，如果够了就不需要再增加。因为我刚开始设置不够，所以加装了一块硬盘，加装后要记得去在linux上挂载

  ![image-20211121233453791](/images/image-20211121233453791-1637572463151.png)

  



### 增加硬盘并挂载

（如果硬盘大于45G，可以不用看这

Linux与Win系统在增加硬盘是有区别，当win插入一块新硬盘时，**我的电脑**会自动多一块如：U盘E之类的，而linux需要我们手动去挂载硬盘。



**1.**

![image-20211121221558251](/images/image-20211121221558251-1637572465819.png)

**2.**



![image-20211121221608307](/images/image-20211121221608307-1637572468338.png)



**3.**

![image-20211121221623286](/images/image-20211121221623286-1637572470738.png)

**4.**

![image-20211121221639029](/images/image-20211121221639029-1637572477727.png)



#### 挂载新硬盘

1.**查看磁盘占用情况**,此时并没有发现刚刚新增加的硬盘

```
df -h
```

![image-20211121234500736](/images/image-20211121234500736-1637572479795.png)

2.查找已经安装并且未格式化的磁盘,使用命令 fdisk -l 列出所有的磁盘

```
fdisk -l
```

![image-20211121234959450](/images/image-20211121234959450-1637572484239.png)

发现此时sdb还没有挂载和格式化



3.**格式化磁盘**

**3.1**

```
fdisk /dev/sdb
```





**3.2** 再以此输入n,p

![image-20211121235409569](/images/image-20211121235409569-1637572487209.png)

**3.3** 分区号这些都默认

![image-20211121235451873](/images/image-20211121235451873-1637572493523.png)

**3.4** 输入p，可以看到默认为sdb1

![image-20211121235757971](/images/image-20211121235757971-1637572495473.png)



**3.5** 再输入w，写入操作

![image-20211121235537881](/images/image-20211121235537881-1637572497622.png)



3.6输入命令 

```
mkfs.ext4 /dev/sdb1
```

 将sdb1分区设为 ext4 的文件系统格式。

![image-20211122000043172](/images/image-20211122000043172-1637572500932.png)



**4.挂载硬盘**

先创建一个新的目录，命名为data1，存放在data1中的数据实际上就是存放在新的硬盘上

![image-20211122000247489](/images/image-20211122000247489.png)

再挂载

```
 mount /dev/sdb1 /data1
```

![image-20211122000438810](/images/image-20211122000438810.png)

通过df -h 查看是否挂载成功

![image-20211122000520229](../GithubLib/GitHubPage/chenxin.github.io/images/image-20211122000520229.png)



**5.开机自动挂载**

通过

```
vim /etc/fstab
```

命令，进行编辑![image-20211122000744544](../GithubLib/GitHubPage/chenxin.github.io/images/image-20211122000744544.png)

先输入 **i**   切换成编辑模式 ，再末尾增加

```
/dev/sdb1 /data1 defaults 0 0
```

![image-20211122000943906](../GithubLib/GitHubPage/chenxin.github.io/images/image-20211122000943906.png)

再按Esc 输入`:wq`退出



通过`cat /etc/fstab` 进行查看

![image-20211122001245689](../GithubLib/GitHubPage/chenxin.github.io/images/image-20211122001245689.png)

**挂载新硬盘完毕**



## 2.安装KVM



==1.检查自己的centOS是否支持虚拟化==

加53**端口**

如果不支持的话，将这些打钩

![image-20211121220631534](/images/image-20211121220631534.png)



==2.查看是否加载KVM模块==

```
lsmod | grep kvm
```

![image-20211121231207487](/images/image-20211121231207487.png)

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

![image-20211121231333989](/images/image-20211121231333989.png)



==4.使用virt-manager安装Win10==

输入命令

```
virt-manager
```

出现下图，说明安装virt-manager安装成功

![image-20211121231552054](/images/image-20211121231552054.png)





## 3.使用virt-manager安装win10

### 1.下载win10

推荐使用主机在[官网](https://www.microsoft.com/zh-cn/software-download/windows10ISO) 下载iso(如果是win电脑会出现让你更新，而不是下载iso，可以F12，然后切换成手机模式，再去下载)，然后再拖入linux桌面

有百度云会员也可以使用这个链接：https://pan.baidu.com/s/1N02korB0h9KUhuHnGBSseA 
提取码：qotj 





### 安装win10

`virt-manager`

![image-20211122002644609](/images/image-20211122002644609.png)



![image-20211122002731369](/images/image-20211122002731369.png)



![image-20211122003007401](/images/image-20211122003007401.png)







![image-20211122003218677](/images/image-20211122003218677.png)



![image-20211122003235769](/images/image-20211122003235769.png)



### CPU建议最最低2G，不然真的卡死



### 给win10配置硬盘

![image-20211122003426842](/images/image-20211122003426842.png)

因为默认只剩下10GB，肯定不够，所以使用添加的前面第二块硬盘

![image-20211122003534151](/images/image-20211122003534151.png)



![image-20211122003546303](/images/image-20211122003546303.png)



![image-20211122003638984](/images/image-20211122003638984.png)

![image-20211122003656918](/images/image-20211122003656918.png)

![image-20211122003716582](/images/image-20211122003716582.png)



![image-20211122003730275](/images/image-20211122003730275.png)



![image-20211122003745110](/images/image-20211122003745110.png)



![image-20211122003801165](/images/image-20211122003801165.png)



![image-20211122003823617](/images/image-20211122003823617.png)



最后完成不出意外的话应该能行

![image-20211119225521807](file://C:\Users\%E9%99%88%E9%91%AB\AppData\Roaming\Typora\typora-user-images\image-20211119225521807.png?lastModify=1637512751)

下载







因为文件直接拖入linux桌面会损失，所以可以**在linux上下载**，或者**使用共享文件夹**

![image-20211122130323877](/images/image-20211122130323877.png)



### 创建共享文件夹

我的win10iso放在D盘的IDm下载里面

![image-20211122121440506](/images/image-20211122121440506.png)



![image-20211122121407466](/images/image-20211122121407466.png)



![image-20211122121351693](/images/image-20211122121351693.png)



![image-20211122121421027](/images/image-20211122121421027.png)



#### 运行linux系统

1.输入命令 `vmware-hgfsclient`

![image-20211122124951729](/images/image-20211122124951729.png)

出现上述共享目录设置成功

2.创建目录 ，并挂载

`mkdir /sharewin`

![image-20211122125205067](/images/image-20211122125205067.png)



3.在命令行输入下列命令 手动挂载

`vmhgfs-fuse .host:/IDM下载 /sharewin`

![image-20211122125325370](/images/image-20211122125325370.png)

可以看到 打开/sharewin文件夹，已经可以看到D盘下的文件

4.永久挂载 输入命令``vim /etc/fstab`

在插入：

`.host:/IDM下载 /sharewin fuse.vmhgfs-fuse allow_other,defaults 0 0`

![image-20211122125532198](/images/image-20211122125532198.png)



5.再输入`mount -a` 是挂载立即生效



![image-20211122125636330](/images/image-20211122125636330.png)

如果出现上述说明成功



### 移动iso

因为直接使用/sharewin文件夹下的iso安装会报错，并没有找到解决方法，所以将/sharewin下的win10移动到 linux目录下有比较大的空间的目录（我放在\data1文件夹下）

1.输入`mv win.iso /data1`，（iso的名字太长了，我重命名了

![image-20211122130013850](/images/image-20211122130013850.png)

2.接下来只要在linux目录下找到iso就可以安装了

![image-20211122130244668](/images/image-20211122130244668.png)
