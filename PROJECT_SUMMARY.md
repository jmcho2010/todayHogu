# 오늘의 호구 : 1초 내기 - 프로젝트 요약

## 📋 프로젝트 개요

**프로젝트명**: 오늘의 호구 : 1초 내기 (Today's Loser: 1 Second Bet)  
**회사**: (주)옐로우독 소프트 (Yellow Dog Soft)  
**개발자**: 대왕누렁이  
**배포 환경**: Vercel  
**라이브 URL**: https://today-hogu.vercel.app/  
**GitHub 저장소**: https://github.com/jmcho2010/todayHogu

---

## 🎮 게임 설명

사용자가 정확히 1초(또는 3초, 5초)를 맞추는 시간 감각 게임입니다.

### 게임 규칙
- **목표**: 시작 버튼을 누른 후 정지 버튼을 눌러 정확히 목표 시간을 맞추기
- **평가 기준**:
  - 완벽 (Perfect): 정확히 목표 시간
  - 거의 다 옴 (Near Miss): 0.01초 이내 오차
  - 실패 (Fail): 그 외
- **저장**: 모드별 최고 기록이 localStorage에 자동 저장됨

### 게임 모드
- **1초 모드**: 가장 기본적인 모드
- **3초 모드**: 중간 난이도
- **5초 모드**: 높은 난이도

---

## 🛠 기술 스택

### 핵심 기술
- **HTML5**: 마크업 구조
- **Vanilla JavaScript (ES6+)**: 게임 로직, 상태 관리, 애니메이션
- **Tailwind CSS**: 반응형 디자인 (CDN 방식)
- **CSS Animations**: 캐릭터 부동, 흔들림, 컨페티 효과

### 주요 라이브러리
- **Google Fonts**: 
  - Noto Sans KR (900 weight) - 제목
  - Jua - 부제목
  - Roboto Mono - 타이머
- **Canvas API**: 컨페티 입자 시스템

### API 활용
- `performance.now()`: 마이크로초 단위 정밀 타이밍
- `requestAnimationFrame`: 부드러운 애니메이션
- `navigator.vibrate()`: 햅틱 피드백
- `navigator.share()`: 소셜 공유 (+ 클립보드 폴백)
- `localStorage`: 데이터 영구 저장

---

## 📱 주요 기능

### 1. 정밀한 타이밍 시스템
- `performance.now()` 기반 마이크로초 단위 측정
- 0.0001초 단위 표시 (예: ?.????)

### 2. 상태 관리 (State Machine)
```
IDLE → RUNNING → RESULT → IDLE
```
- IDLE: 시작 대기
- RUNNING: 게임 진행 중
- RESULT: 결과 표시

### 3. 모드별 멘트 (존댓말)
#### IDLE (초기 상태)
- 1초: "흠... 1초면 쉽지 않나요?"
- 3초: "3초? 할 만한데요?"
- 5초: "5초라니, 너무 길지 않나요?"

#### SUCCESS (완벽)
- 1초: "오호! 이것도 맞추셨어요?" / 캐릭터: "어... 정말이네요?"
- 3초: "오호! 정말 할 만 하네요?" / 캐릭터: "어? 정말이네요."
- 5초: "오호! 5초를 정확히요?" / 캐릭터: "오... 5초를요?"

#### NEAR_MISS (거의 다 옴)
- 1초: "아까워요." / 캐릭터: "아이고... 아까워요."
- 3초: "어라? {시간}초네요." / 캐릭터: "아, 아까워요."
- 5초: "어? {시간}초네요." / 캐릭터: "거의였는데요..."

#### FAIL (실패)
- 1초: "에라 모르겠어요." / 캐릭터: "역시... 어렵네요."
- 3초: "아뇨. {시간}초네요." / 캐릭터: "3초는... 힘들지요?"
- 5초: "5초는 아니네요." / 캐릭터: "5초는 어려운가봐요."

### 4. 애니메이션
- **캐릭터 부동 (Float)**: 3초 루프
- **흔들림 (Shake)**: 실패 시 0.4초 진동
- **컨페티 (Confetti)**: 성공 시 2.5초 낙하 입자 100개

### 5. 반응형 디자인
- 모바일 우선 설계 (Mobile-first)
- 한 화면에 완벽하게 맞춤
- Tailwind 반응형 클래스 (sm:, md: 등)

### 6. 데이터 저장
```javascript
STORAGE_KEY = 'today_hogu_best'
{
  duration: 1.0000,  // 측정 시간
  diff: 0.0000,      // 오차
  mode: 1,           // 게임 모드 (1/3/5)
  iso: "2026-02-04T12:00:00.000Z"  // ISO 타임스탬프
}
```

---

## 🎨 디자인 시스템

### 색상 팔레트
```css
--primary-blue: #3182F6      /* Toss 파란색 */
--primary-black: #1a1a1a     /* 검정 */
--primary-white: #FFFFFF     /* 흰색 */
--bg-light: #F5F5F5          /* 배경 */
--text-dark: #191F28         /* 어두운 텍스트 */
--text-muted: #6B7684        /* 뮤트 텍스트 */
```

### 캐릭터 (SVG 개)
- **신체**: #D4A574 (갈색)
- **테두리**: #8B6F47 (어두운 갈색)
- **크기**: 120×120px (100×100 SVG)
- **구성**: 머리, 몸, 귀, 코, 눈, 입, 발, 꼬리

### 버튼 스타일
- **Primary**: 파란색 그래디언트 (누를 시 아래로 움직임)
- **Secondary**: 흰색 + 파란색 테두리

### 타이포그래피
- **제목 (h1)**: Noto Sans KR 900, 4xl~5xl
- **부제목**: Jua, xl~2xl
- **본문**: Noto Sans KR 400, sm~base
- **타이머**: Roboto Mono, 3xl~5xl

---

## 📂 파일 구조

```
timer/
├── index.html              # 메인 파일 (775줄, 모든 코드 포함)
├── index.backup.html       # MVP 백업 (초기 버전)
├── PROJECT_SUMMARY.md      # 이 파일
└── .git/                   # Git 저장소
```

### index.html 내부 구조
```html
<head>
  - 메타 태그
  - Google Fonts 로드
  - Tailwind CSS CDN
  - 커스텀 CSS (:root 변수, 애니메이션, 컴포넌트 스타일)
</head>
<body>
  - Canvas (컨페티)
  - 앱 컨테이너
    - 헤더 (제목, 부제목, 설명)
    - 카드
      - 최고 기록
      - 모드 선택 (세그먼트 컨트롤)
      - 캐릭터 (SVG)
      - 캐릭터 메시지
      - 타이머 디스플레이
      - 상태 메시지
      - 결과 섹션
      - 액션 버튼 (시작/정지/다시하기)
      - 공유 버튼
      - 광고 영역
    - 푸터
  - 스크립트 (게임 로직)
</body>
```

---

## 🚀 배포 및 운영

### Git 저장소 구조
```bash
remote: jmcho2010/todayHogu
branch: main

주요 커밋 히스토리:
1. Initial commit: Catch 1.0000s game (MVP)
2. Redesign: Premium mobile game UI (Phase 3)
3. Fix: 3초/5초 모드 버튼 동작 복구
4. Feat: 모드별 멘트 추가
5. Fix: 존댓말로 변경, 개발자명 변경
6. Design: 폰트 변경 (가독성 + 임팩트)
7. Design: 제목 영역 간격 및 텍스트 개선
```

### 배포 방식
- **Vercel 연동 배포**: GitHub 푸시 → 자동 빌드 및 배포
- **라이브 URL**: https://today-hogu.vercel.app/
- **배포 시간**: 1-2분

### 배포 명령어
```bash
git add index.html
git commit -m "메시지"
git push origin main
# Vercel 자동 배포 시작
```

---

## 🔧 개발 워크플로우

### 로컬 개발 환경
1. VS Code에서 `index.html` 편집
2. 브라우저에서 파일 열기 (또는 Live Server 확장 사용)
3. 변경사항 실시간 확인

### 기능 추가/수정 체크리스트
```
[ ] 기능 구현/수정 (index.html)
[ ] 로컬 테스트
[ ] git add index.html
[ ] git commit -m "명확한 메시지"
[ ] git push origin main
[ ] Vercel 배포 확인 (1-2분)
[ ] 라이브 환경 테스트
```

---

## 📊 개발 이력

### Phase 1: MVP (초기 개발)
- 기본 타이머 게임 구현
- Toss 디자인 시스템 적용
- localStorage 저장
- 암막 모드, 햅틱 피드백
- 컨페티 애니메이션

### Phase 2: Git & 배포
- GitHub 저장소 생성
- Vercel 배포 설정
- 라이브 환경 오픈

### Phase 3: Premium 리디자인
- 카드 기반 UI
- 캐릭터 (개) 추가
- 3D 버튼 효과
- 상황별 메시지
- 세그먼트 컨트롤 (1초/3초/5초)

### Phase 4: UI 폴리싱
- 타이포그래피 개선
- 다크모드 지원
- 푸터 추가 (회사 정보)

### Phase 5: 톤 & 컬러 리파인
- 폐손한 멘트 → 존댓말 (폐손함 유지)
- 색상: Yellow (#FFD700) → Blue (#3182F6) (Toss 색)
- 커스텀 SVG 개 아이콘 추가
- 모드별 멘트 세분화
- 개발자명: 조준모 → 대왕누렁이

### Phase 6: 레이아웃 및 폰트 최적화
- Black Han Sans → Noto Sans KR 900 (가독성)
- 제목 영역 간격 확대
- 텍스트 자연스럽게 (AI 티 제거)
- 모바일 한 화면 맞춤 완성

---

## 💡 주요 개선사항

### 기술적 개선
| 항목 | Before | After | 이유 |
|------|--------|-------|------|
| 폰트 | Black Han Sans | Noto Sans KR 900 | 가독성 + 임팩트 |
| 색상 | Yellow (#FFD700) | Blue (#3182F6) | Toss 브랜드 일관성 |
| 캐릭터 | Emoji (🐶) | Custom SVG | 커스터마이징 가능 |
| 톤 | 반말/중립 | 존댓말/폐손 | 사용자 심리 분석 |
| 간격 | 붙어있음 | 여유있음 | UX 호흡감 |

### 사용자 경험 개선
- 더 명확한 게임 피드백
- 모드별 맞춤 메시지
- 시각적 임팩트 강화 (컨페티, 애니메이션)
- 정확한 시간 측정 (마이크로초)
- 한 화면에 모든 콘텐츠 (스크롤 불필요)

---

## 🎯 주요 기술 포인트

### 1. 정밀한 타이밍 구현
```javascript
function loop() {
  const now = performance.now();
  const duration = (now - startTime) / 1000;  // 밀리초 → 초
  timerDisplay.textContent = duration.toFixed(4);  // 0.0001초 단위
  rafId = requestAnimationFrame(loop);
}
```

### 2. State Machine 패턴
```javascript
const stateEnum = { IDLE, RUNNING, RESULT };
function setState(nextState) {
  appState = nextState;
  renderState();  // 상태별 UI 업데이트
}
```

### 3. 모드별 동적 메시지
```javascript
if (targetSeconds === 1) {
  characterMessage.textContent = '흠... 1초면 쉽지 않나요?';
} else if (targetSeconds === 3) {
  characterMessage.textContent = '3초? 할 만한데요?';
}
// 5초도 마찬가지
```

### 4. Canvas 기반 컨페티
```javascript
function launchConfetti() {
  const particles = [];
  for (let i = 0; i < 100; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: -20,
      color: colors[Math.floor(Math.random() * colors.length)]
    });
  }
  // 2.5초 동안 낙하 애니메이션
}
```

### 5. localStorage 기반 데이터 지속성
```javascript
const STORAGE_KEY = 'today_hogu_best';
function saveBest(best) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(best));
}
function loadBest() {
  const raw = localStorage.getItem(STORAGE_KEY);
  return raw ? JSON.parse(raw) : null;
}
```

---

## 🔍 성능 최적화

### 1. CSS-in-JS 최소화
- Tailwind CDN 사용 (빌드 불필요)
- 인라인 스타일 최소화
- CSS 애니메이션 (JavaScript 애니메이션보다 빠름)

### 2. 렌더링 최적화
- `requestAnimationFrame` 활용 (60fps 보장)
- 불필요한 리페인트 방지
- Canvas 레이어 분리 (컨페티는 별도)

### 3. 번들 크기
- 단일 HTML 파일 (~30KB)
- 외부 의존성 최소화
- CDN 기반 라이브러리 (Tailwind, Google Fonts)

---

## 🛡️ 브라우저 호환성

- **iOS Safari**: ✅ (vibrate, share API 지원)
- **Chrome**: ✅ (모든 API 지원)
- **Firefox**: ✅ (모든 API 지원)
- **Edge**: ✅ (모든 API 지원)

### 주의사항
- `navigator.vibrate()`: iOS 13+에서 지원
- `navigator.share()`: HTTPS 환경에서만 작동
- localStorage: 프라이빗 모드에서 제한될 수 있음

---

## 📝 다른 환경에서 사용하기

### 1. 로컬 개발
```bash
# 파일 다운로드
wget https://github.com/jmcho2010/todayHogu/raw/main/index.html

# 브라우저에서 열기
open index.html  # macOS
start index.html  # Windows
firefox index.html  # Linux
```

### 2. 다른 호스팅 플랫폼에서 배포
```bash
# Netlify
netlify deploy --prod --dir .

# GitHub Pages
git push origin main  # gh-pages 브랜치로 설정

# Firebase Hosting
firebase deploy

# AWS S3 + CloudFront
aws s3 cp index.html s3://your-bucket/
```

### 3. 커스터마이징 가이드
```javascript
// 색상 변경
--primary-blue: #YOUR_COLOR;

// 회사명 변경 (footer)
(주)옐로우독 소프트 → 당신의 회사명

// 캐릭터 이름 변경
"대왕누렁이" → 당신의 이름

// 게임 모드 추가
targetSeconds = [1, 3, 5, 10]; // 10초 추가
```

---

## 📞 문의 및 지원

**이메일**: help@yellowdog.soft  
**GitHub**: https://github.com/jmcho2010/todayHogu  
**라이브**: https://today-hogu.vercel.app/

---

## 📄 라이선스

이 프로젝트는 Yellow Dog Soft에서 개발했습니다.

---

**문서 작성일**: 2026년 2월 4일  
**마지막 업데이트**: Phase 6 완료
