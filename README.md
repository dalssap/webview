# webview 프로젝트

앱 내에서 웹뷰로 표시되는 간단한 웹페이지 프로젝트입니다.

## 프로젝트 개요

이 프로젝트는 모바일 앱의 웹뷰 컴포넌트에서 로드되는 경량 웹페이지를 제공합니다.
Alpine.js를 사용하여 최소한의 JavaScript로 인터랙티브한 UI를 구현했습니다.

## 주요 기능

- ✅ **페이지 닫기**: `webview://close` URL 스킴으로 앱 복귀
- ✅ **반응형 디자인**: 다양한 모바일 화면 크기 지원
- ✅ **경량 프레임워크**: Alpine.js 사용
- ✅ **터치 최적화**: 44px 이상 터치 영역
- ✅ **한글 지원**: 한국어 폰트 최적화

## 프로젝트 구조

```
webview/
├── pages/              # 웹뷰 페이지들
│   ├── index.html     # 홈 페이지
│   └── detail.html    # 상세 페이지
├── assets/            # 정적 리소스
│   ├── css/
│   │   └── main.css   # 공통 스타일시트
│   ├── js/            # JavaScript 파일
│   └── images/        # 이미지 파일
├── components/        # 재사용 가능한 컴포넌트
│   └── close-button.html  # 닫기 버튼 컴포넌트
├── docs/              # 문서
├── CLAUDE.md          # AI 어시스턴트 가이드
├── REQUIREMENTS.md    # 프로젝트 요구사항 명세
└── README.md          # 이 파일
```

## 시작하기

### 1. 로컬 개발 서버 실행

**Python 사용:**
```bash
python3 -m http.server 8000
```

**Node.js 사용:**
```bash
npx http-server -p 8000
```

### 2. 브라우저에서 접속

```
http://localhost:8000/pages/index.html
```

### 3. 모바일 디바이스에서 테스트

**방법 1: 네트워크를 통한 접속**
1. 로컬 IP 주소 확인 (예: 192.168.0.10)
2. 모바일 디바이스에서 `http://192.168.0.10:8000/pages/index.html` 접속

**방법 2: 디바이스 개발자 모드**
- iOS: Safari > 개발자 메뉴 활성화
- Android: Chrome > `chrome://inspect`

## 페이지 가이드

### 홈 페이지 (`pages/index.html`)

홈 페이지는 다음과 같은 예시를 포함합니다:

- **환영 카드**: 프로젝트 소개
- **기능 리스트**: Alpine.js `x-for` 디렉티브 예시
- **카운터**: 인터랙티브 상태 관리 예시
- **토글**: `x-show` 디렉티브 예시
- **페이지 링크**: 다른 페이지로 이동

### 상세 페이지 (`pages/detail.html`)

상세 페이지는 다음과 같은 예시를 포함합니다:

- **사용자 정보**: 정적 데이터 표시
- **할 일 목록**: CRUD 기능 구현
- **설정**: 체크박스와 데이터 바인딩
- **로딩 상태**: 비동기 작업 시뮬레이션

## 새 페이지 만들기

### 기본 템플릿

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>페이지 제목</title>
  <link rel="stylesheet" href="../assets/css/main.css">
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body>
  <div class="page-container">
    <!-- 헤더 -->
    <header class="page-header">
      <h1 class="page-header__title">페이지 제목</h1>
      <a href="webview://close" class="close-button" aria-label="닫기">✕</a>
    </header>

    <!-- 메인 콘텐츠 -->
    <main class="page-content">
      <!-- 여기에 콘텐츠 추가 -->
    </main>

    <!-- 푸터 -->
    <footer class="page-footer">
      <button onclick="window.location.href='webview://close'" class="btn btn--secondary btn--full">
        닫기
      </button>
    </footer>
  </div>
</body>
</html>
```

## 닫기 버튼 사용법

앱으로 돌아가기 위한 닫기 버튼을 추가하는 방법:

### 방법 1: 헤더 심볼 닫기 버튼
```html
<a href="webview://close" class="close-button" aria-label="닫기">✕</a>
```

### 방법 2: 헤더 텍스트 닫기 버튼
```html
<a href="webview://close" class="close-button close-button--text">닫기</a>
```

### 방법 3: 하단 풀 버튼
```html
<button onclick="window.location.href='webview://close'" class="btn btn--secondary btn--full">
  닫기
</button>
```

### 방법 4: Alpine.js 사용
```html
<button @click="window.location.href='webview://close'" class="close-button">✕</button>
```

## Alpine.js 사용 예시

### 기본 데이터 바인딩
```html
<div x-data="{ message: '안녕하세요!' }">
  <p x-text="message"></p>
</div>
```

### 리스트 렌더링
```html
<div x-data="{ items: ['항목1', '항목2', '항목3'] }">
  <ul>
    <template x-for="item in items" :key="item">
      <li x-text="item"></li>
    </template>
  </ul>
</div>
```

### 이벤트 핸들링
```html
<div x-data="{ count: 0 }">
  <button @click="count++">클릭</button>
  <p x-text="count"></p>
</div>
```

### 조건부 렌더링
```html
<div x-data="{ show: true }">
  <button @click="show = !show">토글</button>
  <p x-show="show">보이는 내용</p>
</div>
```

## 스타일 가이드

### CSS 클래스 네이밍

- **컴포넌트**: `kebab-case` (예: `page-header`, `close-button`)
- **BEM 방법론**: `block__element--modifier` (예: `btn--primary`)

### 주요 CSS 클래스

**레이아웃:**
- `.page-container`: 전체 페이지 컨테이너
- `.page-header`: 헤더 영역
- `.page-content`: 메인 콘텐츠 영역
- `.page-footer`: 푸터 영역

**버튼:**
- `.btn`: 기본 버튼
- `.btn--primary`: 주요 액션 버튼 (파란색)
- `.btn--secondary`: 보조 액션 버튼 (회색)
- `.btn--outline`: 외곽선 버튼
- `.btn--full`: 전체 너비 버튼

**카드:**
- `.card`: 카드 컨테이너
- `.card__title`: 카드 제목
- `.card__content`: 카드 내용

**리스트:**
- `.list`: 리스트 컨테이너
- `.list-item`: 리스트 항목
- `.list-item__title`: 항목 제목
- `.list-item__description`: 항목 설명

**유틸리티:**
- `.text-center`, `.text-left`, `.text-right`: 텍스트 정렬
- `.mt-1`, `.mt-2`, `.mt-3`, `.mt-4`: 상단 마진
- `.mb-1`, `.mb-2`, `.mb-3`, `.mb-4`: 하단 마진
- `.hidden`, `.visible`: 표시/숨김

## 성능 최적화

### 이미지 최적화
- WebP 포맷 사용 권장
- 이미지 압축 (< 200KB)
- 적절한 크기로 리사이징

### 코드 최적화
- CSS/JS 파일 최소화
- 불필요한 라이브러리 제거
- CDN 사용 (Alpine.js)

### 로딩 최적화
- `defer` 또는 `async` 스크립트 로드
- 크리티컬 CSS 인라인
- 지연 로딩 (이미지, 콘텐츠)

## 앱 인터페이스

### 지원하는 URL 스킴

#### `webview://close`
웹뷰를 닫고 앱으로 돌아갑니다.

```javascript
window.location.href = 'webview://close';
```

#### 향후 확장 가능한 스킴 (예시)
```javascript
// 공유 기능
window.location.href = 'webview://share?url=...&text=...';

// 외부 브라우저 열기
window.location.href = 'webview://open?url=...';

// 앱 특정 화면으로 이동
window.location.href = 'webview://navigate?screen=...';
```

## 테스트

### 체크리스트

- [ ] 페이지가 정상적으로 로드됨
- [ ] 닫기 버튼이 명확하게 표시됨
- [ ] 닫기 버튼 클릭 시 `webview://close` 호출됨
- [ ] 다양한 화면 크기에서 레이아웃 정상 동작
- [ ] 터치 인터랙션이 반응함
- [ ] 한글이 올바르게 표시됨
- [ ] 콘솔 에러가 없음
- [ ] Alpine.js 디렉티브가 정상 작동함

### 디버깅

**iOS Safari:**
1. 설정 > Safari > 고급 > Web Inspector 활성화
2. Mac Safari > 개발자 > [디바이스명] > [페이지명]

**Android Chrome:**
1. Chrome에서 `chrome://inspect` 접속
2. 디바이스 연결 후 DevTools 사용

## 문서

- **CLAUDE.md**: AI 어시스턴트를 위한 개발 가이드
- **REQUIREMENTS.md**: 프로젝트 요구사항 명세서
- **README.md**: 프로젝트 사용 설명서 (이 파일)

## 기술 스택

- **HTML5**: 마크업
- **CSS3**: 스타일링
- **Alpine.js 3.x**: 경량 JavaScript 프레임워크
- **Python/Node.js**: 로컬 개발 서버

## 브라우저 지원

- iOS Safari 14+
- Android Chrome 90+
- iOS WKWebView
- Android WebView

## 라이선스

MIT License

## 기여

버그 리포트나 기능 제안은 이슈 트래커를 통해 제출해주세요.

## 문의

프로젝트 관련 문의사항은 팀 멤버에게 연락해주세요.

---

**마지막 업데이트:** 2025-11-15
