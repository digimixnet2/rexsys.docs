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

## 암호화 복호화를 위한 QRCode 생성시

참고 : https://github.com/h2non/jshashes/blob/master/examples/client/hmac.html

```javascript
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <script type="text/javascript" src="js/hashes.js"></script>
    </head>
    <body>
        <script type="text/javascript">

            // sample string 
            var str = 'This is a sample text!';
            // salt key
            var key = 'th!$-!S-@-k3Y';

            // new MD5 instance
            var MD5 = new Hashes.MD5;
            // new SHA1 instance
            var SHA1 = new Hashes.SHA1;
            // new SHA256 instance
            var SHA256 =  new Hashes.SHA256;
            // new SHA512 instace
            var SHA512 = new Hashes.SHA512;
            // new RIPEMD160 instace
            var RMD160 = new Hashes.RMD160;

    
            var now = Date.now();
            var key = SHA256.hex_hmac(now,key); 
           

        </script>
    </body>
</html>
```
