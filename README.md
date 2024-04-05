# calc-mie/pages-calc-mie-jp

計算研究会のホームページです。
[https://www.calc.mie.jp/](https://www.calc.mie.jp/)で運用されています。

## 新しく記事を追加したい場合

新しく記事を追加したい場合はまず、ブランチを切ってください。

その後、`_posts`に`年-月-日付-ページ名.markdown`という形式でファイルを追加します。
現在の日付より未来のものも書くことができますが、無視されてページに表示されません。

完成したらコミットし、プルリクエストをGitHub上で投げてください。

## VSCodeとDockerを用いた編集

VSCodeとDockerを用いることで、ローカルでページを確認しながら更新できます。

![VSCodeによる編集中の画像](./images/2023-04-28_2.39.53.png)

1. VSCodeとDockerをインストールします。
1. VSCodeにdevcontainer拡張機能を導入します。
1. このリポジトリを開きます。
1. `F1`キーを押し、`Dev Containers: Rebuild Container`を選択します。
1. 環境が立ち上がります。
1. ホストのブラウザから[localhost](http://localhost:4000/)へアクセスしてください。
1. 画面下のターミナルを閉じた場合は`jekyll serve -H 0.0.0.0 -s /usr/src/app --watch --verbose --trace`をターミナルで叩き直せば動きます。

- Q: jekyllのログを見たい場合は？
  A: docker desktopとかのcomposeのログを見てください。
- Q: _config.ymlを更新したのに反映されないよ！
  A: `F1`から`Dev Containers: Rebuild Container`してください。多分反映されます。
