# 黑客松 Pixbot 製作過程大公開：（四）pixbot 會思考


這系列文章主要會提到：

- 在 facebook 平台建立 chatbot 的過程
- 使用 api.ai 做自然語言處理
- 使用者與 pixbot 對話記錄的文字探勘

## 前情提要

我們可以想像一下「訂機票」是這樣的一個函數：

```python
booking_flight(date=date,  departure_time=departure_time, from=from, to=to, flight_number=flight_number)
```
其中帶有參數 date 日期、 departure_time 出發時間、 from 出發地、 to 目的地、 flight_number 航班號碼等等。然後我們不斷的透過問答，引導使用者回應出所有該回答的參數。也只有在參數都齊全之後才有辦法進行訂票。

## Entity

發現了嗎，上面這些被解構出來的參數，其實每一個都是 entity，我們必須針對每一個 entity 分別設定。 API.AI 已經幫我們做了一些基本的 entity，降低我們在輸入 entity 時的複雜程度。

下圖顯示了，在 booking_flight 這個 intent 底下，我們將預設的 User says「我要訂20170909 的機票」之中日期的地方反白，賦予一個 `@sys.date` 的 entity。這就是系統預設的日期 entity，如果沒有預設這個 entity 的話，我們就得輸入所有的日期格式了！在右邊的測試區可以看到，輸入「我要訂9月9日的機票」，API.AI 仍然可以解析出這個 entity，並將他輸出成系統預設的 date 格式： 2017-09-09。

![entity_date](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_booking_date.png)

讓我們加上地點的 entity，把例子變得更複雜一些。我們首先手動加入一些地點，例如「舊金山」，和他的同義詞。這邊我們只簡單加入幾個，然後把這些 entity 命名為 US_CITY。


<img src="https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_entity_create.png" height="240"/>


在新增完 entity 之後，重新回到 intent 設定的地方。我們來看看怎麼設定 intent 中的各個 entity：

1. 輸入一個模版句子「我要訂20170909到舊金山的機票」。
2. 將「20170909」的部份反白，在 entity 的地方將他設定為前面提過的 `@sys.date` 。
3. 將「舊金山」的地方反白，在 entity 的地方將他設定為 `@US_CITY` ，這也是我們剛剛手動創建的 entity。
4. 將 REQUIRED 的部份打勾，代表為必答欄位。（如果使用者在這句話沒有回答的話，可以在 PROMPTS 的地方設定預設的問句來引導使用者回答。）
5. 最後，在 chatbot 回應的地方設定「你要訂的日期是 `$date` 。地點是 `$US_CITY` 」。

然後，我們就可以在右邊的測試區看到結果囉，並且 PARAMETER 之中的 `date` 與 `US_CITY` 也都有正確解析出來。

![entity_setting](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_entity_setting.png)

### 與 bot 平台的串接

事實上，真的可以完全不寫任何一段 code 就做好一個 chatbot。既然這樣，為什麼前面的文章裡以及 pixbot 的架構圖中又包含了不少程式呢？原因是我們希望收錄使用者的對話記錄以及一些進階功能，因此我們需要將 API.AI 給出的回應重新導向，所以才需要寫部分的程式碼。如果只是想做個可以簡單互動的 chatbot，是可以不用寫任何程式的哦！

在 Integrations 的地方，打開你想串接的平台，進入設定畫面填入該填的 TOKEN，這樣你的 bot 就可以立刻上線囉～

<img src="https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_integration.png" height="400"/>

##  不是說好不寫 code 嗎

API.AI 提供了不少語言的 SDK，方便我們開發自己的應用，完成一些比較複雜的功能。這邊來整理一下 pixbot 的流程：

1. 使用者傳訊息給 pixbot
2. pixbot 透過 facebook webhook 收到訊息
3. 訊息轉給 API.AI 進行語意分析
4. API.AI 回應適合的答句給 webhook
5. 送出從 API.AI 過來的答句給使用者

在上面的五個步驟裡，如果不寫程式的話，其實就是做了1, 3, 5三個步驟。在我們自行加上 webhook 後，我們至少必須進行兩件事：

1. 透過 API.AI 提供的 SDK 來和 API.AI 傳送與接收訊息
2. 解析 API.AI 傳送的訊息格式，轉為 facebook 的訊息格式

<img src="https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_showjson.png" height="300"/>

在 API.AI 的測試區可以看到一個 SHOW JSON 的按鈕，按下去之後會顯示這個問與答的資料格式：

```
{
  "id": "f665edd1-fc49-4113-8ba5-3f11e00788d9",
  "timestamp": "2017-08-10T03:47:22.994Z",
  "lang": "zh-tw",
  "result": {
    "source": "agent",
    "resolvedQuery": "我要訂 2017-09-09 到 NY 的機票",
    "action": "",
    "actionIncomplete": false,
    "parameters": {
      "date": "2017-09-09",
      "US_CITY": "紐約"
    },
    "contexts": [],
    "metadata": {
      "intentId": "6aaad95d-c44d-45a8-b829-a54ed8a0c5d5",
      "webhookUsed": "false",
      "webhookForSlotFillingUsed": "false",
      "intentName": "booking_flight"
    },
    "fulfillment": {
      "speech": "你要訂的日期是 2017-09-09。地點是 紐約",
      "messages": [
        {
          "type": 0,
          "speech": "你要訂的日期是 2017-09-09。地點是 紐約"
        }
      ]
    },
    "score": 1
  },
  "status": {
    "code": 200,
    "errorType": "success"
  },
  "sessionId": "4f191c49-bbe2-4b62-ab25-6c7edc81b831"
}
```
我們可以寫一個 parser 自行解析 json 封包裡面的重要欄位，並且透過以下利用 API.AI 的 python SDK 來進行資料的交換。這樣一來就可以完成上面 1~5 的完整步驟囉！

```python

import apiai

CLIENT_ACCESS_TOKEN = 'YOUR_TOKEN'

# Conversation API Interface
def talk(message,uid):
    ai = apiai.ApiAI(CLIENT_ACCESS_TOKEN)
    request = ai.text_request()
    
    # 此次 Hackathon Languge Model 是採用 zh_cn
    request.lang = 'zh_cn'  
    request.session_id = uid
    request.query = message

    respone = request.getresponse()
    rdata = str(response.read(),'utf-8')
    robj = json.loads(rdata)
    djson(robj)

    return robj
```
