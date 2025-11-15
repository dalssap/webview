# CLAUDE.md - webview 프로젝트 AI 어시스턴트 가이드

**최종 업데이트:** 2025-11-15
**저장소:** dalssap/webview
**상태:** 개발 중

---

## 개요

이 문서는 webview 코드베이스에서 작업하는 AI 어시스턴트를 위한 종합 가이드입니다. 프로젝트 구조, 개발 워크플로우, 코딩 규칙 및 효과적인 기여를 위한 핵심 고려사항을 설명합니다.

### 중요 사항

**모든 대화와 문서는 한국어로 작성되어야 합니다.**

이 프로젝트에서 AI 어시스턴트와의 모든 커뮤니케이션은 한국어로 진행됩니다.

---

## 목차

1. [프로젝트 정보](#프로젝트-정보)
2. [코드베이스 구조](#코드베이스-구조)
3. [기술 스택](#기술-스택)
4. [개발 워크플로우](#개발-워크플로우)
5. [코딩 규칙](#코딩-규칙)
6. [테스팅 가이드라인](#테스팅-가이드라인)
7. [일반 작업](#일반-작업)
8. [AI 어시스턴트 모범 사례](#ai-어시스턴트-모범-사례)
9. [문제 해결](#문제-해결)

---

## 프로젝트 정보

### 목적

이 프로젝트는 **앱 내에서 오픈되는 웹페이지**를 개발하는 프로젝트입니다.

**주요 특징:**
- 모바일 앱에 임베디드되어 표시되는 웹뷰 페이지
- 경량화되고 빠른 로딩을 위한 최적화
- 앱과의 인터페이스를 고려한 설계

### 아키텍처 개요

**웹뷰 기반 페이지 시스템**

- **타입:** 정적 웹페이지 컬렉션
- **렌더링:** 앱 내 웹뷰 컴포넌트에서 표시
- **인터랙션:** Alpine.js를 사용한 경량 상호작용
- **배포:** 앱에서 로드 가능한 HTML/CSS/JS 번들

---

## 코드베이스 구조

### 디렉토리 구조

```
/
├── pages/            # 개별 웹뷰 페이지들
├── assets/           # 정적 리소스 (이미지, 폰트 등)
│   ├── css/         # 스타일시트
│   ├── js/          # JavaScript 파일
│   └── images/      # 이미지 파일
├── components/       # 재사용 가능한 컴포넌트
├── docs/            # 프로젝트 문서
└── CLAUDE.md        # AI 어시스턴트 가이드 (이 파일)
```

### 주요 파일

**페이지 파일:**
- 각 페이지는 독립적인 HTML 파일
- 앱의 특정 기능이나 화면에 대응

**설정 파일:**
- 추후 빌드 도구 추가 시 업데이트 예정

---

## 기술 스택

### 언어 및 프레임워크

**핵심 기술:**
- **HTML5** - 마크업 구조
- **CSS3** - 스타일링
- **Alpine.js** - 경량 JavaScript 프레임워크
  - 반응형 데이터 바인딩
  - 선언적 이벤트 핸들링
  - 작은 번들 사이즈로 웹뷰에 최적화

### 개발 도구

- **버전 관리:** Git
- **에디터:** 제한 없음
- **브라우저:** 모바일 웹뷰 환경을 고려
- **빌드 도구:** 추후 필요시 추가

---

## 개발 워크플로우

### 브랜치 전략

**현재 개발 브랜치:** `claude/claude-md-mhzu2wftxgweonxb-01SQehDVhGq8ggKWH385mMKa`

#### 브랜치 네이밍 규칙

- `main` 또는 `master` - 프로덕션 준비 코드
- `develop` - 기능 통합 브랜치
- `feature/*` - 기능 개발 브랜치
- `claude/*` - AI 어시스턴트 개발 브랜치
- `bugfix/*` - 버그 수정 브랜치
- `hotfix/*` - 긴급 프로덕션 수정

#### Git 워크플로우

1. **기능 브랜치 생성/전환**
   ```bash
   git checkout -b feature/기능명
   ```

2. **변경사항 커밋**
   ```bash
   git add .
   git commit -m "feat: 기능 설명"
   ```

3. **원격 저장소에 푸시**
   ```bash
   git push -u origin feature/기능명
   ```

4. **풀 리퀘스트 생성**
   - `gh pr create` 또는 웹 인터페이스 사용
   - 변경사항 설명 포함
   - 관련 이슈 참조

### 커밋 메시지 규칙

Conventional Commits 형식 준수:

```
<타입>(<범위>): <제목>

<본문>

<푸터>
```

**타입:**
- `feat`: 새로운 기능
- `fix`: 버그 수정
- `docs`: 문서 변경
- `style`: 코드 스타일 변경 (포맷팅 등)
- `refactor`: 코드 리팩토링
- `test`: 테스트 추가 또는 수정
- `chore`: 유지보수 작업
- `perf`: 성능 개선

**예시:**
```
feat(login): 로그인 페이지 추가
fix(button): 클릭 이벤트 오류 수정
docs(readme): 설치 방법 업데이트
```

---

## 코딩 규칙

### 일반 원칙

1. **코드 명확성:** 명확한 변수/함수명으로 자체 문서화된 코드 작성
2. **DRY 원칙:** 반복하지 않기 - 공통 로직 추출
3. **단순성 우선:** 복잡한 솔루션보다 단순한 해결책 선호
4. **에러 핸들링:** 항상 에러를 우아하게 처리
5. **보안 우선:** 일반적인 취약점 방지 (XSS 등)

### HTML 스타일 가이드

**들여쓰기:**
- 2칸 공백 사용
- 중첩된 요소는 들여쓰기

**네이밍:**
- 클래스명: `kebab-case` (예: `user-profile`)
- ID: `camelCase` (예: `loginButton`)

**구조:**
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>페이지 제목</title>
  <link rel="stylesheet" href="/assets/css/main.css">
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body>
  <!-- 콘텐츠 -->
</body>
</html>
```

### CSS 스타일 가이드

**들여쓰기:**
- 2칸 공백 사용

**네이밍:**
- BEM 방법론 권장 (Block__Element--Modifier)
- 예: `.user-card__title--large`

**구조:**
```css
/* 컴포넌트별로 섹션 구분 */
/* ========== Button Component ========== */
.btn {
  /* 기본 스타일 */
}

.btn--primary {
  /* 수정자 스타일 */
}
```

### Alpine.js 스타일 가이드

**디렉티브 사용:**
- `x-data`: 컴포넌트 데이터 정의
- `x-show`/`x-if`: 조건부 렌더링
- `x-for`: 리스트 렌더링
- `x-on` (또는 `@`): 이벤트 리스너
- `x-bind` (또는 `:`): 속성 바인딩

**예시:**
```html
<div x-data="{ open: false }">
  <button @click="open = !open">토글</button>
  <div x-show="open">
    내용
  </div>
</div>
```

**컴포넌트 구조:**
```html
<div x-data="componentName()">
  <!-- 템플릿 -->
</div>

<script>
function componentName() {
  return {
    // 데이터
    count: 0,

    // 메서드
    increment() {
      this.count++
    }
  }
}
</script>
```

### 코드 리뷰 체크리스트

코드 커밋 전 확인사항:

- [ ] 스타일 가이드라인 준수
- [ ] 보안 취약점 없음 (특히 XSS)
- [ ] 모바일 웹뷰 환경에서 테스트
- [ ] 파일 크기 최적화 (웹뷰 로딩 속도 고려)
- [ ] 문서 업데이트
- [ ] 주석 처리된 코드나 디버그 구문 제거
- [ ] 하드코딩된 자격증명이나 비밀키 없음
- [ ] 한국어 주석 및 문자열 사용

---

## 테스팅 가이드라인

### 테스트 전략

**수동 테스트:**
- 실제 모바일 디바이스에서 테스트
- 다양한 화면 크기 확인
- 앱 웹뷰 환경에서 동작 확인

**크로스 브라우저 테스트:**
- iOS Safari (WKWebView)
- Android Chrome (WebView)

**성능 테스트:**
- 페이지 로딩 시간
- JavaScript 번들 크기
- 리소스 최적화

### 테스트 체크리스트

- [ ] 모바일 반응형 디자인 확인
- [ ] 터치 이벤트 정상 동작
- [ ] 앱과의 인터페이스 정상 동작
- [ ] 느린 네트워크에서 로딩 테스트
- [ ] 메모리 누수 확인

---

## 일반 작업

### 개발 환경 설정

```bash
# 1. 저장소 클론
git clone <repository-url>
cd webview

# 2. 로컬 서버 실행 (선택사항)
# Python 3
python -m http.server 8000

# 또는 Node.js http-server
npx http-server

# 3. 브라우저에서 접속
# http://localhost:8000
```

### 새 페이지 생성

1. `pages/` 디렉토리에 새 HTML 파일 생성
2. 템플릿 구조 작성
3. Alpine.js 컴포넌트 추가
4. 스타일 작성
5. 앱에서 테스트

### 디버깅

**모바일 디버깅:**

**iOS:**
- Safari > 개발자 > [디바이스명] > [페이지명]
- Web Inspector 사용

**Android:**
- Chrome > chrome://inspect
- DevTools 사용

**일반 디버깅:**
- `console.log()` 사용
- Alpine.js DevTools (크롬 확장 프로그램)
- 브라우저 개발자 도구

---

## AI 어시스턴트 모범 사례

### 컨텍스트 이해

이 코드베이스에서 작업할 때:

1. **먼저 읽기:** 편집 전 항상 Read 도구로 파일 확인
2. **전략적 검색:** Grep/Glob으로 관련 코드 찾기
3. **의존성 이해:** 컴포넌트 간 상호작용 확인
4. **최근 변경사항 검토:** Git 히스토리로 컨텍스트 파악

### 변경사항 작성

1. **최소한의 변경:** 집중적이고 최소한의 변경사항 작성
2. **스타일 유지:** 기존 코드 스타일과 패턴 일치
3. **철저한 테스트:** 변경사항이 기능을 망가뜨리지 않는지 확인
4. **의도 문서화:** 명확한 커밋 메시지 사용

### 커뮤니케이션

1. **명시적으로:** 어떤 변경사항을 만드는지 명확히 설명
2. **이유 설명:** 왜 변경이 필요한지 설명
3. **위험 강조:** 잠재적 이슈나 부작용 지적
4. **불확실할 때 질문:** 요구사항이 불명확하면 명확히 요청
5. **한국어 사용:** 모든 커뮤니케이션은 한국어로

### 웹뷰 특화 고려사항

**성능:**
- 이미지 최적화 (WebP, 압축)
- CSS/JS 파일 최소화
- 불필요한 라이브러리 제거
- Alpine.js의 경량성 활용

**호환성:**
- 모바일 웹뷰 API 제한 고려
- iOS/Android 웹뷰 차이점 인지
- Polyfill 필요성 검토

**사용자 경험:**
- 터치 친화적 UI (최소 44px 터치 타겟)
- 빠른 로딩 (스켈레톤 스크린 활용)
- 오프라인 동작 고려

### 보안 고려사항

**웹뷰 환경에서 특히 중요:**

- **XSS 방지:** 사용자 입력 항상 이스케이프
- **민감 데이터:** 로컬 스토리지에 민감 정보 저장 금지
- **비밀키:** 절대 커밋하지 않음
- **HTTPS:** 모든 외부 리소스는 HTTPS로 로드
- **CSP:** Content Security Policy 고려
- **입력 검증:** 모든 사용자 입력 검증

---

## 문제 해결

### 일반적인 이슈

#### 이슈 1: Alpine.js 작동 안 함

**증상:** x-data, x-show 등 디렉티브가 작동하지 않음

**원인:**
- Alpine.js 스크립트 로드 실패
- 스크립트 로드 순서 문제
- 문법 오류

**해결방법:**
```html
<!-- defer 속성 추가 확인 -->
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

<!-- 또는 로컬 파일 사용 -->
<script defer src="/assets/js/alpine.min.js"></script>
```

#### 이슈 2: 모바일에서 클릭 이벤트 느림

**증상:** 버튼 클릭 시 300ms 지연

**원인:** 모바일 브라우저의 더블 탭 줌 감지

**해결방법:**
```html
<!-- viewport meta 태그에 추가 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
```

```css
/* 또는 CSS로 해결 */
button {
  touch-action: manipulation;
}
```

#### 이슈 3: 한글 깨짐

**증상:** 한글이 깨져서 표시됨

**원인:** 문자 인코딩 문제

**해결방법:**
```html
<!-- HTML 파일 상단에 UTF-8 선언 -->
<meta charset="UTF-8">
```

파일 저장 시 UTF-8 인코딩으로 저장

### 도움 받기

- **문서:** README.md 및 docs/ 확인
- **이슈 트래커:** 기존 이슈 검색
- **로그:** 브라우저 콘솔 로그 확인
- **커뮤니티:** 팀 멤버에게 문의

---

## 유지보수

### 이 문서 업데이트

**업데이트가 필요한 경우:**

- 프로젝트 구조 변경
- 새로운 규칙 도입
- 기술 추가/변경
- 일반적인 이슈 발견
- 개발 워크플로우 진화

**업데이트 프로세스:**

1. CLAUDE.md 변경
2. 상단의 "최종 업데이트" 날짜 갱신
3. 커밋 메시지: `docs(claude): AI 어시스턴트 가이드 업데이트`
4. 모든 팀원과 AI 어시스턴트에게 공지

### 버전 히스토리

| 날짜       | 변경사항                          | 작성자    |
|------------|-----------------------------------|-----------|
| 2025-11-15 | Alpine.js 웹뷰 프로젝트로 업데이트 | Claude AI |
| 2025-11-15 | 초기 템플릿 생성                   | Claude AI |

---

## 빠른 참조

### 필수 명령어

```bash
# 로컬 서버 실행
python -m http.server 8000
# 또는
npx http-server

# Git 작업
git status
git add .
git commit -m "feat: 기능명"
git push -u origin 브랜치명
```

### 중요 경로

- HTML 페이지: `pages/`
- 스타일시트: `assets/css/`
- JavaScript: `assets/js/`
- 이미지: `assets/images/`
- 문서: `docs/`

### 핵심 리소스

**Alpine.js:**
- [공식 문서](https://alpinejs.dev/)
- [Alpine.js 한국어 가이드](https://alpinejs.dev/)

**웹뷰 최적화:**
- 이미지: WebP 포맷 사용
- 스크립트: defer 또는 async 사용
- 스타일: 인라인 크리티컬 CSS

---

## 부록

### 용어집

- **웹뷰 (WebView):** 앱 내에서 웹 콘텐츠를 표시하는 컴포넌트
- **Alpine.js:** 경량 JavaScript 프레임워크
- **반응형 (Reactive):** 데이터 변경 시 자동으로 UI 업데이트
- **디렉티브 (Directive):** Alpine.js에서 `x-`로 시작하는 HTML 속성

### 외부 리소스

- [Alpine.js 공식 문서](https://alpinejs.dev/)
- [MDN Web Docs (한국어)](https://developer.mozilla.org/ko/)
- [웹뷰 모범 사례](https://developer.android.com/guide/webapps/best-practices)

---

**AI 어시스턴트 참고사항:**

이 문서는 살아있는 가이드입니다. 코드베이스 작업 중 누락되거나 오래된 정보를 발견하면 업데이트를 제안하여 문서를 최신 상태로 유지하세요.

**중요:** 모든 작업과 커뮤니케이션은 반드시 한국어로 진행하세요.
