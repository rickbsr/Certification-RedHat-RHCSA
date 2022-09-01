# RHCSA 05. 設置「Crontab」

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

替使用者「roger」配置一個「Crontab」，在每天早上七點至八點之間，每五分鐘執行一次以下命令：

- /bin/echo "Good Morning"

---

## Answer

#### Step 1. 配置「Crontab」

```shell
crontab -u roger -e 
```

並輸入以下內容：

```
*/5 7 * * * /bin/echo "Good Morning" 
```

###### 說明：在「crontab」中，其五個星號依序代表「分、時、日、月、週」；上述內容中的「`*/5`」代表每「5」分鐘，而「7」代表上午七點。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q05_crontab.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`