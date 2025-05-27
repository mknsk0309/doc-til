# SFCへの記述の基本 | テンプレートブロック編

## マスタッシュ構文

変数を表示させる基本構文は `{{ }}` を使用する。

## 属性に変数をバインドする

```txt
v-bind:属性名="テンプレート変数"
```

```html
<a v-bind:href="url" target="_blank">Nuxt.jsのサイト</a>
```

## イベントを設定する

```txt
v-on:イベント名="イベント発生時に実行するメソッド名"
```

## 双方向データバインディング

```txt
v-model="テンプレート変数"
```

```html
<input type="text" v-model="inputNameModel">
```

## HTML 文字列をそのまま表示させる

```txt
v-html="HTML記述のテンプレート変数
```

```html
<section v-html="htmlStr"></section>
```

## 静的コンテンツ表示

マスタッシュ構文も含め、は以下のタグ内のテンプレート記述を全て無効化する。

```html
<section v-pre>
  <p v-on:click="showHello">{{ hello! }}</p>
</section>
```

## データバインディングを初回のみに制限する

最初に表示した時点の値で固定され、その後、変数の値が変化しても表示内容は変化しない。

```html
<p v-once>金額は{{ price }}円です。</p>
```

## マスタッシュ構文の非表示

マスタッシュ構文がレンダリングされて、テンプレート変数 `hello` の値が `p` タグないに表示されるまで、`p` タグには `v-cloak` 属性が付与される。
`hello` の値が表示されると同時に、`v-cloak` 属性が削除される。

```vue
<template>
  <p v-cloak>{{ hello }}</p>
</template>
<style>
  [v-cloak] {
    display: none;
  }
</style>
```

## 条件分岐

条件に合致しなかった場合、タグそのものはレンダリングされない。

```txt
v-if="条件"
  ...
v-else-if="条件"
  ...
v-else
```

```html
<p>
  点数は{{ randomNumber }}点で
  <span v-if="randomNumber >= 80">優です。</span>
  <span v-else-if="randomNumber >= 70">良です。</span>
  <span v-else-if="randomNumber >= 60">可です。</span>
  <span v-else>不可です。</span>
</p>
```

## 表示／非表示の切り替え

条件によらずレンダリングされ、その上で条件が `false` の場合は非表示となる。

```txt
v-show="条件"
```

```html
<p v-show="showOrNot">
  条件に合致したので表示
</p>
```

## `v-if`, `v-show` の使い分け

- `v-if`

  表示／非表示の切り替えレンダリングコストがかかるため、表示／非表示が画面表示段階で決まっている場合に使用する。

- `v-show`

  初回レンダリングコストはかかるが、表示／非表示の切り替えコストが低いため、画面表示後に表示／非表示が頻繁に切り替わる場合に使用する。

## ループ処理

```txt
v-for="エイリアス in ループ対象"
```

`v-for` を利用する場合は、`v-bind:key` ディレクティブを記述することが推奨されている。
`v-bind:key` ディレクティブの値でもって、Vue 本体がループによって生成された各要素を識別する。

### 配列のループ

```txt
v-for="要素を格納する変数 in ループ対象の配列"
  または
v-for="(要素を格納する変数, インデックスを格納する変数) in ループ対象の配列"
```

```html
<ul>
  <li
    v-for="(cocktailName, index) in cocktailList"
    v-bind:key="cocktailName">
      {{ cocktailName }}(インデックス{{ index }})
  </li>
</ul>
```

### オブジェクトのループ

```txt
v-for="(各プロパティの値を格納する変数, 各プロパティ名を格納する変数) in ループ対象のオブジェクト"
  または
v-for="(各プロパティの値を格納する変数, 各プロパティ名を格納する変数, インデックス値を格納する変数) in ループ対象のオブジェクト"
```

```html
<dl>
  <template
    v-for="(value, key) in whiteLady"
    v-bind:key="key">
    <dt>{{ key }}</dt>
    <dd>{{ value }}</dd>
  </template>
</dl>
```

### Mapのループ

```txt
v-for="[各要素のキーを格納する変数, 各要素の値を格納する変数] in ループ対象のMap"
```

```html
<ul>
  <li
    v-for="[id, cocktailName] in cocktailList"
    v-bind:key="id">
      IDが{{ id }}のカクテルは{{ cocktailName }}
  </li>
</ul>
```
