# RHCSA 04. 使用者、群組管理

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

Create the following users, groups, and group memberships:

- A group named manager.
- A user nasun who belongs to manager as a secondary group.
- A user roger who also belongs to manager as a secondary group.
- A user wayne who does not have access to an interactive shell on the system, and who is not a member of manager.
- Nasun, roger, and wayne should all have the password of "redhat".

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

在「Linux」系統中，我們可以針對「使用者」設定「主要群組」和「次要群組」，依照題目的要求，我們要將「manager」群組新增為「nasun」和「roger」的「次要群組」，因此，我們藉由指令「`usermod -aG`」來達到該需求，如下：

```shell
# nasun & roger boths belongs to manager as a secondary group
usermod -aG	manager nasun
usermod -aG	manager roger
```

###### 說明：在「`usermod`」中，參數「g」代表修改使用者的主要群組，而參數「Ｇ」，則是代表修改使用者的次要群組；另外，參數「a」的意思則是代表「新增」，通常搭配「Ｇ」使用，意即「新增次要群組」。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_group_manager.png?raw=true)

此外，題目還要求將「wayne」設置為「無法登入」，因此我們就須將「wayne」加入「`/sbin/nologin`」檔案中，指令如下：

```shell
# wayne does not have access to an interactive shell on the system
usermod -s "/sbin/nologin" wayne
```

###### 說明：在「usermod」中，參數「s」代表與實際檔案有關；而「/sbin/nologin」則是個實際檔案，當使用者被加入這個檔案中，就代表該使用者「無法登入」。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_nologin.png?raw=true)

#### Step 4. 設定使用者密碼

逐一為使用者設定密碼

```shell
echo "redhat" | passwd --stdin nasun
echo "redhat" | passwd --stdin roger
echo "redhat" | passwd --stdin wayne
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_ch_pwd.png?raw=true)

---

###### tags: `Red Hat Certification` `RHCSA`