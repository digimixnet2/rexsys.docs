게시판 목록 조회
==========================

게시판의 글을 조회합니다.

## API URL

/api/ide/note/board/item/list

## Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|---|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|id|미디어 index 혹은 미디어의 id|string|${\color{red}필수}$|관리자 페이지에서 생성한 미디어의 index 혹은 id 값|
|page|페이지번호|int|선택|페이지번호 미 입력시 기본값 = 1 |
|per_record_num|한 페이지에 보여지는 미디어수|int|선택|미 입력시 기본값 = 50|

### 목록조회 예제(jQuery)

```javascript
var url = '/api/ide/media/item/list';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키',
	category: 'media-1' // or database table column tb_idx
	page : 1, // 1페이지 호출
	per_record_num : 100 // 한페이지에 100개 보여줌.
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

### Return Result Json. ( /api/media/item/list )

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
                        "tag": []
                    },
                    "realname": "thumb_5-19__1__.jpg",
                    "thumb": "http://127.0.0.1/media/demo/10/thumb_thumb_5-19__1___1_2.jpg",
                    "timestamp": 1719209760,
                    "uri": "/media/demo/10/thumb_5-19__1___1_2.jpg",
                    "url": "http://127.0.0.1/media/demo/10/thumb_5-19__1___1_2.jpg",
                    "used": "y",
                    "writer": "아무개"
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
                        "tag": ["산", "바다", "하늘"]
                    },
                    "realname": "thumb_5-19_.jpg",
                    "thumb": "http://127.0.0.1/media/demo/10/thumb_thumb_5-19__1.jpg",
                    "timestamp": 1719209760,
                    "uri": "/media/demo/10/thumb_5-19__1.jpg",
                    "url": "http://127.0.0.1/media/demo/10/thumb_5-19__1.jpg",
                    "used": "y",
                    "writer": "아무개"
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
