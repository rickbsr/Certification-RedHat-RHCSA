# RHCSA 02. 配置「YUM」儲存庫

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

請配置「YUM」儲存庫，儲存庫的「url」如下：

- `http://content.example.com/rhel8.2/x86_64/dvd/BaseOS`
- `http://content.example.com/rhel8.2/x86_64/dvd/AppStream`

###### 提示：將配置內容存放在檔案「`/etc/yum.repos.d/exam.repo`」之中。
###### 提示：不須確認「GPG signatures」。

---

## Answer

#### Step 1. 建立「exam.repo」

在題目所指定的目錄下依敘述建立「`exam.repo`」，指令如下：

```shell
touch /etc/yum.repos.d/exam.repo
```

完成後，建議以指令：「`ls`」確認執行結果，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_touch_repo.png?raw=true)


#### Step 2. 編輯「exam.repo」的內容

在「Step 1」建立的「`exam.repo`」中，輸入以下內容：

```properties
[BaseOS]
name=RedHat Exam BaseOS
baseurl=http://content.example.com/rhel8.2/x86_64/dvd/BaseOS
enabled=1
gpgcheck=0

[AppStream]
name=RedHat Exam AppStream
baseurl=http://content.example.com/rhel8.2/x86_64/dvd/AppStream
enabled=1
gpgcheck=0
```

###### 說明：儲存庫的配置設定中，「name」的「值」可自行定義，該內容僅供辨識用。

在檔案編輯完成以後，建議使用指令「`cat`」確認，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_config_repo.png?raw=true)

#### Step 3. 驗證

本題的驗證方式可以藉由「`repolist`」指令來查看「儲存庫」的「狀態列表」，指令如下：

```shell
yum repolist all
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_verify.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`