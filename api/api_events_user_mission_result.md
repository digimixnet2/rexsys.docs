이벤트 사용자 미션 수행 결과
==========================
이벤트의 사용자별 미션 수행 목록을 모두 출력한다.

### API URL

/api/ide/events/user/mission/result

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|userkey|사용키|string|${\color{red}필수}$|이벤트 체크인한 후 부여받은 사용자키|

### 이벤트 사용자 미션 수행 결과 예제 (jQuery)
```javascript
var url = '/api/ide/events/user/mission/result';
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
        "result": {
            "data": [
                {
                    "datetime": "2024-08-27 20:05:30",
                    "idx": 1,
                    "mission_id": "client-0",
                    "mission_idx": 46,
                    "mission_name": "",
                    "mission_point": 1000,
                    "remote": "192.168.0.15",
                    "timestamp": 1724756730
                },
                {
                    "datetime": "2024-08-27 20:13:31",
                    "idx": 2,
                    "mission_id": "A-01",
                    "mission_idx": 45,
                    "mission_name": "",
                    "mission_point": 1000,
                    "remote": "192.168.0.15",
                    "timestamp": 1724757211
                },
                {
                    "datetime": "2024-08-27 20:13:38",
                    "idx": 3,
                    "mission_id": "autoland-gj-1",
                    "mission_idx": 11,
                    "mission_name": "",
                    "mission_point": 1000,
                    "remote": "192.168.0.15",
                    "timestamp": 1724757218
                }
            ],
            "mileage": 3000
        },
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1724757226,
            "version": "2.0"
        }
    }
}
```
