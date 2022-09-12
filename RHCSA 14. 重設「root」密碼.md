# RHCSA 14. 設置「root」密碼

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/redhat-rhcsa.png?raw=true)

---

## Description

將系統的密碼重設為「`redhat`」。

---

## Answer

#### Step 1. 重啟「系統」

由於是在沒有「密碼」的情況下，所以本題的前幾個步驟都不能以遠端「SSH」連線來操作。

另外，由於是練習環境，因此，我們的「Server」是以「虛擬機」建置，所以我們必須開啟虛擬機的操作介面，並開始目標伺服器的「Terminal」，並選擇重啟，如下：

![](https://github.com/rickbsr/Certification-RedHat-RHCSA/blob/main/pics/q14_vm_terminal_reboot.png?raw=true)

然後，再重啟時，輸入「`e`」，此時就會進到「GRUB」的畫面。

操作截圖如下：


---

<!-- ###### tags: `rhcsa` `redhat` `linux` -->