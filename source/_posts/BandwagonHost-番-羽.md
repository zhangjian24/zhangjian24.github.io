---
title: 'BandwagonHost-番#羽'
date: 2018-09-08 12:45:40
copyright: true
comments: true
tags:
  - vpn
categories:
  - 工具
  - 网络
---

# 国外服务器

## 注册账号

[BandwagonHost官网](https://www.bwh1.net/clientarea.php)

{% asset_img 注册账号.png 注册账号 %}

## 购买服务器

- 点击`VPS Hosting`, 选择`$19.99` 下面的`order kvm` ;

  {% asset_img 购买服务器.jpg 购买服务器 %}

- 然后点击 `Add Cart`, 也就是 `加入购物车` 的意思;

- 然后点击`Checkout`, 也就是`结算` ;

- 选择 `支付宝` 支付，完成订单；

   {% asset_img 支付.png 支付 %}


- 接下来的页面，点解`pay now` ，进行支付宝付款，就购买完成。

## 配置服务器

- 登录网站，`client area` -> `my services` -> `control panel`  ，进入kvm 管理界面 ;

  {% asset_img 配置服务器.png 配置服务器 %}

- 默认安装的是centos，个人更习惯Ubuntu，先在 `main controls` 里面`stop` 掉机器，然后 `install new os` 可以选择安装Ubuntu系统；

- 然后，会收到邮件，告知，root密码，ssh端口；

  {% asset_img 邮件通知.png 邮件通知 %}

# shadow-socks配置

## 服务端

- 安装

```shell
apt-get install python-pip
pip install shadowsocks
```



- 使用



 ```shell
ssserver -p 443 -k password -m rc4-md5
 ```

  

如果要后台运行：

  ```shell
sudo ssserver -p 443 -k password -m rc4-md5 --user nobody -d start
  ```

  

如果要停止：

  ```shell
sudo ssserver -d stop

  ```

 

 如果要检查日志：

```shell
sudo less /var/log/shadowsocks.log
```



- 报错



```
AttributeError: /usr/local/ssl/lib/libcrypto.so.1.1: undefined symbol: EVP_CIPHER_CTX_cleanup
```

 

vim打开文件openssl.py

> 路径不同根据报错路径而定

 修改libcrypto.EVP_CIPHER_CTX_cleanup.argtypes

`:%s/cleanup/reset/`

`:x`

> 以上两条为VIM命令， 替换文中**libcrypto.EVP_CIPHER_CTX_cleanup.argtypes** 为**libcrypto.EVP_CIPHER_CTX_reset.argtypes **共两处，并保存



重新运行

## 客户端

github 上下载window客户端

{% asset_img 客户端1.png 客户端1 %}
{% asset_img 客户端配置.png 客户端配置 %}
ubuntu客户端:

```shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

debiancn源
```shell
echo "deb https://repo.debiancn.org/ testing main" | sudo tee /etc/apt/sources.list.d/debiancn.list;
wget https://repo.debiancn.org/pool/main/d/debiancn-keyring/debiancn-keyring_0~20161212_all.deb -O /tmp/debiancn-keyring.deb;
sudo apt install /tmp/debiancn-keyring.deb;
sudo apt update;
rm /tmp/debiancn-keyring.deb;
```
https://github.com/debiancn/repo
