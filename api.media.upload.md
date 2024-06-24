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
```
## jQuery 사용시. 예제


```javascript
var url = '/api/media/item/upload';
var data = {
	project : '프로젝트 코드'
	token : '키키',
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
		console.log( '** token', rs.rexsys.result.token );
		console.log( '** client id', rs.rexsys.result.clientid );
		console.log( '** io', rs.rexsys.result.config.io );
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

```
{
    "rexsys": {
        "result": {
            "clientid": "클라이언트ID",
            "clients": "유효클라이언트수",
            "config": {
                "io": {
                    "client": "/io/프로젝트코드/client",
                    "user": "/io/프로젝트코드/user"
                }
            },
            "expire": {
                "datetime": "2030-12-31 23:59:59",
                "timestamp": 1924959599
            },
            "namespace": "ide",
            "productkey": "제품키",
            "project": "프로젝트명",
            "token": "발급된 토큰"
        },
        "server": {
            "namespace": "ide",
            "remote-addess": "127.0.0.1",
            "runtime": 0,
            "status": "success",
            "timestamp": 1719204446,
            "version": "2.0"
        }
    }
}
```
