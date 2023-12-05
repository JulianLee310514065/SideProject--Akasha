|[中文版](https://github.com/JulianLee310514065/Akasha_Project/edit/main/Akasha%20-%20Web_Scrapy/DrissionPage/README.md)|[English version](https://github.com/JulianLee310514065/Akasha_Project/blob/main/Akasha%20-%20Web_Scrapy/DrissionPage/README_eng.md)|
-|-|

---
# ✅️️Install
  > Python 3.9.12 (anaconda) + VSCode

### 📌 Install or Upgrade
```py
  # Install
  pip install DrissionPage
  # Upgrade
  pip install DrissionPage --upgrade
```
# ✅️Open Browser


### 📌 There are three ways to open the browser: `WebPage`, `ChromiumPage`, and `SessionPage`. However, I have only used `ChromiumPage`.

  Since I typically use Selenium, I haven't encountered issues with the no exist of `chrome.exe` or problems in opening web pages. If you face problems when opening a webpage, feel free to ask me.
    
  ```python
    from DrissionPage import ChromiumPage
    page = ChromiumPage()  
  ```
    
### 📌 Configuration
    
  *  timeout
  
      Set the retry time in event of timeout. The page will be retried if there is no response within the specified time. There are two ways to set the timeout:
      ```python    
        # 1.Create a page with a specific timeout
        page = ChromiumPage(timeout=5)        
        # 2.Modify page.timeout
        page.timeout = 5
      ```

  * Set Loading Strategy
  
      By setting the `set.load_strategy` property of the `ChromiumPage` object, you can set the time for when the page stops loading. During page is loading, it will stop when the timeout is reached or the set state is reached, effectively saving scraping time. There are three modes:
      * `page.set.load_strategy.normal()`: Normal mode, waits for the page to load completely.

      * `page.set.load_strategy.eager()`: Stops loading after the DOM is loaded, without loading images or animations, saving time.

      * `page.set.load_strategy.none()`: Stops loading after the connections are completed.

      * The default setting is normal.
       
      ```py      
        page = ChromiumPage()
        page.set.load_strategy.eager()
      ```

  * To prevent being blocked due to frequent crawling, use a proxy.

      ```py
        co = ChromiumOptions()
        if proxy_ip == None:
            pass
        else:
            co.set_proxy(proxy_ip)
        page = ChromiumPage(addr_driver_opts=co)
      ```

  * Headless browsing allows the browser to operate in the background without displaying the webpage. However, some websites may detect headless browsing and block access, so it should be used according to the requirements of different websites.
      ```python
        co = ChromiumOptions()
        co.set_headless(True)          
        page = ChromiumPage(addr_driver_opts=co)
      ```


### 📌 Retrieve webpage information is similar to Selenium, and it is also done using `get()`

```py
  page.get(YOUR_URL)
```

# ✅️Locating Elements, most methods are documented [here](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/)

### 📌 Use `page.ele()` to find a single element, and it is recommended to use `xpath`, similar to `find_element()` in Selenium. 

```python
    from DrissionPage import ChromiumPage

    page = ChromiumPage()

    page.get('http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/')
    ele_class = page.ele('xpath://html/body/div[3]/main/div/div[3]/article')    
```

### 📌 Use `page.eles()` to find multiple elements, similar to `find_elements()` in Selenium.
   
```python
    from DrissionPage import ChromiumPage

    page = ChromiumPage()

    page.get('http://g1879.gitee.io/drissionpagedocs/ChromiumPage/find_elements/')
    p_eles = page.eles('tag:p')
    print(p_eles[0].text)      
```

### 📌 Once an element is found, convert it to HTML, and then use BeautifulSoup to find child elements.

```py
    elementSoup = BeautifulSoup(page_eles.html, 'html.parser')
```


# ✅️ ️Element Interaction

Assuming `ele` is the button or object you have found.

### 📌[Clicking Elements](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/element_operation/#_1)
   
   Examples:
   
```python
   
   # Simulate a click on the ele element, will click even if obstructed
   ele.click()

   # Click the ele element using JavaScript, ignoring overlay
   ele.click(by_js=True)

   # If the element is not obstructed, use simulated click, otherwise use JavaScript click
   ele.click(by_js=None)

   # Right-click
   ele.click.right()

   # Middle-click
   ele.click.middle()

   # Double-click
   ele.click.twice()

   # Click at a specific location
   click.at(x, y)
```

### 📌[Input](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/element_operation/#_2)
   
```python
   # Input text
   ele.input('Hello world!')

```

### 📌[Key Actions](http://g1879.gitee.io/drissionpagedocs/ChromiumPage/action_chains/#key_up)

Simulate pressing  ctrl+a

```py
   from DrissionPage import ChromiumPage
   from DrissionPage.common import Keys, ActionChains
   
   # Create a page
   page = ChromiumPage()
   # Create an ActionChains object
   ac = ActionChains(page)

   # Move the mouse to the <input> element
   ac.move_to('tag:input')
   # Click the mouse to place the cursor in the element
   ac.click()
   # Press the ctrl key
   ac.key_down(Keys.CTRL)
   # Type 'a'
   ac.type('a')
   # Release the ctrl key
   ac.key_up(Keys.CTRL)
```

# ✅️Other Tips

1. Server Address: `page.address`

2. Is page still alive?
    `page.is_alive`

3. Is page loaded?
    `page.ready_state`

4. Check cookies:
    `page.cookies`

5. Navigate back and forward:

    ```py
    page.back() # Go back to the previous page
    page.forward() # Go forward to the next page
    ```
