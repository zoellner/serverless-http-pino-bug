# serverless-http-pino-bug

This repo demonstrates a bug introduced in `serverless-http@3.1.1`

Use with
```
npm start
```
Then run
```
curl localhost:8080
```

You can see the request is logged twice:
```
GET / (λ: ProxyFunction)
{"level":30,"time":1687812431617,"pid":52647,"hostname":"laptop.local","req":{"id":1,"method":"GET","url":"/","query":{},"params":{},"headers":{"host":"localhost:8080","user-agent":"curl/7.82.0","accept":"*/*","x-request-id":"56a2a57a-89d7-4ff6-b6b1-d33705d0422f","content-length":0},"remoteAddress":"127.0.0.1"},"res":{"statusCode":200,"headers":{"x-powered-by":"Express","content-type":"application/json; charset=utf-8","content-length":"15","etag":"W/\"f-VaSQ4oDUiZblZNAEkkN+sX+q3Sg\""}},"responseTime":3,"msg":"request aborted"}
{"level":30,"time":1687812431617,"pid":52647,"hostname":"laptop.local","req":{"id":1,"method":"GET","url":"/","query":{},"params":{},"headers":{"host":"localhost:8080","user-agent":"curl/7.82.0","accept":"*/*","x-request-id":"56a2a57a-89d7-4ff6-b6b1-d33705d0422f","content-length":0},"remoteAddress":"127.0.0.1"},"res":{"statusCode":200,"headers":{"x-powered-by":"Express","content-type":"application/json; charset=utf-8","content-length":"15","etag":"W/\"f-VaSQ4oDUiZblZNAEkkN+sX+q3Sg\""}},"responseTime":3,"msg":"request aborted"}
(λ: ProxyFunction) RequestId: 1a89d934-694b-4862-8242-16fdee7ba79e  Duration: 255.43 ms  Billed Duration: 256 ms
```

If you run the same commands after downgrading to `serverless-http@3.1.0` using `npm i serverless-http@3.1.0` the request is only logged only once as expected:

```
GET / (λ: ProxyFunction)
{"level":30,"time":1687812464394,"pid":52684,"hostname":"laptop.local","req":{"id":1,"method":"GET","url":"/","query":{},"params":{},"headers":{"host":"localhost:8080","user-agent":"curl/7.82.0","accept":"*/*","x-request-id":"731338fb-db68-4c0b-8de9-4391319079d2","content-length":0},"remoteAddress":"127.0.0.1"},"res":{"statusCode":200,"headers":{"x-powered-by":"Express","content-type":"application/json; charset=utf-8","content-length":"15","etag":"W/\"f-VaSQ4oDUiZblZNAEkkN+sX+q3Sg\""}},"responseTime":3,"msg":"request aborted"}
(λ: ProxyFunction) RequestId: ebdb38ba-c2a5-4ea2-897b-e8e5aae8f7c7  Duration: 204.69 ms  Billed Duration: 205 ms
```
