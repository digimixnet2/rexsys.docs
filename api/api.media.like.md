미디어 아이템 좋아요(추천)
========================

## Parameter ( Method : GET )

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|idx|미디어 고유 index|int|필수*|-|
|point|추가할 포인트(점수)|int|필수*|-|


### 좋아요 포인트 가산 예제(jQuery)

URL /api/ide/media/like/add

```javascript
var url = '/api/ide/media/like/add';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키',
	idx: 1 // 미디어 리스트의 idx 항목
	point : 1 // 미디어에 가산되는 포인트 점수
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

### 좋아요 포인트 업데이트 예제(jQuery)

URL /api/ide/media/like/update


```javascript
var url = '/api/ide/media/like/update';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키',
	idx: 1 // 미디어 리스트의 idx 항목
	point : 1 // 변경되는 포인트
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