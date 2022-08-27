# RHCSA 02. RHCSA 02. 配置「YUM」儲存庫

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

Configure your system to use default repositories from below:

- `http://content.example.com/rhel8.2/x86_64/dvd/BaseOS`
- `http://content.example.com/rhel8.2/x86_64/dvd/AppStream`

###### Info: Configure the repository in the `/etc/yum.repos.d/exam.repo` file.
###### Info: Do not check GPG signatures.

---

## Answer

#### Step 1. 建立「exam.repo」

在題目所指定的目錄下依題目敘述建立「`exam.repo`」，指令如下：

```shell
touch /etc/yum.repos.d/exam.repo
```

完成後，建議以指令：「`ls`」確認一下執行結果，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_touch_repo.png?raw=true)


#### Step 2. 編輯「exam.repo」的內容

在剛建立的「`exam.repo`」輸入以下內容：

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

###### 說明：上述「Repo Config」的設定中，「name」的「值」可自行定義，該內容僅供辨識用。

在內容編輯完成後，建議用指令「`cat`」確認，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_config_repo.png?raw=true)

#### Step 3. 驗證

我們可以指令：「`repolist`」來查看「Repo」的狀態清單，指令如下：

```shell
yum repolist all
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q02_verify.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`