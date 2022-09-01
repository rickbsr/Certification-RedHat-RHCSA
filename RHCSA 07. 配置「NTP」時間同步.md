# RHCSA 07. 配置「NTP」時間同步

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description



---

## Answer

#### Step 1. 配置「NTP」

```shell
vim /etc/chrony.conf
```

添加以下內容：

```
server classroom.example.com iburst

systemctl restart chronyd
```


###### 說明：

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q05_crontab.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`