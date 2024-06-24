클라이언트 인증 및 토큰 발급
==========================

parameter
|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|필수*|-|
|projectkey|제품키|string|필수*|관리자 페이지에서 생성한 클라이언트의 제품키|

jQuery 사용시.

Example

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
