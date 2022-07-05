https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

# SQL Injection

먼저 [나무위키](https://namu.wiki/w/SQL%20injection)에 정의된 SQL 인젝션은 아래와 같다.

> SQL 인젝션(SQL 삽입, SQL 주입으로도 불린다)은 코드 인젝션의 한 기법으로 클라이언트의 입력값을 조작하여 서버의 데이터베이스를 공격할 수 있는 공격방식을 말한다. 주로 사용자가 입력한 데이터를 제대로 필터링, 이스케이핑하지 못했을 경우에 발생한다. 공격의 쉬운 난이도에 비해 파괴력이 어마어마하기 때문에 시큐어 코딩을 하는 개발자라면 가장 먼저 배우게 되는 내용이다.

SQL 인젝션 방어를 위한 기본사항:

-   매개 변수는 이미 준비된 것으로만 사용한다.
-   올바르게 구성된 저장 프로시저 사용
-   허용 목록 입력 유효성 검사
-   모든 사용자 제공 입력 이스케이프
-   최소 권한 적용
-   동적 쿼리 사용 금지

### **_1. 준비된 문(매개 변수화된 쿼리와 함께)의 사용_**

#### **_Prepared Statements (with Parameterized Queries)_**

아래 코드와 같이 사용하지 말고!

```java
String query = "SELECT account_balance FROM user_data WHERE user_name = "
             + request.getParameter("customerName");
try {
    Statement statement = connection.createStatement( ... );
    ResultSet results = statement.executeQuery( query );
}
...
```

다음 코드와 같이 사용해야 한다.

```java
// This should REALLY be validated too
String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( );

```
