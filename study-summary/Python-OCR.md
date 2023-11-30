# OCR (Optical Character Recognition)

## 정의
OCR (Optical Character Recognition)은 이미지나 스캔된 문서에서 문자를 인식하여 텍스트 데이터로 변환하는 기술을 말합니다. OCR 기술을 사용하면 종이에 인쇄된 텍스트 문서를 디지털 포맷으로 빠르게 변환할 수 있습니다.

## 사용 분야
1. **문서 자동화**: 스캔된 문서나 사진에서 텍스트를 추출해 디지털 문서로 변환
2. **은행**: 청구서나 수표의 금액 및 정보를 자동으로 인식
3. **도서관**: 오래된 책이나 문서를 디지털 아카이브로 변환
4. **자동차 번호판 인식**: 주차 관리나 교통 법규 위반 감시에 사용
5. **모바일 응용 프로그램**: 사진이나 이미지에서 텍스트를 인식하여 번역, 검색 등의 작업 수행

## 현재 발전 내용
- **딥러닝과 AI**를 활용한 OCR: 고전적인 방법보다 더 정확하고 복잡한 폰트나 배경에서도 문자를 잘 인식합니다.
- **실시간 인식**: 스마트폰 카메라를 통해 실시간으로 텍스트를 인식하고 변환하는 기술 발전
- **다양한 언어 및 폰트 지원**: 전세계 다양한 언어와 스타일의 글씨체를 인식할 수 있는 능력 향상
- **증강 현실 (AR)과의 통합**: AR 앱에서 실제 환경의 텍스트를 인식하고 번역하거나 추가 정보 제공

OCR 기술은 지속적으로 발전하고 있으며, 다양한 분야에서 효율적인 정보 처리와 자동화를 위해 활용되고 있습니다.


# Python을 이용한 OCR 예제

Python에서는 주로 `pytesseract` 라이브러리를 활용하여 OCR을 구현합니다. `pytesseract`는 Google의 Tesseract-OCR 엔진을 Python에서 사용할 수 있게 해주는 래퍼(wrapper)입니다. 

아래에는 이미지에서 영어와 한국어 텍스트를 추출하는 간단한 예제들을 제시합니다.

## 환경 준비

1. Tesseract 설치
    - Windows, Linux, macOS 등의 OS에 따라 Tesseract 설치 방법이 다를 수 있습니다. 
    - 공식 문서나 관련 가이드를 참고하여 설치하세요.

2. Python 라이브러리 설치:
```bash
pip install pytesseract pillow
```

## 예제 코드

```python
from PIL import Image
import pytesseract

# 이미지 파일 경로
img_path = 'path_to_your_image.jpg'

# 이미지 열기
image = Image.open(img_path)

# OCR 실행
text_english = pytesseract.image_to_string(image, lang='eng')  # 영어
text_korean = pytesseract.image_to_string(image, lang='kor')  # 한국어

print("영어 텍스트:")
print(text_english)
print("\n한국어 텍스트:")
print(text_korean)
```

## 10가지 팁:

1. **이미지 전처리**: 노이즈 제거, 명암 조절 등의 전처리 작업으로 OCR의 정확도를 높일 수 있습니다.
2. **다양한 언어**: `lang` 파라미터를 통해 여러 언어를 동시에 인식할 수 있습니다. 예: `lang='eng+kor'`
3. **페이지 분할 모드**: `--psm` 옵션을 통해 페이지의 레이아웃을 명시할 수 있습니다.
4. **사용자 사전**: Tesseract에게 특정 단어나 용어를 알려주기 위해 사용자 사전을 제공할 수 있습니다.
5. **바운딩 박스**: `image_to_boxes` 함수를 사용하여 인식된 문자별로 위치 정보를 가져올 수 있습니다.
6. **글씨체 학습**: Tesseract를 특정 폰트나 스타일에 특화되게 학습시킬 수 있습니다.
7. **PDF 변환**: `pytesseract`를 사용하여 이미지를 검색 가능한 PDF로 변환할 수 있습니다.
8. **Batch Processing**: 여러 이미지 파일을 한번에 처리할 수 있습니다.
9. **Configurations**: `config` 파라미터를 통해 Tesseract의 다양한 설정을 조절할 수 있습니다.
10. **HOCR 출력**: `image_to_pdf_or_hocr` 함수를 사용하여 HOCR 형식의 출력을 얻을 수 있습니다. HOCR은 OCR 결과를 HTML 형식으로 제공하는 표준입니다.

이렇게 Python과 `pytesseract`를 사용하면 이미지에서의 문자 인식이 간편하고 효과적으로 이루어질 수 있습니다.

물론이죠! 아래는 Python과 `pytesseract`를 사용하여 이미지에서 텍스트를 추출하는 간단한 예제 코드를 나열하였습니다.

## 1. 기본적인 텍스트 추출

```python
from PIL import Image
import pytesseract

image = Image.open('sample.jpg')
text = pytesseract.image_to_string(image, lang='eng')
print(text)
```

## 2. 이미지 전처리와 OCR

```python
from PIL import Image, ImageEnhance, ImageFilter

image = Image.open('sample.jpg')
image = image.convert('L')  # 그레이스케일로 변환
image = image.filter(ImageFilter.SHARPEN)  # 이미지 선명하게
text = pytesseract.image_to_string(image, lang='eng')
print(text)
```

## 3. 여러 언어 동시에 인식

```python
image = Image.open('sample.jpg')
text = pytesseract.image_to_string(image, lang='eng+kor')
print(text)
```

## 4. 글자의 바운딩 박스 가져오기

```python
image = Image.open('sample.jpg')
boxes = pytesseract.image_to_boxes(image, lang='eng')
print(boxes)
```

## 5. 페이지 분할 모드 사용

```python
image = Image.open('sample.jpg')
text = pytesseract.image_to_string(image, lang='eng', config='--psm 6')
print(text)
```

## 6. 사용자 사전 사용

- 사용자 사전 준비 (예: `user_words.txt`에 단어 목록을 저장)

```python
image = Image.open('sample.jpg')
text = pytesseract.image_to_string(image, lang='eng', config='--user-words user_words.txt')
print(text)
```

## 7. 검색 가능한 PDF 생성

```python
from pytesseract import image_to_pdf_or_hocr


image = Image.open('sample.jpg')
pdf = image_to_pdf_or_hocr('sample.jpg', extension='pdf')
with open('output.pdf', 'w+b') as f:
    f.write(pdf)
```

## 8. Batch Processing

```python
images = ['sample1.jpg', 'sample2.jpg', 'sample3.jpg']
for img in images:
    image = Image.open(img)
    text = pytesseract.image_to_string(image, lang='eng')
    print(f"=== {img} ===")
    print(text)
```

## 9. Configurations

```python
image = Image.open('sample.jpg')
text = pytesseract.image_to_string(image, lang='eng', config='--psm 6 --oem 3')
print(text)
```

## 10. HOCR 출력

```python
hocr = pytesseract.image_to_pdf_or_hocr('sample.jpg', extension='hocr')
with open('output.hocr', 'w+b') as f:
    f.write(hocr)
```

이 예제들은 기본적인 이미지 파일(`sample.jpg`)에서 텍스트를 추출하기 위한 것이므로 실제 사용할 때에는 이미지 파일 경로나 설정을 적절히 조정해야 합니다.
OCR을 위한 다양한 라이브러리와 도구들이 있습니다. `pytesseract`와 Tesseract-OCR는 가장 널리 알려져 있고 무료로 사용할 수 있기 때문에 많이 사용되지만, 그 외에도 여러 라이브러리와 서비스가 있습니다. 아래는 그 중 일부입니다:

1. **OpenCV**: 이미지 처리와 컴퓨터 비전 라이브러리로, OCR 전처리를 위해 많이 사용됩니다. OpenCV 자체는 OCR 기능을 제공하지 않지만, 이미지 처리를 통해 OCR의 정확도를 높일 수 있습니다.

2. **EasyOCR**: Python 기반의 라이브러리로, 딥러닝을 기반으로 한 OCR 기능을 제공합니다. 여러 언어를 지원하며, 상당히 높은 정확도를 보입니다.
   ```bash
   pip install easyocr
   ```

   ```python
   import easyocr
   reader = easyocr.Reader(['en', 'ko'])
   results = reader.readtext('sample.jpg')
   for result in results:
       text = result[1]
       print(text)
   ```

3. **CRAFT (Character Region Awareness for Text Detection)**: 딥러닝 기반의 텍스트 탐지 알고리즘으로, 텍스트의 영역을 탐지하는 데 특화되어 있습니다.

4. **ABBYY FineReader**: 상용 OCR 소프트웨어로, 높은 정확도와 다양한 기능을 제공합니다.

5. **Amazon Textract**: AWS에서 제공하는 OCR 서비스로, 클라우드 기반으로 동작하며 높은 정확도와 확장성을 제공합니다.

6. **Google Cloud Vision API**: Google Cloud 플랫폼에서 제공하는 OCR 서비스로, 이미지 분석 및 문자 인식 기능을 포함합니다.

7. **Microsoft Azure Computer Vision API**: Azure 플랫폼에서 제공하는 이미지 분석 및 OCR 서비스입니다.

이 중 일부는 무료로 사용할 수 있지만, 사용량이나 기능에 따라 비용이 발생할 수 있습니다. 사용 사례와 필요에 따라 가장 적합한 도구나 라이브러리를 선택하는 것이 좋습니다.

# EasyOCR 사용법 및 자동차 번호판 인식 예제

## EasyOCR 기본 사용법

1. **설치**: 
    ```bash
    pip install easyocr
    ```

2. **기본적인 텍스트 추출**:
    ```python
    import easyocr
    reader = easyocr.Reader(['en'])
    results = reader.readtext('image.jpg')
    for result in results:
        text = result[1]
        print(text)
    ```

3. **여러 언어 지원**:
    ```python
    reader = easyocr.Reader(['en', 'ko'])
    ```

4. **텍스트 영역의 좌표 얻기**:
    ```python
    results = reader.readtext('image.jpg')
    for result in results:
        coords = result[0]
        print(coords)
    ```

5. **텍스트 탐지 정확도**:
    ```python
    results = reader.readtext('image.jpg')
    for result in results:
        confidence = result[2]
        print(confidence)
    ```

6. **결과 필터링**:
    ```python
    results = [result for result in reader.readtext('image.jpg') if result[2] > 0.9]
    ```

7. **상세 정보 출력**:
    ```python
    results = reader.readtext('image.jpg', detail=1)
    ```

8. **이미지 내부의 특정 영역에서 텍스트 읽기**:
    ```python
    bounds = [(10, 10, 100, 100)]
    results = reader.readtext('image.jpg', allowlist=bounds)
    ```

9. **이미지 전처리로 OCR 향상**: 
    - OpenCV와 같은 라이브러리를 사용하여 이미지의 명암, 샤프니스 등을 조절할 수 있습니다.

10. **GPU 지원**:
    - EasyOCR은 GPU를 지원하므로, GPU가 설치되어 있으면 처리 속도가 빨라집니다.

## 자동차 번호판 인식 예제

```python
import easyocr

# 번호판을 인식하기 위한 Reader 생성
reader = easyocr.Reader(['en'])

# 이미지에서 텍스트 추출
results = reader.readtext('license_plate.jpg')

# 번호판이 주로 큰 텍스트로 표시되므로 가장 긴 문자열을 찾음
license_plate_text = max(results, key=lambda r: len(r[1]))[1]

print("License Plate:", license_plate_text)
```

이 예제는 간단하게 자동차의 번호판을 인식하는 방법을 보여줍니다. 실제로 번호판 인식을 구현할 때에는 다양한 전처리 단계와 추가 로직이 필요할 수 있습니다.

