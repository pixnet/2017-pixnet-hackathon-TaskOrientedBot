
## 開放資料

PIXNET 為本次 hackathon 開放了 9 萬篇熱門文章，以及痞客邦網站的客服問答等資料，參賽者可多加利用。

檔案下載位址：[請點我](https://storage.googleapis.com/2017-hackathon-data-download/2017-pixnet-hackathon-data.tar.gz)

### 資料說明

檔案解壓縮之後的目錄結構如下：

- article （熱門文章）
   - constellation.json （星座運勢）
   - food.json （美味食記）
   - makeup.json （美妝 styleMe）
   - medic.json （醫療保健）
   - mombaby.json （親子育兒）
   - movie.json （電影評論）
   - sport.json （運動體育）
   - travel_foreign.json （國外旅遊）
   - travel_taiwan.json （國內旅遊）
- service （客服內容）
   - faq.json （痞客邦客服常見問題）
   - qa.json （2017年部分痞客邦所收到的的客服問題內文與問題回覆）
   - tempalte.json （客服問題回覆模版）

### 熱門文章資料格式

在 article 目錄下的所有 json 檔案皆為 newline delimited json 格式，每一列為一筆資料。

#### 資料格式

```
{
  "category": 痞客邦文章分類,
  "post_date": 發文時間,
  "hits": 人氣,
  "author": 作者,
  "title": 文章標題,
  "url": 文章 url,
  "tags": 作者定義之文章標籤,
  "content": 文章內文,
  "comment_count": 回應次數,
  "post_at": timestamp,
  "comment_ids":發表回應之會員,
  "article_id": 文章id
}
```

#### 資料範例

```json
{
  "category": "美味食記",
  "post_date": "2015-01-29T15:49:20+08:00",
  "hits": 65020,
  "author": "a3320985",
  "title": "【高雄●食記】高盧專廚法式餐廳●高雄推薦法式料理●枕頭牛排●排餐",
  "url": "http://a3320985.pixnet.net/blog/post/408027946",
  "tags": [
    "枕頭牛排",
    "法式料理",
    "法式餐廳",
    "浪漫排餐",
    "法國餐館"
  ],
  "content": "<p><a href=\"http://a3320985.pixnet.net/album/photo/572618356\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253558-10260949_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>上次錯過的高盧法式餐廳~ ~這次終於補回來囉!!</p>\r\n<p>位在高雄中正路上的高盧法式料理</p>\r\n<p>生意非常地好，電話預約非常困難</p>\r\n<p>因為他們很忙是不接電話的喔!!建議提早多天前訂位：)</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572617981\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253498-2323873630_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>&nbsp;一進到店內果然滿座，門口處擺放許多紅白酒與氣泡酒，可提供給客人</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618134\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253528-3448507816_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253532-3503592709_n.jpg\" alt=\"image.jpg\" border=\"0\" /></p>\r\n<p>餐點的部份我們同行的四人皆選擇他們家著名的枕頭牛排套餐，附贈開胃菜、麵包、沙拉、雪霜、濃湯、甜點及飲料</p>\r\n<p>另外也有不同的主餐可供選擇</p>\r\n<p><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253822-971434488_n.jpg\" alt=\"image.jpg\" border=\"0\" /></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618074\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253515-46388912_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a> &nbsp;&nbsp;</p>\r\n<p>&nbsp;<span style=\"color: #0000ff;\">&nbsp;開胃菜，<span style=\"color: #000000;\">鮮蝦番茄佐.....什麼醬的忘記了</span></span></p>\r\n<p><span style=\"color: #0000ff;\"><a href=\"http://a3320985.pixnet.net/album/photo/572618662\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253611-3745252330_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></span></p>\r\n<p><span style=\"color: #0000ff;\">海鮮濃湯</span>，魚肉、蛋、海鮮料，料都是作成塊狀，不會全部打散讓湯稠稠的感覺，上面還附上麵包塊</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618173\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253532-15907116_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><span style=\"color: #0000ff;\">現烤麵包，附奶油與鯷魚醬，<span style=\"color: #000000;\">大家都一致喜歡鯷魚醬，很香搭配麵包很好吃一點腥味都沒有喔，我們還吃完了再續麵包也續鯷魚醬&gt; &lt;</span></span></p>\r\n<p><span style=\"color: #0000ff;\"><a href=\"http://a3320985.pixnet.net/album/photo/572618659\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253611-1707341533_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></span></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618647\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253606-721632117_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618653\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253607-673423082_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>前菜的部份是屬無菜單方式，依當天主廚料理所以每天都並不一樣</p>\r\n<p>當日是綜合生魚片、凱撒沙拉及烤田螺系列三選一</p>\r\n<p><span style=\"color: #0000ff;\">綜合生魚片</span>，鮭魚、鮪魚與鮮蝦，想不到法式餐廳也吃到生魚片？魚很是新鮮呢</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618293\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253543-326531372_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618305\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253544-1133898807_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>普通的<span style=\"color: #0000ff;\">凱薩沙拉</span>，但melissa堅持愛吃草嘛!!一大盤的生菜沙拉吃起來清爽無負擔</p>\r\n<p><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253563-3465279053_n.jpg\" alt=\"image.jpg\" border=\"0\" /></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572619268\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253821-176917692_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>&nbsp;滿特別的前菜<span style=\"color: #0000ff;\">烤田螺</span>系列，搭配<span style=\"color: #0000ff;\">竹炭杏包菇</span>、<span style=\"color: #0000ff;\">紅酒洋蔥</span>及<span style=\"color: #0000ff;\">芝麻味增蛋糕<span style=\"color: #000000;\">，食用方式先吃上層的田螺，撕掉保鮮膜之後再吃下層的鮭魚卵、魚凍等等</span></span></p>\r\n<p><span style=\"color: #0000ff;\"><span style=\"color: #000000;\">口感好特別，吃起來像海綿一樣的是芝麻味增蛋糕，有點淡淡甜甜的</span></span></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618356\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253558-10260949_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a> &nbsp;</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618389\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253564-3324184959_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>上主餐前都會附上<span style=\"color: #0000ff;\">雪霜</span>，去除口中膩味，較能完全品嚐出主餐的味道，淡淡的</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618641\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253606-1434201180_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>&nbsp;<span>另人期待的主餐：</span><span style=\"color: #0000ff;\">美國枕頭牛佐西班牙蒜味醬</span></p>\r\n<p>服務人員會向您詢問要不要加洋蔥</p>\r\n<p>牛排搭配大蒜、洋蔥才好吃呢：)</p>\r\n<p>牛排上面覆蓋著烤乳酪醬，一切開肉汁都鎖在裡面</p>\r\n<p>果真是招牌主餐!!&nbsp;</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618632\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253601-720787469_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>&nbsp;另一主餐：<span style=\"color: #0000ff;\">藍帶豬排鮮蝦捲野菇紅酒</span></p>\r\n<p><span style=\"color: #000000;\">因為melissa忘記品嚐了所以也不好分享口感</span></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618650\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253600-3898497760_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>&nbsp;甜點也算用心又好吃的組合，巧可力蛋糕搭配奶油草莓蛋糕</p>\r\n<p>只可惜我們用餐時間太晚有點趕，因此倉促結束甜點與飲料時間~ ~ 未能細細品嚐</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618422\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253568-3609287602_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>過了用餐時間客人陸續離開(我們是最後一組客人耶)</p>\r\n<p>才能順便拍到店內的佈置</p>\r\n<p>算是溫馨又帶有點古典的感覺</p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618434\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253569-3579931067_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618611\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253596-2322246286_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p><a href=\"http://a3320985.pixnet.net/album/photo/572618620\"><img title=\"image.jpg\" src=\"http://pic.pimg.tw/a3320985/1422253597-67726307_n.jpg\" alt=\"image.jpg\" border=\"0\" /></a></p>\r\n<p>《整體用餐心得》：</p>\r\n<p>算是cp值不錯高，兼具創意與美味的法式餐廳</p>\r\n<p>尤其主餐枕頭牛排果然是不負眾望</p>\r\n<p>整體服務也不錯，很適合家庭聚餐喔</p>\r\n<p>但周末假日生意實在太好電話都打不進去呢，melissa一度想放棄的說!!</p>\r\n<p>&nbsp;</p>\r\n<p>二訪高廬法式料理●高廬專廚法式餐廳：<span style=\"color: #ff00ff;\"><a href=\"http://a3320985.pixnet.net/blog/post/435980320\"><span style=\"color: #ff00ff;\">http://a3320985.pixnet.net/blog/post/435980320</span></a></span></p>\r\n<p>&nbsp;</p>\r\n<h2 class=\"other_header\" style=\"margin: 0px; padding: 0px; border: 0px; font-family: 微軟正黑體, Helvetica, Arial, sans-serif; font-weight: inherit; font-stretch: inherit; line-height: 21.7600002288818px; font-size: 1.2em; vertical-align: baseline; color: #be252c; width: 280px; position: relative;\"><a class=\"ga_tracking\" style=\"margin: 0px; padding: 0px; border: 0px; font-family: inherit; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-size: 15.3599996566772px; vertical-align: baseline; color: #be252c; text-decoration: none; width: 190px; display: inline-block;\" href=\"http://www.ipeen.com.tw/shop/672224\" data-category=\"WEB_cmm\" data-action=\"right_shopname\" data-label=\"高盧專廚法式餐廳\">高盧專廚法式餐廳</a></h2>\r\n<ul>\r\n<li><span style=\"font-family: 新細明體; line-height: 21.7600002288818px;\">電話：07-241-2068</span></li>\r\n<li><span style=\"font-family: 新細明體;\"><span style=\"line-height: 21.7600002288818px;\">地址：高雄市新興區中正四路53號&nbsp;</span><a class=\"ga_tracking\" style=\"margin: 0px; padding: 0px; border: 0px; font-family: inherit; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-size: 12.8000001907349px; vertical-align: baseline; color: #0077b1; text-decoration: none;\" href=\"http://www.ipeen.com.tw/map/#!/s=0/f=0|0|0|0|0|10|0|0|0/c=22.630574,120.300127/z=18/sid=672224/\" target=\"_blank\" data-category=\"WEB_cmm\" data-action=\"right_shopaddress\" data-label=\"看地圖\"><span style=\"color: #000000;\">(近美麗島捷運站，旁邊有汽車停車場)</span></a></span></li>\r\n<li><span style=\"font-family: 新細明體;\"><span class=\"_CK _TX\" style=\"line-height: 16.1200008392334px;\">營業時間：</span><a class=\"fl\" style=\"color: #1a0dab; cursor: pointer; font-family: arial, sans-serif; font-size: 13px; line-height: 16.1200008392334px;\"><span style=\"color: #000000;\">11:30&ndash;14:30,&nbsp;17:30&ndash;22:00</span></a></span></li>\r\n</ul>\r\n<p><span style=\"font-family: 新細明體;\"> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a style=\"color: #3b5998; text-decoration: none; font-family: 'lucida grande', tahoma, verdana, arial, sans-serif; font-size: 11px;\" title=\"Melissa life\" href=\"https://www.facebook.com/mybloga3320985\" target=\"_TOP\">Melissa life</a><br style=\"font-family: Verdana; font-size: small;\" /><a style=\"color: #555555; text-decoration: none; font-family: Verdana; font-size: small;\" title=\"Melissa life\" href=\"https://www.facebook.com/mybloga3320985\" target=\"_TOP\"><img src=\"https://badge.facebook.com/badge/336491406463565.1292.814708368.png\" alt=\"\" /></a><br style=\"font-family: Verdana; font-size: small;\" /><a style=\"color: #3b5998; text-decoration: none; font-family: 'lucida grande', tahoma, verdana, arial, sans-serif; font-size: 11px;\" title=\"建立你的名片貼！\" href=\"https://zh-tw.facebook.com/advertising\" target=\"_TOP\">也可以宣傳你的粉絲專頁</a></span></p>",
  "comment_count": 0,
  "post_at": 1422517760,
  "comment_ids": [],
  "article_id": "408027946"
}
```

### 客服內容資料格式

在 service 目錄下的所有 json 檔案皆為 newline delimited json 格式，每一列為一筆資料。

#### FAQ

檔案 `faq.json` 是[痞客邦客服中心](https://help.pixnet.tw/)常見問題列表，如下圖

![痞客邦客服中心常見問題](https://storage.googleapis.com/2017-hackathon-data-download/faq.jpg)

##### FAQ 資料格式

```
{
  "star": 會員評分，可參考 https://help.pixnet.tw/index/category?category_id=6,
  "name": 問題描述,
  "msg": 問題回應
}
```
##### FAQ 資料範例

```json
{
  "star": 3,
  "name": "會員頭像是否能自行設定大小？",
  "msg": "雖然我們知道目前一定會有網友希望照片顯示的更大，但經過我們的抽樣調查了解後，大多網友對於[名片]仍希望它主要目的為”了解個人基本資訊”，而非展示照片，名片圖像僅是為了辨別，因此在各方考量下，名片圖像設定最大是200x200，而將來是否可以做更彈性的開放，歡迎提供想法意見囉！\r\n\r\n我們會持續評估，盡量在安全性範圍內開放讓大家方便喔！"
}
```

#### QA

檔案 `qa.json` 是[痞客邦客服中心](https://help.pixnet.tw/)今年所收到的部分問題

##### QA 資料格式

```
{
  "article_title": 問題標題,
  "comment_desc": 回應,
  "article_desc": 問題描述
}
```


##### QA 資料範例

```json
{
  "article_title": "在網路上無法搜尋到我所發佈的文章",
  "comment_desc": "您好：\n\n感謝您的提問，還請您不吝協助：\n\n1.請問您是在哪個搜尋引擎進行搜尋？(痞客邦首頁？Google？Yahoo？)\n2.請問您搜尋的關鍵字為？\n3.請問您希望搜尋的文章為？\n\n服務人員收到您的回覆，將為您進行確認及查詢。\n\n謝謝您",
  "article_desc": "用關鍵字搜尋,,,甚至直接搜尋文章標題,,,也無法搜尋到我所發佈的文章????"
}
```

#### Template

檔案 `template.json` 是[痞客邦客服中心](https://help.pixnet.tw/)常見問題的回應模版

##### Template 資料格式

```
{
  "template_title": 問題,
  "template_content": 回應
}
```


##### Template 資料範例

```json
{
  "template_title": "改帳號(舊後台)",
  "template_content": "您好：\r\n\r\n為保護會員帳號資料安全，站方未有開放會員申請更改(換)帳號之服務，需請您的諒解。\r\n\r\n但您可於登入後進入「部落格後台」，選擇「管理首頁」右側的「變更暱稱」進行修改，可依個人喜好來設定暱稱，而痞客邦PIXNET前台顯示帳號的地方（網址、部落格名片頁暱稱後方括弧除外）都將逐步替換成您的暱稱，不會再顯示您的帳號。\r\n\r\n不提供帳號更換的服務適用全站所有身份會員\r\n會員可參考站方公告說明： http://admin.pixnet.net/blog/post/25980962 第七點\r\n\r\n謝謝您"
}
```

##  資料授權使用說明

以上資料 是 2017 PIXNET Hackathon 活動中開放的資料集。詳細的資料說明與授權如下。


若您下載上述連結所提供的資料集 (Dataset)，表示您同意以下的資料使用授權：

**您可以：**

自由應用提供的資料集，產生新的程式、文件、圖表等著作。
自由修改提供的資料集，產生衍生的資料集。

**您必須：**

在您的著作或衍生資料集明確標示資料來源與此份說明文件的連結。

**您不可以：**

使用可能混淆或困擾的商標或名稱。
造成痞客邦會員產生違反痞客邦會員條款之行為。
違反中華民國法令或造成第三人發生違反中華民國法令的行為。
另為提供他人資料集下載。亦即，您不可以複製一份資料集到您自己的網路服務上供他人下載，但您可以提供他人此份說明文件的連結。
如您利用提供的資料集，開發任何妨礙善良風俗之違法服務或程式工具，PIXNET 並不為此負任何法律連帶責任。

