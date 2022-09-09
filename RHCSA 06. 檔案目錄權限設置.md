# RHCSA 06. 檔案目錄權限設置

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

建立「`/home/rhcsa`」目錄，並依照以下條件配置該目錄的權限：

- 目錄「`/home/rhcsa`」的群組權限是「manager」。
- 僅該目錄的擁有者、群組用戶，擁有「讀取」、「寫入」以及「訪問」的權限。
- 在該目錄下所創建的所有「檔案」及「資料夾」，都會被自動配置上群組權限為「manager」。

---

## Answer

#### Step 1. 建立資料夾

依題目敘述建立資料夾：「`/home/rhcsa`」，指令如下：

```shell
# 創建資料夾
mkdir -p /home/rhcsa
```

#### Step 2. 設定資料夾的管理權限

將該目錄的群組權限設置為「manager」，指令如下：

```shell
chown :manager /home/rhcsa
```

指令「chown」可以改變「檔案」與「目錄」的存取權限；「`:`」的意思代表後面接的是「群組」。

接著，依照題目的敘述，該目錄的僅「擁有者」與「群組用戶」都需擁有「讀取」、「寫入」和「訪問」的權限；此外，題目還要求在該目錄下所創建的所有「檔案」及「資料夾」，都會被自動配置上群組權限為「manager」。

指令如下：

```shell
chmod 2770 /home/rhcsa
```

上述指令中，「770」代表的是「rwx」權限，而「770」意思是「user」與「group」都具有「rwx」權限，但「other」不具有任何權限。

而「2」代表的是「SetGID」的意思，它是一種「特殊權限」，若對「目錄」設置「SetGID」，意即在該「目錄」下所建立之檔案的「群組權限」會變得與「目錄」相同。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q06_chmod_rhcsa.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`