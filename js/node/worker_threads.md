# Worker Thread概要
## 特徴
- CPU insentiveな処理には向いている。I/O insentiveな処理だとあまりお役には立てないかもしれないとのこと。I/OについてはNode.js自体が持つ非同期なI/O処理のほうがWorkersよりは向いている。
- 公式参考：https://nodejs.org/api/worker_threads.html#worker_threads_worker_threads

## 導入バージョンについて
- v10.5.0から導入されている
- v11.10.0においてもまだexperimental扱いなのでまだ改修が入るかもしれない

## MessageChannel
- Actor modelを参考にしているようでスレッド間のメッセージパッシングがClass:MessageChannelを利用できる。以下オフィシャルのコードをそのまま参考に掲載
- TODO：どうやってやりとりをする先を指定しているのかやり方を調べる。
- 公式参考：https://nodejs.org/api/worker_threads.html#worker_threads_class_messagechannel



```javascript

const { MessageChannel } = require('worker_threads');

const { port1, port2 } = new MessageChannel();
port1.on('message', (message) => console.log('received', message));
port2.postMessage({ foo: 'bar' });
// Prints: received { foo: 'bar' } from the `port1.on('message')` listener

```