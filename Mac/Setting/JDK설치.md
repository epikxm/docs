# Mac

### JDK 설치하기

다운로드 경로  
https://www.oracle.com/java/technologies/downloads/#jdk19-mac

> **JDK 17: 2024년 9월까지 업데이트 지원**
>
> <img width="800" src="https://github.com/epikxm/docs/blob/main/Mac/Setting/2023-02-06-01.png?raw=true" />

> **JDK 8 : 2030년 12월까지 업데이트 지원**
>
> <img width="800" src="https://github.com/epikxm/docs/blob/main/Mac/Setting/2023-02-06-02.png?raw=true" />

> **JDK 11: 2026년 9월까지 업데이트 지원**
>
> <img width="800" src="https://github.com/epikxm/docs/blob/main/Mac/Setting/2023-02-06-03.png?raw=true" />

#### Java 8, 11, 17

Java에는 다양한 버전이 존재한다. 그중 가장 많이 쓰이는 버전은 Java 8, 11, 17이다. 이 세 가지 버전이 많이 사용되는 이유는 이 버전들이 LTS(Long Term Support) 버전이기 때문이다.  
LTS란 말 그대로 장기간에 걸쳐 지원을 해주겠다는 뜻이다. LTS 지원 버전은 출시 이후 8년간 보안 업데이트와 버그 수정을 지원해준다. 그 외에 6개월 간격으로 non-LTS 버전들이 출시되는데, 이러한 버전들은 짧은 기간만 해당 버전을 지원해준다.  
따라서, LTS 버전인 Java 8, 11, 17이 가장 많이 사용되고 있다.  
간단하게 각 버전들의 특징을 정리하자면 다음과 같다.  

##### Java 8
- 오라클이 자바 인수 후 출시한 첫 번째 LTS 버전
- 32bit를 지원하는 마지막 공식 Java 버전
- Oracle JDK(Oracle사에서 지원하는 버전으로 유료) , Open JDK(오픈소스 기반의 무료)로 나뉨
- 새로운 날짜와 시간 API(LocalDateTime 등)
- 람다식(Lambda), Stream API
- PermGen 영역 삭제
- Static Link JNI Library

##### Java 11
- Oracle JDK와 Open JDK 통합
- Oracle JDK가 구독형 유료 모델로 전환
- 람다 지역 변수 사용법 변경
- Third Party JDK로의 이전 필요
- HTTP 클라이언트 표준화 기능

##### Java 17
- 가장 최신 LTS 버전
- 봉인 클래스(Sealed Class) 정식 추가
- 패턴 매칭 프리뷰 단계
- Incubator (Foreign Function & Memory API)
- 애플 M1 및 이후 프로세서 탑재 제품군에 대한 정식 지원 (Mac 유저들 환호)
- 난수 생성 API 추가

> 출처: https://code-lab1.tistory.com/253