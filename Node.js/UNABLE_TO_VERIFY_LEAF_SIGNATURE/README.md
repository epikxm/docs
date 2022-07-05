# UNABLE_TO_VERIFY_LEAF_SIGNATURE 에러 대처

Nodejs 프로젝트에서 라이브러리 다운로드를 위해 `npm i` 했을 때 `UNABLE_TO_VERIFY_LEAF_SIGNATURE` 라는 에러가 나왔다.
단순히 구글링하여 찾은 문제의 원인은 `프록시를 통해 외부 인터넷 사용시 생기는 인증서 문제` 라고.  
[출처](https://engkimbs.tistory.com/895)

일단 npm 에서 뱉어낸 에러이니 NPM docuemnt를 찾아봤다.

[NPM docuemnt](https://docs.npmjs.com/common-errors#ssl-error) 에서 `UNABLE_TO_VERIFY_LEAF_SIGNATURE`를 검색하다보면 다음과 같은 방법을 알려주는데, 둘 중 하나를 선택하여 사용한다.

> npm config set ca "" or npm config set strict-ssl false

`npm config set strict-ssl false` 수행하니 `npm i`가 제대로 동작하는 것을 확인함.  
각 동작은 아래와 같다.

## 1. npm config set strict-ssl false

[strict-ssl](https://docs.npmjs.com/cli/v8/using-npm/config#strict-ssl)

-   Default: true
-   Type: Boolean

Whether or not to do SSL key validation when making requests to the registry via https.
(https를 통해 레지스트리에 요청할 때 SSL 키 유효성 검사를 수행할지 여부)

## 2. npm config set ca ""

[ca](https://docs.npmjs.com/cli/v8/using-npm/config#ca)

-   Default: null
-   Type: null or String (can be set multiple times)

The Certificate Authority signing certificate that is trusted for SSL connections to the registry.
(레지스트리에 대한 SSL 연결에 대해 신뢰할 수 있는 인증 기관 서명 인증서.)

Values should be in PEM format (Windows calls it "Base-64 encoded X.509 (.CER)") with newlines replaced by the string "\n".
(값은 PEM 형식이어야 한다.(Windows에서는 "Base-64로 인코딩된 X.509.").CER)), 줄 바꿈은 문자열 "\n"로 대체함)

For example:

> ca="-----BEGIN CERTIFICATE-----\nXXXX\nXXXX\n-----END CERTIFICATE-----"

Set to null to only allow "known" registrars, or to a specific CA cert to trust only that specific signing authority.
("알려진" 등록자만 허용하거나 특정 CA 인증서가 해당 서명 기관만 신뢰하도록 하려면 null로 설정한다.)

Multiple CAs can be trusted by specifying an array of certificates:
(인증서 배열을 지정하여 여러 CA를 신뢰할 수 있다.)

> ca[]="..."
> ca[]="..."
