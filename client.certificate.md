클라이언트 인증 및 토큰 발급
==========================

## Parameter

키오스크 혹은 웹사이트는 프로젝트 코드와 제품키를 관리자 페이지를 통해 발급 받아야 하며, API를 이용시 필요한 토큰를 생성하여 한다.

## URL

/api/rexsys/cgi/certificate/productkey

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|필수*|-|
|projectkey|제품키|string|필수*|관리자 페이지에서 생성한 클라이언트의 제품키|

## jQuery 사용시. 예제

```javascript
var url = '/api/rexsys/cgi/certificate/productkey';
var data = {
	project : '프로젝트 코드'
	productkey : '관리자 페이지에서 생성한 클라이언트의 제품키',
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
