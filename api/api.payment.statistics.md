기부 통계
==========================

기부 통계를 가져옵니다.

### API URL

/api/ide/payment/statistics


## Parameter (Method : POST, Only API)

API 로 접근할때만 사용하며, JSON CACHE 데이터는 파라미터를 전송하지 않습니다.

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|

## 기부 통계 불러오기 ( API : jQuery )

```javascript
var url = '/api/ide/payment/statistics
';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키'
};

var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };

$.ajax({
	url: url,
	data: encodedata,
	method: 'POST',
	dataType: 'json'
})

.done(function (rs) {
	if( rs.rexsys.result.token != null )
	{
		console.log( '** data', rs.data );	
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

## 기부 통계 결과


```javascript

{
    "rexsys": {
        "result": {
            "clients": [
                {
                    "id": "kiosk-1",
                    "point": 165000
                },
                {
                    "id": "kiosk-2",
                    "point": 8000
                },
                {
                    "id": "kiosk-3",
                    "point": 30000
                }
            ],
            "event": {
                "count": 128,
                "point": 128000
            },
            "course": [
				{
                    "id": "orphanage-1",
                    "point": 165000
                },
                {
                    "id": "orphanage-2",
                    "point": 8000
                },
                {
                    "id": "orphanage-3",
                    "point": 30000
                }
			],
			"starter-point": 0,
            "today": {
                "count": 0,
                "point": 0
            },
            "total": {
                "count": 376,
                "point": 1525000
            },
			
        },
        "server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1720420151,
            "version": "2.0"
        }
    }
}


````