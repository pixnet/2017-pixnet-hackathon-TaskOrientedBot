# 黑客松 Pixbot 製作過程大公開：（三）pixbot 學說話


這系列文章主要會提到：

- 在 facebook 平台建立 chatbot 的過程
- 使用 api.ai 做自然語言處理
- 使用者與 pixbot 對話記錄的文字探勘

![system architecture](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/architecture.png)
---

## 前情提要

前面我們提到了如何進行 facebook 訊息的傳送與接收。另外，也提到如何使用複雜一點的 payload 型態來傳送按鈕與 quick reply 等等功能。這些功能可以讓我們的 bot 與使用者互相傳送訊息，但我們也提到了，這樣並沒有辦法讓 bot 理解使用者傳送訊息的語意（也就是只有架構圖的右半部）。因此，這邊我們要介紹一個工具：「API.AI」。

## 不用寫 code 也可以做 chatbot

###  建立新的 bot 服務

在 [API.AI](https://api.ai/) 的網頁註冊好帳號之後，首先需要 create agent。如下圖，也就是建立一個機器人的服務，這邊請**注意語系的選擇**，這關係到 API.AI 會使用哪一個內建的語言模型來處理我們的對話，如果選擇到英文的話就別怪他沒有辦法幫你處理中文對話囉！

![create_agent](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_create_agent.png)

在 agent 建立完成之後，就會來到 API.AI 的主畫面。後面我們會介紹 intent、entity 與 training 的部份。如果你看到下面的畫面，代表已經可以開始對 bot 進行設定了。

![enter image description here](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_default_intent.png)

## Intent

上圖中，我們可以看到 Default Welcome Intent 以及 Default Fallback Intent。這兩個 intent 是當 agent 開起來就會存在的。例如，Default Fallback Intent 就是當 bot 看不懂使用者問的問題的時候所對應的 intent。

當我們尚未建立任何 intent 時，bot 本身是不認得任何文字的。API.AI 提供了一個方便的測試區塊，也就是下圖中紅色框框的部份。我們嘗試隨便輸入一句話，可以看到 API.AI 自動幫我們的輸入「貓咪為什麼這麼可愛」對應到了「Default Fallback Intent」，而該 intent 的回覆為「請您再說一遍」。

![default_fallback_intent](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_default_fallback_intent.png)

於是我們應該為自己的 chatbot 建立 intent，不然的話你向 chatbot 說什麼，他可是什麼都聽不懂的。

在 API.AI 建立 intent 的方法非常簡單，如下圖，這是一個回應「評分標準」的 intent，我們將 intent name 命名為 score。在下面的 `User says` 欄位，顧名思義就是使用者對 bot 說了什麼話。這邊我們把一些可能的問法都列出來，讓這些問法都能夠 mapping 到這個 intent。在最下方的 `Text response` 這個欄位中，必須填上要給使用者的回覆。也就是說，當使用者輸入的句子 mapping 到這個 intent 時，chatbot 該給出的回覆。可以看到這裡寫了兩個回覆，一個是正確的評分標準，另一個是「不告訴你」。API.AI 會從這兩個句子中隨機挑選一個回覆。

![apiai_score](https://storage.googleapis.com/2017-hackathon-data-download/hackathon-bot-img/apiai_score_intent.png)

在這邊可以看到，在畫面右邊的測試區輸入問題後，chatbot 已經可以正確把「評分標準」對應到 score 這個 intent，我們的 chatbot 就可以正確做回覆囉。按下測試區的麥克風按鈕和 play 按鈕，還可以用語音來輸入輸出，實在是很炫的功能。

我們會建議大家在還沒有開始實作 chatbot 之前，先把 chatobot 可能遇到的問題想一想，並且整理下來。並在整理完之後對這些問題進行整理，把類似的問題群聚在一起，將聚在一起的問題賦予一個共同的 intent。另外，也可以開始進行 entity 的解構，將這些問題中可能的 entity 先行提取出來。就像寫程式那樣，逐步對問題進行抽象，直到最後變成 intent 與 entity。

舉個複雜一點的例子來說，假如我們想實現訂機票的功能。那麼可能的問題如下：

- 我要訂機票
- 我要訂飛機票
- 我要訂 9/9 的飛機票
- 我要訂 9/9 到舊金山的飛機票
- 我要訂 9/9 從台北到舊金山的飛機票
- 我要訂 9/9 從台北到舊金山，航班號碼為 PIX123 的機票
- 我要訂到舊金山的飛機票

上面這些句子都對應到了「訂機票」這個 intent，所以他們都該歸類在 `booking_flight` 這個 intent 底下。但我們可以發現，雖然都是訂機票的句子，可是有的句子講的很清楚，有的句子講的不明不白，有很多資訊需要補齊。這些需要被補齊的資訊就是 entity。

因此，我們可以想像一下「訂機票」是這樣的一個函數：

```python
booking_flight(date=date,  departure_time=departure_time, from=from, to=to, flight_number=flight_number)
```

其中帶有參數 `date` 日期、 `departure_time` 出發時間、 `from` 出發地、 `to` 目的地、 `flight_number` 航班號碼等等。然後我們不斷的透過問答，引導使用者回應出所有該回答的參數。也只有在參數都齊全之後才有辦法進行訂票。

下次再讓我們來看看 etity 的設定～
