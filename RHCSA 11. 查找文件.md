# RHCSA 10. 配置使用者帳戶

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description



---

## Answer

#### Step 1. 建立「Group」

依題目敘述，建立一個名為「manager」的「群組」，指令如下：

```shell
groupadd manager
```

#### Step 2. 建立「User」

同樣依題目敘述，依序建立三個使用者帳戶，分別為「nasun」、「roger」和「wayne」，指令如下：

```shell
useradd nasun
useradd roger
useradd wayne
```

#### Step 3. 設定使用者的權限

在「Linux」系統中，「使用者」可以屬於多個，而且可以分為「主要群組」和「次要群組」兩種。

而題目要求我們要將「manager」群組新增為「nasun」和「roger」的「次要群組」，指令如下：

```shell
# nasun & roger boths belongs to manager as a secondary group
usermod -aG	manager nasun
usermod -aG	manager roger
```

###### 說明：在「`usermod`」指令的參數中，小寫的參數「g」代表修改使用者的「主要群組」，而大寫的參數「Ｇ」則是代表修改使用者的「次要群組」；此外，在「Linux」中，使用者可以同時屬於多個「次要群組」，因此，若是要「新增」次要群組，而非「修改」，可以使用參數「a」，其意思則是代表「新增」，通常搭配「Ｇ」使用，意即「新增次要群組」。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q04_group_manager.png?raw=true)

此外，題目還要求將「wayne」設置成「無法登入」，其意思也就是將該用戶，也就是「wayne」，加入「`/sbin/nologin`」檔案中，指令如下：

```shell
# wayne does not have access to an interactive shell on the system
usermod -s "/sbin/nologin" wayne
```

###### 說明：在「`usermod`」中，參數「s」代表與實際檔案有關；而「`/sbin/nologin`」則是個實際檔案，當使用者被加入這個檔案中，就代表該使用者「無法登入」。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q04_nologin.png?raw=true)

#### Step 4. 設定使用者密碼

逐一為使用者設定密碼，指令如下：

```shell
echo "redhat" | passwd --stdin nasun
echo "redhat" | passwd --stdin roger
echo "redhat" | passwd --stdin wayne
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q04_ch_pwd.png?raw=true)

---

###### tags: `RHCSA` `RedHat` `Linux`