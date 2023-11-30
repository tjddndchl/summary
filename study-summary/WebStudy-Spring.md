# Framework (프레임워크)

프레임워크는 특정 문제를 해결하기 위한 공통의 코드 구조와 API를 제공하는 반제품(미완성) 소프트웨어입니다. 프레임워크는 애플리케이션의 핵심 구조와 동작 방식을 정의하며, 개발자는 주어진 프레임워크의 구조 안에서 필요한 코드를 작성하여 애플리케이션을 완성합니다.

**주요 특징**:

- **재사용성**: 프레임워크에는 특정 문제 영역에 대한 일반적인 해결 방법이 포함되어 있어, 개발자는 새로운 코드를 처음부터 작성하는 것을 피하면서 해당 문제를 해결할 수 있습니다.
- **Inversion of Control (IoC)**: 프레임워크는 애플리케이션의 '흐름 제어'를 담당하며, 개발자는 필요한 부분만을 구현합니다.
- **확장성**: 프레임워크는 보통 모듈화된 구조를 가지고 있어, 필요한 부분만 확장하거나 변경이 가능합니다.

# JSP에서 Spring Framework의 탄생 배경

**JSP (JavaServer Pages)**는 자바를 사용하여 웹 페이지를 동적으로 생성하는 서버사이드 스크립트 언어입니다. 초기의 웹 애플리케이션 개발에서는 JSP와 같은 기술들을 사용하여 비즈니스 로직과 프레젠테이션 로직이 혼재된 형태로 개발되었습니다.

**배경**:

1. **복잡한 엔터프라이즈 애플리케이션**: 초기 웹 애플리케이션은 간단했으나, 시간이 지나면서 엔터프라이즈 애플리케이션의 복잡성이 증가하게 되었습니다.
2. **문제의 복잡성**: JSP/Servlet만으로는 비즈니스 로직과 프레젠테이션 로직의 분리, 트랜잭션 관리, 보안 등 복잡한 요구사항을 충족시키기 어려웠습니다.
3. **코드의 중복**: 많은 코드가 중복되었으며, 유지보수가 어려운 상태였습니다.

이러한 문제점들로 인해, 웹 애플리케이션 개발의 효율성과 확장성을 높이기 위해 **Spring Framework**가 탄생하게 되었습니다.

**Spring Framework의 주요 특징**:

- **의존성 주입 (DI)**: 객체 간의 의존성을 외부에서 주입하는 방식으로, 유연한 애플리케이션 구조를 지원합니다.
- **AOP (Aspect Oriented Programming)**: 관점 지향 프로그래밍을 통해 코드의 중복을 줄이고, 관심사의 분리를 달성합니다.
- **다양한 모듈 제공**: 데이터 액세스, 웹 MVC, 보안, 트랜잭션 관리 등 다양한 모듈을 제공하여, 개발자가 필요한 기능만 선택하여 사용할 수 있습니다.

Spring Framework는 이러한 배경과 특징을 바탕으로 많은 자바 기반의 애플리케이션에서 널리 사용되게 되었습니다.

# Spring MVC

Spring MVC는 Spring 프레임워크의 웹 모듈로, Model-View-Controller (MVC) 패턴을 기반으로 웹 애플리케이션을 구축하기 위한 구조를 제공합니다. 이를 통해 클라이언트의 요청을 효과적으로 처리하고 응답을 반환할 수 있습니다.

## 특징

1. **분리된 구조**: Model, View, Controller의 역할이 분리되어 있어, 관심사의 분리 (Separation of Concerns, SoC)를 통해 코드의 유지 보수성이 향상됩니다.
2. **확장성**: 다양한 뷰 기술 (JSP, Thymeleaf, FreeMarker 등)을 지원하며, 사용자 정의 뷰도 쉽게 추가할 수 있습니다.
3. **다양한 데이터 바인딩**: 요청 파라미터를 객체로 자동 변환하거나 검증하는 기능을 제공합니다.
4. **포괄적인 주제 지원**: RESTful 웹 서비스, 데이터 검증, 파일 업로드, 국제화 및 지역화 등의 주제를 지원합니다.
5. **AOP와 통합**: 관점 지향 프로그래밍을 통한 로깅, 트랜잭션 관리, 보안 등의 기능을 웹 애플리케이션에 쉽게 적용할 수 있습니다.
6. **의존성 주입**: Spring의 DI 기능을 이용하여 컨트롤러와 서비스 객체에 필요한 의존성을 자동으로 주입할 수 있습니다.

## 구조

### 1. DispatcherServlet
- 클라이언트의 요청을 가장 먼저 받는 프론트 컨트롤러 역할을 합니다.
- 적절한 컨트롤러에 요청을 전달하고, 응답을 클라이언트에 반환합니다.

### 2. Controller
- 클라이언트의 요청을 실제로 처리하는 객체입니다.
- 요청을 처리한 후, 응답으로 보낼 뷰의 이름과 모델 객체를 반환합니다.

### 3. Model
- 뷰에 전달할 데이터를 포함하는 객체입니다.
- 컨트롤러는 모델에 데이터를 추가하고, 이 데이터는 뷰에서 사용될 수 있습니다.

### 4. View
- 실제 사용자에게 보여지는 화면을 구성합니다.
- 컨트롤러에서 전달받은 모델 데이터를 사용하여 화면을 렌더링합니다.

### 5. View Resolver
- 컨트롤러가 반환한 뷰 이름을 기반으로 실제 뷰 객체를 찾아 반환합니다.
- 예를 들면, "home"이라는 뷰 이름을 가지고 "home.jsp" 파일을 찾아 뷰로 사용합니다.

### 6. Handler Mapping
- 클라이언트의 요청 URL을 기반으로 적절한 컨트롤러를 찾아줍니다.

## 예시:

```java
@Controller
@RequestMapping("/hello")
public class HelloController {

    @GetMapping
    public String hello(Model model) {
        model.addAttribute("message", "Hello, Spring MVC!");
        return "helloView";
    }
}
```

위의 예제에서 `HelloController`는 "/hello" URL에 대한 요청을 처리하고, "helloView"라는 뷰 이름을 반환합니다. 이 때, `model` 객체에는 "Hello, Spring MVC!"라는 메시지가 포함되어 있어, 뷰에서 이 메시지를 사용하여 화면을 렌더링 할 수 있습니다.


## STS (Spring Tool Suite)
STS는 Spring 기반 프로젝트의 개발에 최적화된 Eclipse 기반의 IDE입니다. STS는 Spring 프로젝트 개발을 쉽게 시작할 수 있게 해주며, 다양한 플러그인 및 툴들이 포함되어 있습니다.

#### STS 설치 방법 (spring boot)
1. [Spring Tool Suite 공식 다운로드 페이지](https://spring.io/tools)로 이동합니다.
2. 적절한 버전의 STS를 선택하여 다운로드 받습니다.
3. 다운로드 받은 파일을 실행하여 설치를 진행합니다.

### spring MVC Project templates 이용방법 
1. 최근 STS 4 는 spring boot 만 사용가능
2. spring legacy proejct (spring MVC proejct)는 STS3 버전을 사용해야함.
3.  [Spring Tool Suite 3 verion 공식 다운로드 페이지](https://docs.spring.io/sts/nan/v3917/NewAndNoteworthy.html)로 이동합니다.
![image](https://github.com/leeapgil/study-summary/assets/36579880/269da4e4-28ee-4ab4-8010-d38afcf81947)
![image](https://github.com/leeapgil/study-summary/assets/36579880/d7b3e819-8da3-4b69-be7e-85ba2634fee2)
4.다운로드 후 파일명을 짧게 수정(이름이 길어서 압출풀때 문제가 생김)

### STS 3.9.17는 JAVA JDK 11을 사용해야함 

1. [adoptium opensource 다운 ](https://adoptium.net/temurin/releases/)로 이동합니다.
2. ![image](https://github.com/leeapgil/study-summary/assets/36579880/d75fbf3c-545f-4243-a581-669b21429469)
   ![image](https://github.com/leeapgil/study-summary/assets/36579880/78d5e13c-c621-48a4-9a2d-c14e5b471778)

3. JDK설치 후 STS.ini 설정 파일에 -vm jdk경로 설정
4. ![image](https://github.com/leeapgil/study-summary/assets/36579880/6f6c2b04-71dc-43dd-81d8-7a381559cac0)
5. 이후 실행
![image](https://github.com/leeapgil/study-summary/assets/36579880/9aa3300c-19b8-4b39-b3df-13a5d4d533d6)

 
---

#### Maven
Maven은 프로젝트 관리 및 빌드 자동화 도구입니다. 의존성 관리, 라이프사이클 관리 등의 기능을 제공합니다.
STS에는 의존성 맞는 maven을 사용해야 되어 아래 과정은 생략

### Maven 설치 방법
1. [Maven 공식 다운로드 페이지](https://maven.apache.org/download.cgi)로 이동합니다.
2. 적절한 버전의 Maven을 다운로드 받습니다.
3. 다운로드 받은 압축 파일을 원하는 경로에 압축 해제합니다.
4. 시스템 환경 변수에 Maven의 bin 폴더 경로를 추가합니다.

   ```markdown
   **환경 변수 설정**
   - `M2_HOME` : Maven이 압축 해제된 경로를 지정합니다.
   - `PATH` or `Path` : `%M2_HOME%\bin`을 추가합니다.
   ```

5. 설치가 완료되면, 터미널 혹은 명령 프롬프트에서 `mvn -v` 명령어로 설치를 확인합니다.

---

## Spring MVC 프로젝트 시작하기

STS를 사용하여 Spring MVC 프로젝트를 시작하는 방법은 다음과 같습니다.

1. STS를 실행합니다.
2. server 추가 
3. `File` > `New` > `spring legacy project` > `spring MVC Project`를 선택합니다.
4. ![image](https://github.com/leeapgil/study-summary/assets/36579880/8cc8e638-1ef8-4712-88d4-86e9263b04f2)
   ![image](https://github.com/leeapgil/study-summary/assets/36579880/f84f8dc2-69b4-4286-b1cf-80b8f17d1129)



---

이렇게 STS와 Maven을 설정하면, Spring 기반의 웹 애플리케이션 개발을 쉽게 시작할 수 있습니다.
