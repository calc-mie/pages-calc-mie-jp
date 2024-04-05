---
layout: post
title: "唐突にでてきたJSONインジェクションについて"
author: "_cyan13"
---

なんか唐突に出てきたjsonインジェクションについて書きます。

# まあとりあえず例

json文字列の中に変数を受け込みたい場合以下みたいにコーディングする時があります。

```javascript
dataStr = "value2";
jsonStr = "{'key1':'value1', 'key2':'" + dataStr + "'}";

console.log(jsonStr); // => {'key1':'value1', 'key2':'value2'}
```

これをすこし工夫すると、以下のようにキー値対が増やせてしまいます。


```javascript
dataStr = "value2', 'key1':'fake_value1";
jsonStr = "{'key1':'value1', 'key2':'" + dataStr + "'}";

console.log(jsonStr); 
// => {'key1':'value1', 'key2':'value2', 'key1':'fake_value1'}
```

# 実用上の問題

上のコードの`dataStr`にクライアントから送信された文字列をそのまま代入していた場合、データを不正に増やせるので、クライアントに本来書き換え権限が無いデータを書き換えられてしまう可能性があります。

# 対策

直接文字列経由するようなものはやめ、一回オブジェクトに起こして、それを`JSON.stringify()`するなどすると回避できそうですね。（適当なので間違ってたらコメントしてください）。

```javascript
dataStr = "value2', 'key1':'fake_value1";
temp_obj = {'key1':'value1', 'key2': dataStr};
jsonStr = JSON.stringify(temp_obj);
```

### 参考文献

「JSON文字列へのインジェクション」と「パラメータの追加」：NoSQLを使うなら知っておきたいセキュリティの話 - ＠IT
http://www.atmarkit.co.jp/ait/articles/1306/05/news006.html 


