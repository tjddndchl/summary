# 웹 크롤링, 파싱, 스크레핑

이 문서는 웹 크롤링, 파싱, 스크레핑의 개념과 그에 따른 주의사항에 대해 설명합니다.

## 웹 크롤링 (Web Crawling)

**정의**: 웹 크롤링은 인터넷 상의 웹 페이지들을 방문하고 내용을 자동으로 수집하는 과정을 말합니다.

- 사용 도구: 크롤러(Crawler) 또는 스파이더(Spider)라고 부릅니다.
- 주요 목적: 검색 엔진에서 웹 페이지의 최신 정보를 갱신하거나 웹 콘텐츠의 색인 생성 등의 작업을 위해 사용됩니다.

## 파싱 (Parsing)

**정의**: 파싱은 특정 정보를 추출하기 위해 문서나 데이터를 분석하는 과정을 의미합니다.

- 사용 도구: BeautifulSoup, lxml, xml 파서 등의 라이브러리가 주로 사용됩니다.
- 주요 목적: 크롤링을 통해 수집한 웹 콘텐츠에서 필요한 정보만을 추출하기 위해 사용됩니다.

## 웹 스크레핑 (Web Scraping)

**정의**: 웹 스크레핑은 웹 사이트의 데이터를 추출하는 행위입니다. 이때 웹 크롤링과 파싱을 함께 사용하는 경우가 많습니다.

- 사용 도구: Scrapy, BeautifulSoup, Selenium 등의 도구와 라이브러리가 있습니다.
- 주요 목적: 웹 사이트에서 데이터를 추출하여 다양한 용도로 활용하기 위함입니다.

## 주의사항

1. **이용 약관 확인**: 대부분의 웹 사이트는 이용 약관에 웹 크롤링 및 스크레핑에 대한 정책을 명시하고 있습니다. 반드시 해당 사이트의 약관을 확인하고 준수해야 합니다.
2. **robots.txt 확인**: 웹 사이트의 root 디렉터리에 위치한 `robots.txt` 파일은 웹 크롤러가 접근할 수 있는 영역을 지정합니다. 이 파일을 반드시 확인하고 지침을 따라야 합니다.
3. **서버 부하 주의**: 크롤링 시 너무 많은 요청을 빠르게 보내면 웹 사이트의 서버에 부하를 줄 수 있습니다. 적절한 간격을 두고 요청을 보내야 합니다.
4. **개인정보 보호**: 웹 스크레핑을 통해 수집한 데이터 중 개인정보가 포함될 수 있습니다. 이러한 정보는 적절한 방법으로 보호하며, 불법적으로 수집하거나 사용하지 않아야 합니다.
5. **저작권 문제**: 웹 사이트의 콘텐츠는 저작권이 존재할 수 있습니다. 무단으로 수집한 콘텐츠를 재배포하거나 상업적으로 이용하는 것은 법적 제재를 받을 수 있습니다.

웹 크롤링과 스크레핑은 많은 정보를 효율적으로 수집하는 도구로 활용될 수 있지만, 위의 주의사항을 반드시 지켜야 합니다.

# BeautifulSoup과 Requests를 사용한 Python 정적 웹 크롤링

## 설치

먼저 필요한 라이브러리를 설치해야 합니다.

```bash
pip install requests
pip install beautifulsoup4
```

## 기본 사용법

### Requests 사용

`requests.get(url)`를 사용하여 웹 페이지의 HTML을 가져옵니다.

```python
import requests

response = requests.get('https://www.example.com/')
```

### BeautifulSoup 사용

가져온 HTML을 `BeautifulSoup` 객체로 변환합니다.

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.content, 'html.parser')
```

### HTML 요소 찾기

`find`나 `find_all` 메서드를 사용하여 특정 태그나 속성을 가진 요소를 찾을 수 있습니다.

```python
# 첫 번째 <a> 태그를 찾습니다.
first_a_tag = soup.find('a')

# 모든 <a> 태그를 찾습니다.
all_a_tags = soup.find_all('a')
```

## 속성으로 요소 찾기와 값 가져오기

### 요소에서 속성 값 가져오기

```python
# 요소에서 href 속성을 가져옵니다.
link = element['href']

# 요소에서 class 속성을 가져옵니다.
classes = element['class']
```

### 특정 속성으로 요소 찾기

```python
# class가 'my-class'인 div 요소를 찾습니다.
element = soup.find('div', attrs={'class': 'my-class'})
```

## CSS 선택자 사용

### select 메서드

`select` 메서드는 CSS 선택자에 일치하는 모든 요소를 리스트로 반환합니다.

```python
elements = soup.select('div.my-class')
```

### select_one 메서드

`select_one` 메서드는 CSS 선택자에 일치하는 첫 번째 요소를 반환합니다.

```python
element = soup.select_one('div.my-class')
```

## 예제

```python
from bs4 import BeautifulSoup

# 예시 HTML 페이지
html_content = '''
<!DOCTYPE html>
<html>
<head>
    <title>Test Page</title>
</head>
<body>
    <div class="container">
        <a href="https://www.example1.com" class="my-link" id="link1">Example 1</a>
        <a href="https://www.example2.com" class="my-link" id="link2">Example 2</a>
    </div>
</body>
</html>
'''

# BeautifulSoup 객체 생성
soup = BeautifulSoup(html_content, 'html.parser')

# class가 'my-link'인 모든 a 태그를 선택하고 href 값을 출력합니다.
for a_tag in soup.select('a.my-link'):
    print(a_tag.get('href'))

## 동적 웹 크롤링 Selenium과 Python 사용법

### 1. Selenium과 WebDriver 소개
- **예제**: Selenium 공식 문서 또는 Wiki 페이지에서 Selenium의 발전 과정 읽기
- **응용**: Selenium이 어떤 문제들을 해결하려 했는지 이해하고, 다른 테스트 자동화 도구와 비교

### 2. 환경 설정
- **예제**: `pip install selenium` 실행 후 ChromeDriver 설치하기
- **응용**: 다양한 브라우저의 WebDriver 설치 및 테스트하여 각 브라우저별 차이점 파악하기

### 3. 첫 번째 Selenium 스크립트 작성
- **예제**:
  ```python
  from selenium import webdriver

  driver = webdriver.Chrome()
  driver.get("http://www.google.com")
  print(driver.title)
  driver.quit()
  ```
- **응용**: 다양한 웹사이트로 이동하면서 페이지 제목 가져오기

### 4. 웹 요소 찾기
- **예제**: Google 홈페이지에서 검색창 요소 찾기
  ```python
  search_box = driver.find_element(By.NAME,"q")
  ```
- **응용**: 다양한 웹사이트에서 여러 요소를 찾아보며 탐색 기술 향상

### 5. 웹 요소와 상호작용
- **예제**: 검색창에 텍스트 입력하고 검색 버튼 클릭하기
  ```python
  search_box.send_keys("Selenium Python")
  search_box.submit()
  ```
- **응용**: 로그인 페이지에서 아이디/비밀번호 입력하고 로그인 버튼 클릭해보기

### 6. 대기 (Waiting)
- **예제**: 웹 요소가 로드될 때까지 최대 10초 대기
  ```python
  from selenium.webdriver.common.by import By
  from selenium.webdriver.support.ui import WebDriverWait
  from selenium.webdriver.support import expected_conditions as EC

  element = WebDriverWait(driver, 10).until(
      EC.presence_of_element_located((By.ID, "myElement"))
  )
  ```
- **응용**: 페이지 로드 시간이 긴 웹사이트에서 여러 요소의 로드를 대기하며 테스트하기

### 7. Frame 및 Window 관리
- **예제**: iframe 내부의 웹 요소와 상호작용하기
  ```python
  driver.switch_to.frame("frameName")
  ```
- **응용**: 팝업 창 처리, 여러 프레임이 있는 페이지에서 데이터 수집하기

### 8. 고급 웹 요소 상호작용
- **예제**: 드래그 앤 드롭 액션 수행하기
  ```python
  from selenium.webdriver import ActionChains

  source_element = driver.find_element(By.ID,"source")
  target_element = driver.find_element(By.ID,"target")
  actions = ActionChains(driver)
  actions.drag_and_drop(source_element, target_element).perform()
  ```
- **응용**: 다양한 웹 애플리케이션에서 마우스 및 키보드 액션을 조합해 테스트하기

### 9. Selenium 활용 스크린샷 및 로깅
- **예제**: 웹 페이지의 스크린샷 저장하기
  ```python
  driver.save_screenshot("screenshot.png")
  ```
- **응용**: 에러 발생 시 자동으로 스크린샷 찍어 로깅하기
  

하위 페이지가 있다고 가정하고, 웹 크롤링 및 상호작용을 위한 기본적인 Selenium 사용법을 Markdown 형식으로 작성하겠습니다. 이 가이드는 페이지 내부에 있는 링크로 이동하는 방법과 해당 하위 페이지에서 웹 요소와 상호작용하는 방법을 중점적으로 다룹니다.

```markdown
## Selenium을 활용한 하위 페이지 상호작용 방법

### 1. 주요 페이지 접근
- 원하는 웹 페이지에 접근하기
  ```python
  from selenium import webdriver

  driver = webdriver.Chrome()
  driver.get("http://example.com")
  ```

### 2. 하위 페이지 링크 찾기
- 페이지 내의 원하는 링크를 탐색하기
  ```python
  link_to_subpage = driver.find_element_by_partial_link_text("Subpage")
  ```

### 3. 하위 페이지로 이동
- 찾은 링크를 클릭하여 하위 페이지로 이동하기
  ```python
  link_to_subpage.click()
  ```

### 4. 하위 페이지의 웹 요소와 상호작용
- 하위 페이지 내의 웹 요소 찾기
  ```python
  element_on_subpage = driver.find_element_by_id("elementId")
  ```
  
- 웹 요소와의 상호작용 예 (텍스트 입력):
  ```python
  input_box = driver.find_element_by_name("inputName")
  input_box.send_keys("Hello, Selenium!")
  ```

### 5. 하위 페이지에서 정보 수집
- 웹 요소로부터 텍스트 정보 가져오기
  ```python
  text_from_element = element_on_subpage.text
  ```

### 6. 다른 하위 페이지로의 이동
- 동일한 메인 페이지에서 다른 하위 페이지로 이동하려면 스텝 2와 3을 반복합니다.

### 7. 종료
- 작업이 끝나면 웹드라이버를 종료합니다.
  ```python
  driver.quit()
  ```

> **참고**: 웹 페이지나 웹 요소가 완전히 로드될 때까지 기다리기 위해서는 Selenium의 `WebDriverWait`와 같은 대기 기능을 사용하는 것이 좋습니다.
```


# XPath와 BeautifulSoup를 이용한 웹 스크레핑

XPath는 XML 문서의 구조를 통해 요소에 대한 경로를 표현하는 언어입니다. 웹 스크레핑에서는 종종 CSS 선택자로 원하는 요소를 선택하기 어려울 때 XPath를 사용합니다. BeautifulSoup 자체는 XPath를 직접 지원하지 않기 때문에, lxml과 같은 다른 파서를 사용해야 합니다.

## 설치

먼저 필요한 라이브러리를 설치해야 합니다.

```bash
pip install requests
pip install lxml
pip install beautifulsoup4
```

## 기본 사용법

### Requests 사용

웹 페이지의 HTML을 가져오기 위해 `requests.get(url)`를 사용합니다.

```python
import requests

response = requests.get('https://www.example.com/')
```

### BeautifulSoup와 lxml 사용

`lxml` 파서를 사용하여 HTML을 처리하고 XPath를 사용하여 요소를 선택합니다.

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.content, 'lxml')
```

## XPath를 이용한 요소 선택

```python
# 모든 <a> 태그를 선택합니다.
a_tags = soup.xpath('//a')

# href 속성이 'https://www.example.com/'인 <a> 태그를 선택합니다.
specific_a_tag = soup.xpath('//a[@href="https://www.example.com/"]')
```

## 예제

```python
from bs4 import BeautifulSoup
import requests

# 예시 웹 페이지를 가져옵니다.
response = requests.get('https://www.example.com/')

# BeautifulSoup 객체를 lxml 파서로 생성합니다.
soup = BeautifulSoup(response.content, 'lxml')

# class가 'my-link'인 모든 a 태그를 선택합니다.
a_tags = soup.xpath('//a[@class="my-link"]')

# 각 a 태그의 href 값을 출력합니다.
for a_tag in a_tags:
    print(a_tag['href'])
```

이 예제에서는 `xpath` 메서드를 사용하여 `class`가 "my-link"인 모든 `<a>` 태그를 선택하고, 각 태그의 `href` 값을 출력합니다.

## 주의사항

- XPath 표현식은 종종 복잡하게 보일 수 있지만, 대부분의 웹 브라우저 개발자 도구에서는 원하는 요소의 XPath를 쉽게 복사할 수 있습니다.
- `lxml`은 XML 및 HTML 처리를 위한 매우 빠르고 유연한 라이브러리이며, BeautifulSoup와 잘 작동합니다.
- XPath는 웹 크롤링에서 매우 강력한 도구로, 복잡한 선택자를 쉽게 작성할 수 있게 해줍니다.


# Selenium에서 XPath 사용하기

Selenium은 웹 애플리케이션 테스트를 위한 프레임워크로, 실제 브라우저를 사용하여 웹 페이지의 자동화된 테스트를 수행할 수 있습니다. Selenium에서는 원하는 웹 요소를 선택하기 위해 XPath와 CSS 선택자를 사용할 수 있습니다. 이 문서는 Selenium에서 XPath를 사용하는 방법에 중점을 둡니다.

## 설치

먼저 필요한 라이브러리와 드라이버를 설치해야 합니다.

```bash
pip install selenium
```

또한 사용할 브라우저에 맞는 웹 드라이버도 다운로드해야 합니다. 예를 들어, Chrome을 사용한다면 ChromeDriver가 필요합니다.

## 기본 사용법

### WebDriver 설정

Selenium은 다양한 웹 브라우저를 지원합니다. 이 예에서는 Chrome을 사용하겠습니다.

```python
from selenium import webdriver

driver = webdriver.Chrome('/path/to/chromedriver')
```

### 웹 페이지 접근

`get` 메서드를 사용하여 웹 페이지에 접근합니다.

```python
driver.get('https://www.example.com/')
```

### XPath를 이용한 요소 선택

```python
# 첫 번째 <a> 태그를 선택합니다.
first_a_tag = driver.find_element_by_xpath('//a')

# 모든 <a> 태그를 선택합니다.
all_a_tags = driver.find_elements_by_xpath('//a')
```

## 예제

```python
from selenium import webdriver

# WebDriver 객체 생성
driver = webdriver.Chrome('/path/to/chromedriver')
driver.get('https://www.example.com/')

# class가 'my-link'인 모든 a 태그를 선택하고, 각 태그의 텍스트를 출력합니다.
a_tags = driver.find_elements_by_xpath('//a[@class="my-link"]')
for a_tag in a_tags:
    print(a_tag.text)

# 브라우저 닫기
driver.close()
```

## 주의사항

1. **암묵적 대기**: 웹 페이지의 모든 요소가 로드될 때까지 충분한 시간을 기다려야 할 때가 있습니다. 이를 위해 `implicitly_wait`을 사용할 수 있습니다.
   ```python
   driver.implicitly_wait(10)  # 최대 10초 동안 대기
   ```
2. **명시적 대기**: 특정 조건(예: 요소가 로드됨, 요소가 클릭 가능)까지 대기하는 것입니다. `WebDriverWait`와 `expected_conditions`을 사용합니다.
3. **드라이버 경로**: `webdriver.Chrome()`을 사용할 때, chromedriver의 경로를 지정해야 할 수도 있습니다. 드라이버의 경로를 환경 변수에 추가하면 경로를 직접 지정하지 않아도 됩니다.
4. **웹드라이버 종료**: 스크립트 마지막에 `driver.close()` 또는 `driver.quit()`을 사용하여 웹드라이버 세션을 종료해야 합니다.

XPath는 웹 페이지의 구조와 관계를 기반으로 요소를 선택하는 강력한 도구입니다. Selenium과 함께 사용하면 웹 페이지의 동적인 요소도 쉽게 선택하고 조작할 수 있습니다.
