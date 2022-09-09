# RHCSA 09. 設置文件的「ACL」權限

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

請依照以下敘述設置檔案「`/var/tmp/fstab`」的「ACL」權限：

- The file `/var/tmp/fstab` is owned by the root user.
- The file `/var/tmp/fstab` belongs to the group root.
- The file `/var/tmp/fstab` should not be executable by anyone.
- The user nasun is able to read and write `/var/tmp/fstab`.
- The user roger can neither write nor read `/var/tmp/fstab`.
- All other users (current or future) have the ability to read `/var/tmp/fstab`.

---

## Answer

#### Step 1. 複製「fstab」

依題目敘述，將檔案「`/etc/fstab`」複製一份至「`/var/tmp/fstab`」，指令如下：

```shell
cp /etc/fstab /var/tmp/fstab
```

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q04_ch_pwd.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`