사용자 로드맵 로그 데이터
==========================

사용자 로드맵 로그 데이터

### API URL

/api/ide/user/roadmap/log

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|userkey|사용자키|string|${\color{red}필수}$|이벤트 체크인 성공시 부여 받은 사용자키|

### 사용자키 로드맵 로그 예제 (jQuery)

```javascript
var url = '/api/ide/user/roadmap/log';
var postdata = {
	project : '프로젝트 코드'
	userkey : '이벤트 체크인 성공시 부여 받은 사용자키',
};

var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
$.ajax({
	url: url,
	data: encodedata,
	method: 'POST',
	dataType: 'json'
})

.done(function (rs) {
	console.log( '*** roadmap data', rs.rexsys.result );
})
.fail(function (rs) {
	console.warn('There is a communication failure with the Rexsys server.');
});
```
