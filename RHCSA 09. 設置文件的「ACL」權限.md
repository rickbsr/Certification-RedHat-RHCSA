# RHCSA 09. 設置文件的「ACL」權限

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

請依照以下敘述設置檔案「`/var/tmp/fstab`」的「ACL」權限：

- 將檔案「`/var/tmp/fstab`」的擁有者設置成「root」。
- 將檔案「`/var/tmp/fstab`」的群組設置成「root」。
- 將檔案「`/var/tmp/fstab`」的設置為任何人都無法「執行」。
- 使用者「nasun」擁有檔案「`/var/tmp/fstab`」的「讀取」和「寫入」權限。
- 使用者「roger」沒有檔案「`/var/tmp/fstab`」的「讀取」和「寫入」權限。
- 其它使用者僅擁有檔案「`/var/tmp/fstab`」的「讀取」權限。

---

## Answer

#### Step 1. 複製「fstab」

依題目敘述，將檔案「`/etc/fstab`」複製一份至「`/var/tmp/fstab`」，指令如下：

```shell
cp /etc/fstab /var/tmp/fstab
```

完成後，建議用「`ls`」確認一下，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q09_cp_fstab.png?raw=true)

#### Step 2. 設置檔案的存取權限

先依照題目敘述，將「`/var/tmp/fstab`」的「擁有者」設置為「root」；同時也將該檔案的群組設置為「root」，指令如下：

```shell
chown root:root /var/tmp/fstab
```

上述指令中，「`root`」代表的是「root user」，而「`:root`」代表的則是「root group」。

接著，將「`/var/tmp/fstab`」設置任何人都無法「執行」，且「other」僅唯讀，指令如下：

```shell
chown 664 /var/tmp/fstab
```

上述指令中，「6」代表的是「rw-」，也就是僅不能「執行」；而「4」代表的則是「r--」，也就是「唯讀」。

設置完成後，可以用指令：「`ls -l`」確認一下「`/var/tmp/fstab`」的檔案狀態，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q09_chown.png?raw=true)

#### Step 3. 設置檔案的「ACL」

接著是針對特定使用者的「客製化」權限設定，這時候就無法使用傳統的「Linux」權限配置方式來處理，而是需要藉由「ACL」權限來達成。

首先是「nasun」的部分，題目的需求是「nasun」擁有檔案「`/var/tmp/fstab`」的「讀取」和「寫入」權限，指令如下：

```shell
setfacl -m u:nasun:rw /var/tmp/fstab
```

接著是「roger」的部分，他沒有檔案「`/var/tmp/fstab`」的任何權限，指令如下：

```shell
setfacl -m u:roger:- /var/tmp/fstab
```

如上，「ACL」權限的設置指令是「`setfacl -m`」，其中，參數「m」是「modify」的意思；而「u」代表「user」，而「g」則代表「group」。

完成後可以藉由「`getfacl`」確認一下「`/var/tmp/fstab`」的檔案狀態，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q09_acl.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`