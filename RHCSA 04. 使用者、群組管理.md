# RHCSA 04. 使用者、群組管理

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

請依照以下條件創建「使用者」、「群組」，並設置相關權限：

- 建立一名稱為「manager」的群組。
- 使用者「nasun」為「manager」的成員，該群組是「nasun」的次要群組。
- 使用者「roger」同樣為「manager」的成員，該群組同樣是「roger」的次要群組。
- 使用者「wayne」沒有權限訪問系統上的「Shell」，此外，「wayne」也非「manager」的成員。
- 使用者「nasun」、「roger」和「wayne」的「使用者密碼」皆設為「`redhat`」。

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

在指令「`usermod`」的中，修改「群組」的參數分別是大寫的「Ｇ」，與小寫的「g」；前者是修改的是「主要群組」，而後者則是「次要群組」。

此外，在「Linux」中，由於使者用可以擁有多個「次要群組」，因此，倘若用戶的需求是「新增」一個「次要群組」，而非異動原本既有的群組，那麼，那就使用參數「aG」；「a」是新增的意思，常搭配參數「Ｇ」使用，意即「新增次要群組」。

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q04_group_manager.png?raw=true)

此外，題目還要求將「wayne」設置成無權限操作「Shell」。

其作法就是將「wayne」，加入「`/sbin/nologin`」檔案中，指令如下：

```shell
# wayne does not have access to an interactive shell on the system
usermod -s "/sbin/nologin" wayne
```

在指令「`usermod`」中，參數「s」通常是與實際存在的「檔案」有關；而「`/sbin/nologin`」就是個實際存在的檔案，當使用者被加入這個檔案中，就代表該使用者「無法登入」。

代表與實際檔案有關；而「`/sbin/nologin`」則是個實際檔案，當使用者被加入這個檔案中，就代表該使用者「無法登入」。

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

###### tags: `rhcsa` `redhat` `linux`