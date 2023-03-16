---
title: "SlackのPush通知ガイド"
author: "@naca_nyan"
---

<style>
img {
  margin: 0 auto;
  border: 2px solid #ccc;
  width: 100%;
}
hr {
  margin: 50px auto;
  width: 80%;
}
@media (min-width: 600px) {
  img {
    margin: 0 auto;
    display: block;
    width: 50%;
  }
}
</style>

Slackのスマホへの通知をいい感じにするガイド。

情報ソースは[ここ](http://qiita.com/satodainu/items/ed8d09aacc3ce24a25c7)から。

## Slackの通知
Slackのアプリの通知の受信設定には２種類あって、

1. Slackチーム全体の通知設定
2. チャンネル単位の通知設定

を変更できます。

デフォルトの設定では、チーム全体設定は

* Only direct messages/highlight words (DMとハイライトのみ)

チャンネルは

* Mentions or highlight words (メンションとハイライト)

になっているはずです。

おすすめは、全体設定はいじらずに、通知を受け取りたいチャンネルだけ
All activityにしておく、ですかね。

特定のチャンネルはすべてのPostを通知するようにして、
他のチャンネルでは `@username` とか `@channel` とか言われない限り
通知を受け取らない、という感じになります。

以下、iOSでの変更の仕方を解説していきます。

## Slackチーム全体の通知設定

メッセージ画面で左←にスワイプして、Settingsをタップします。

![](/images/slack-notify-01.png)

---

Push Notificationsをタップします。

![](/images/slack-notify-02.png)

---

 * Activity of any kind (全ての通知を受信)
 * Only direct messages/highlight words (DMとハイライトのみ)
 * Only highlight words (ハイライトのみ)
 * Only direct messages (DMのみ)
 * Nothing (通知を受信しない)

という設定ができます。

![](/images/slack-notify-03.png)

## チャンネル単位の通知設定

設定したいチャンネルに行き、チャンネル名の部分をタップします。

![](/images/slack-notify-04.png)

---

Notificationsをタップします。

![](/images/slack-notify-05.png)

---

 * All activity (すべての通知を受信)
 * Mentions or highlight words (メンションとハイライト)
 * Nothing (通知を受信しない)

が設定できます。

![](/images/slack-notify-06.png)

