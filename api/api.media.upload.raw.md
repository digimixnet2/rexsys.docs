미디어 파일 업로드(raw - base64)
==========================

키오스크 혹은 웹사이트에서 미디어파일을 업로드 합니다.

### API URL

/api/ide/media/item/upload

## Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|
|category|미디어ID|string|${\color{red}필수}$|관리자 페이지 미디어 메뉴에서 생성한 미디어 카테고리 혹은 미디어 그룹 ID|
|raws|이미지 base64|array|${\color{red}필수}$|base64 |
|id|노트 Id|string|선택|노트 Id|
|tag|노트 태그|string|선택|검색 키워드로 사용할 Tag<br>(콤마 , 단위로 구분하여 작성)|
|writer|미디어 작성자|string|선택|미디어 업로드 계정 혹은 작성자|
|name|노트 제목|string|선택|노트 제목|
|link|노트 링크|string|선택|http:// or https:// 포함 웹주소|
|content|노트 내용(본문)|string|선택|HTML 태그 포함 String 전송|
|custom|사용자데이터|string|선택|사용자 데이터로 Json String 으로 전송|

## HTML From 

다수의 파일을 함께 업로드 할 때는 input 태그 안에 multiple 을 입력, 한개만 업로드할 경우는 삭제합니다.

미디어 파일만 업로드할 경우, accept 에 확장자를 넣어, 다른 확장자의 파일이 업로드되는 것을 방지 합니다.

```javascript
<form id="filesform" accept-charset="UTF-8">
      <input class="form-control" type="file" name="files[]" id="inp-upload-files" accept=".jpg, .png, .gif, .mp3, .mp4, .webm" multiple>
</form>
<input type="button" value="전송" id="btn-upload-files">
```
## 파일업로드 예제 (jQuery)

```javascript
var files = [];
var raws = [];

$('#inp-upload-files').on ( 'change', function(e){

  files = Array.prototype.slice.call(e.target.files);
  for( var i = 0; i < files.lengh; ++i )
  {
    let reader = new FileReader();
    reader.onloadend = function () { 
        raws.push(reader.result);
    };                      
    reader.readAsDataURL(f);
  }
});

$('#btn-upload-files').on( 'click', function(e){
	MultipleUpload();
});

function MultipleUpload(){

	var url = '/api/media/item/upload';
	var postdata = {
		project : '프로젝트 코드'
		token : '토큰키',
		category '미디어 카테고리의 index or id',
		writer : '작성자', //선택 사항
		tag : '가, 나, 다', //선택 사항 콤마단위 or "["가", "나", "다"]
		name : '미디어 제목',
		id : 'm-1',
		link : 'http://digimix.co.kr',
		content: '<span color="#ff000">레드</span>',
		coustom: JSON.stringify( { id : 'test", sub :'xxxxx' } ),
		raws : raws
	};

	var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
  $.ajax({
  	url: url,
  	data: encodedata,
  	method: 'POST',
  	dataType: 'json'
  })
  
  .done(function (rs) {
      console.log( '** response result', rs );	
  })
  .fail(function (rs) {
  	console.warn('There is a communication failure with the Rexsys server.');
  });
	$.ajax({
		url: url,
		data: encodedata,
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
        "result": [
            {
                "category": 62,
                "datetime": "2024-12-16 10:27:43",
                "filename": "ljkuzkkd9o_1734312463.png",
                "filesize": 72780,
                "group": "image",
                "idx": 250,
                "like": 0,
                "mimetype": "image/png",
                "note": {
                    "content": "",
                    "custom": null,
                    "id": "",
                    "link": "",
                    "name": "",
                    "tag": "[]"
                },
                "realname": "Image.png",
                "thumb": "http://192.168.0.15/media/haccp/62/thumb_ljkuzkkd9o_1734312463.png",
                "timestamp": 1734312463,
                "uri": "/media/haccp/62/ljkuzkkd9o_1734312463.png",
                "url": "http://192.168.0.15/media/haccp/62/ljkuzkkd9o_1734312463.png",
                "used": "n",
                "writer": ""
            }
        ],
        "server": {
            "namespace": "ide",
            "remote-addess": "127.0.0.1",
            "runtime": 0,
            "status": "success",
            "timestamp": 1719211671,
            "version": "2.0"
        }
    }
}
```
