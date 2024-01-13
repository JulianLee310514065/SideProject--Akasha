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

```python3
url = 'YOUR_URL'
head = {
'cookie':xxxx,
'user-agent': xxxxx
}
page = requests.get(url, headers = head, timeout= 5, proxies={"http":'TOUR_PROXY', "https":'YOUR_PROXY'})
```


## selenium刮取動態網站 
selenium的速度很慢，但是卻可以做到很多request做不到的功能，如點擊某按鈕、等待動態網頁加載無限下拉等功能，**下圖為selenium的範例程式:**

```python3
opts = Options()
'''
Add yout chrome option here
'''
browser = webdriver.Chrome(options= opts)
browser.get('YOUR_URL')

page = WebDriverWait(browser,30).until(lambda driver:driver.find_element(By.XPATH, "YOUR_XPATH")) #盡量使用xpath
elementHTML = page.get_attribute('outerHTML')
elementSoup = BeautifulSoup(elementHTML,'html.parser')

find_example = elementSoup.find_all('li', class_ = 'text red') #根據自己的需求使用`find_all`
```



## DrissionPage繞過cloudflare
DrissionPage專欄在[這邊](https://github.com/JulianLee310514065/SideProject--Akasha/tree/main/Akasha%20-%20Web_scrapy_system/Akasha%20-%20Web_scrapy/DrissionPage)，整理出了詳細的DrissionPage的使用方法，**下圖為DrissionPage之範例:**

```python3
newsflashes = 'YOUR_URL'  
co = ChromiumOptions()
'''
Add your chrome option here
'''
browser = ChromiumPage(addr_driver_opts=co)      
browser.get(newsflashes)

page_eles = browser.ele('xpath:/{YOUR_XPATH}')
elementSoup = BeautifulSoup(page_eles.html, 'html.parser')
comp_list = elementSoup.find_all('tr')  #根據自己的需求使用`find_all`
```



## BeautifulSoup做資料提取
藉由BeautifulSoup的find、findall功能可以做到查找資料目的，**下圖為範例:**

```python3
# comp_list為元素串列
for comp in comp_list:
    strs = comp.find('div', class_='title_con').text.strip()
    cursor.execute('''SELECT * FROM korean_table WHERE Title = "{}"'''.format(strs))
    result = cursor.fetchone() #查找有無重複
    if result is None:

        link = comp.a['href']
        
        timee = pd.to_datetime('today').replace(microsecond= 0).tz_localize('Asia/Shanghai')
        time_string = str(timee)[:-6]

        content = comp.find('div', class_ = 'text_con').text.strip()
```


## Telegram推送
為了第一步取得刮到資料，且不管是吃飯、上課還是出門都可以獲取第一線訊息，我們使用了Telegram來做訊息的傳遞與紀錄，Telegram提供了免費且快速的telegram bot API，讓我們可以透過API來讓Bot送資料到群組中，**下圖為程式範例:**

```python3
def send_bot(strs, hreff, proxy, head, not_show= True, from_place= None, chat_id= chat_id, urls = ETC_url):
    try:
        parameter = {
            'chat_id':chat_id,
            'text': f"{strs}\n{hreff}",
            'disable_web_page_preview':not_show,
        }
        requests.get(urls, params= parameter, proxies={"http":proxy, "https":proxy}, headers= head)
    except:
        pass
```



**Telegram推送範例:**
![image](https://user-images.githubusercontent.com/101493861/197339555-97411ef0-ec56-4f47-9310-42fc4306a88d.png)

## 總結
目前大概爬了50~60個網站，並且使用While讓他們持續跑，且考量到有些網站會擋IP，我們還使用了浮動ip來規避IP偵測，使之能做到24hr不停歇的爬蟲。

**While迴圈:**

```python3
# 執行函數
def main_fun():
  get_web1(proxy_ip, browser, not_show= True)    
  get_web2(proxy_ip, browser, not_show= True) 
  get_web3(proxy_ip, browser, not_show= True)     
  get_web4(proxy_ip, browser, not_show= True)


while True:
  try:
    cursor = conn.cursor()
    cursor.execute('USE {YOUR DATABASE}') 
    
    main_fun() 
    
    time.sleep(15) #自訂單圈休息秒數
  except:
    conn = pymysql.connect(host= '127.0.0.1', port= 3306, user= 'root', passwd=passwd, charset= 'utf8')
    cursor = conn.cursor()
    
  finally:
    cursor.close()
```

