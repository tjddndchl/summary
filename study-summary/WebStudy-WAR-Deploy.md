

## Tomcat에 WAR로 배포하는 방법

1. **Tomcat 설치 확인**:
    - Tomcat이 설치되어 있는지 확인합니다.
    - 아직 설치되지 않았다면, [Tomcat 공식 웹사이트](http://tomcat.apache.org/)에서 해당하는 버전을 다운로드하고 설치합니다.

2. **Tomcat 실행**:
    - `bin` 디렉토리에 있는 `startup.bat` 파일을 실행하여 Tomcat을 시작합니다.

3. **WAR 파일 준비**:
    - 웹 어플리케이션을 `.war` 형식으로 패키징합니다.
  
  ![설치1](https://github.com/leeapgil/study-summary/blob/master/img/1.png)
  ![설치1](https://github.com/leeapgil/study-summary/blob/master/img/2.png)

4. **배포**:
    - Tomcat의 `webapps` 디렉토리로 `.war` 파일을 복사하거나 이동합니다.
    - Tomcat은 자동으로 `.war` 파일을 압축 해제하고 배포를 시작합니다.

5. **Tomcat Manager를 사용한 배포** (선택 사항):
    - `conf/tomcat-users.xml` 파일에 사용자 권한을 설정합니다.
    - Tomcat Manager에 로그인 후, WAR 파일 업로드 섹션에서 `.war` 파일을 선택하고 업로드합니다.

---

## Windows에서 포트 충돌 오류 시 해결 방법

1. **포트 사용 확인**:
    ```bash
    netstat -ano | findstr :[PORT_NUMBER]
    ```

2. **프로세스 종료**:
    ```bash
    taskkill /F /PID [PID]
    ```

---

아래는 `logging.properties` 파일에서 UTF-8 인코딩 설정을 하는 방법을 Markdown 형식으로 설명합니다:

---

## Tomcat 로그 파일의 한글 깨짐 처리 방법

Tomcat의 로그 설정은 `logging.properties` 파일에 있습니다. 이 파일에서 한글 로깅을 위한 UTF-8 인코딩 설정을 추가/변경할 수 있습니다.

1. **`logging.properties` 파일 열기**:
    - Tomcat의 `conf` 디렉토리 안에 있는 `logging.properties` 파일을 텍스트 에디터로 엽니다.

2. **인코딩 설정 추가/변경**:
    - 파일 내에서 다음 항목을 찾습니다:
    ```properties
    java.util.logging.ConsoleHandler.encoding = ...
    ```

    - 해당 라인의 값을 `UTF-8`로 설정하거나, 해당 라인이 없다면 추가합니다:
    ```properties
    java.util.logging.ConsoleHandler.encoding = UTF-8
    ```

    - 또는 주석처리 
    ```properties
    #java.util.logging.ConsoleHandler.encoding = UTF-8
    ```
3. **Tomcat 재시작**:
    - 설정 변경 후, Tomcat을 재시작합니다.

---

이렇게 설정하면 Tomcat 콘솔 로그에서 한글이 깨지는 문제가 해결될 수 있습니다.
