# XSS (Cross-Site Scripting)

- 웹 애플리케이션에서 일어나는 취약점으로 관리자가 아닌 권한이 없는 사용자가
  웹 사이트에 스크립트를 삽입하는 공격 기법을 의미한다.

XSS 란 SQL injection 과 함께 웹 상에서 가장 기초적인 취약점 공격 방법 중 하나로,
권한이 없는 사용자가 악의적인 용도로 웹 사이트에 스크립트를 삽입하는 공격 기법을 말한다.

다른 웹사이트와 정보를 교환하는 식으로 작동하므로 사이트 간 스크립팅이라고도 부른다.

XSS 는 웹 애플리케이션이 사용자로부터 입력 받은 값을 제대로 검사하지 않고 사용할 경우 나타나며,
공격에 성공하면 사이트에 접속한 사용자는 삽입된 코드를 실행하게 되어,
의도치 않은 행동을 수행시키거나 쿠키, 세션 토큰 등 민감한 정보를 탈취할 수 있다.

XSS 는 자바스크립트를 사용하여 공격하는 경우가 가장 많고, 사용자의 세션을 공격자의 서버로
전송해서 탈취하거나 악성코드가 있는 페이지로 리다이렉트 시키는 방식으로 공격이 주로 행해진다.

그 외에도 자바스크립트를 활용해서 내부 네트워크 포트스캔과 같은 공격도 가능하다.

```txt
XSS의 공격 순서

1. 해커가 사전에 만든 웹페이지에 사용자가 브라우저로 액세스를 시도한다.
2. XSS 공격 link가 포함된 웹페이지가 브라우저에 표시된다.
3. 사용자가 link를 클릭한다.
4. 사용자가 느끼지 못하는 사이 취약한 사이트에 있는 해커의 스크립트에 엑세스된다.
5. 사용자의 웹브라우저 상에서 해커의 스크립트가 실행된다.
```

---

## XSS의 종류

XSS는 크게 Reflected-XSS, Stored-XSS 두 종류로 나뉘며, 사용자의 브라우저가 악성 스크립트를
실행하게 하거나 그 방식에 따라 나뉜다.

**Reflected XX**
- URL의 변수 부분처럼 스크립트 코드를 입력하는 동시에 결과가 바로 전해지는 공격기법
- 반사된 XSS는 피싱 공격의 일부로 주로 사용되며 악용하기도, 차단하기도 가장 쉽다.
- 공격자가 HTTP 요청에 악성 콘텐츠를 주입하면 그 결과가 사용자에게 "반사되는" 형태
- 링크를 클릭하도록 피해자를 속이고, 유인해 세션을 하이재킹 할 수 있는 공격
- 반사된 XSS 는 피싱 공격에서 가장 많이 사용됨

**Stored XSS**
- 가장 일반적인 XSS 공격 유형
- 정상적 평문 x -> 스크립트 코드를 입력
  
- 사용자가 게시물을 열람시, 공격자가 입력해놓은 악성 스크립트가 실행되어
  사용자의 쿠키 정보가 유출되거나, 악성 스크립트가 기획한 공격에 당한다.
  
- 지속적인 XSS 공격은 공격자가 웹 애플리케이션을 속여 데이터베이스에 
  악성코드를 저장하도록 하는 수법으로, 서버에 저장된 악성코드는 시스템 자체를 공격
  할 수 있으며 웹 앱 사용자 상당수는 또는 전체에 악성 코드를 전송 할 수 있다.
  
  일반적인 예로는 블로그 댓글에 악성코드를 게시하는 것이 있다.

---

## XSS 대응 방안

사용자의 입력에 대해서는 무조건 의심을 하고 검증하는 작업이 필요하다.

즉, 스크립트 등 해킹에 사용될 수 있는 코딩에 사용되는 입력 및 출력 값에 대해서 검증하고 무효화시켜야 한다.

입력 값에 대한 유효성 검사는 데이터가 입력되기 전에 가능하면, 입력 데이터에 대한 길이, 문자, 형식 및 사업적
규칙 유효성을 검사해야한다.

1. 입력 값 제한 -> 사용자의 입력값을 제한하여 스크립트를 삽입하지 못하게 한다.
   
2. 입력 값 치환 -> XSS 공격은 기본적으로 script 태그를 사용하기 때문에 XSS 공격을 차단하기 위해
   태그 문자 등 위험한 문자 입력시 문서 참조로 필터링하는 등의 방법으로 입력 값을 치환시켜야 한다.
   
3. 스크립트 영역에 출력 자제 -> 이벤트 핸들러 영역에 스크립트가 삽입되는 경우 보호기법들을 우회할 수 
   있기에 사용자의 입력을 출력하는 것을 최대한 자제한다.

4. 라이브러리 이용 -> 예를 들어 XSS 막아주는 Anti XSS 라이브러리 여러 회사에서 제공한다.

---

## XSS 공격을 방지하는 7계명

1. 허용된 위치가 아닌 곳에 신뢰할 수 없는 데이터가 들어가는 것을 허용하지 않는다.
2. 신뢰할 수 없는 데이터는 검증을 하자.
3. HTML 속성에 신뢰할 수 없는 데이터가 들어갈 수 없도록 하자.
4. 자바스크립트에 신뢰할 수 없는 값이 들어갈 수 없도록 하자.
5. CSS의 모든 신뢰할 수 없는 값에 대해서 검증하자.
6. URL 파라미터에 신뢰할 수 없는 값이 있는지 검증하자.
7. HTML 코드를 전체적으로 한번 더 검증하자.
