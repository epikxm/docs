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

```javascript
JavaScript:
const id = <사용자로 부터 입력받은 값>;
const sql = 'SELECT * FROM users WHERE id=' + id;
connection.query(sql, function(err, rows) {
  ...
});
```

```java
JavaCode:
String query = "SELECT account_balance FROM user_data WHERE user_name = "
             + request.getParameter("customerName");
try {
    Statement statement = connection.createStatement( ... );
    ResultSet results = statement.executeQuery( query );
}
...
```

다음 코드와 같이 사용해야 한다.

```javascript
JavaScript:

escape() 함수

// SQL Injection을 막기 위해서는 위의 코드처럼 사용자로 부터 입력받은 안전하지 않은 데이터는
// connection.escape()를 통해 sql 구문을 생성하여야 합니다.
const id = <사용자로 부터 입력받은 값>;
const sql = 'SELECT * FROM users WHERE id=' + connection.escape(id);
connection.query(sql, function(err, rows) {
  ...
});


? 문자

// escape함수대신에 ?문자를 사용할 수 있습니다. ?를 사용하면 위의 방법보다 더 간단하게
// 사용할 수 있습니다. 여기서 ?와 params 배열은 순서대로 매치 됩니다.
const id = <사용자로 부터 입력받은 값>;
const sql = 'INSERT INTO users(id, password) VALUES(?, ?)';
const params = [id, password];
conn.query(sql, params, function(err, rows) {
  ...
});
// 순서대로 매치된다.
db.query(`update author set name=?, profile=? where id=?`, [post.name, post.profile, post.id], function (error, result) {
    if (error) throw error;
    response.writeHead(302, { Location: `/author` });
    response.end();
});


escapeId() 함수
// 데이터베이스, 테이블, 컬럼이름등과 같은 SQL Identifier을 사용자로 부터입력받는 경우,
// escape함수가 아닌 escapeId함수로 escape할 수 있습니다.
const tableName = <사용자로 부터 입력받은 값>;
const sql = 'SELECT * FROM ' + connection.escapeId(tableName);
connection.query(sql, function(err, rows) {
  ...
});


?? 문자
// 앞서 언급한 ?문자와 마찬가지로 escapeId() 함수를 대체하여 사용 할 수 있습니다.
// ??문자도 마찬가지로 params배열과 순서대로 매치 됩니다.
const tableName = <사용자로 부터 입력받은 값>;
const sql = 'SELECT * FROM ??';
const params = [tableName];
connection.query(sql, params, function(err, rows) {
  ...
});
```

```java
JavaCode:
// This should REALLY be validated too
String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( );

```
