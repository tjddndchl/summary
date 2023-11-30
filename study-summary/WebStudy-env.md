
## 1. 필수 소프트웨어 설치
### 1.1 이클립스 EE 다운로드
이클립스를 이용한 웹 프로젝트는 일반 이클립스(이클립스 IDE for Java Developers)로는 만들 수 없습니다. 따라서 웹 프로젝트를 만들 수 있는 Eclipse IDE for Enterprise Java and Web Developers(이하 이클립스 EE) 버전을 다운받아야 합니다.

![설치1](https://github.com/leeapgil/study-summary/blob/master/img/setting1.PNG)

[이클립스 EE 다운로드](https://www.eclipse.org/downloads/packages/release/2021-03/r)

### 1.2 OpenJDK 다운로드 (JDK있다면 생략)

다음으로 JDK를 다운 받아야 합니다. 오라클에서 제공하는 버전을 다운받아도 되지만 저는 OpenJDK로 다운을 받도록 하겠습니다. 추가적으로 가장 보편적으로 사용하는 Java 17 을 설치하도록 하겠습니다.

[OpenJDK 다운로드](https://adoptium.net/).
또는 
[OpenJDK 다운로드](https://www.oracle.com/java/technologies/downloads/)

### 1.3 아파치 톰캣 설치

Apache Tomcat은 웹 애플리케이션 서버로서 Java 언어를 사용하여 개발된 웹 애플리케이션을 호스팅하고 실행하는 데 사용됩니다. 주로 Java Servlet 및 JavaServer Pages (JSP) 기술을 이용한 웹 애플리케이션을 실행하는 데 사용됩니다. Apache Tomcat은 Apache Software Foundation에서 개발하고 유지 관리하는 오픈 소스 프로젝트로서, 사용자는 무료로 사용하고 수정하고 배포할 수 있습니다.

![설치2](https://github.com/leeapgil/study-summary/blob/master/img/setting2-1.PNG)

### 1.3.1 아파치와 톰캣이란?

- WEB 서버 : 정적인 자료를 처리하는 서버(html,css,image등 내용이 변하지 않는 정적인 파일처리, 클라이언트 요청 처리.
- WAS(Web Application Server) 서버 : 동적인 자료를 처리하는 서버(DB연동, 비즈니스로직)등을 처리
  -Apache server는 WEB 역할, Tomcat server는 WAS 역할
  -Apache Tomcat Server는 WEB + WAS 서버임.
  
### 1.3.2 아파치 톰캣 특징
- Servlet Container: Apache Tomcat의 주요 기능 중 하나는 Java Servlet Container로서의 역할입니다. Servlet Container는 Java Servlet API를 구현하고, 클라이언트 요청을 받아 해당 서블릿을 실행한 후 응답을 반환하는 기능을 제공합니다.
- JavaServer Pages (JSP): Tomcat은 JSP를 지원하므로 개발자는 HTML 페이지 내에 Java 코드를 포함하여 동적인 웹 페이지를 생성할 수 있습니다.
- WebSocket Support: Tomcat은 WebSocket 프로토콜을 지원하여 실시간 양방향 통신을 가능하게 합니다. 이를 통해 개발자는 채팅 애플리케이션, 온라인 게임 등을 구현할 수 있습니다.
- Security: Apache Tomcat은 다양한 보안 기능을 제공합니다. 예를 들어, SSL/TLS를 통한 데이터 암호화, 사용자 인증 및 권한 부여 등의 기능을 제공합니다.
### 1.3.3 웹 서버 구축을 위한 아파치 톰캣 설치 

[아파치 톰캣 다운로드](https://tomcat.apache.org/download-90.cgi)

![설치2](https://github.com/leeapgil/study-summary/blob/master/img/setting2.PNG)

- connector port 8090 으로 변경
- admin/admin
- 설치경로 c:\tools\tomcat9\ 
- finish 창에서 checkbox 선택 해제

## 2. 기본 설정 진행

### 2.1 파일 인코딩 설정

먼저 인코딩 설정을 진행합니다. Window > Preferences에서 encoding을 검색하여 Text File Encoding을 UTF-8로 바꿔줍니다.

![설치3](https://github.com/leeapgil/study-summary/blob/master/img/setting3.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4-1.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4-2.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4-3.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4-4.PNG)
![설치4](https://github.com/leeapgil/study-summary/blob/master/img/setting4-5.PNG)

### 2.2 출력 브라우저 변경

기본적으로 이클립스는 이클립스 자체 화면에 출력 화면을 띄우게 됩니다. 하지만 일부 CSS 등이 제대로 적용되지 않고 실제 웹 브라우저에서 동작하는 모습을 볼 수 없어 개발에 불편한 요소가 많습니다. 따라서 기본 출력 브라우저를 변경할 필요가 있습니다. Window > Preferences에서 Web Browser를 검색하여 기본(default) 값으로 되어있는 웹 브라우저를 크롬 또는 원하는 브라우저로 변경합니다. 이때 위에 Use Internal Web Browser를 Use External Web Browser로 변경해주어야 정상적으로 출력됩니다.

![설치5](https://github.com/leeapgil/study-summary/blob/master/img/setting5.PNG)

### 2.3 서버 만들기

브라우저에 만들어진 파일을 출력하기 위해서는 서버를 만들어야 합니다. 하단의 Server 탭을 클릭하면 현재 새로 만들어진 프로젝트기 때문에 서버가 만들어져 있지 않은 상태를 볼 수 있습니다. 앞에서 설치한 톰캣 버전에 맞춰서 Server Type을 선택한 후 Finish를 눌러줍니다.

![설치7](https://github.com/leeapgil/study-summary/blob/master/img/setting7.PNG)

### 2.4 새 프로젝트 만들기

다음으로 프로젝트를 만들어 보겠습니다. File > New > Dynamic Web Project를 눌러서 새 프로젝트를 만듭니다. 프로젝트 명을 설정한 후 Finish를 눌러줍니다. 일반적으로 우리가 작성하게 될 파일 대부분은 WebApp 폴더 하위에 작성하게 됩니다.

- 간단한 코드 작성 후 화면 우클릭 - Run As - Run on Server 를 통해 만든 파일을 브라우저 화면에 출력할 수 있음.

![설치8](https://github.com/leeapgil/study-summary/blob/master/img/setting8.PNG)
![설치10](https://github.com/leeapgil/study-summary/blob/master/img/setting10.PNG)
![설치10](https://github.com/leeapgil/study-summary/blob/master/img/setting11.PNG)

- port충돌 오류시
  + (1) 관리자 권한 cmd(명령프롬프트)실행
  + (2) netstat -a -o
  + (3) 충돌 포트 확인 후 포트사용 프로세스 번호 확인 후 (4)을 통해 종료 후 
  + (4) taskkill /f /pid 프로세스번호
* 위 내용을 수행 후 재실행 





