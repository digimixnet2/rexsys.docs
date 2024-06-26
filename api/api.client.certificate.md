클라이언트 인증 및 토큰 발급
==========================

키오스크 혹은 웹사이트는 프로젝트 코드와 제품키를 관리자 페이지를 통해 발급 받아야 합니다.
제공 받은 프로젝트코드(project)와 제품키(productkey)를 전송하여, 인증을 받고, Token key를 부여 받습니다.

### API URL

/api/rexsys/cgi/certificate/productkey

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|projectkey|제품키|string|${\color{red}필수}$|관리자 페이지에서 생성한 클라이언트의 제품키|

*** 현재 버전은 project 코드를 전송하지 않아도 인증되지만, 2024년 7월 10일 부터는 필수로 입력하여 인증 받을 수 있습니다.

### 인증 및 토큰키 발급 예제 (jQuery)

```javascript
var url = '/api/rexsys/cgi/certificate/productkey';
var postdata = {
	project : '프로젝트 코드'
	productkey : '관리자 페이지에서 생성한 클라이언트의 제품키',
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
		console.log( '** token', rs.rexsys.result.token );		// api 접근 가능한 토큰키
		console.log( '** client id', rs.rexsys.result.clientid );	// 제품키의 클라이언트 id
		console.log( '** io', rs.rexsys.result.config.io );		// 생성된 socketio 채널
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

### Retrun Result Json. (/api/rexsys/cgi/certificate/productkey)

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
