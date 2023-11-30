# 도커란? 도커 개념 정리

## 1. 도커란?
![도커](https://github.com/leeapgil/study-summary/blob/master/img/docker.png)
![도커](https://github.com/leeapgil/study-summary/blob/master/img/docker1.png)
도커는 리눅스 기반의 어플리케이션을 프로세스 격리 기술을 사용하여 컨테이너로 패키징하여 실행하고 관리할 수 있게 해주는 오픈소스 프로젝트입니다. 이를 통해 개발 환경과 운영 환경의 차이를 최소화하고, 어플리케이션의 배포와 확장을 쉽게 할 수 있습니다.

## 2. 가상머신 vs 도커 컨테이너
![도커](https://github.com/leeapgil/study-summary/blob/master/img/docker1.JPG)
- **가상머신**: 하드웨어를 에뮬레이션하여 여러 운영체제를 동시에 실행할 수 있게 해주는 기술입니다. 각 운영체제는 독립된 자원과 시스템을 가지며, 하이퍼바이저를 통해 관리됩니다.
- **도커 컨테이너**: 리눅스의 기본 기능을 활용하여 프로세스를 격리된 환경에서 실행합니다. 가상머신에 비해 오버헤드가 적고, 빠르게 시작하고 중지할 수 있습니다.

## 3.도커(Docker)의 탄생 배경

Docker는 2013년에 등장했으며, 애플리케이션을 개발부터 배포까지 일관된 환경에서 실행할 수 있게 해 주는 플랫폼입니다. 이전에는 여러 환경에서 동작하는 애플리케이션을 구축하는 것이 어려웠는데, Docker는 이 문제를 해결하고자 탄생했습니다.

1. **환경 문제**: 개발자가 자신의 기기에서 작성한 코드가 다른 환경에서 제대로 실행되지 않는 문제에 직면하게 되었습니다. 이 문제를 "내 기기에서는 잘 돌아가는데..."라고 표현하기도 합니다.
2. **서비스 확장**: 클라우드 환경과 마이크로서비스 아키텍처의 부상으로, 어플리케이션을 더 빠르게 배포하고 확장할 수 있는 방법이 필요했습니다.

### 도커의 인기 이유

1. **일관성**: 애플리케이션 실행 환경이 일관되므로 '나의 컴퓨터에서는 작동하는데' 문제를 줄여줍니다.
2. **경량화**: 가상화보다 더 경량화된 방법으로 애플리케이션과 그 의존성을 패키징합니다.
3. **이식성**: Docker 컨테이너는 어디서든 실행될 수 있습니다.
4. **마이크로서비스 아키텍처**: 도커는 마이크로서비스 아키텍처를 쉽게 구현할 수 있게 도와줍니다.

### 중요한 특징

- **컨테이너 기반**: Docker는 가상화의 한 형태지만 전통적인 VM보다 더 경량화되어 있습니다. VM은 각각의 OS를 갖지만, Docker 컨테이너는 도커 엔진 위에서 공통의 OS 커널을 공유합니다.
- **빠른 시작**: 컨테이너는 빠르게 시작되고 중단될 수 있습니다.
- **버전 관리**: Docker 이미지는 버전 관리가 가능하여 이전 버전으로 롤백하거나, 다양한 버전의 애플리케이션을 동시에 실행할 수 있습니다.

## 4. 도커 구성요소

- **도커 클라이언트**: 사용자의 명령을 받아 도커 데몬에 전달합니다. `docker build`, `docker pull`, `docker run` 등의 명령을 실행합니다.
- **도커 호스트**: 도커 엔진이 실행되는 서버를 의미하며, 여기서 컨테이너와 이미지가 관리됩니다.
- **도커 데몬**: 사용자의 명령을 받아 컨테이너를 생성, 시작, 중지 등의 작업을 수행합니다.
- **레지스트리**: 도커 이미지를 저장하는 저장소로, Docker Hub나 AWS ECR 등의 서비스가 있습니다.

## 5. 도커 이미지와 도커 컨테이너

- **도커 이미지**: 어플리케이션과 그 실행 환경을 포함하는 패키지입니다. 이미지는 여러 레이어로 구성되며, 읽기 전용입니다.
- **도커 컨테이너**: 이미지를 기반으로 실행되는 격리된 환경입니다. 컨테이너는 이미지의 실행 버전으로 생각할 수 있으며, 필요에 따라 여러 컨테이너를 동시에 실행할 수 있습니다.

---

# 도커 기본 명령어 

## Ubuntu에 Docker를 설치하는 방법

1. **필요한 패키지 설치**: HTTPS를 통해 저장소를 사용하려면 다음 패키지들이 필요합니다.
    ```
    sudo apt-get update
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    ```

2. **Docker의 공식 GPG 키 추가**:
    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

3. **Docker 저장소 설정**:
    ```
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

4. **Docker CE(Community Edition) 설치**:
    ```
    sudo apt-get update
    sudo apt-get install docker-ce
    ```

5. **Docker가 정상적으로 설치되었는지 확인**:
   
    ```
    sudo systemctl status docker
    ```

6. **(선택 사항) 사용자를 Docker 그룹에 추가**: Docker를 `sudo` 없이 사용하려면 현재 사용자를 `docker` 그룹에 추가해야 합니다.
   
    ```
    sudo usermod -aG docker ${USER}
    ```
    위의 명령을 실행한 후 로그아웃하고 다시 로그인하여 변경사항을 적용하세요.

8. **(선택 사항) Docker를 부팅시 자동 시작 설정**:
   
    ```
    sudo systemctl enable docker
    ```
    
---

- **Docker 기본 명령어 **

```markdown
- **이미지 조회**
  ```bash
  docker images
  ```

- **컨테이너 실행**
  ```bash
  docker run [IMAGE]
  ```

- **실행중인 컨테이너 조회**
  ```bash
  docker ps
  ```

- **모든 컨테이너 조회**
  ```bash
  docker ps -a
  ```

- **컨테이너 중지**
  ```bash
  docker stop [CONTAINER_ID]
  ```

- **컨테이너 삭제**
  ```bash
  docker rm [CONTAINER_ID]
  ```

- **이미지 삭제**
  ```bash
  docker rmi [IMAGE_ID]
  ```
---

도커 이미지는 애플리케이션, 의존성, 라이브러리, 바이너리 및 실행 환경을 포함하는 패키지입니다. 컨테이너 실행을 위한 기본 단위로, 이 이미지를 기반으로 여러 독립적인 컨테이너를 생성할 수 있습니다.

**도커 이미지 사용법 가이드**

1. **이미지 검색**
   Docker Hub 같은 공개 도커 레지스트리에서 필요한 이미지를 검색할 수 있습니다.
   ```bash
   docker search [이미지 이름]
   ```

2. **이미지 다운로드**
   도커 이미지를 로컬 시스템에 다운로드합니다.
   ```bash
   docker pull [이미지 이름]
   ```

3. **로컬에 저장된 이미지 목록 확인**
   ```bash
   docker images
   ```

4. **컨테이너 실행**
   다운로드한 이미지를 기반으로 컨테이너를 실행할 수 있습니다.
   ```bash
   docker run [이미지 이름]
   ```

5. **이미지 생성**
   Dockerfile을 사용하여 자신만의 도커 이미지를 만들 수 있습니다. 예를 들어, 현재 디렉토리에 Dockerfile이 있다면 다음 명령어로 이미지를 빌드할 수 있습니다.
   ```bash
   docker build -t [사용자 이름/이미지 이름]:[태그] .
   ```

6. **이미지 업로드**
   Docker Hub나 다른 레지스트리에 자신의 이미지를 업로드할 수 있습니다.
   ```bash
   docker push [사용자 이름/이미지 이름]:[태그]
   ```

7. **이미지 삭제**
   로컬에서 불필요한 이미지를 삭제할 수 있습니다.
   ```bash
   docker rmi [이미지 ID 또는 이름]
   ```

---

