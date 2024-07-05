아키텍처 기부처 불러오기
==========================

기본적으로는 아키텍처 데이터를 가져오는 방법과 같습니다.
불어오는 방법은 api에서 직접 호출하는 방법과 JSON 캐시 데이터를 가져오는 2가지 방법이 있습니다.
가급적 JSON 캐시 데이터를 불러오는 방법을 권장합니다.

### API URL

/api/ide/media/item/upload

### JSON CACHE DATA URL

/data/{프로젝트명}/architecture/architecture.{아키텍처ID}.min.js

## Parameter (Method : POST)

API 로 접근할때만 사용하며, JSON CACHE 데이터는 파라미터를 전송하지 않습니다.

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|category|아키텍처 id 혹은 idx|string or int |${\color{red}필수}$|관리자 페이지에서 생성한 아키텍처의 id 혹은 idx|

## 아키텍처 불러오기 ( API : jQuert )

```javascript
var files = [];

$('#inp-upload-files').on ( 'change', function(e){

	files = Array.prototype.slice.call(e.target.files);
	
});

$('#btn-upload-files').on( 'click', function(e){
	MultipleUpload();
});