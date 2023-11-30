---

### Eclipse에서의 Dynamic Web Project 구조

Dynamic Web Project를 생성한 후에는 왼쪽의 Project Explorer 창에서 다음과 같이 생성된 폴더들을 확인할 수 있습니다. 
![설명1](https://github.com/leeapgil/study-summary/blob/master/img/web1.PNG)

#### 1) proj
- **설명**: 방금 생성한 프로젝트를 나타냅니다.

#### 2) Java Resources
- **설명**: 자바 전용 폴더입니다.
- **내용**: 자바 파일(.java)이 저장됩니다.

  ##### 2-1) src/main/java
  - **설명**: 이 폴더에 자바 파일들을 배치합니다. 해당 폴더 안에 있는 자바 파일만 컴파일을 수행합니다.
  - **참고**: `src` 폴더에서는 소스 컴파일을 수행하며, 실행은 `WebContent`에서 이루어집니다.

#### 3) WebContent (Eclipse IDE 2022 버전에서는 webAbb)
- **설명**: 이 폴더에는 JSP 파일이나 HTML 파일과 같이 컴파일이 필요 없는 파일들을 넣어줍니다.
- **내용**: `META-INF`와 `WEB-INF` 폴더가 들어있습니다.

#### 4) WEB-INF
- **설명**: 이 폴더 안에는 확장 라이브러리와 배포 서술자가 들어있습니다.
- **내용**: 확장 라이브러리를 위한 `lib` 폴더와 배포 서술자인 `web.xml` 파일이 들어있습니다.

#### 5) Servers
- **설명**: 설정을 마친 톰캣 서버가 들어있습니다.

---
### JSP (JavaServer Pages)의 주요 목적과 사용 예시

#### JSP의 주요 목적
- JSP는 웹 브라우저에 띄울 HTML 파일을 생성하는 것이 주된 목적입니다.
- 서블릿과의 차이: 서블릿은 UI 요소가 없으며, 제어나 기타 처리를 담당합니다.

#### JSP 예시 코드
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%!
String str1 = "JSP";
String str2 = "안녕하세요..";
%>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Hello, JSP</title>
</head>
<body>
  <h2>처음 만들어보는 <%= str1 %></h2>
  <p>
    <%
    out.println(str2 + str1 + "입니다. 열공합시다! ^^");
    %>
  </p>
</body>
</html>
```

#### 추가된 요소들
- JSP 파일은 일반적인 HTML 파일에 몇 가지 요소가 추가되어 있습니다.
- 이 추가된 요소들은 크게 **지시어(Directives)**와 **스크립트 요소(Script Elements)**로 분류할 수 있습니다.

물론입니다! 다음은 Markdown 형식으로 정리한 내용입니다:

---

### 지시어 (Directive)에 대한 설명

#### 지시어의 역할
- 지시어는 JSP 페이지를 Java(서블릿) 코드로 변환하는데 필요한 정보를 JSP 엔진에 알려주는 역할을 합니다.
- 주로 스크립트 언어나 인코딩 방식 등을 설정합니다.

####  지시어의 기본 구문
```jsp
<%@ 지시어 종류 속성1="값1" 속성2="값2" ...%>
```

#### 지시어의 종류
- `page` 지시어
- `include` 지시어
- `taglib` 지시어

#### page 지시어
- 문서의 타입, 에러 페이지, MIME 타입 등을 설정합니다.

#### page 지시어의 속성들
##### language, contentType, pageEncoding 속성
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
```
- `language`: 스크립팅 언어를 지정합니다.
- `contentType`: 생성할 응답 문서의 MIME 타입을 지정합니다.
- `pageEncoding`: 인코딩을 지정합니다.

#####  import 속성
- 외부 클래스를 임포트하기 위해 사용합니다.

####  import 속성을 이용한 날짜 표시 페이지
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.text.SimpleDateFormat" %> 
<%@ page import="java.util.Date" %> 
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Today is? | page 지시어 - import 속성 예제</title>
</head>
<body>
  <%
  Date today = new Date();
  SimpleDateFormat dateformat = new SimpleDateFormat("yyyy-MM-dd");
  String dateStr = dateformat.format(today);
  out.println("오늘 날짜 : " + dateStr);
  %>
</body>
</html>
```

- `SimpleDateFormat` 클래스와 `Date` 클래스를 임포트하여 오늘 날짜를 출력합니다.
- 이 클래스들은 `java.lang` 패키지에 속하지 않으므로, `import` 속성을 사용해야 합니다.

---
# JSP 디렉티브: Page, Taglib, Include

JSP 디렉티브는 JSP 페이지의 작동 방식을 제어하는데 사용됩니다. 이 문서에서는 `page`, `taglib`, `include` 디렉티브에 대한 설명과 주의사항을 다룹니다.

## Page 디렉티브

### 설명
- `page` 디렉티브는 JSP 페이지의 일반적인 속성과 설정을 정의합니다.
  
### 코드 예시
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
```

### 주의사항
- 페이지에 여러 개의 `page` 디렉티브가 있다면 충돌이 발생할 수 있습니다.
- 한 페이지에서 한 번만 정의되어야 하는 속성이 여러 번 정의되면 에러가 발생합니다.

### 자주 실수하는 부분
- `contentType`과 `pageEncoding`을 명시적으로 설정하지 않아 발생하는 인코딩 문제.
  
---

## Taglib 디렉티브

### 설명
- `taglib` 디렉티브는 태그 라이브러리를 JSP 페이지에 포함시킵니다.

### 코드 예시
```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
```

### 주의사항
- `uri`와 `prefix`는 반드시 명시되어야 합니다.
- 동일한 `prefix`를 여러 `uri`에 할당하면 안 됩니다.

### 자주 실수하는 부분
- 라이브러리가 서버에 설치되지 않았거나 잘못된 `uri`를 사용하여 태그가 제대로 작동하지 않는 경우.
  
---

## Include 디렉티브

### 설명
- `include` 디렉티브를 사용하여 다른 JSP 파일이나 HTML 파일을 현재 페이지에 포함시킵니다.

### 코드 예시
```jsp
<%@ include file="header.jsp" %>
```

### 주의사항
- 포함되는 파일 내에서 정의된 변수나 메서드가 이미 있는 경우 충돌이 발생할 수 있습니다.
  
### 자주 실수하는 부분
- 상대 경로나 절대 경로를 잘못 설정하여 파일을 찾을 수 없는 경우.
- 순환 참조에 의해 스택 오버플로우가 발생하는 경우.

---

이러한 디렉티브들은 JSP 페이지의 작동 방식을 제어하며, 올바르게 사용될 경우 유용한 기능을 제공합니다. 그러나 주의사항과 자주 발생하는 실수를 잘 이해하고 있어야 합니다.

# JSP 페이지의 구성요소와 주의사항

JavaServer Pages (JSP)는 웹 애플리케이션 개발을 위한 서버사이드 스크립트 언어입니다. 이 문서에서는 JSP 페이지의 주요 구성요소와 주의사항을 다룹니다.

## 스크립트 요소

### 스크립트릿 (Scriptlet)
  
#### 설명
- 자바 코드를 내장할 수 있는 영역입니다.
  
#### 코드 예시
```jsp
<% 
  int x = 10;
  int y = 20;
  int sum = x + y;
%>
```
  
#### 주의사항
- 스크립트릿은 페이지의 가독성을 떨어뜨릴 수 있으니 최소화하는 것이 좋습니다.
  
---

### 표현식 (Expression)
  
#### 설명
- 값을 출력할 때 사용합니다.
  
#### 코드 예시
```jsp
<%= sum %>
```
  
#### 주의사항
- 표현식은 세미콜론(`;`)으로 끝나면 안 됩니다.
  
---

### 선언부 (Declaration)
  
#### 설명
- 페이지 전체에서 사용할 변수나 메서드를 선언합니다.
  
#### 코드 예시
```jsp
<%! 
  int multiply(int x, int y) {
    return x * y;
  }
%>
```

#### 주의사항
- 선언부에 선언된 변수나 메서드는 JSP 페이지 내에서만 사용 가능합니다.

---

## 자주 실수하는 부분

1. **디렉티브 설정 누락**: 필요한 페이지 속성을 설정하지 않아서 발생하는 문제들이 있습니다.
2. **스크립트릿의 과도한 사용**: 로직이 복잡해질수록 페이지의 가독성과 유지보수가 어려워집니다.
3. **표현식에서의 세미콜론 사용**: 표현식은 자동으로 값을 출력하므로 세미콜론이 필요하지 않습니다.

이 요소들을 적절하게 사용하면 JSP로 강력한 웹 애플리케이션을 만들 수 있습니다. 하지만 주의사항과 자주 발생하는 실수를 인지하고 있어야 효율적인 개발이 가능합니다.

# JSP: EL, 표준 액션 태그, 커스텀 태그

JSP에서는 Expression Language (EL), 표준 액션 태그, 커스텀 태그를 사용하여 웹 페이지를 더 쉽게 작성하고 유지할 수 있습니다. 각 요소의 특징과 사용법, 그리고 주의사항을 다룹니다.

## Expression Language (EL)

### 설명
- EL은 JSP 페이지에서 데이터를 쉽게 접근하고 출력하는 데 사용됩니다.

### 코드 예시
```jsp
${user.name}
```

### 주의사항
- EL은 스크립트릿에서는 작동하지 않습니다.
  
### 자주 실수하는 부분
- 객체나 배열의 속성에 접근할 때 잘못된 표현을 사용하는 경우.

---

## 표준 액션 태그

### 설명
- JSP 페이지에서 객체를 사용하거나 흐름을 제어하는 등의 작업을 할 때 사용합니다.

### 코드 예시
```jsp
<jsp:include page="header.jsp" />
```

### 주의사항
- `jsp:include`와 `jsp:forward` 등을 혼용해서 사용할 때, 응답이 이미 커밋되었는지 확인해야 합니다.

### 자주 실수하는 부분
- `jsp:useBean`에서 클래스 이름을 잘못 지정하여 객체가 제대로 생성되지 않는 경우.

---

## 커스텀 태그

### 설명
- 개발자가 정의한 태그를 사용하여 재사용 가능한 UI 컴포넌트나 로직을 쉽게 적용할 수 있습니다.

### 코드 예시
```jsp
<mytag:welcomeMessage user="John" />
```

### 주의사항
- 커스텀 태그 라이브러리의 `uri`와 `prefix`를 정확하게 설정해야 합니다.

### 자주 실수하는 부분
- 커스텀 태그의 속성명이나 태그 이름을 잘못 사용하여 컴파일 에러나 런타임 에러가 발생하는 경우.

---

EL, 표준 액션 태그, 커스텀 태그는 JSP의 가독성과 재사용성을 향상시키지만, 잘못 사용될 경우 문제가 발생할 수 있습니다. 이러한 요소들의 세부적인 사용 방법과 주의사항을 숙지하면 더 효과적인 웹 개발이 가능합니다.


