아키텍처 api 혹은 cache 데이터
==========================

API 데이터 접근, JSON 캐시 데이터를 가져오는 2가지 방법이 있습니다.
JSON 데이터는 API 데이터를 JSON STRING 파일로 추출된 파일로 읽기 속도가 빠릅니다.

가급적 JSON 파일을 불러오기를 권장합니다.

### API URL

/api/ide/architecture/data/cache


## Parameter (Method : POST, Only API)

API 로 접근할때만 사용하며, JSON CACHE 데이터는 파라미터를 전송하지 않습니다.

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|category|아키텍처 id 혹은 idx|string or int |${\color{red}필수}$|관리자 페이지에서 생성한 아키텍처의 id 혹은 idx|

## 아키텍처 불러오기 ( API : jQuert )


```javascript
var url = '/api/ide/architecture/data/cache';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키',
	category: '아키텍처 아이디' // 아키텍처 id 혹은 idx
	
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

### JSON CACHE DATA URL

JSON 파일은 관리자 아키텍처 메뉴에서 EXPORT 된 파일입니다.

```
/data/{프로젝트명}/architecture/architecture.{아키텍처ID}.min.js
```

