## 解决问题

我们常用promise和async，await去解决回调地狱的问题，但却抛出另一个问题（异常捕获），每次处理异常，要么使用promise的catch拦截，要么使用try catch捕获，从而让我们的代码上看起来非常不优雅，而await-to-js收口了这个功能，让我们代码在处理异常上更加美观

## 基本使用

``` ts
const to = require('await-to-js').default

const test = () => (
	new Promise(r => {
		setTimeout(() => {
		
			r(12)
		}, 3000);
	})
)

async function run () {
	const [err, data] = await to(test())
	console.log(err, data)
}

run()

```


## 源码分析

翻看源码，其本质上就是通过promise来处理：
1. 返回当前的promise
2. 对返回的promise进行then和catch的拦截处理，如果成功，必然执行then，则就返回[null, data], 如果失败，则触发catch，返回[error, undefined]

```js
const to = (promise) => {
  return promise.then(data => [null, data]).catch(err => [err, undefined])
}

```