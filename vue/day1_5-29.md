# やったこと
1. 環境構築
2. 使う画像素材を反映させてみる

# 環境構築について
教えていただいたコマンドをそのまま打っていただけなので、意味がわからない・怪しい単語について調べました。 
1. `brew install yarn`
  homebrew… ソースコードを取得してビルドするパッケージ管理システム
  yarn… npm(Node package Manager)にかわるパッケージマネージャ(ライブラリの追加やインストールを容易にしてくれるもの)
2. `yarn (global) add @vue/cli`
  vue-cli…Commnad Line Interfaceの略で前準備をしてくれる
私はglobalを入れなかったのでこのプロジェクトのみで使えるvue-cliをインストールしました。
3. `yarn -s run vue -V`
  vueを実行して -Vのオプションでバージョンを確認することができました。
4. `vue create  .`
  プロジェクトの作成をしました。 .には任意のプロジェクト名を入れられます。
5. `yarn serve`
  プロジェクトを立ち上げます。

**localhost:8080で表示されました〜！**

# ファイルの構成
![https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/436259/ef6ddaf7-2076-5404-2e2a-3c221ebe3a48.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/436259/ef6ddaf7-2076-5404-2e2a-3c221ebe3a48.png)

- babel.config.js…Babelという次世代JavaScriptをES5に変換してくれるツールの設定をする
全部のブラウザが最新型のJavaScriptを理解できない場合もあるから昔の言葉に直す必要もある！

# 表示でけた！
index.htmlをのぞいてみると、、、

```html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```
![screencapture-localhost-8080-2020-05-30-00_32_49.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/436259/b4a5b87e-19d6-0692-a8df-d1090ccceef1.png)
あら不思議！何か表示されてる！

- ヤマメを揺らす女の子
- ヤマメ
- クロアシネコ

main.jsを見てみると、、、

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

mout()関数を使って#appにAppとやらを足している、、、？
`import App from './App.vue'` なのでApp.vueをのぞいてみよう！

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <Girl msg="女の子出てきて" />
    <Fish msg="ヤマメ" />
    <Cat msg="猫" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Girl from "./components/characters/Girl.vue";
import Fish from "./components/characters/Fish.vue";
import Cat from "./components/characters/Cat.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Girl,
    Fish,
    Cat
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```

`from ~`のファイルから取ってきたものをtemplateとしてexportしてる！
それぞれのファイルを見てみると、、、

```vue
<!-- Girl.vue -->
<template>
  <div class="girl">
    <img src="@/assets/girl.png" alt="女の子" />
  </div>
</template>

<script>
export default {
  name: "Girl",
  props: {
    msg: String
  }
};
</script>

```

```vue
<!-- Fish.vue -->
<template>
  <div class="fish">
    <img src="@/assets/fish.png" alt="お魚" />
  </div>
</template>

<script>
export default {
  name: "Fish",
  props: {
    msg: String
  }
};
</script>

```

```vue
<!-- Cat.vue -->
<template>
  <div class="cat">
    <img src="@/assets/cat.png" alt="猫" />
  </div>
</template>

<script>
export default {
  name: "Cat",
  props: {
    msg: String
  }
};
</script>

```

それぞれexportしてますね！`name`の部分が`App.vue`のタグになってます！

今日はここまで！