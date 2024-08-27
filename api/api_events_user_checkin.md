이벤트 사용자 인증
==========================
이벤트 사용자 체크인으로 부터 부여 받은 사용자키(USERKEY) 유효한지 검사한다.

### API URL

/api/ide/events/user/certificate

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|userkey|사용키|string|${\color{red}필수}$|이벤트 체크인한 후 부여받은 사용자키|

### 이벤트 사용자 인 예제 (jQuery)
```javascript
var url = '/api/ide/events/user/certificate';
var postdata = {
	project : '프로젝트 코드'
	userkey : '이벤트 체크인한 후 부여받은 사용자키',
};

var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
$.ajax({
	url: url,
	data: encodedata,
	method: 'POST',
	dataType: 'json'
})

.done(function (rs) {
	if( rs.rexsys.result. != null )
	{
		console.log( '** result', rs.rexsys.result );		// 미션 수행 내역(Array)
	}
	else
	{
		console.warn('There is a communication failure with the Rexsys server.');
	}
})
.fail(function (rs) {
	console.warn('There is a communication failure with the Rexsys server.');
});
```

### Retrun Result Json.

```javascript
{
    "rexsys": {
        "result": "checkin-user",
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1724753878,
            "version": "2.0"
        }
    }
}
```
|코드|상태|
|------|-----|
|checkin-user|체크인 중인 사용자(체크인 데이터 있음)|
|checkout-user|체크아웃 상태인 사용자(체크인 데이터 없음)|
|expired-user|사용자 키가 만료된 상태|


