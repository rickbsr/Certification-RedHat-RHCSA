# RHCSA 11. 查找文件

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

將使用者「john」所擁有的文件都複製一份並放到名稱為「`/root/backup`」的目錄。

---

## Answer

#### Step 1. 建立「資料夾」

```shell
mkdir /root/backup
```

#### Step 2. 查找文件並複製到指定目錄

```shell
find / -user john -type f -exec cp -a {} /root/backup \;
```

查找的指令是「`find`」，後面接的是要尋找的目錄；而「user」意思是指「檔案的擁有者」，所以其後必須接「使用者」；此外，若要找查找的檔案目錄是「不屬於任何人」的，可以使用參數「nouser」。

然後「type」是指要尋找是「檔案目錄類」型，後面的「f」，代表「files」，意即「檔案」。

接著是「exec」，是「執行」的意思，後面接「要被執行的指令」，而「`{}`」則代表輸入的內容，也就是前面「`find`」所找到的內容。

另外，上述指令中的參數「a」是指令「`cp`」的參數，等同於複合參數「dpR」，意即保留「鏈接」與「文件屬性」，並複製目錄下的所有內容。

而指令最後的「`\;`」則是代表指令結束。

當完成後，我們可以藉由「`ls`」確認一下「`/root/backup`」目錄，操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q11_find.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`