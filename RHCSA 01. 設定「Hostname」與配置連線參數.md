# RHCSA 01. Configure network settings

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

Configure primary to have the following network configuration:

- ###### Hostname: `exam.example.com`

- ###### IP address: `172.25.250.10`

- ###### Netmask: `255.255.255.0`

- ###### Gateway: `172.25.250.10`

- ###### Name server（DNS）: `172.25.250.10`

---

## Answer

#### Step 1. 修改「Hostname」

依題目敘述，將「hostname」更改為「`exam.example.com`」，指令如下：

```shell
hostnamectl set-hostname exam.example.com
```

另外，在異動「hostname」的前後，會建議使用指令：「`hostname`」來確認「hostname」是否修改成功，其操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_set_hostname.png?raw=true)

#### Step 2. 配置「Connection」的配置內容

依題目需求，我們接著要去配置網路連線參數，也就是修改「Connection」的內容，因此，我們必須先取得目標「Connection」的「con-name」，而查詢的指令如下：

```shell
nmcli con show
```

結果如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_show.png?raw=true)

根據截圖的畫面，我們可以得知當前「Connection」的「con-name」是「`Wired connection 1`」；接著就是依照題目需求來配置網路連線參數，指令如下：

```shell
# 修改「IP address」& 「Netmask」
nmcli con mod "Wired connection 1" ipv4.addresses 172.25.250.10/24

# 修改「Gateway」
nmcli con mod "Wired connection 1" ipv4.gateway 172.25.250.10

# 修改「Dns」
nmcli con mod "Wired connection 1" ipv4.dns 172.25.250.10
```

###### 說明：在上述的「ipv4.addresses」配置指令中，我們可以看到其配置的參數為「IP Address」再加上「/24」，其「/」後代表「網路遮罩」的設定值，「24」代表將「網路遮罩」的值設定為「255.255.255.0」。

在配置完所有題目指定的連線參數後，還有兩個重要設定要配置，其一是將「連線方法」改為「手動」；然後是將「自動連線」設定為「Yes」；如此一來，該連線設定在重啟時才會生效，指令如下：

```shell
# 修改「Method」
nmcli con mod "Wired connection 1" ipv4.method manual

# 修改「Gateway」
nmcli con mod "Wired connection 1" autoconnect yes
```

完成後，可以藉由指令「`nmcli con show`」來確認異動的內容，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_mod.png?raw=true)

#### Step 3. 將「Connection」重啟

為了使上述的網路配置生效，我們須重啟「Connection」，指令如下：

```shell
nmcli con up "Wired connection 1"
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_con_up.png?raw=true)

#### Step 4. 驗證

再重啟後，使用指令：「`ip a`」來確認「IP Address」與「Netmask」是否如預期的被修改，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q01_verify.png?raw=true)

---

###### tags: `Red Hat Certification` `RHCSA`