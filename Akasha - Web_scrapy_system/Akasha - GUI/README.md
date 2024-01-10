# Akasha GUI
> 如果是看資料，那也許用MySQL Workbench即可，但是若查看以外還要查找關鍵字、編輯、排序或甚至加Tag於新聞上，且要方便批量操作，那就必須使用程式加速操作，但是跑Python不美觀也不直覺，所以做了圖形化介面來改善之

## 已實作
1. **新聞觀看區**: 連結SQL，顯示新聞供觀看、並有稍後觀看鈕並且有五個小分頁及兩個總攬小分頁來展示新聞
2. **已編輯新聞、稍後觀看之新聞**: 單獨的編輯新聞、稍後觀看大分頁，以單獨存放編輯過之新聞與存到稍後觀看的新聞
3. **新聞搜尋區**: 搜尋功能，目前有搜尋新聞關鍵字、搜尋編輯庫中的關鍵字及搜尋新聞的出處
4. **標籤互動區**: 標籤過濾與增減，可以手動給新聞上標籤，以在未來查找
5. **設置與新聞頻率**: 查看新聞出現頻率，以防止網站因改版等狀況停擺，也有設置了可以改字體與字型的地方
6. **新聞編輯區**: 新聞編輯區則有標題、內容、心得可以編寫，也是圈選tag的地方

## 新聞觀看區
a. 為新聞觀看區，點選過的會灰掉，供使用者知道哪些看過哪些沒看過

b. 為稍後觀看，勾選下去後就會被存到稍後觀看區

c. 不同分頁提供不同語言或類型的新聞
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/5ab77bf6-c2b9-4fa5-9884-25c32f099875)

## 已編輯新聞、稍後觀看之新聞
上圖為稍後觀看之新聞，下圖為編輯後的新聞

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/98fa06cd-2ab1-4d6f-a78f-4cfb8e890284)
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/7bb6c586-5b87-45df-9427-43660e760ff5)

## 新聞搜尋區
Search(N): Normal，搜尋一般DB內的資料
Search(S): Special，搜尋已編輯區的資料
Search(P): Place，搜尋新聞來源

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/12d9abcf-e062-40e4-b58d-5ee30d3a1399)

## 標籤互動區
a.區塊可以選擇tag，可複選

b.區塊為符合所以選取的tag之新聞
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/96618c5c-87c6-483a-a944-b7729b38b385)

## 設置與新聞頻率
a. 可以看新聞頻率，防止網站突然掛掉

b. 增減tag

c. 更改字體大小跟字形
![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/40aad517-830a-41c1-9076-de0c63fdfcd5)

## 新聞編輯區
a. 有三個方框可以編輯，標題、內容與自己的意見

b. 增減tag，提供新聞分類用

![image](https://github.com/JulianLee310514065/SideProject--Akasha/assets/101493861/6109cec0-0d5d-4454-90d9-0f8eb315ffb3)

