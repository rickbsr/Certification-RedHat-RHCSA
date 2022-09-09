# RHCSA 10. 配置使用者帳戶

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

將使用者「johb」的用戶「Id」設置為「`3456`」，並將之密碼設為「`redhat`」。

---

## Answer

#### Step 1. 修改使用者「Id」

修改使用者「john」的用戶「Id」，指令如下：

```shell
usermod -u 3456 john
```

建議修改前後可以藉由指令「`id john`」來確認一下，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q10_ch_id.png?raw=true)

#### Step 2.修改使用者密碼

指令如下：

```shell
echo "redhat" | passwd --stdin john
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q10_ch_pwd.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`