## Spring Framework vs Spring Boot

 ![설치1](https://github.com/leeapgil/study-summary/blob/master/img/boot.JPG)
### Spring Framework

**목표:** 
- 엔터프라이즈 애플리케이션 개발에 필요한 기능과 구조를 제공합니다.
- 제어 역행(IoC: Inversion of Control), AOP(Aspect-Oriented Programming), 데이터 액세스, 트랜잭션 관리 등의 주요 개념을 도입하여 개발의 생산성과 유지 보수성을 높입니다.

**장단점:**

**장점:**
1. 유연한 구조로 다양한 환경과 통합 가능
2. 광범위한 엔터프라이즈 서비스 제공
3. 확장성이 좋고 커스터마이징이 용이
4. 잘 정립된 생태계와 커뮤니티 지원

**단점:**
1. 설정과 초기화에 상대적으로 많은 시간과 노력 필요
2. 학습 곡선이 다소 가파름

**적합한 프로젝트:** 
- 복잡한 엔터프라이즈 애플리케이션에서 높은 유연성과 커스터마이징이 필요한 경우

### Spring Boot

**목표:** 
- Spring 기반의 애플리케이션 개발을 더욱 빠르고 쉽게 만들기 위해 제공됩니다.
- 복잡한 설정을 최소화하고, 바로 실행 가능한 스탠드얼론 애플리케이션 개발에 초점을 맞춥니다.

**장단점:**

**장점:**
1. 빠르게 프로토타입 및 애플리케이션 개발 가능
2. 많은 기본 설정이 제공되어 별도의 구성 작업이 크게 줄어듦
3. 내장된 Tomcat, Jetty 등의 서버로 스탠드얼론 애플리케이션 실행이 쉽다.
4. Spring Boot Starter를 통한 프로젝트 의존성 관리 용이

**단점:**
1. 기본 설정과 기능에 너무 의존하게 되면 내부 동작을 완전히 이해하지 못할 수 있음
2. 매우 맞춤화된 작업이 필요한 경우 기본 설정에서 벗어나 작업하기가 복잡할 수 있음

**적합한 프로젝트:** 
- 빠른 개발과 배포가 필요한 프로젝트, 마이크로서비스 아키텍처, MVP(최소 기능 제품) 개발 등

### 결론

Spring Framework는 기능과 유연성을 중시하는 복잡한 프로젝트에 적합하며, Spring Boot는 빠르게 실행 가능한 애플리케이션을 원하는 개발자나 초기 단계의 프로젝트에 적합합니다. 하지만 둘은 서로 보완적이기 때문에 많은 Spring Boot 프로젝트에서도 Spring Framework의 기능을 활용하게 됩니다.
**적합한 프로젝트:** 빠른 개발이 필요한 프로젝트, 마이크로서비스, MVP

### **표: Spring Framework와 Spring Boot 비교**


| 항목                          | Spring Framework                                                                                             | Spring Boot                                                                                                                                     |
|-------------------------------|---------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| 사용처                        | Java EE 프레임워크로 애플리케이션을 구축하기 위해 사용됩니다.                                                         | 주로 REST API를 개발하기 위해 사용됩니다.                                                                                                          |
| 주요 기능                      | 의존성 주입(DI)                                                                                                 | 자동 구성(Autoconfiguration)                                                                                                                     |
| 사용 이유                      | Java EE 개발을 더 쉽게 하여 개발자의 생산성을 향상시키기 위해.                                                          | 더 빠른 애플리케이션 개발을 위해 Spring 프레임워크에 RAD(빠른 애플리케이션 개발) 기능을 제공합니다.                                                        |
| 애플리케이션 개발 유형            | 느슨하게 결합된 애플리케이션을 생성하는데 도움을 줍니다.                                                                | 스탠드얼론 애플리케이션을 생성하는데 도움을 줍니다.                                                                                                     |
| 서버 의존성                    | Spring 프로젝트를 테스트하기 위해 서버를 명시적으로 설정해야 합니다.                                                     | 내장 서버(예: Tomcat, Jetty)를 제공합니다.                                                                                                          |
| 배포 서술자                     | Spring 애플리케이션을 실행하기 위해 배포 서술자가 필요합니다.                                                             | 배포 서술자가 필요 없습니다.                                                                                                                         |
| 인메모리 데이터베이스 지원         | 인메모리 데이터베이스를 지원하지 않습니다.                                                                             | H2와 같은 인메모리 데이터베이스를 지원합니다.                                                                                                          |
| 보일러플레이트 코드               | 최소한의 작업에도 많은 코드(보일러플레이트 코드)가 필요합니다.                                                             | 보일러플레이트 코드를 피하므로 시간이 절약되고 생산성이 향상됩니다.                                                                                           |
| 구성                           | 수동으로 구성을 작성해야 합니다.                                                                                     | 빠른 부트스트래핑을 허용하는 기본 구성이 있습니다.                                                                                                        |
| 의존성                         | 웹 앱을 생성하기 위해 여러 의존성이 필요합니다.                                                                         | 애플리케이션을 작동시키기 위해 하나의 의존성만 필요합니다. 기본적으로 최종 아카이브에 필요한 여러 의존성이 추가됩니다.                                               |
| HTTP 인증                      | 보안 확인을 활성화하기 위해 HTTP 기본 인증이 필요합니다. 여기에는 여러 의존성과 구성이 필요합니다.                                                     | Spring Boot도 이러한 의존성이 필요하지만, classpath에 관련 의존성을 자동으로 추가하는 spring-boot-starter-security의 의존성만 정의하면 됩니다.                    |
| 테스트                         | 많은 소스 코드로 인해 Spring Framework에서의 테스트는 Spring Boot에 비해 어렵습니다.                                                  | 소스 코드의 양이 줄어들어 Spring Boot에서의 테스트가 더 쉽습니다.                                                                                          |
| XML 구성                        | XML 구성이 필요합니다.                                                                                           | XML 구성이 필요 없습니다.                                                                                                                          |
| CLI 도구                       | 애플리케이션 개발 및 테스트를 위한 CLI 도구를 제공하지 않습니다.                                                           | Spring Boot 애플리케이션 개발 및 테스트를 위한 CLI 도구를 제공합니다.                                                                                      |
| 플러그인                       | Spring Boot처럼 Maven, Gradle 등의 플러그인을 제공하지 않습니다.                                                          | Maven 및 Gradle을 위한 빌드 도구 플러그인을 제공합니다. 이 플러그인들은 실행 가능한 jar의 패키징과 같은 다양한 기능을 제공합니다.                                     |


### **Spring Boot 프로젝트 생성**

- [spring initializr로 프로젝트 시작하기](https://start.spring.io/)

---
## Maven vs Gradle

### **Maven**
**사용 목적:**
- 프로젝트 빌드 자동화
- 의존성 관리
- 프로젝트 정보 관리

**특징:**
- XML 기반의 `pom.xml` 파일을 통한 프로젝트 구성
- 생명주기(Lifecycle)와 플러그인 구조를 기반으로 한 빌드 프로세스
- 중앙 리포지토리를 통한 의존성 관리
- 다양한 플러그인과 확장성 제공

### **Gradle**
**사용 목적:**
- 프로젝트 빌드 자동화
- 의존성 관리
- 스크립팅 기능을 통한 빌드 프로세스의 맞춤화

**특징:**
- Groovy 또는 Kotlin DSL을 기반으로 한 `build.gradle` 파일
- 성능 최적화와 캐싱을 통해 빠른 빌드 속도
- Maven과 Ivy의 저장소를 지원하며, 기존 Maven 프로젝트와의 호환성도 제공
- 동적인 스크립팅 기능으로 더욱 유연한 빌드 프로세스 구성 가능

### **차이점**

| 항목                   | Maven                                                  | Gradle                                                |
|------------------------|-------------------------------------------------------|-------------------------------------------------------|
| 구성 파일              | XML 기반의 `pom.xml`                                  | Groovy/Kotlin DSL 기반의 `build.gradle`               |
| 빌드 언어              | XML                                                    | Groovy 또는 Kotlin                                    |
| 성능                   | 의존성 변경 시 전체 다시 빌드                         | 증분 빌드를 지원하여 변경된 부분만 빌드               |
| 확장성                 | 플러그인을 통해 확장                                  | 스크립트 작성을 통한 동적인 확장                     |
| 의존성 관리            | 중앙 리포지토리를 통한 관리                            | Maven, Ivy 저장소 지원 및 특정 의존성 캐싱            |
| 사용자 커뮤니티        | 오랜 기간 동안 잘 정립된 커뮤니티                     | 점점 성장하는 커뮤니티                                |

---

Maven과 Gradle 모두 Java 프로젝트의 빌드와 의존성 관리를 위해 널리 사용되는 도구들입니다. 

Spring Boot 프로젝트에서 Maven 또는 Gradle을 사용하여 빌드 및 의존성 관리를 하기 위한 방법에 대해 알려드리겠습니다.

### 1. **Maven을 사용하는 경우**

1. **pom.xml 초기화**

   Spring Boot 프로젝트를 생성할 때 기본적으로 `pom.xml`이 생성됩니다. 이 파일에서 프로젝트의 구성, 의존성, 플러그인 등의 정보를 정의합니다.

2. **Spring Boot Starter Parent 추가**

   `pom.xml`에 Spring Boot Starter Parent를 추가합니다. 이로 인해 기본적인 Maven 설정과 함께 Spring Boot에 필요한 여러 의존성의 버전을 자동으로 관리할 수 있습니다.

   ```xml
   <parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>2.6.1</version>
   </parent>
   ```

3. **의존성 추가**

   필요한 Spring Boot Starter 및 기타 의존성을 추가합니다.

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>
   </dependencies>
   ```

4. **플러그인 추가**

   Spring Boot Maven 플러그인을 추가하여 실행 가능한 JAR 파일을 생성합니다.

   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-maven-plugin</artifactId>
           </plugin>
       </plugins>
   </build>
   ```

5. **빌드 및 실행**

   Maven 명령을 사용하여 프로젝트를 빌드하고 실행합니다.

   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

### 2. **Gradle을 사용하는 경우**

1. **build.gradle 초기화**

   Spring Boot 프로젝트를 Gradle로 생성하면 `build.gradle` 또는 `build.gradle.kts` 파일이 생성됩니다.

2. **Spring Boot 플러그인 및 의존성 추가**

   `build.gradle`에 Spring Boot 플러그인과 필요한 의존성을 추가합니다.

   ```groovy
   plugins {
       id 'org.springframework.boot' version '2.6.1'
       id 'io.spring.dependency-management' version '1.0.11.RELEASE'
       id 'java'
   }

   dependencies {
       implementation 'org.springframework.boot:spring-boot-starter-web'
   }
   ```

3. **빌드 및 실행**

   Gradle 명령을 사용하여 프로젝트를 빌드하고 실행합니다.

   ```bash
   ./gradlew clean build
   ./gradlew bootRun
   ```

---

**Thymeleaf와 JSP** 모두 웹 애플리케이션에서 사용되는 서버 사이드 템플릿 엔진입니다. 두 기술은 비슷한 목적을 가지고 있지만, 구조와 기능에는 몇 가지 주요한 차이점이 있습니다.

## Thymeleaf

### 목적:
- 웹 및 비웹 환경에서 사용할 수 있는 현대적인 서버 사이드 Java 템플릿 엔진을 제공합니다.
- 웹 브라우저에서 직접 열 수 있는 유효한 HTML/XML 템플릿을 작성할 수 있게 해 줍니다.
- Spring과의 통합을 목표로 설계되었습니다.

### 특징:
1. **자연스러운 템플릿**: Thymeleaf 템플릿은 웹 브라우저에서 직접 열릴 수 있는 유효한 HTML입니다. 이를 통해 디자인과 개발 프로세스를 분리할 수 있습니다.
2. **표준과 확장**: Thymeleaf는 자체 태그 세트를 제공하며, 사용자 정의 방식으로 확장할 수 있습니다.
3. **Spring 통합**: Spring Framework와의 깊은 통합을 제공합니다. 특히 Spring Security와의 통합도 간편합니다.
4. **비웹 환경에서의 사용**: 웹 애플리케이션 외부에서도 사용할 수 있습니다. 이를 통해 이메일 템플릿, 정적 사이트, 등을 생성할 수 있습니다.

## JSP (JavaServer Pages)

### 목적:
- Java 애플리케이션에서 동적 웹 컨텐츠를 생성하기 위한 표준 기술을 제공합니다.

### 특징:
1. **태그 기반**: JSP는 HTML과 유사한 태그를 사용하여 동적 콘텐츠를 생성합니다.
2. **Java 코드 임베딩**: HTML 템플릿 안에 Java 코드를 직접 삽입할 수 있습니다.
3. **태그 라이브러리**: JSTL (JavaServer Pages Standard Tag Library)과 같은 표준 태그 라이브러리를 사용하여 로직을 템플릿에서 분리할 수 있습니다.

## 주요 차이점:

1. **자연스러운 템플릿**: Thymeleaf는 웹 브라우저에서도 바로 볼 수 있는 "자연스러운 템플릿"을 지향합니다. JSP는 이러한 특징을 지니고 있지 않습니다.
2. **통합**: Thymeleaf는 Spring Framework와의 통합에 좀 더 초점을 맞추고 있습니다. JSP는 일반적인 Java EE 환경과 더 잘 통합됩니다.
3. **태그 및 코드**: JSP에서는 자바 코드를 직접 삽입할 수 있습니다. 반면, Thymeleaf는 이를 지양하며, 표현식을 사용하여 로직을 처리합니다.
4. **비웹 환경**: Thymeleaf는 웹 애플리케이션 외부에서도 사용될 수 있는 반면, JSP는 주로 웹 환경에서만 사용됩니다.

**JPA (Java Persistence API)**와 **MyBatis**는 둘 다 데이터베이스 연동에 사용되는 자바 라이브러리입니다. 두 프레임워크는 데이터베이스와의 상호 작용을 돕지만, 그 접근 방식과 목적에서 차이점이 있습니다.

## JPA (Java Persistence API)

### 목적:
- 자바 애플리케이션에서 RDBMS에 접근하기 위한 표준 인터페이스를 제공합니다.
- 객체와 관계형 데이터베이스 간의 매핑 (ORM: Object-Relational Mapping)을 간소화합니다.

### 특징:
1. **ORM**: 객체와 테이블 간의 매핑을 자동화하며, 개발자는 SQL 대신 객체 지향적으로 데이터를 처리할 수 있습니다.
2. **표준**: JPA는 자바 표준이므로 다양한 구현체 (예: Hibernate, EclipseLink, OpenJPA 등)를 사용할 수 있습니다.
3. **DDL 생성**: 엔터티 클래스에 기반하여 데이터베이스 스키마를 자동으로 생성할 수 있습니다.
4. **쿼리 언어**: JPQL (Java Persistence Query Language)을 제공하여 객체 지향적인 쿼리를 지원합니다.

## MyBatis

### 목적:
- SQL 질의와 프로그래밍 코드를 명확히 분리하며, 개발자가 SQL을 직접 작성하고 최적화하는 것을 지원합니다.
- 데이터베이스와의 상호 작용을 단순화하고자 합니다.

### 특징:
1. **SQL 중심**: 개발자가 직접 SQL을 작성하고, MyBatis는 결과를 객체로 매핑합니다.
2. **동적 SQL**: 조건에 따라 동적으로 SQL을 생성하고 실행할 수 있습니다.
3. **맵핑**: SQL 쿼리의 결과를 POJO (Plain Old Java Object) 또는 맵(Map)에 직접 매핑할 수 있습니다.
4. **통합**: Spring, Spring Boot와의 통합이 간편합니다.

## 주요 차이점:
1. **접근 방식**: JPA는 객체 지향적인 접근 방식을 제공하며, ORM에 중점을 둡니다. 반면 MyBatis는 SQL 중심의 접근 방식을 취합니다.
2. **SQL 작성**: JPA는 대부분의 일반적인 SQL을 자동으로 생성하지만, MyBatis는 개발자가 SQL을 직접 작성하도록 합니다.
3. **유연성**: MyBatis는 복잡한 SQL 쿼리와 프로시저를 처리하는데 유리하며, JPA는 일반적인 CRUD 작업을 빠르게 처리하는데 유리합니다.
4. **복잡도**: JPA는 내부적으로 복잡한 처리를 수행하기 때문에, 때로는 예상하지 못한 SQL이 실행될 수 있습니다. MyBatis는 개발자가 제공하는 SQL만을 실행하므로 예측이 더 쉽습니다.


