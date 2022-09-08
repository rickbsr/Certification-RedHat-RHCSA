# RHCSA 01. 設定「Hostname」與配置連線參數

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

請設定「Hostname」與配置連線參數，配置內容如下：

- ###### Hostname: `exam.example.com`

- ###### IP address: `172.25.250.10`

- ###### Netmask: `255.255.255.0`

- ###### Gateway: `172.25.250.10`

- ###### DNS: `172.25.250.10`

---

## Answer

#### Step 1. 修改「Hostname」

依題目敘述，將「Hostname」更改為「`exam.example.com`」，指令如下：

```shell
hostnamectl set-hostname exam.example.com
```

另外，在異動「Hostname」的前後，會建議使用「`hostname`」指令來確認「Hostname」是否修改成功，其操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_set_hostname.png?raw=true)

#### Step 2. 配置連線參數

接著是配置網路連線參數，也就是修改「Connection」的內容。

若要修改「Connection」的內容，就必須先取得目標「Connection」的「名稱」，而查詢指令如下：

```shell
nmcli con show
```

畫面截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_show.png?raw=true)

根據顯示內容，我們可以得知當前「Connection」的「Name」是「`Wired connection 1`」。

接著，根據「連線名稱」並依題目要求逐一設置網路連線參數，指令如下：

```shell
# 修改「IP address」& 「Netmask」
nmcli con mod "Wired connection 1" ipv4.addresses 172.25.250.10/24

# 修改「Gateway」
nmcli con mod "Wired connection 1" ipv4.gateway 172.25.250.10

# 修改「Dns」
nmcli con mod "Wired connection 1" ipv4.dns 172.25.250.10
```

上面的指令中，「`ipv4.addresses`」項目的配置值是「`172.25.250.10/24`」；其中，「`/`」前是「IP Address」，而「`/`」後是「子網路遮罩」的「設定值」；而「`24`」的意思即「`255.255.255.0`」。

在配置完所有題目指定的連線參數以後，其實還有兩個設定須要配置。

第一個是「`ipv4.method`」，須將之改為「`manual`」；然後是「`autoconnect`」，須設為「`yes`」；如此一來，該連線設定在重啟時才會生效，指令如下：

```shell
# 修改「Method」
nmcli con mod "Wired connection 1" ipv4.method manual

# 修改「Auto-Connect」
nmcli con mod "Wired connection 1" autoconnect yes
```

完成後，可以藉由指令「`nmcli con show`」來確認異動的內容，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_mod.png?raw=true)

#### Step 3. 重啟

為了讓異動後的網路配置生效，我們須重啟「Connection」，指令如下：

```shell
nmcli con up "Wired connection 1"
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_up.png?raw=true)

#### Step 4. 驗證

在重啟連線後，使用指令「`ip a`」，就可以確認「IP Address」與「Netmask」是否有修改成功，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_verify.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`