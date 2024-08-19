사용자 키 발급
==========================

개인별 데이터를 기록하기 위해서는 서버로 부터 사용자키를 부여 받는다.

### API URL

/api/ide/user/event/certificate

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|userkey|사용자키|string|${\color{red}필수}$|이벤트 체크인 성공시 부여 받은 사용자키|

### 사용자키 인증 및 만료 체크 예제 (jQuery)

```javascript
var url = '/api/ide/user/event/certificate';
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
	if( rs == 'not-existed-userkey' || rs == 'expired-userkey' )
	{
		console.log( '사용자키가 존재하지 않거나, 만료된 키 입니다.' );
		return;
	}
	if( rs == 'closed-service')
	{
		console.log( '현재 이벤트가 중단된 상태입니다.' );
		return;
	}
	console.log( '인증된 사용자키 입니다.' );
})
.fail(function (rs) {
	console.warn('There is a communication failure with the Rexsys server.');
});
```