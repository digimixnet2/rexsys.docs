게시판 등록
==========================

키오스크 혹은 웹사이트에서 글을 쓰고, 첨부파일을 전송합니다.

### API URL

/api/ide/note/board/item/add

## Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|category|미디어ID|string|${\color{red}필수}$|관리자 페이지 미디어 메뉴에서 생성한 미디어 카테고리 혹은 미디어 그룹 ID|
|type|노트 타입|string|${\color{red}필수}$|기본 "board"|
|name|글 제목|string|${\color{red}필수}$|게시물의 제목|
|writer|글 작성자|string|${\color{red}필수}$|게시물 계정 혹은 작성자|
|tag|글 태그|string|${\color{red}필수}$|검색 키워드로 사용할 Tag<br>(콤마 , 단위로 구분하여 작성)|
|link|글 링크|string|${\color{red}필수}$|http:// or https:// 포함 웹주소|
|content|글 내용(본문)|string|${\color{red}필수}$|HTML 태그 포함 String 전송|

## HTML From 

다수의 파일을 함께 업로드 할 때는 input 태그 안에 multiple 을 입력, 한개만 업로드할 경우는 삭제합니다.

미디어 파일만 업로드할 경우, accept 에 확장자를 넣어, 다른 확장자의 파일이 업로드되는 것을 방지 합니다.

```javascript
<form id="filesform" accept-charset="UTF-8">
      <input type="file" name="files[]" id="inp-upload-files" accept=".jpg, .png, .gif, .mp3, .mp4, .webm" multiple>
      <input type="text" id="input-name">
      <input type="text" id="input-writer">
      <input type="text" id="input-type">
      <input type="text" id="input-tag">
      <input type="text" id="input-link">
      <input type="text" id="input-content">
</form>
<input type="button" value="전송" id="btn-upload-files">
```

## 글 작성 예제 (jQuery)

```javascript
var files = [];

$('#inp-upload-files').on ( 'change', function(e){

	files = Array.prototype.slice.call(e.target.files);
	
});

$('#btn-upload-files').on( 'click', function(e){
	MultipleUpload();
});

function MultipleUpload(){

	var url = '/api/ide/note/board/item/add';
	var postdata = {
		project : '프로젝트 코드'
		token : '토큰키',
		category '미디어 카테고리의 index or id',
            	type : 'board',
		writer : '작성자', //선택 사항
		tag : '가, 나, 다', //선택 사항 콤마단위 or "["가", "나", "다"]
		name : '미디어 제목',
		link : 'http://digimix.co.kr',
		content: '<span color="#ff000">레드</span>'
		
	};
	var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
	var formdata = new FormData();
	for( var i = 0; i < files.length; ++ i )
	{
		formdata.append ( 'files[]', files[i] );
	}
	formdata.append ( 'EncodeData', encodedata.EncodeData );
	$.ajax({
		url: url,
		data: formdata,
		type: 'post',
		cache: false,
		contentType: false,
		processData: false,  
		xhr: function () {
			var pdata = $.ajaxSettings.xhr();
			if( pdata.upload )
			{
				// 업로드 프로그레스
				pdata.upload.addEventListener( 'progress', function (e) {
					if (e.lengthComputable) 
					{
						var percent = Math.floor( e.loaded * 100 / e.total );
						console.log( '** upload progress', percent, '%' );
					}
				}, false );
			}
			return pdata;
		},
		success : function( response ) 
		{
			consoel.log( response )
		}
	});

}


```

### Retrun Result Json. (/api/ide/media/item/upload)

```
{
    "rexsys": {
        "result": "success",
        "server": {
            "build": "20240102813",
            "namespace": "ide",
            "remote-addess": "192.168.0.15",
            "runtime": 0,
            "status": "success",
            "timestamp": 1732522481,
            "version": "2.0"
        }
    }
}
```



