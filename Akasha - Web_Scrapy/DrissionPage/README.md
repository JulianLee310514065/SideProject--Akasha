|[中文版](https://github.com/JulianLee310514065/Akasha_Project/edit/main/Akasha%20-%20Web_Scrapy/DrissionPage/README.md)|[English version](https://github.com/JulianLee310514065/Akasha_Project/blob/main/Akasha%20-%20Web_Scrapy/DrissionPage/README_eng.md)|
-|-|

---
# ✅️️Install
  > Python 3.9.12 (anaconda) + VSCode

### 📌 安裝或升級
```py
  # Install
  pip install DrissionPage
  # Upgrade
  pip install DrissionPage --upgrade
```
# ✅️️打開瀏覽器


### 📌他有三種開啟方式，`WebPage`、`ChromiumPage`、`SessionPage`，但我只用過`ChromiumPage`


  因為我平時有在用`Selenium`所以沒有遇到`chrome.exe`不存在或是打不開網頁的問題，如果在開網頁時發生困難可以再問我
    
  ```python
    from DrissionPage import ChromiumPage
    page = ChromiumPage()  
  ```
    
### 📌配置参数信息
    
  *  timeout

      設定超時重試時間，多久網頁沒反應則重試，有兩種方式

      ```python    
        # 创建页面指定
        page = ChromiumPage(timeout=5)        
        # 修改 page.timeout
        page.timeout = 5
      ```

  * 设置加载策略

      通过设置`ChromiumPage`对象的`set.load_strategy`属性，可设置页面停止加载的时机。 页面加载时，在到达超时时间，或达到设定的状态，就会停止，可有效节省采集时间。有以下三种模式：

      * `page.set.load_strategy.normal()`：常规模式，会等待页面加载完毕

      * `page.set.load_strategy.eager()`：加载完 DOM 即停止加载，不會載入圖片或動畫，可省時間

      * `page.set.load_strategy.none()`：完成连接即停止加载

      * 默认设置为normal。
       
      ```py      
        page = ChromiumPage()
        page.set.load_strategy.eager()
      ```

  * 若要防止太頻繁爬蟲被鎖，可以使用代理

      ```py
        co = ChromiumOptions()
        if proxy_ip == None:
            pass
        else:
            co.set_proxy(proxy_ip)
        page = ChromiumPage(addr_driver_opts=co)
      ```

  * 無頭瀏覽器，可以不顯示網頁在背景運作，但是有些網站會偵測無頭導致被封鎖，所以必須依不同網站去使用 
      ```python
        co = ChromiumOptions()
        co.set_headless(True)          
        page = ChromiumPage(addr_driver_opts=co)
      ```


### 📌獲取網頁訊息，與`selenium`相似，也是用`.get()`
```py
  page.get(YOUR_URL)
```
# ✅️️查找元素，方法幾乎都寫在[這裡](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/)

### 📌找單一element可使用`page.ele()` ，建議用`xpath`，如`selenium`中的`find_element`   

```python
    from DrissionPage import ChromiumPage

    page = ChromiumPage()

    page.get('http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/')
    ele_class = page.ele('xpath://html/body/div[3]/main/div/div[3]/article')    
```

### 📌找多個element可使用`page.eles()`，如`selenium`中的`find_elements`
   
```python
    from DrissionPage import ChromiumPage

    page = ChromiumPage()

    page.get('http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/')
    p_eles = page.eles('tag:p')
    print(p_eles[0].text)      
```

### 📌找到元素之後可以轉成html，之後再使用Beautifulsoup來找尋子元素

```py
    elementSoup = BeautifulSoup(page_eles.html, 'html.parser')
```
# ✅️️元素互動

假設`ele`為你找到的按鈕或是物件

### 📌[点击元素](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/element_operation/#_1)
   
   示例：
   
```python
   
   # 对ele元素进行模拟点击，如判断被遮挡也会点击
   ele.click()

   # 用js方式点击ele元素，无视遮罩层
   ele.click(by_js=True)

   # 如元素不被遮挡，用模拟点击，否则用js点击
   ele.click(by_js=None)

   # 右鍵
   ele.click.right()

   # 中鍵
   ele.click.middle()

   # 左鍵兩側
   ele.click.twice()

   # 點指定位置
   click.at(x, y)
```

### 📌[input()](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/element_operation/#_2)
   
```python
   # 输入文本
   ele.input('Hello world!')

   # 输入文本并回车
   ele.input('Hello world!\n')
```

### 📌[按鍵動作](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/action_chains/#key_up)

模拟输入 ctrl+a

```py
   from DrissionPage import ChromiumPage
   from DrissionPage.common import Keys, ActionChains
   
   # 创建页面
   page = ChromiumPage()
   # 创建动作链对象
   ac = ActionChains(page)

   # 鼠标移动到<input>元素上
   ac.move_to('tag:input')
   # 点击鼠标，使光标落到元素中
   ac.click()
   # 按下 ctrl 键
   ac.key_down(Keys.CTRL)
   # 输入 a
   ac.type('a')
   # 提起 ctrl 键
   ac.key_up(Keys.CTRL)
```
# ✅️其他技巧

1. 伺服器地址: `page.address`

2. 還活著?
    `page.is_alive`

3. 讀取完了嗎?
    `page.ready_state`

4. 看cookies
    `page.cookies`

5. 上一頁下一頁

    ```py
    page.back() #上一頁
    page.forward() #下一頁
    ```
