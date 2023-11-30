# Java Servlet 생성 및 주요 메서드

Java Servlet은 Java EE 스펙의 일부로, 클라이언트의 요청을 처리하고 동적으로 웹 페이지를 생성하는 서버측 프로그램입니다.

## Servlet 생성

Servlet 클래스를 생성하기 위해서는 `javax.servlet.http.HttpServlet` 클래스를 상속받아야 합니다. 그리고 웹 서버에 해당 Servlet을 매핑하기 위해 `@WebServlet` 어노테이션을 사용할 수 있습니다.

```java
import javax.servlet.*;
import javax.servlet.http.*;

@WebServlet("/main")
public class MyServlet extends HttpServlet {
  // 메서드 구현
}
```

## 주요 메서드

### service()

- 클라이언트의 요청을 받아 처리하고 응답을 반환합니다.
- `doGet()` 또는 `doPost()` 등의 메서드를 내부적으로 호출합니다.

### doGet(), doPost()

- HTTP GET 또는 POST 요청을 처리합니다.
- 일반적으로 이 메서드들을 오버라이딩하여 사용자의 요청을 처리합니다.

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) {
  // 로직
}

protected void doPost(HttpServletRequest request, HttpServletResponse response) {
  // 로직
}
```

### init(), destroy()

- `init()` 메서드는 Servlet이 처음 초기화될 때 호출됩니다.
- `destroy()` 메서드는 Servlet이 종료될 때 호출됩니다.

## @WebServlet("/main")

- 이 어노테이션은 URL 패턴(`/main`)을 해당 Servlet에 매핑합니다.

## Request Encoding

- 요청 데이터의 문자 인코딩을 설정합니다.
  
```java
request.setCharacterEncoding("UTF-8");
```

## Response Encoding

- 응답 데이터의 문자 인코딩을 설정합니다.
  
```java
response.setContentType("text/html; charset=UTF-8");
```

## PrintStream

- `PrintStream`은 바이트 출력 스트림을 텍스트 데이터를 출력할 수 있는 스트림으로 변환해 줍니다.
- Servlet에서는 주로 `PrintWriter`를 사용하여 응답을 작성하게 됩니다, `PrintStream`은 일반적으로 파일이나 콘솔 출력에 더 자주 사용됩니다.

```java
PrintWriter out = response.getWriter();
out.println("<h1>Hello World!</h1>");
```

### 주의사항

- 인코딩 설정은 파라미터 읽기 또는 응답 쓰기 전에 이루어져야 합니다.
- Servlet 생명주기를 정확하게 이해하고 `init()`와 `destroy()` 메서드를 적절히 사용해야 합니다.

이러한 기능과 메서드들은 Servlet 프로그래밍의 기초를 이루며, 이를 통해 동적인 웹 애플리케이션을 구축할 수 있습니다.



아래에 `index.html`과 `ServletMain`의 예제 코드.

### index.html

```html
<!DOCTYPE html>
<html>
<head>
  <title>Servlet Example</title>
</head>
<body>

<h1>GET and POST Example</h1>

<!-- GET Method -->
<form action="main" method="get">
  <label for="nm">Name (GET):</label>
  <input type="text" id="nm" name="nm">
  <input type="submit" value="GET 요청">
</form>

<!-- POST Method -->
<form action="main" method="post">
  <label for="nm">Name (POST):</label>
  <input type="text" id="nm" name="nm">
  <input type="submit" value="POST 요청">
</form>

</body>
</html>
```

### ServletMain.java

```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/main")
public class ServletMain extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
    String name = request.getParameter("nm");
    response.setContentType("text/html; charset=UTF-8");
    PrintWriter out = response.getWriter();
    out.println("<h1>Received via GET: " + name + "</h1>");
  }

  @Override
  protected void doPost(HttpServletRequest request, HttpServletResponse response) throws IOException {
    request.setCharacterEncoding("UTF-8");
    String name = request.getParameter("nm");
    response.setContentType("text/html; charset=UTF-8");
    PrintWriter out = response.getWriter();
    out.println("<h1>Received via POST: " + name + "</h1>");
  }
}
```

### 코드 설명

- `index.html`에서는 두 개의 폼을 제공합니다. 하나는 GET 방식, 다른 하나는 POST 방식으로 서블릿 `/main`에 데이터를 전송합니다.
- `ServletMain.java`에서는 `doGet()`와 `doPost()` 메서드를 오버라이딩하여 각각 GET과 POST 요청을 처리합니다.
- `getParameter("nm")`을 통해 전송된 데이터를 읽습니다.
- 문자 인코딩은 GET에서는 URL에 의해, POST에서는 `request.setCharacterEncoding("UTF-8")`을 통해 설정됩니다.

이 예제를 통해 기본적인 GET과 POST 요청 처리 방법을 확인할 수 있습니다.




# web.xml: Servlet 매핑과 Filter 사용법

`web.xml` 파일은 웹 애플리케이션의 배포 설정과 초기화 파라미터, 보안 설정 등을 정의합니다. Servlet 매핑과 Filter 설정을 위해 주로 사용됩니다.

## Servlet 매핑

### 설명
- `web.xml`을 사용하여 서블릿을 URL에 매핑할 수 있습니다.

### XML 예시
```xml
<servlet>
  <servlet-name>MyServlet</servlet-name>
  <servlet-class>com.example.MyServlet</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>MyServlet</servlet-name>
  <url-pattern>/main</url-pattern>
</servlet-mapping>
```

### 주의사항
- `servlet-name`은 고유해야 하며, `servlet-class`는 완전한 클래스 경로를 지정해야 합니다.
  
---

## Filter 사용법

### 설명
- Filter는 요청이 서블릿에 도달하기 전과 후에 특별한 처리를 수행할 수 있습니다.

### XML 예시
```xml
<filter>
  <filter-name>MyFilter</filter-name>
  <filter-class>com.example.MyFilter</filter-class>
</filter>

<filter-mapping>
  <filter-name>MyFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

### 주의사항
- `filter-name`은 고유해야 하며, `filter-class`는 완전한 클래스 경로를 지정해야 합니다.
- `url-pattern`은 필터가 적용될 URL 패턴을 지정합니다.

---

### 작동 순서
1. 클라이언트의 요청이 들어옵니다.
2. 필터가 적용되며, 필요한 전처리 작업을 수행합니다.
3. 요청이 서블릿에 전달되어 처리됩니다.
4. 필터에서 후처리 작업이 수행됩니다.
5. 응답이 클라이언트에 전달됩니다.

### 자주 실수하는 부분
- 서블릿과 필터의 `name`이나 `class` 경로를 잘못 설정하여 404 에러나 클래스 불러오기 실패가 발생할 수 있습니다.
- `url-pattern` 설정을 잘못하여 필터가 적용되지 않거나, 더 많은 URL에 적용되는 실수를 할 수 있습니다.

`web.xml`을 이용한 설정은 XML 기반의 설정으로, 오타나 구조적 실수가 쉽게 발생할 수 있으므로 주의가 필요합니다.
