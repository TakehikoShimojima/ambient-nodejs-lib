# ambient-lib Ambientのnode.jsライブラリー

Ambientのnode.jsライブラリーです。
[Ambient](https://ambidata.io)はIoT用のクラウドサービスで、センサーデーターを受信し、蓄積し、可視化(グラフ化)します。

## インストール

```sh
$ npm install ambient-lib
```

## モジュールの読み込み

```javascript
var ambient = require('ambient-lib');
```
## Ambientへの接続

```javascript
ambient.connect(チャネルId, ライトキー[, リードキー[, ユーザーキー]]);
```
Ambientにデーターを送信するときは、チャネルIdとライトキーを指定してAmbientに接続します。

## Ambientへのデーター送信

```javascript
ambient.send(data, callback(err, res, body));
```

* パラメーター
 * ```data```: 次のようなJSON形式で、キーは```d1```から```d8```のいずれかを指定します。
```javascript
var data = {d1: 1.1, d2: 2.2};
```
 * ```callback```: データー送信後に呼ばれるコールバック関数。パラメーターは```request```モジュールのコールバック関数のパラメーターと同じです。

こんな風に使います。

```javascript
ambient.send({d1: 1.1, d2: 2.2}, function(err, res, body) {
    if (err) {
        console.log(err);
    }
    console.log(res.statusCode);
});
```

## Ambientへの複数データー一括送信

複数データー一括送信も用意しました。

```javascript
ambient.bulk_send(dataarray, callback(err, res, body));
```

* パラメーター
 * ```dataarray```: 次のような形式の配列です。
 ```created```はデーターの生成時刻で、値は“YYYY-MM-DD HH:mm:ss.sss”という形式か、 数値を渡します。
 数値を渡した場合は1970年1月1日00:00:00からのミリ秒と解釈されます。

```javascript
var dataarray = [
    {created: '2016-07-07 12:00:00', d1: 1.1, d2: 2.1},
    {created: '2016-07-07 12:01:00', d1: 1.5, d2: 3.8},
    {created: '2016-07-07 12:02:00', d1: 1.0, d2: 0.8}
];
```
