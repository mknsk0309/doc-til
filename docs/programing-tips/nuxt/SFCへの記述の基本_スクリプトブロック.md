# SFCへの記述の基本 | スクリプトブロック編

## SFCとは

単一ファイルコンポーネント（`Single-File Componenjs`）  
HTML、CSS、JavaScript/TypeScript をひとつのファイルにまとめることができる。

## リアクティブ変数の定義

```js
const 変数名 = ref();
```

```js
const 変数名 = reactive(
  オブジェクト
);

// 例
const rectangle = reactive({
  width: widthInit,
  width: heightInit
});
```

### リアクティブ変数の監視

```js
watchEffect(
  (): void => {
    リアクティブな変数に応じて実行される処理
  }
);

// 例
watchEffect(
  (): void => {
    priceMsg.value =getCocktailInfo(cocktailNo.value)
  }
);
```

```js
watch(監視対象リアクティブな変数,
  (newVal: データ型, oldVal: データ型): void => {
    監視対象が変化した際に実行される処理
  },
  {immediate: true} //アプリケーションの初回起動時にアロー関数内の処理を実行するか
);

// 例
watch(cocktailNo,
  (): void => {
    prioceMsg.value = getCocktailInfo(cocktailNo.value);
  }
);
```

## 算出プロパティの定義

```js
const 変数名 = computed(
  (): 算出結果のデータ型 => {
    算出処理
    return 算出結果
  }
);
```

## メソッドの定義

```js
const メソッド名 = (引数): void => {
  ...
}
```

### アロー関数の引数定義のパターン

1. 引数なし

    ```js
    const onButtonClick = (): void => {
      ...
    }
    ```

2. イベントオブジェクトのみ

    ```js
    const onButtonClick = (event: Event): void => {
      ...
    }
    ```

3. 任意の引数

    ```js
    const onButtonClick = (label: string, point: number): void => {
      ...
    }
    ```

4. 任意の引数とイベントオブジェクト

    ```js
    const onButtonClick = (label: string, event: Event): void => {
      ...
    }
    ```

## ライフサイクルフック

| ライフサイクルフック関数 | 実行タイミング                                                             |
| ------------------------ | -------------------------------------------------------------------------- |
| `onBeforeMount`          | コンポーネントの解析処理後、決定したDOMをレンダリングする直前              |
| `onMounted`              | DOMのレンダリングが完了し、表示状態（Mounted 状態）になった時点            |
| `onBeforeUpdate`         | りアクティブデータが変更され、DOMの再レンダリング処理を行う前              |
| `onUpdated`              | DOMの再レンダリングが完了した時点                                          |
| `onBeforeUnmount`        | コンポーネントのDOMの非表示処理を開始する直前                              |
| `onUnmounted`            | コンポーネントのDOMの非表示処理が完了した（Unmounted な状態になった）時点  |
| `onErrorCaptured`        | は以下のコンポーネントを含めてエラーを検知したとき                         |
| `onActivated`            | コンポーネントが待機状態でなくなった時点                                   |
| `onDeactivated`          | コンポーネントが待機状態になった時点                                       |
| `onRenderTracked`        | りアクティブ変数に初めてアクセスが発生した時点                             |
| `onRenderTriggered`      | リアクティブ変数が変更されたのを検知して、その変数へのアクセスがあった時点 |

- `onRenderTracked()`, `onRenderTriggered()` 以外

  ```js
  onMounted(
    (): void => {
      行う処理
    }
  );
  ```

- `onRenderTracked()`, `onRenderTriggered()` ; デバッグようの関数

  ```js
  onRenderTracked(
    (event: DebuggerEvent): void => {
      行う処理
    }
  );
  ```
