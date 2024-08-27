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
        "result": [
            {
                "datetime": "2024-08-27 18:56:39",
                "idx": 1,
                "mission_id": "CODE-1",
                "mission_idx": 16,
                "mission_name": "",
                "remote": "192.168.0.15",
                "timestamp": 1724752599
            }
            ...
            {
                "datetime": "2024-08-27 18:50:39",
                "idx": 1,
                "mission_id": "CODE-2",
                "mission_idx": 11,
                "mission_name": "",
                "remote": "192.168.0.15",
                "timestamp": 1724753001
            }

        ],
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1724753101,
            "version": "2.0"
        }
    }
}
```
