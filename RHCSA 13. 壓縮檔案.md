# RHCSA 13. 壓縮檔案

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

將「`/usr/local/`」的內容打包，並以「`gz`」的方式壓縮，其檔名為「`/root/backup.tar.gz`」。

---

## Answer

#### Step 1. 依題目需求將目標目錄壓縮

指令如下：

```shell
tar -zcvPf /root/backup.tar.gz /usr/local/
```

在指令「`tar`」中，「c」是「create」的意思，也就是「打包」；而「v」則是「verbose」的意思，代表要顯示正在處理的訊息，其實就是顯示「Log」。

另外題目有指令以「`gz`」格式壓縮，其中「z」就是代表以「`gz`」格式壓縮；其它常見壓縮格式還有「`bz2`」，參數為「j」；「`xz`」，參數為「J」。

最後是「P」，其實這是因為「tar」預設的檔案名稱是以「相對路徑」表示，而上述指令是以「絕對路徑」表示；而「P」的意思就是指以「絕對路徑」表示檔名；若不加「P」，其實也仍成功打包並壓縮，只是會顯示以下的錯誤訊息：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q13_tar_error.png?raw=true)

完整操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q13_tar_gz_archive.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`