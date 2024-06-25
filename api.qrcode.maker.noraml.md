QRCode 생성 및 삽입
==========================

서버 API를 이용하여 쉽게 QRCode를 생성합니다.

## URL

/api/ide/qrcode/preview

## Parameter ( Method : GET )

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|tag|프로젝트 코드|string|필수*|-|

## 단순 웹주소의 QRCode 생성시.

img 태그에 직접 URL를 입력하여 QRCode를 출력할 수 있습니다.

```javascript
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <script type="text/javascript" src="js/hashes.js"></script>
    </head>
    <body>
        <img src="http://서버주소/api/ide/qrcode/preview?tag=http://digimix.co.kr">
    </body>
</html>
```

## 암호화 QRCode 생성시

동적 URL 생성과 QRCODE의 유효기간을 설정하기 위해서 다음과 같이 시간과 함께 Encode 한 주소와 함께 QRCode를 생성한다.

해당 코드는 단순히 base64를 이용한 것이므로, 보안에 취약하다. 이를 해결하기 위해서, 비공고애 암호화 복호화를 이용한 스크립트를 권장한다.

```javascript
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    </head>
    <body>
        <div id="tmp"></div>
        <script type="text/javascript">

            var now = Date.now().toString();
            var enc_date = window.btoa(encodeURIComponent(JSON.stringify( { timestamp : now } )));
            var tag_url = 'http://127.0.0.1/event.html?key='+enc_date;
			var encodedata = window.btoa(encodeURIComponent(JSON.stringify( { tag : tag_url } )));
            document.getElementById('tmp').appendChild(img);
            /*
                QRCode 의 URL => http://127.0.0.1/event.html?key=JTdCJTIydGltZXN0YW1wJTIyJTNBJTIyMTcxOTIxNjgzNDgxMiUyMiU3RA==
            */
        </script>
    </body>
</html>

```
## 복호화 QRCode의 유효성 검사

    QRCode URL : http://127.0.0.1/event.html?key=JTdCJTIydGltZXN0YW1wJTIyJTNBJTIyMTcxOTIxNjgzNDgxMiUyMiU3RA==

```javascript
var now = Date.now();
var key = GetURLParameter( 'key' );
var data = JSON.parse(decodeURIComponent(window.atob(key)));
console.log( 'data:', data );
var timestamp = parseInt( data.timestamp );
var expire = now - timestamp;
if( expire > 3600 )
{
	console.warn( "!!!! 시간이 만료된 URL" );
}
			
function GetURLParameter(name) {
	name = name.replace(/[\[]/, "\\[").replace(/[\]]/, "\\]");
        var regex = new RegExp("[\\?&]" + name + "=([^&#]*)"),
        results = regex.exec(location.search);
        return results === null ? "" : decodeURIComponent(results[1].replace(/\+/g, " "));
};
```
