# 網路爬蟲
> 目的是要時時抓取特定網站上的重要資訊，來達到資訊平衡，或是利用此資訊做交易或分析

## 已實作
1. request刮取靜態網站 
2. selenium刮取動態網站 
3. 使用BeautifulSoup資料處理
4. Telegram推送

## request刮取靜態網站 (request.get)
request的優點是速度快，刮下來為HTML，可以使用BeautifulSoup來進行資料的處理及查找。**下圖為request的範例程式:**

![image](https://user-images.githubusercontent.com/101493861/197339117-352ba54f-c200-45d3-87a4-4ecb59fd8edd.png)

## selenium刮取動態網站 
selenium的速度很慢，但是卻可以做到很多request做不到的功能，如點擊某按鈕、等待動態網頁加載無限下拉等功能，**下圖為selenium的範例程式:**

![image](https://user-images.githubusercontent.com/101493861/197339201-8de02d1d-e4e9-4e68-9ead-c566b43a18c0.png)

## 使用BeautifulSoup 做資料提取
藉由BeautifulSoup的find、findall功能可以做到查找資料目的，**下圖為範例:**

![image](https://user-images.githubusercontent.com/101493861/197339339-1c929bdc-966e-451b-8c21-0461b40d86eb.png)

## Telegram推送
為了第一步取得刮到資料，且不管是吃飯、上課還是出門都可以獲取第一線訊息，我們使用了Telegram來做訊息的傳遞與紀錄，Telegram提供了免費且快速的telegram bot API，讓我們可以透過API來讓Bot送資料到群組中，**下圖為程式範例:**

![image](https://user-images.githubusercontent.com/101493861/197339484-b9972dcb-b241-407e-98ba-4aacc21de423.png)

**Telegram推送範例:**
![image](https://user-images.githubusercontent.com/101493861/197339555-97411ef0-ec56-4f47-9310-42fc4306a88d.png)

## 總結
目前大概爬了50~60個網站，並且使用While讓他們持續跑，且考量到有些網站會擋IP，我們還使用了浮動ip來規避IP偵測，使之能做到24hr不停歇的爬蟲。

**網站範例**

![image](https://user-images.githubusercontent.com/101493861/197339786-cbd879f8-70f5-43ec-8f74-f9ab60c36fd6.png)

**While迴圈**

![image](https://user-images.githubusercontent.com/101493861/197339818-7971bd37-ef54-44be-b69a-1f9395b9838d.png)


## 待練習
除了request與selenium，現在還有種爬蟲方式叫做Scrapy，聽說也不錯用，未來有時間可以來試試看
