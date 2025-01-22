# express 미들웨어는 동기로 되어 있을까? 비동기로 되어 있을까?
기본적으로 express의 미들웨어는 stack로 구성되어 콜백 형식으로 함수들을 다음으로 전달한다.

예를 들어 아래와 같은 코드가 구성되어 있다고 가정하자.
```javascript
app.get('/hello', function (req, res, next) {
  console.log('test1')
  next()
}, function (req, res) {
  res.send('test')
})
```

`/hello`에 미들웨어 함수가 하나있고 그 후 다음 응답을 처리하는 함수가 존재한다.
이럴 경우 아래 이미지와 같이 /hello라는 경로의 stack 프로퍼티에 함수의 배열로 저장된다.

