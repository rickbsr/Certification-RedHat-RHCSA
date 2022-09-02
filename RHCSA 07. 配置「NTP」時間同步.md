# RHCSA 07. 配置「NTP」時間同步

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

配置您的系統，使其成為「`classroom.example.com`」 的「NTP」客戶端。

---

## Answer

#### Step 1. 配置「NTP」

關於「NTP」的配置，其方式是修該「`/etc/chrony.conf`」，用「vim」開啟後，加入以下內容：

```
server classroom.example.com iburst
```

截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q07_chrony_content.png?raw=true)

使生效，指令如下：

```
systemctl restart chronyd
```

完成後可以使用指令「`chronyc sources -c`」來驗證，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q07_chrony.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`