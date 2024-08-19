사용자 체크인 및 사용자키(USERKEY) 발급
==========================

이벤트 참여를 위해서 개인 정보 입력하고, 고유 사용자키를 서버로 부터 발급받는다.

### API URL

/api/ide/user/event/checkin

### Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|nickname|사용자 별명|string|${\color{red}필수}$|서비스 이용시 사용될 별칭 혹은 별명|
|user_phone|사용자 휴대폰번호|string|${\color{red}필수}$|이벤트 이용 중 정보 전달을 위한 휴대폰 번호|
|email|사용자 이메일주소|string|${\color{red}필수}$|이벤트 이용 중 정보 전달을 위한 이메일 주소|
|agree|개인정보 수집 동의 여부|string|${\color{red}필수}$|이벤트 이용 중 개인정보 수집 동의 여부 ( y or n )|


### 사용자 체크인 및 사용자키(USERKEY) 발급 예제 (jQuery)

```javascript
var url = '/api/ide/user/event/checkin';
var postdata = {
	project : '프로젝트 코드'
	nickname : '사용자 별명',
	user_phone : '사용자 휴대폰 번호',
	email : '사용자 이메일주소',
	agree : '사용자 동의 여부'

};

var encodedata =  { EncodeData: window.btoa(encodeURIComponent(JSON.stringify( postdata ))) };
$.ajax({
	url: url,
	data: encodedata,
	method: 'POST',
	dataType: 'json'
})

.done(function (rs) {
	if( rs.rexsys.result == 'existed-user-phone' )
	{
		console.log( '이미 체크인된 휴대폰 번호입니다.' );
		return;
	}
	var decodedata = JSON.parse(decodeURIComponent(window.atob(rs.rexsys.result))
	console.log( '*** userkey', decodedata.userkey );
  console.log( '*** userkidx', decodedata.useridx );
  console.log( '*** nickname', decodedata.nickname );
  console.log( '*** user_phone', decodedata.user_phone );
  console.log( '*** email', decodedata.email );
})
.fail(function (rs) {
	console.warn('There is a communication failure with the Rexsys server.');
});
```
