# 網路爬蟲
> 目的是要時時抓取特定網站上的重要資訊，來達到資訊平衡，或是利用此資訊做交易或分析

## 已實作
1. request刮取靜態網站 
2. selenium刮取動態網站
3. 使用DrissionPage來繞過Cloudflare阻擋之網站
4. 使用BeautifulSoup資料處理，並提取重要資訊
5. Telegram推送

## request刮取靜態網站 (request.get)
request的優點是速度快，刮下來為HTML，可以使用BeautifulSoup來進行資料的處理及查找。**下圖為request的範例程式:**

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/212d9400-10cc-4a6d-af17-a5c6af4dee94)


## selenium刮取動態網站 
selenium的速度很慢，但是卻可以做到很多request做不到的功能，如點擊某按鈕、等待動態網頁加載無限下拉等功能，**下圖為selenium的範例程式:**

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/544f9895-5364-4093-a8d4-82847d4bcf28)


## DrissionPage繞過cloudflare
DrissionPage專欄在[這邊](https://github.com/JulianLee310514065/SideProject--Akasha/tree/main/Akasha%20-%20Web_scrapy_system/Akasha%20-%20Web_scrapy/DrissionPage)，整理出了詳細的DrissionPage的使用方法，**下圖為DrissionPage之範例:**
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/6e879694-3dfa-4ee5-90c9-d524172838f8)


## BeautifulSoup做資料提取
藉由BeautifulSoup的find、findall功能可以做到查找資料目的，**下圖為範例:**

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/72bbe2ef-aeb6-4949-95ad-a5a5d7ae6548)


## Telegram推送
為了第一步取得刮到資料，且不管是吃飯、上課還是出門都可以獲取第一線訊息，我們使用了Telegram來做訊息的傳遞與紀錄，Telegram提供了免費且快速的telegram bot API，讓我們可以透過API來讓Bot送資料到群組中，**下圖為程式範例:**
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/7cb98a46-9875-4c12-8858-82d8c1557060)



**Telegram推送範例:**
![image](https://user-images.githubusercontent.com/101493861/197339555-97411ef0-ec56-4f47-9310-42fc4306a88d.png)

## 總結
目前大概爬了50~60個網站，並且使用While讓他們持續跑，且考量到有些網站會擋IP，我們還使用了浮動ip來規避IP偵測，使之能做到24hr不停歇的爬蟲。

**While迴圈:**

![image](https://user-images.githubusercontent.com/101493861/197339818-7971bd37-ef54-44be-b69a-1f9395b9838d.png)

