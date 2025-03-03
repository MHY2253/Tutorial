# [VPS服务器部署](https://github.com/cloud-fs/cloud-fs.github.io/releases) 

> ### 1.安装程序

```
wget https://github.com/cloud-fs/cloud-fs.github.io/releases/download/v0.8.3/clouddrive-2-linux-aarch64-0.8.3.tgz && tar -zxvf clouddrive-2-linux-aarch64-0.8.3.tgz && mv clouddrive-2-linux-aarch64-0.8.3 /usr/local/bin/clouddrive-2 && rm ~/clouddrive-2-linux-aarch64-0.8.3.tgz
```

> ### 2.配置开机启动
```
vim /etc/systemd/system/clouddrive.service
```
写入以下内容
```
[Unit]
Description=clouddrive service
Wants=network.target
After=network.target network.service

[Service]
Type=simple
WorkingDirectory=/usr/local/bin/clouddrive-2
ExecStart=/usr/local/bin/clouddrive-2/clouddrive server
KillMode=process

[Install]
WantedBy=multi-user.target
```
> ### 3.启动clouddrive

```
systemctl enable --now clouddrive
```
> ### 4.查看运行状态

```
systemctl status clouddrive
```

## OPENWRT软路由部署

> ### 1. 下载安装程序
```
wget https://github.com/cloud-fs/cloud-fs.github.io/releases/download/v0.7.21/clouddrive-2-linux-x86_64-0.7.21.tgz && tar -zxvf clouddrive-2-linux-x86_64-0.7.21.tgz && mv clouddrive-2-linux-x86_64-0.7.21 /usr/bin/clouddrive-2 && rm clouddrive-2-linux-x86_64-0.7.21.tgz
```
> ### 2. 配置开机启动
```
vim /etc/init.d/clouddrive
```
输入以下内容
```
#!/bin/sh /etc/rc.common
START=15
USE_PROCD=1

start_service() {
  procd_open_instance "clouddrive-2_service"
  procd_set_param command "/usr/bin/clouddrive-2/clouddrive"
  procd_close_instance
}
```


> ### 3. 赋予可执行权限并启动
```
chmod +x /etc/init.d/clouddrive && /etc/init.d/clouddrive start
```
> ### 4. 设置开机启动
```
/etc/init.d/clouddrive enable
```
> ### 5. 查看是否生效
```
ls -l /etc/rc.d
```
