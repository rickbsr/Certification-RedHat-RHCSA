# RHCSA 06. 檔案目錄權限設置.md

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

創建一個資料夾：「`/home/rhcsa`」，並依照以下條件設置權限：

- Group ownership of `/home/rhcsa` is manager.
- The directory should be readable, writable, and accessible to members of manager and to the user owner, but not to any other user (It is understood that root has access to all files and directories on the system).
- Files created in `/home/rhcsa` automatically have group ownership set to the manager group.

---

## Answer

#### Step 1. 建立資料夾

依題目敘述建立資料夾：「`/home/rhcsa`」，指令如下：

```shell
# 創建資料夾
mkdir -p /home/rhcsa
```

#### Step 2. 設定資料夾的管理權限

將群組「manager」設為該目錄的「Ownership」，指令如下：

```shell
chown :manager /home/rhcsa
```

###### 說明：「chown」可以改變檔案目錄的擁有者、群組，但群組須在前面加上「`:`」以代表為群組。

接著是設定資料夾「rwx」權限，依照題目敘述，該檔案除了「other」用戶之外，應該都要具有，「讀取」、「寫入」和「執行」的權限；此外，題目還要求在該「目錄」下所建立之檔案的「Groups」會變得和「目錄」相同；因此，指令如下：

```shell
# The dir should be readable, writable, and accessible to members of manager and to the user owner, but not to any other user
# Files created in `/home/rhcsa` automatically have group ownership set to the manager group
chmod 2770 /home/rhcsa
```

###### 說明：關於「2770」的解讀，要分為「2」與「770」來看；前者表示的是「特殊權限」，「2」的意思是特殊權限中的「SetGID」，若其針對「目錄」設置，意即在該「目錄」下所建立之檔案的「Groups」會變得與「目錄」相同；而後者則是表示檔案的「rwx」權限，而「770」意思是「user」與「group」都具有「rwx」權限，但「other」不具有任何權限。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q06_chmod_rhcsa.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`