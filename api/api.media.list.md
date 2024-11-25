미디어 목록 조회
==========================

관리자 페이지를 통해 업로드된 미디어 혹은 사용자에 의해 업로드된 미디어를 조회합니다.

## API URL

/api/ide/media/item/list

## Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|---|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|category|미디어 index 혹은 미디어의 id|string|${\color{red}필수}$|관리자 페이지에서 생성한 미디어의 index 혹은 id 값|
|page|페이지번호|int|선택|페이지번호 미 입력시 기본값 = 1 |
|per_record_num|한 페이지에 보여지는 미디어수|int|선택|미 입력시 기본값 = 50|
|text|검색어|string|선택|Tag 검색어 조회|
|sort|정렬방법|string|선택|미 입력시 기본값 = 'desc'<br>(desc : 최근순, asc : 오랜된 순, like : 인기순)|
|used|승인된 미디어 여부|stirng|선택|미 입력시 기본값 = ''<br>(모두 : '', 승인된 미디어만 : y, 미승인된 미디어만 : n)|
|term|유효기간 설정여부|int|선택|미 입력시 기본값 = ''<br>(모두 : '', 유효기간 내 미디어만 : y )|

### 목록조회 예제(jQuery)

```javascript
var url = '/api/ide/note/board/item/list';
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
            "data": [
		...
                {
                    "attach": [
                        {
                            "filename": "20240511__2.png",
                            "group": "image",
                            "mimetype": "image/png",
                            "realname": "첨부파일2.png",
                            "size": 68176,
                            "thumb": "http://192.168.0.15/media/haccp/board/61/thumb_20240511__2.png",
                            "uri": "/media/haccp/board/61/20240511__2.png",
                            "url": "http://192.168.0.15/media/haccp/board/61/20240511__2.png"
                        },
                        {
                            "filename": "20240511__1.png",
                            "group": "image",
                            "mimetype": "image/png",
                            "realname": "첨부파일1.png",
                            "size": 68311,
                            "thumb": "http://192.168.0.15/media/haccp/board/61/thumb_20240511__1.png",
                            "uri": "/media/haccp/board/61/20240511__1.png",
                            "url": "http://192.168.0.15/media/haccp/board/61/20240511__1.png"
                        }
                    ],
                    "category": 61,
                    "content": "<p>내용~~~~</p>",
                    "count": 0,
                    "datetime": "2024-11-20 14:03:47",
                    "idx": 3,
                    "link": "http://digimix.co.kr",
                    "name": "하이요~",
                    "tag": "키오스크,웹,인터렉션",
                    "timestamp": 1732079027,
                    "writer": "차마담"
                }
            ],
            "page": 1,
            "total_block": 1,
            "total_page": 1,
            "total_record": 9
        },
        "server": {
            "build": "20240112518",
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1732531383,
            "version": "2.0"
        }
    }
}
```
