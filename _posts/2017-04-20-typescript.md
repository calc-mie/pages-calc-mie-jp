---
layout: post
title: "TypeScriptについて"
author: "naca_cyan13"
---

[](
TypeScriptとはなにか\
*JavaScriptとの比較\
使い方とGreetingプログラム\
TSCについて\
文法の良いところ\
tsconfigについて\
強力なデバッグ機能のsourceMapについて\
今後やりたいこと
)

AltJsの一つです。静的型付け言語で、フロントエンドを記述することができます。

# 使い方

TypeScriptのコンパイラ`tsc`は以下のコマンドでインストールできます。(`npm`が必要)

```shell
$ npm install -g typescript
```

TypeScriptのチュートリアルでよくあるGreeterプログラムを試しにかいてみます。

```
//main.ts
class Greeter {
      private name : string;
      constructor(name : string) {
        this.name = name;
      }
      public Greet() : string {
        return "Hello, This is " + this.name + ".";
      }
}

var naca_cyan13 = new Greeter("naca_cyan13");

document.body.innerHTML = naca_cyan13.Greet();
```

インストールした`tsc`コマンドで`main.ts`をコンパイル。

```shell
$ tsc main.ts
```

`main.js`というファイルが生成されるので、適当なHtmlに読み込ませてブラウザで実行すると`Hello, This is naca_cyan13.`と表示されます。

# TypeScriptでいいところ

Microsoftが開発元であることもあり、言語仕様がC#と似ています。VisualStudioでの開発にも対応していたり、ドキュメントも結構豊富なので学習がしやすいです。
TypeScriptは複数の`.ts`ファイルをコンパイルして一個の`.js`にする感じでコンパイルすることができます。この機能によってjavascriptよりもモジュール分割（ファイル分割）が簡単です。
すでに多数のTypeScript対応のゲームフレームワークが登場しているので、ゲーム開発にも向いているでしょう。

# tsconfig.json

`tsconfig.json`とは`tsc`を使用するときにコンパイルオプションを渡せる設定ファイルです。

試しに以下のようなjsonを`tsconfig.json`として配置してみましょう。

```json
{
    "compilerOptions": {
    	"module": "system",
    	"noImplicitAny": true,
    	"removeComments": true,
    	"preserveConstEnums": true,
    	"sourceMap": true,
    	"outFile": "main.js"
    },
    "include": [
	    "./"
    ]
}
```

この`tsconfig.json`が配置されているディレクトリで`tsc`を起爆すると

- `./`に存在するすべての`.ts`ファイルが`main.js`にまとめてコンパイルされる。
- その際`<any>`型を認めない。
- `main.js`にはコメントを含まない。
- 列挙体の順序を保存する。
- デバッグ機能**sourceMap**を有効にする。

というようなコンパイルが実行されます。

# 強力なデバッグ機能**sourceMap**

`.ts`をコンパイルすると`.js`が出てきます。そのコードがブラウザ上でエラーを出した時、`.js`ファイルのどこでエラーを起こしているのかは開発者コンソールを覗けば直ぐわかります。
しかし、`.ts`ファイルでわからないと意味がないです。
そこで登場するのが**sourceMap**です。

**sourceMap**は`.js`と`.ts`を結びつける関係を定義してあるもので、`.js`でエラーが発生したらそのエラーと対応する`.ts`の行をブラウザが提示してくれるようになります。またこの**sourceMap**はtypescriptに限った機能ではなく他のAltJsなどのコンパイラの機能にもあったりします。

# 今後やりたいこと

phaserというゲームフレームワークでTypeScriptを使ってゲームをつくってみたいと考えています。