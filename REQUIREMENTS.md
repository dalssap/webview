# REQUIREMENTS.md - webview 프로젝트 요구사항 명세서

**최종 업데이트:** 2025-11-15
**저장소:** dalssap/webview
**상태:** 개발 중

---

## 목차

1. [프로젝트 개요](#프로젝트-개요)
2. [웹뷰 환경 요구사항](#웹뷰-환경-요구사항)
3. [기능 요구사항](#기능-요구사항)
4. [기술 요구사항](#기술-요구사항)
5. [디자인 요구사항](#디자인-요구사항)
6. [성능 요구사항](#성능-요구사항)
7. [보안 요구사항](#보안-요구사항)

---

## 프로젝트 개요

### 목적

이 프로젝트는 **모바일 앱 내에서 웹뷰로 표시되는 간단한 웹페이지**를 개발하는 것을 목표로 합니다.

### 범위

- 정적 HTML/CSS/JavaScript 기반 웹페이지
- 앱 웹뷰에서 로드 및 표시
- 앱과의 기본적인 인터페이스 (페이지 닫기 등)

---

## 웹뷰 환경 요구사항

### 플랫폼

- **iOS**: WKWebView
- **Android**: WebView

### 제약사항

- 모든 페이지는 앱의 웹뷰 컨테이너 내에서 실행
- 네이티브 앱 기능은 특정 URL 스킴을 통해 접근
- 새 창(팝업) 사용 불가
- 일부 웹 API 제한 가능

---

## 기능 요구사항

### FR-001: 페이지 닫기 기능

**우선순위:** 필수
**설명:** 사용자가 웹뷰 페이지를 닫고 앱으로 돌아갈 수 있어야 합니다.

**구현 방법:**
- 닫기 버튼 클릭 시 `webview://close` URL로 이동
- 앱이 이 URL 스킴을 인터셉트하여 웹뷰 닫기 처리

**예시 코드:**
```html
<!-- 링크 방식 -->
<a href="webview://close" class="close-button">닫기</a>

<!-- 버튼 방식 -->
<button onclick="window.location.href='webview://close'" class="close-button">
  닫기
</button>

<!-- Alpine.js 방식 -->
<button @click="window.location.href='webview://close'" class="close-button">
  닫기
</button>
```

**기대 동작:**
1. 사용자가 닫기 버튼 클릭
2. `webview://close` URL로 이동 시도
3. 앱이 URL을 감지하고 웹뷰 종료
4. 사용자가 이전 앱 화면으로 돌아감

### FR-002: 반응형 레이아웃

**우선순위:** 필수
**설명:** 다양한 모바일 디바이스 화면 크기에 대응

**요구사항:**
- 세로 방향(Portrait) 주로 지원
- 가로 방향(Landscape) 선택적 지원
- 최소 화면 너비: 320px (iPhone SE)
- 최대 화면 너비: 428px (iPhone 14 Pro Max 등)

### FR-003: 터치 인터페이스

**우선순위:** 필수
**설명:** 모바일 터치 환경에 최적화된 UI

**요구사항:**
- 터치 타겟 최소 크기: 44x44px (iOS 기준)
- 스와이프, 핀치 줌 등 제스처 고려
- 터치 피드백 제공

---

## 기술 요구사항

### TR-001: 기술 스택

**필수 기술:**
- HTML5
- CSS3
- JavaScript (ES6+)
- Alpine.js 3.x (경량 프레임워크)

**선택 기술:**
- 빌드 도구 (추후 필요 시)
- CSS 전처리기 (추후 필요 시)

### TR-002: 브라우저 호환성

**지원 대상:**
- iOS Safari 14+
- Android Chrome 90+
- 웹뷰 환경: iOS WKWebView, Android WebView

**미지원:**
- 데스크톱 브라우저 (선택적 지원)
- IE 및 레거시 브라우저

### TR-003: 외부 의존성

**허용:**
- CDN을 통한 Alpine.js 로드
- 웹 폰트 (Google Fonts 등)
- 최소한의 외부 라이브러리

**제한:**
- 대용량 라이브러리 금지 (React, Vue 등)
- 불필요한 의존성 최소화
- 번들 크기 최적화

---

## 디자인 요구사항

### DR-001: UI/UX 원칙

**원칙:**
1. **단순성**: 명확하고 직관적인 인터페이스
2. **일관성**: 모든 페이지에서 일관된 디자인 언어
3. **접근성**: 읽기 쉬운 글꼴 크기 및 색상 대비
4. **성능**: 빠른 로딩과 부드러운 인터랙션

### DR-002: 닫기 버튼 디자인

**위치:**
- 우선순위 1: 상단 오른쪽 (일반적인 모바일 패턴)
- 우선순위 2: 하단 고정 버튼
- 페이지 컨텍스트에 따라 적절한 위치 선택

**스타일:**
- 명확하게 인식 가능해야 함
- 최소 터치 영역: 44x44px
- 아이콘 또는 텍스트 사용 가능
- 예: "✕", "닫기", "← 뒤로"

### DR-003: 타이포그래피

**한글 폰트:**
- 본문: 14px 이상
- 제목: 20px 이상
- 줄 간격: 1.5 이상
- 시스템 폰트 우선 사용 (성능)

**폰트 스택 예시:**
```css
font-family: -apple-system, BlinkMacSystemFont,
             "Malgun Gothic", "맑은 고딕",
             "Apple SD Gothic Neo", "Noto Sans KR",
             sans-serif;
```

### DR-004: 색상 및 테마

**기본 요구사항:**
- 충분한 색상 대비 (WCAG AA 기준)
- 다크 모드 지원 (선택적)
- 브랜드 컬러 일관성 유지

---

## 성능 요구사항

### PR-001: 로딩 성능

**목표:**
- 초기 로딩 시간: 2초 이내 (3G 네트워크)
- First Contentful Paint (FCP): 1.5초 이내
- Time to Interactive (TTI): 3초 이내

**최적화 방법:**
- 이미지 최적화 (WebP, 압축)
- CSS/JS 최소화
- 중요 리소스 우선 로드
- 불필요한 외부 요청 제거

### PR-002: 런타임 성능

**목표:**
- 60fps 부드러운 스크롤 및 애니메이션
- JavaScript 실행 시간 최소화
- 메모리 사용량 제한 (< 50MB)

**최적화 방법:**
- Alpine.js의 경량성 활용
- 무거운 연산 회피
- 이벤트 핸들러 최적화

### PR-003: 리소스 크기

**제한:**
- HTML 파일: < 50KB
- CSS 파일: < 100KB
- JavaScript 파일: < 100KB (Alpine.js 제외)
- 이미지: < 200KB (페이지당)
- 총 페이지 크기: < 500KB

---

## 보안 요구사항

### SR-001: XSS 방지

**필수 조치:**
- 모든 사용자 입력 이스케이프 처리
- innerHTML 사용 최소화
- Alpine.js의 안전한 데이터 바인딩 활용

### SR-002: 민감 정보 보호

**금지 사항:**
- 하드코딩된 API 키, 비밀번호
- 로컬 스토리지에 민감 정보 저장
- 콘솔 로그에 개인정보 출력

### SR-003: 안전한 통신

**요구사항:**
- 모든 외부 리소스 HTTPS로 로드
- Mixed Content 금지
- CSP(Content Security Policy) 적용 권장

### SR-004: URL 스킴 보안

**webview:// 스킴 사용:**
- 허용된 액션만 사용 (`close` 등)
- 사용자 입력으로 URL 스킴 생성 금지
- 앱 측에서 검증 필수

**예시:**
```javascript
// ✅ 안전: 하드코딩된 URL
window.location.href = 'webview://close';

// ❌ 위험: 사용자 입력 기반
const action = userInput; // XSS 위험
window.location.href = `webview://${action}`;
```

---

## 앱 인터페이스 명세

### 지원하는 URL 스킴

#### webview://close

**목적:** 웹뷰 페이지 닫기
**파라미터:** 없음
**동작:** 웹뷰를 닫고 이전 앱 화면으로 돌아감

**사용 예시:**
```html
<a href="webview://close">닫기</a>
<button onclick="window.location.href='webview://close'">닫기</button>
```

#### 향후 확장 가능한 스킴 (예시)

```
webview://share?url=...&text=...  # 공유 기능
webview://open?url=...            # 외부 브라우저 열기
webview://navigate?screen=...     # 앱 특정 화면으로 이동
```

---

## 개발 가이드라인

### 페이지 구조 템플릿

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>페이지 제목</title>
  <link rel="stylesheet" href="/assets/css/main.css">
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body>
  <!-- 헤더: 닫기 버튼 포함 -->
  <header class="page-header">
    <h1>페이지 제목</h1>
    <a href="webview://close" class="close-button" aria-label="닫기">✕</a>
  </header>

  <!-- 메인 콘텐츠 -->
  <main class="page-content">
    <!-- 콘텐츠 영역 -->
  </main>

  <!-- 선택적: 하단 고정 버튼 -->
  <footer class="page-footer">
    <button onclick="window.location.href='webview://close'" class="btn btn-secondary">
      닫기
    </button>
  </footer>
</body>
</html>
```

### 닫기 버튼 스타일 예시

```css
/* 상단 우측 닫기 버튼 */
.page-header {
  position: relative;
  padding: 16px;
  border-bottom: 1px solid #e0e0e0;
}

.close-button {
  position: absolute;
  top: 12px;
  right: 12px;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  color: #333;
  text-decoration: none;
  border-radius: 50%;
  transition: background-color 0.2s;
}

.close-button:active {
  background-color: rgba(0, 0, 0, 0.1);
}
```

---

## 테스트 요구사항

### 테스트 환경

**필수 테스트:**
- iOS 실제 디바이스 (최신 버전)
- Android 실제 디바이스 (최신 버전)
- 앱 웹뷰 환경에서 테스트

**선택 테스트:**
- 다양한 iOS 버전
- 다양한 Android 버전
- 태블릿 화면 크기

### 테스트 체크리스트

- [ ] 페이지가 정상적으로 로드됨
- [ ] 닫기 버튼이 명확하게 표시됨
- [ ] 닫기 버튼 클릭 시 웹뷰가 닫힘
- [ ] 다양한 화면 크기에서 레이아웃 정상 동작
- [ ] 터치 인터랙션이 반응함
- [ ] 로딩 시간이 2초 이내
- [ ] 한글이 올바르게 표시됨
- [ ] 이미지가 최적화되어 로드됨
- [ ] 콘솔 에러가 없음

---

## 비기능 요구사항

### 유지보수성

- 명확한 코드 구조
- 주석을 통한 문서화
- 일관된 네이밍 규칙
- 모듈화된 컴포넌트

### 확장성

- 새로운 페이지 추가 용이
- 공통 컴포넌트 재사용
- 스타일 시스템 확장 가능

### 접근성

- 시맨틱 HTML 사용
- ARIA 레이블 적용
- 키보드 네비게이션 (선택적)
- 스크린 리더 고려

---

## 제약사항 및 가정

### 제약사항

1. **웹뷰 환경**: 일부 웹 API 제한
2. **네트워크**: 불안정한 모바일 네트워크 고려
3. **성능**: 모바일 디바이스의 제한된 리소스
4. **플랫폼**: iOS/Android 웹뷰 차이

### 가정

1. 사용자는 최신 또는 최근 OS 버전 사용
2. 앱이 `webview://` URL 스킴을 올바르게 처리
3. 인터넷 연결 필요 (CDN 리소스 로드)
4. 사용자는 한국어 사용

---

## 우선순위

### P0 (필수)

- 페이지 닫기 기능 (webview://close)
- 기본 반응형 레이아웃
- 모바일 웹뷰 호환성
- 한글 지원

### P1 (높음)

- 성능 최적화
- 접근성 개선
- 보안 강화

### P2 (중간)

- 다크 모드 지원
- 고급 애니메이션
- 오프라인 지원

### P3 (낮음)

- 데스크톱 지원
- 추가 URL 스킴
- A/B 테스트 지원

---

## 버전 히스토리

| 날짜       | 버전  | 변경사항                | 작성자    |
|------------|-------|-------------------------|-----------|
| 2025-11-15 | 1.0.0 | 초기 요구사항 명세 작성 | Claude AI |

---

## 승인 및 검토

**작성자:** Claude AI
**검토자:** TBD
**승인자:** TBD
**승인일:** TBD

---

**참고:**
- 이 문서는 프로젝트의 요구사항을 정의합니다
- 구현 세부사항은 CLAUDE.md를 참조하세요
- 요구사항 변경 시 버전을 업데이트하고 변경 이력을 기록하세요
