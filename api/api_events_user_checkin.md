이벤트 사용자 체크인
==========================
이벤트 사용자 체크인으로 일정한 정보를 받고, 사용자키를 부여 받는다.

### API URL

/api/ide/events/user/certificate

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|user_nickname|사용자 이름(실명)|string|${\color{red}필수}$|사용자가 사용할 별칭 혹은 별명|
|user_name|사용자 이름(실명)|string|${\color{red}필수}$|없으면 빈공간으로 전송|
|user_email|사용자 이메일주소|string|${\color{red}필수}$|없으면 빈공간으로 전송|
|user_phone|사용자 휴대폰번호|string|${\color{red}필수}$|하이퍼(-) 없이 전송|
|agree|개인정보 동의여부|string|${\color{red}필수}$|y or n|

### 이벤트 사용자 인 예제 (jQuery)
```javascript
var url = '/api/ide/events/user/checkin';
var postdata = {
	project : '프로젝트 코드'
	user_nickname : '사용자 별명',
	user_name : '사용자 이름',
	user_email : '사용자 이메일 주소',
	user_phone : '사용자 휴대폰 번호',
	agree : 'y'
};

var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
$.ajax({
	url: url,
	data: encodedata,
	method: 'POST',
	dataType: 'json'
})

.done(function (rs) {
	if( rs.rexsys.result.EncodeData != null )
	{
		var decodedata = JSON.parse(decodeURIComponent(window.atob(rs.rexsys.result.EncodeData)))
		console.log( '** result', decodedata );	
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
        "result": {
            "EncodeData": "eyJ1c2VyX25hbWUiOiAiXHVjYzI4XHV...DBnRVdpVzdCaTRZemF4T2FoZWRzUjcweFlnZ1Jsd1kwZXZuZ3ZDTGZIUlBaRzFXQVQ1S25ROUlNYTZJRTdvaEF1RmQzcWdHYzF1YUxjR1hidXkraEJUMWFYWGZGaGhVMHA2UlhURS9tcXUrcld6UWU3TFJ1V0NtdVBxKzhzVnJpWWNzcXJyUUFheVJoSEY0UmFGWWRScWVPRVV0eTQ0PSIs...0NDUwLCAicmVtb3RlaXAiOiAiMTkyLjE2OC4wLjE1IiwgInBvaW50IjogMCwgInVzZXJfbmlja25hbWUiOiA...n0="
        },
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1724754450,
            "version": "2.0"
        }
    }
}
```
### EncodeData Decode 내용
```javascript
{
  "user_name": "차우람",
  "userkey": "dZFGcHaBHxEKT0gEWiW7Bi4YzaxOa...HRPZG1WAT5KnQ9IMa6IE7...6RXTE/mqu+rWzQe7LRuWCmuPq+8sVriYcsqrrQAayRhHF4...4=",
  "user_phone": "01012345678",
  "user_email": "",
  "user_idx": 13,
  "timestamp": 1724754450,
  "remoteip": "192.168.0.15",
  "point": 0,
  "user_nickname": "차마담"
}
```

