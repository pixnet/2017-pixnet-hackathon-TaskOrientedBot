# 黑客松 Pixbot 製作過程大公開：（二）pixbot 的邏輯


很多開發者的心得是「做 bot 除了程式設計之外，更重要的是情境設計」，我們也不例外。我們發現，當使用者一開始接觸到 pixbot 的時候，大家不清楚要如何使用。像是我們預設使用者會提問「活動主持人是誰？」，也預先設計好了對應的回答。但實際上可能根本沒人想到這個問題，導致我們一開始設計好的所有對話可能幾乎沒有被問到。因此，我們重新設計使用情境，讓使用者能更清楚 pixbot 的功能。這部份我們就來談談如何製作 `Button Template` 與 `Quick Reply` 。


<img src="https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/button_template.PNG" height=500 />

## 傳送訊息範本

### Button Template

與[發送一般文字訊息](https://github.com/pixnet/2017-pixnet-hackathon-TaskOrientedBot/blob/master/development-of-pixbot/development-of-pixbot-1.md#發送訊息)給使用者略有不同，要傳送 button template，這裡的 payload 需改成以下格式：

```python
payload = {
    "recipient":{
        "id":"USER_ID"
    },
    "message":{
        "attachment":{
            "type":"template",
            "payload":{
                "template_type":"button",
                "text":"我是 PIXBOT，以下是今年 PIXNET HACKATHON 的活動資訊\n日期：9/9(六）\n地點：華山西一館\n時間：08:30-20:00\n報名日期：7/7起",
                "buttons":[
                    {
                        "type":"web_url",
                        "url":"https://goo.gl/fPNqam",
                        "title":"立刻報名"
                },
                    {
                        "type":"postback",
                        "title":"開始聊天",
                        "payload":"DEVELOPER_DEFINED_PAYLOAD_FOR_START"
                    }
                ]
            }
        }
    }
}
```

這是當使用者第一次對 pixbot 說話時，pixbot 傳送給使用者的訊息。可以看到裡面的 `payload` 欄位有一個值 `DEVELOPER_DEFINED_PAYLOAD_FOR_START` 。意思是，當使用者選擇了「開始聊天」這個行為，我們的 webhook 將會收到這個 payload。我們就可以針對收到的 payload 種類進行處理。

咦，前面不是說只要靠 API.AI 來做 intent 的管理就好了嗎？沒錯，但那僅限於傳送純文字的部份。在這個地方，當使用者按下「開始聊天」時，雖然 messenger 上會顯示使用者輸入了「開始聊天」，但在 webhook 中，我們並不是收到純文字的訊息：

```json
payload = {
  "recipient": {
    "id": "USER_ID"
  },
  "message": {
    "text": "開始聊天"
  }
}
```

因此我們若將「開始聊天」作為純文字來解析，是收不到任何回應的。這也是為什麼我們前面的 parser 之中，存在以下幾行程式碼的理由。

```python
# 這裡處理訊息以外的 payload
# 例如 facebook 提供的按鈕範本
if query.get('postback'):    
    p_type = query['postback']['payload']
    r['type'] = p_type
    return r
```
        
當我們發現使用者回傳的訊息格式，存在著 `payload` 欄位時，我們將 `payload` 的形態，也就是 `DEVELOPER_DEFINED_PAYLOAD_FOR_START` 記錄下來。這樣一來，我們就知道這代表使用者按下「開始聊天」的事件，便可以來做後續的處理囉。

### Quick Reply

在我們的 pixbot 之中，當使用者按下「開始聊天」後，pixbot 會提供三個選項給使用者做選擇

> user: 開始聊天
>
> pixbot: 這次比賽共有兩大主題，你想知道哪一個呢？
>
> quick_reply_1（智慧黑白講）
> quick_reply_2（生活嚮導機器人）
> quick_reply_3（比賽的規則是什麼）

那麼，我們要怎樣在傳送給使用者的訊息中，加上下方的 quick reply 呢？其實非常簡單，只需要修改[傳送訊息](https://github.com/pixnet/2017-pixnet-hackathon-TaskOrientedBot/blob/master/development-of-pixbot/development-of-pixbot-1.md#傳送訊息) 時提到的 payload 內容即可。把下面的 payload 塞到 `fb_message_sender()` 函數中，就可以發送帶有 quick reply 的訊息囉。

```json
payload = {
            "recipient": {"id": "USER_ID"},
            "message":{
                "text":"這次比賽共有兩大主題，你想知道哪一個呢？",
                "quick_replies":[
                  {
                    "content_type":"text",
                    "title":"智慧黑白講",
                    "payload":"DEVELOPER_DEFINED_PAYLOAD_FOR_CHITCHATBOT"
                  },
                  {
                    "content_type":"text",
                    "title":"生活嚮導機器人",
                    "payload":"DEVELOPER_DEFINED_PAYLOAD_FOR_FUNCTIONALBOT"
                  },
                  {
                    "content_type":"text",
                    "title":"比賽的規則是什麼",
                    "payload":"DEVELOPER_DEFINED_PAYLOAD_FOR_RULE"
                  }
                ]
              }
        }
```

這邊請注意，當使用者按下了 「智慧黑白講」的按鈕之後，這按下按鈕的動作仍然不屬於純文字訊息，必須透過下列判斷式來進行後續的處理哦！

```python
if postback['type'] == "DEVELOPER_DEFINED_PAYLOAD_FOR_CHITCHATBOT":
    payload = chitchatbot_response(postback)
