### 红米 note4x (mido) 

.  

### 重刷 postmarketOS

---

1. 下载 [Edge镜像](https://images.postmarketos.org/bpo/edge/xiaomi-mido/) 

2. 下载后分别解压为 i.img boot.img lk2nd.img

3. 手机 音量键下 + 电源键进入 fastboot

4. fastboot命令按顺序刷入

   ```sh
   fastboot flash userdata i.img
   fastboot flash boot boot.img
   fastboot flash boot lk2nd.img
   ```

5. 默认密码: 147147

.     

### postmarketOS 开局

---

> 以下命令默认为root用户执行,请 'sudo -i' 切换用户或命令前加 'sudo'

#### 启动 sshd 并添加到开机自启

```sh
rc-service sshd start
rc-update add sshd
```

#### 加入到sudo

```sh
 echo "user  ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-sb
```

#### 换源-更新源

```sh
sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
apk update
```

#### 安装必备软件

```sh
apk add vim 
```

#### 配置中文

```sh
apk add font-noto-cjk
```

```sh
vim /etc/environment
```

```ini
LANG=zh_CN.UTF-8
LC_CTYPE="zh_CN.UTF-8"
LC_NUMERIC="zh_CN.UTF-8"
LC_TIME="zh_CN.UTF-8"
LC_COLLATE="zh_CN.UTF-8"
LC_MONETARY="zh_CN.UTF-8"
LC_MESSAGES="zh_CN.UTF-8"
LC_PAPER="zh_CN.UTF-8"
LC_NAME="zh_CN.UTF-8"
LC_ADDRESS="zh_CN.UTF-8"
LC_TELEPHONE="zh_CN.UTF-8"
LC_MEASUREMENT="zh_CN.UTF-8"
LC_IDENTIFICATION="zh_CN.UTF-8"
LC_ALL=
```

#### 修改为bash(可选)

```sh
vim /etc/passwd
```

> root 和 user 修改为/bin/bash

#### 设置时区

```sh
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

> 验证 : date -R

.  

### 踩坑

---

自带输入法无中文

三大金刚键未适配

phosh桌面 输入法无法关闭? -长按底部白条关闭或弹出

firefox 在本地桌面闪屏

mido 移动数据目前处于部分实施状态 -[参照](https://wiki.postmarketos.org/wiki/Devices)

