미디어 목록 조회
==========================

등록된 미디어를 조회합니다.

## URL

/api/media//item/list

## Parameter

|파라미터|개요|타입|필수여부|비고|
|---|---|---|---|---|
|project|프로젝트 코드|string|필수*|-|
|token|토큰(키)|string|필수*|클라이언트 인증에서 받은 토큰키|
|category|미디어 index 혹은 미디어의 id|string|필수*|관리자 페이지에서 생성한 미디어의 index 혹은 id 값|
|page|페이지번호|int|선택|페이지번호 미 입력시 기본값 = 1 |
|per_record_num|한 페이지에 보여지는 미디어수|int|선택|미 입력시 기본값 = 50|
|text|검색어|string|선택|Tag 검색어 조회|
|sort|정렬방법|string|선택|미 입력시 기본값 = 'desc'<br>(desc : 최근순, asc : 오랜된 순, like : 인기순)|
|used|승인된 미디어 여부|stirng|선택|미 입력시 기본값 = ''<br>(모두 : '', 승인된 미디어만 : y, 미승인된 미디어만 : n|
|term|유효기간 설정여부|int|선택||미 입력시 기본값 = ''<br>(모두 : '', 유효기간 설정된 미디어만 : y |

## jQuery 사용시. 예제

```javascript
var url = '/api/media//item/list';
var data = {
	project: '프로젝트 코드'
	token: '토큰키',
};

var postdata= window.btoa(encodeURIComponent(JSON.stringify( data )));
$.ajax({
	url: url,
	data: postdata,
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

## Result Json.

```json
{
     "rexsys": {
        "result": {
            "current_block": 1,
			"page": 1,
            "total_block": 1,
            "total_page": 1,
            "total_record": 45,
            "url": "http://127.0.0.1"	
            "data": [
                {
                    "category": 10,
                    "datetime": "2024-06-24 15:16:00",
                    "filename": "thumb_5-19__1___1_2.jpg",
                    "filesize": 7034,
                    "group": "image",
                    "idx": 45,
                    "like": 0,
                    "mimetype": "image/jpeg",
                    "note": {
                        "content": "",
                        "custom": null,
                        "id": "",
                        "link": "",
                        "name": "Untitled",
                        "tag": ""
                    },
                    "realname": "thumb_5-19__1__.jpg",
                    "thumb": "http://127.0.0.1/media/demo/10/thumb_thumb_5-19__1___1_2.jpg",
                    "timestamp": 1719209760,
                    "uri": "/media/demo/10/thumb_5-19__1___1_2.jpg",
                    "url": "http://127.0.0.1/media/demo/10/thumb_5-19__1___1_2.jpg",
                    "used": "y"
                },
                {
                    "category": 10,
                    "datetime": "2024-06-24 15:16:00",
                    "filename": "thumb_5-19__1.jpg",
                    "filesize": 4995,
                    "group": "image",
                    "idx": 44,
                    "like": 0,
                    "mimetype": "image/jpeg",
                    "note": {
                        "content": "",
                        "custom": null,
                        "id": "",
                        "link": "",
                        "name": "Untitled",
                        "tag": ""
                    },
                    "realname": "thumb_5-19_.jpg",
                    "thumb": "http://127.0.0.1/media/demo/10/thumb_thumb_5-19__1.jpg",
                    "timestamp": 1719209760,
                    "uri": "/media/demo/10/thumb_5-19__1.jpg",
                    "url": "http://127.0.0.1/media/demo/10/thumb_5-19__1.jpg",
                    "used": "y"
                }
			]
	}
	"server": {
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1719209805,
            "version": "2.0"
        }
	}
}
```
