클라이언트를 위한 Socket.IO
==========================

Rexsys 서버 그리고, 클라이언트 간에 실시간 통신을 위해서 Python 기반의 Socket.IO javascript 를 사용합니다.
Socket.IO 접속시 사용되는 Token, uid, 생성된 Socet.IO 주소는 [클라이언트 인증 및 토큰 발급](https://github.com/digimixnet2/rexsys.docs/blob/main/api.client.certificate.md) 참고하시기 바랍니다.

## Socket.IO 스크립트 파일 다운로드

[soket.io.min.js](https://github.com/digimixnet2/rexsys.docs/blob/main/js/socket.io.min.js)

```
<script src="socket.io.min.js"></script>
```

## Socket.IO 접속 및 로그인 그리고 데이터 받기 함수

```javascript
var url = 'http://웹주소/io/프로젝트코드/client';
var websock =  io.connect( url );
/*
    response connect
    처음 접속 후 처리
*/
websock.on( 'connect', function ( rs ){	
    if ( typeof(rs) === 'object' ) 
    {
        // console.log( rs );
        // 접속에 성공하면, io 서버에 로그인함.
        websock.emit( 'login', {
            uid: "클라이언트ID",
            sid: rs.sid,
            token: "서버토큰",
    	});
    }
});

// response : login
websock.on( 'login', function ( rs ) 
{
    // 로그인 성공시, 메세지.
    console.log( 'socketio login : ', JSON.stringify(rs) );				
});

// response : touid
websock.on( 'touid', function ( rs ) 
{
    // 클라이언트 혹은 서버로부터 받은 메세지
    /*
        rs = {
            command : "명령",
            data : { ... }
        }
    */
    console.log( 'socketio touid : ', JSON.stringify(rs) );				
});

```

## Socket.IO를 통해 다른 클라이언트에 데이터 전송 (Single : Vanilla JS, jQuery )
```javascript
var senddata = {
    channel: 'client',
    sender: '보내는 클라이언트의 ID',
    receiver: '받는 클라이언트의 ID',
    command: '명령',
    data: {...}
};

websock.emit( 'request', sendata );
```
## Socket.IO를 통해 다른 클라이언트에 데이터 전송 (Single : Vue3 axios )

Vue3에서 동일한 emit가 있어서 전송이 안되거나, 할때는 API를 이용한다.

```javascript

let postdata = {
	token : '발급받은 서버 토큰',
	project : '프로젝트 ID',
	channel: 'client',
    sender: '보내는 클라이언트의 ID',
    receiver: '받는 클라이언트의 ID',
    command: '명령',
    data: JSON.stringify({...}) // JSON.stringify 는 서버의 dictionary 와 호환이 안될 수 있으므로 에러시 처리....
}
let encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };

let url = '/api/ide/io/send';
const customHeaders = {
	'content-type': 'text/plain'
};
axios.post( url, encodedata, customHeaders )
.then((response) => {

	let rs = response.data.rexsys.result;
	
	console.log( rs );

}) .catch(function (error) {
	// 오류발생시 실행
	console.log( error )
})

```

## Socket.IO를 통해 모든 클라이언트 데이터 전송 (Broadcast)
```javascript
준비 중...
```
