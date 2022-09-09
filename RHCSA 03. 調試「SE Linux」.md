# RHCSA 03. 調試「SE Linux」

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

在非預設端口，「82 port」上執行「Web」服務器，在提供內容時遇到問題；請根據需要除錯以解決問題，並須滿足以下條件：

- 「Web」服務器要能夠提供「`/var/www/html/file.html`」中的內容。
- 「Web」服務器要能夠在「82 port」上提供內容，並在系統啟動時，自動啟動。

###### 提示：不要刪除或以其他方式改動現有的文件內容。

---

## Answer

#### Step 1. 設定傾聽「目標端口」

題目要求我們能夠在「82 port」上讀取「`/var/www/html/file.html`」中的內容，嘗試指令如下：

```shell
curl http://127.0.0.1:82/file.html
```

結果如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_curl_refused.png?raw=true)

其顯示為「Connection refused」。

因此，我們首先要改的是「Httpd」的預設傾聽「埠號」，設定檔位址在「`/etc/httpd/conf/httpd.conf`」，用「vim」開啟，並將預設傾聽的「80 port」的改成「80 port」，截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_httpconf_ch_port.png?raw=true)

修改完成後須將「Http」重啟，指令如下：

```shell
systemctl restart httpd.service
```

但若此時重啟，會出現「Error」，如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_httpd_restart_error.png?raw=true)

這是因為「82 port」並非「SE Linux」中「`http_port_t`」預設的端口，因此我們須將其新增，指令如下：

```shell
semanage port -a -t http_port_t -p tcp 82
```

指令「`semanage port`」是「`semanage`」用來管理網路設定的子命令。

在指令中，參數「a」是「add」的意思，意即「新增」；而參數「t」則是「Type」，意即「類別」，所以在其後必須接上類型，以本題來說，要新增的端口類別是「`http_port_t`」；而後是「p」，意即「port」，而後面接的是「Protocol」，本題使用的協議類型是「TCP」；最後在加上端口號「82」。

另外，在添加端口前後，可以用指令「`semanage port -l`」來確認是否有成功添加，整個操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_semanage_port.png?raw=true)

完成後，就可以重啟「Httpd」，指令如下：

```shell
systemctl restart httpd.service
```

當重啟「Http」完成後，再嘗試讀取一次「`/var/www/html/file.html`」中的內容，指令如下：

```shell
curl http://127.0.0.1:82/file.html
```

結果如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_curl_no_permission.png?raw=true)

錯誤訊息從「拒絕連線」變成「權限不足」；雖然一樣有錯誤，但錯誤訊息已與剛才不同，前者是是因為無法連線導致，而後者是已經連接到伺服器，且能碰觸到目標檔案了，只是權限不足，無法讀取而已。

其實，這的錯誤同樣與「SE Linux」相關，其問題在於「安全性文本」的配置。

#### Step 2. 修改「安全性文本」

藉由指令「`ls -Z`」來查看檔案，就會發現「`file.html`」的「安全性本文」中的「type」是「`user_home_t`」，如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_security_context.png?raw=true)

因此，我們須將之改為「`httpd_sys_content_t`」，指令如下：

```shell
semanage fcontext -m -t httpd_sys_content_t '/var/www/html/file\.html'
```

安全性本文的組成可以分為「Identify（身份識別）」、「role（角色）」以及「type（類型）」；其之間用「`:`」隔開。

而指令「semanage fcontext」就是與「SE Linux」的「安全性本文」操作有關的指令，其可藉由參數「m」來修改「安全性本文」的內容，「m」代表「modify」；附帶一提，若碰到尚未定義的「檔案」，此時就無法使用「m」，要改用參數「a」，即「新增」的意思。

最後是「t」，代表「type」的意思，因此，其後面須接「類型」。

修改完後，記得套用，指令如下：

```shell
restorecon -Rv /var/www/html/
```

上述中，指令「restorecon」的「R」是「遞迴」的意思，「v」則是「可見的」。

若當一切操作完成後，我們就可以用「`curl`」正確地讀取到「`/var/www/html/file.html`」的內容了，整體操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_semanage_fcontext_m.png?raw=true)

#### Step 3. 在「防火牆」的例外端口上，添加「目標端口」

最後，為了能讓「外部讀取」，我們還必須設定「防火牆」。

事實上，在上面那個步驟應該就已經完成題目要求了，但為了保險起見，我們還是設定一下「防火牆」，指令如下：

```shell
firewall-cmd --zone=public --add-port=82/tcp --permanent
```

然後重啟，指令如下：

```shell
firewall-cmd --reload
```

當操作完成後，可以藉由指令「`firewall-cmd`」的「--list-all」來確認，指令如下：

```shell
firewall-cmd --zone=public --list-all | grep "82" -C 3
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q03_firewall.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`