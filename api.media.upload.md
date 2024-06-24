미디어 파일 업로드
==========================

키오스크 혹은 웹사이트에서 미디어파일을 업로드 합니다.

## URL

/api/rexsys/cgi/certificate/productkey

## Parameter

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|필수*|-|
|projectkey|제품키|string|필수*|관리자 페이지에서 생성한 클라이언트의 제품키|

## HTML From 
```javascript
<form id="filesform" accept-charset="UTF-8">
      <input class="form-control" type="file" name="files[]" id="inp-upload-files" style="display:none;" accept=".jpg, .png, .gif, .mp3, .mp4, .webm" multiple>
</form>
<input type="button" value="전송" id="btn-upload-files">
```
## jQuery 사용시. 예제


```javascript
var files = [];

$('#inp-upload-files').on ( 'change', function(e){

	files = Array.prototype.slice.call(e.target.files);
	
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
		tag : '가, 나, 다' //선택 사항 콤마단위
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

## Result Json.

```
{
    "rexsys": {
        "result": [
            {
                "filename": "5-21__1.jpg",
                "group": "image",
                "mimetype": "image/jpeg",
                "realname": "5-21_.jpg",
                "size": 63153
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
