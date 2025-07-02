# HTML, CSS, JavaScript 기초 학습 프로젝트

이 프로젝트는 웹 개발의 3가지 핵심 기술인 HTML, CSS, JavaScript의 기본 개념을 학습하기 위한 간단한 웹 애플리케이션입니다.

## 프로젝트 구조

```
html_basic/
├── index.html    # HTML 구조 정의
├── styles.css    # CSS 스타일 정의
├── script.js     # JavaScript 동작 정의
└── README.md     # 프로젝트 설명
```

## 핵심 기술 설명

### 1. HTML (HyperText Markup Language)
- 웹 페이지의 구조와 콘텐츠를 정의하는 마크업 언어
- 주요 요소:
  - `<!DOCTYPE html>`: HTML5 문서 선언
  - `<html>`: 전체 HTML 문서의 루트 요소
  - `<head>`: 메타데이터, 스타일, 스크립트 참조 등을 포함
  - `<body>`: 사용자에게 보이는 실제 콘텐츠
  - `<header>`, `<main>`, `<footer>`: 시맨틱 구조 요소
  - `<form>`, `<input>`, `<select>`: 사용자 입력 요소

### 2. CSS (Cascading Style Sheets)
- 웹 페이지의 시각적 표현과 레이아웃을 정의하는 스타일 언어
- 주요 개념:
  - 선택자(Selector): 스타일을 적용할 HTML 요소 지정
  - 속성(Property): 색상, 크기, 여백 등의 스타일 특성
  - 값(Value): 속성에 할당되는 구체적인 설정
  - 박스 모델: 콘텐츠, 패딩, 테두리, 마진으로 구성된 레이아웃 모델
  - 반응형 디자인: 다양한 화면 크기에 맞게 조정되는 레이아웃

### 3. JavaScript
- 웹 페이지에 동적 기능을 추가하는 프로그래밍 언어
- 주요 기능:
  - DOM 조작: HTML 요소 선택, 수정, 추가, 삭제
  - 이벤트 처리: 사용자 상호작용(클릭, 입력 등)에 반응
  - 폼 유효성 검사: 사용자 입력 데이터 검증
  - 동적 콘텐츠 생성: 데이터에 기반한 HTML 콘텐츠 생성
  - 애니메이션: 시각적 효과 구현

### 4. DOM 객체 활용
- DOM(Document Object Model)은 HTML 문서를 프로그래밍적으로 조작할 수 있는 인터페이스
- 주요 활용 방법:
  - **DOM 객체 참조 획득**: `document.getElementById()`, `querySelector()` 등을 사용하여 HTML 요소 참조
  - **이벤트 리스너 등록**: `addEventListener()`를 사용하여 사용자 상호작용에 반응하는 함수 등록
  - **이벤트 처리 및 DOM 조작**: 이벤트 발생 시 `innerHTML`, `textContent` 등을 사용하여 HTML 콘텐츠 변경
  - **이벤트 기본 동작 방지**: `event.preventDefault()`를 사용하여 폼 제출 시 페이지 새로고침 방지

#### DOM 객체 활용 원리 상세 설명

이 프로젝트에서 제출 버튼을 누르면 우측에 결과가 나타나는 과정은 다음과 같은 DOM 객체 활용 원리를 따릅니다:

1. **DOM 트리 구성**: 브라우저가 HTML을 파싱하여 DOM 트리를 구성합니다. 각 HTML 요소는 DOM 노드가 됩니다.
2. **DOM 객체 참조**: JavaScript에서 `document.getElementById()`와 같은 메서드로 DOM 노드에 접근합니다.
3. **이벤트 감지**: 사용자가 제출 버튼을 클릭하면 `submit` 이벤트가 발생합니다.
4. **이벤트 처리**: 등록된 이벤트 리스너가 이벤트를 감지하고 콜백 함수를 실행합니다.
5. **DOM 조작**: 콜백 함수 내에서 DOM 객체의 속성이나 내용을 변경하여 화면에 결과를 표시합니다.

#### 실제 코드 흐름 설명

```javascript
// 1. DOM 객체 참조 획득 - HTML 요소를 JavaScript 변수에 할당
const userForm = document.getElementById('user-form'); // 폼 요소 참조
const nameInput = document.getElementById('name'); // 이름 입력 필드
const ageInput = document.getElementById('age'); // 나이 입력 필드
const colorSelect = document.getElementById('color'); // 색상 선택 필드
const resultDisplay = document.getElementById('result-display'); // 결과 표시 영역

// 2. 이벤트 리스너 등록 - 폼 제출 이벤트 감지
userForm.addEventListener('submit', function(event) {
    // 3. 기본 동작 방지 - 페이지 새로고침 방지
    event.preventDefault();
    
    // 4. 입력값 가져오기
    const name = nameInput.value.trim();
    const age = ageInput.value.trim();
    const color = colorSelect.value;
    
    // 5. 입력값 검증
    if (!name || !age) {
        alert('이름과 나이를 모두 입력해주세요.');
        return;
    }
    
    // 6. 결과 표시 함수 호출
    displayResult(name, age, color);
});

// 7. DOM 조작으로 결과 표시 함수
function displayResult(name, age, color) {
    // 8. HTML 템플릿 생성
    const resultHTML = `
        <h3>입력 정보 결과</h3>
        <p><strong>이름:</strong> ${name}</p>
        <p><strong>나이:</strong> ${age}세</p>
        <p>
            <strong>좋아하는 색상:</strong> 
            <span class="color-display" style="background-color: ${color};"></span>
            ${getColorName(color)}
        </p>
    `;
    
    // 9. DOM 요소 내용 변경 - innerHTML 속성 사용
    resultDisplay.innerHTML = resultHTML;
    
    // 10. 스타일 속성 변경 - CSS 속성 직접 조작
    resultDisplay.style.borderColor = color;
    
    // 11. 클래스 조작 - 애니메이션 효과 추가
    resultDisplay.classList.add('fade-in');
    
    // 12. 타이머 설정 - 일정 시간 후 클래스 제거
    setTimeout(() => {
        resultDisplay.classList.remove('fade-in');
    }, 500);
}
```

#### DOM 객체 활용의 장점

1. **동적 UI 업데이트**: 페이지 전체를 새로고침하지 않고 특정 부분만 업데이트할 수 있습니다.
2. **사용자 경험 향상**: 빠른 응답성과 부드러운 전환 효과로 사용자 경험이 향상됩니다.
3. **서버 부하 감소**: 필요한 데이터만 주고받아 서버 부하를 줄일 수 있습니다.
4. **상태 유지**: 페이지 새로고침 없이 애플리케이션 상태를 유지할 수 있습니다.

#### DOM 조작 방식 비교

| 방식 | 코드 예시 | 용도 |
|------|----------|------|
| `innerHTML` | `element.innerHTML = '<p>새 내용</p>'` | HTML 마크업을 포함한 내용 변경 |
| `textContent` | `element.textContent = '새 텍스트'` | 텍스트만 변경 (보안에 더 안전) |
| `appendChild` | `element.appendChild(newElement)` | 새 요소 추가 |
| `classList` | `element.classList.add('highlight')` | CSS 클래스 조작 |
| `style` | `element.style.color = 'red'` | 인라인 스타일 직접 조작 |

이러한 DOM 조작 기능은 JavaScript의 핵심 기능 중 하나로, 정적인 HTML 페이지를 동적으로 변경할 수 있게 해줍니다. 이를 통해 페이지를 새로고침하지 않고도 사용자와 상호작용하는 웹 애플리케이션을 만들 수 있습니다.

## 핵심 코드 설명

### HTML 핵심 코드
```html
<!-- 기본 HTML 구조 -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>웹 기초 학습</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- 콘텐츠 구조 -->
    <header>...</header>
    <main>
        <section id="user-input-section">...</section>
        <section id="result-section">...</section>
    </main>
    <footer>...</footer>
    <script src="script.js"></script>
</body>
</html>
```

### CSS 핵심 코드
```css
/* 기본 스타일 설정 */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: 'Arial', sans-serif;
}

/* 레이아웃 구성 */
main {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

/* 반응형 디자인 */
@media (max-width: 768px) {
    main {
        flex-direction: column;
    }
    
    section {
        min-width: 100%;
    }
}
```

### JavaScript 핵심 코드
```javascript
// DOM 로드 후 실행
document.addEventListener('DOMContentLoaded', function() {
    // 요소 참조 가져오기
    const userForm = document.getElementById('user-form');
    
    // 이벤트 리스너 등록
    userForm.addEventListener('submit', function(event) {
        // 기본 동작 방지
        event.preventDefault();
        
        // 입력값 가져오기 및 처리
        const username = usernameInput.value.trim();
        
        // 유효성 검사 및 결과 표시
        if (조건) {
            showError('메시지');
        } else {
            displayResult(데이터);
        }
    });
});
```

## 실행 방법

1. 프로젝트 폴더의 `index.html` 파일을 웹 브라우저에서 열기
2. 또는 로컬 웹 서버를 사용하여 실행:
   ```
   # Python을 사용한 간단한 웹 서버 실행 예시
   python -m http.server
   ```
   그리고 브라우저에서 `http://localhost:8000` 접속

## 학습 포인트

1. **HTML**: 시맨틱 태그 사용, 폼 구조, 문서 구조화
2. **CSS**: 선택자, 박스 모델, Flexbox 레이아웃, 반응형 디자인
3. **JavaScript**: DOM 조작, 이벤트 처리, 폼 유효성 검사, 동적 콘텐츠 생성
4. **DOM 활용**: DOM 객체 참조, 이벤트 리스너, 동적 콘텐츠 업데이트, 사용자 상호작용 처리

이 프로젝트를 통해 웹 개발의 기초를 이해하고, 세 가지 핵심 기술이 어떻게 상호작용하는지 배울 수 있습니다.
