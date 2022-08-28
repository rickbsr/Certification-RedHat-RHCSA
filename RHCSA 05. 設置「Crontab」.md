# RHCSA 05. 設置「Crontab」
---

![](https://github.com/rickbsr/RedHat_Certification/raw/main/RHCSA/pics/redhat-rhcsa.png?raw=true)

---

## Description

The user roger must configure a cron job that runs daily and executes the following command every 5 minutes between 7:00 to 8:00:

- /bin/echo "Good Morning" > /home/roger/morning-call

---

## Answer

#### Step 1. 


```shell
crontab -e -u roger 

*/5 7 * * * /bin/echo "Good Morning" > /home/roger/morning-call
```


#### Step 2. 驗證

---

###### tags: `Red Hat Certification` `RHCSA`