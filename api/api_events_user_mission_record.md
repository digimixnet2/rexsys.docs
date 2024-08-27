이벤트 사용자 미션 기록
==========================
이벤트의 사용자별 미션 수행한 내용으로 저장한다.

### API URL

/api/ide/events/user/mission/record

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|userkey|사용키|string|${\color{red}필수}$|이벤트 체크인한 후 부여받은 사용자키|
|mission_id|미션아이디|string|${\color{red}필수}$|아키텍처의 오브젝트 아이디|
|point|미션아이디|int|${\color{blue}선택}$|미션 수행에 따른 지급 포인트|

### 이벤트 사용자 미션 수행 결과 예제 (jQuery)
```javascript
var url = '/api/ide/events/user/mission/record';
var postdata = {
	project : '프로젝트 코드'
	userkey : '이벤트 체크인한 후 부여받은 사용자키',
	mission_id : '아키텍처 아이디',
	point : '포인트'
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
		console.log( '** result', rs.rexsys.result );
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
            "data_id": "dgmx-kiosk-2",
            "data_idx": 18,
            "data_type": "client",
            "point": 1000,         
            "regi_datetime": "2024-08-27 19:37:14",
            "remote_ip": "192.168.0.15",
            "timestamp": 1724755034,
            "user_key": "XMN2kfcwZSCCLka...5xkptfWcUtNn1dXhhBDpRN...cX3DAZBZRldtG6ICkymcV2jPSar...t9vs6u7H7bw="
        },
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1724755034,
            "version": "2.0"
        }
    }
}
```
