# RHCSA 12. 查找字串

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

搜尋文件「`/usr/share/dict/words`」中，所有包含字串「`unexamin`」的句子，並將那些句子放到檔案「`/root/lines.txt`」之中。

---

## Answer

#### Step 1. 搜尋目標字串並匯出

依題目敘述，搜尋「`/usr/share/dict/words`」中的字串：「`unexamin`」，指令如下：

```shell
grep unexamin /usr/share/dict/words > /root/lines.txt
```

#### Step 2. 驗證

這題的驗證方式就大致比對一下「grep」與「cat」輸出的內容與行數即可，指令如下：

```shell
// 顯示 grep 輸出的內容
grep unexamin /usr/share/dict/words

// 顯示 grep 輸出內容的行數
grep -c unexamin /usr/share/dict/words

cat -n /root/lines.txt
```

操作截圖如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q12_grep.png?raw=true)

---

###### tags: `rhcsa` `redhat` `linux`