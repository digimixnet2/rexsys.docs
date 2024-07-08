결제 내역 전송 (기부)
==========================

rexsys.desktop 에서 결제 요청 후, return 받은 변수를 모두 전송합니다.

### API URL

/api/ide/payment/process

## Parameter (Method : POST)

|파라미터|개요|타입|필수여부|비고|
|------|---|---|---|---|
|project|프로젝트 코드|string|${\color{red}필수}$|-|
|token|토큰(키)|string|${\color{red}필수}$|클라이언트 인증에서 받은 토큰키|

|section|포인트 지급 구분|string|${\color{red}필수}$|포인트 지급에 대한 구분 (기부 : donation, 체크인 : checkin 등...|
|sensor_uid|센서 Id|string|${\color{red}필수}$|NFC 혹은 비콘등 센서를 이용할 경우, 기본값 = '' |
|content_id|콘텐츠 Id|string|${\color{red}필수}$|동일한 기능의 클라이언트가 다수 있을 경우에 통용되는 지칭 Id( 체크인 : checkin )|
|content_section|콘텐츠 구분|string|${\color{red}필수}$|포인트의 구분. (point, payment...)|
|user_key|사용자 키|string|${\color{red}필수}$|-|
|user_name|사용자 이름|string|${\color{red}필수}$|-|
|user_nickname|사용자 별칭(별명)|string|${\color{red}필수}$|-|
|user_nickname|포인트|string|${\color{red}필수}$|사용자가 결제한 금액 혹은 지급 포인트|

|course_id|기부처|string|${\color{red}필수}$|결제한 금액을 기부할 곳|

|tranCode|결제여부|string|Return|결제 성공여부|
|outRtn|-|string|Return|-|
|outReplyCode|-|string|Return|-|
|outReplyMsg1|-|string|Return|-|
|outReplyMsg2|-|string|Return|-|
|outCatId|-|string|Return|-|
|outWCC|-|string|Return|-|
|outCardNo|-|string|Return|-|
|outTranAmt|-|string|Return|-|
|outVatAmt|-|string|Return|-|
|outSvcAmt|-|string|Return|-|
|outJanAmt|-|string|Return|-|
|outAuthNo|승인번호|string|Return|-|
|outReplyDate|승인날짜|string|Return|-|
|outAccepterCode|-|string|Return|-|
|outAccepterName|-|string|Return|-|
|outIssuerCode|-|string|Return|-|
|outIssuerName|-|string|Return|-|
|outTranNo|-|string|Return|-|
|outMerchantRegNo|-|string|Return|-|

```javascript
var url = '/api/ide/payment/process';
var postdata = {
	project: '프로젝트 코드'
	token: '토큰키',
	idx: 1 // 미디어 리스트의 idx 항목
	point : 1 // 미디어에 가산되는 포인트 점수
};

var postdata = {
	section		: 'donation',
	project		: '프로젝트 코드',
	token		: '토큰키',
	sensor_uid	: '',				// 기부 키오스크시, 값 없음.
	content_id	: 'kiosk',			// 기부 키오스크시, kiosk
	content_section	 : 'payment',	// 기부 키오스크시, payment
	clientid	: '키오스크 클라이언트 Id',
	user_key	: '',				// 기부 키오스크시, ''
	user_name	: '',				// 기부 키오스크시, ''
	user_nickname :'',				// 기부 키오스크시, ''
	pay_point	: 1000,				// 결제 금액
	
	
	// 이하 결제 단말기로 부터 리턴 받은 값
	// 이하 값들은 예시이므로, 꼭 리턴 받은 받은 값으로 전송해야 함.
	
	tranCode	: 'D1',
	outRtn		: 0,
	outReplyCode: '000',
	outReplyMsg1: '승    인',
	outReplyMsg2: '은행 매입불가 전표임',
	outCatId	: '12345678',
	outWCC		: 'C',
	outCardNo	: '123456',
	outInstallment: '00',
	outTranAmt 	: 1000,
	outVatAmt 	: 0,
	outSvcAmt	: 0,
	outJanAmt	: 0,
	outAuthNo	: '12345678',
	outReplyDate: '240521',
	outAccepterCode: '03',
	outAccepterName: '디지카드',
	outIssuerCode: '15',
	outIssuerName: '디지카드',
	outTranNo : '',
	outMerchantRegNo : '00913235744'
}

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
		console.log( '** data', rs.data );	
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