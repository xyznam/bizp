# BizPlanet PC Web UI 가이드
> 소호 사장님용 PC 웹 서비스 공통 적용 기준
> Noto Sans KR 단일 폰트 체계 / 다크 사이드바

---

## 1. 색상 토큰

```css
:root {
  /* 배경 */
  --bg:        #F5F6FA;   /* 페이지 배경 */
  --surface:   #FFFFFF;   /* 카드, 테이블, 입력창 */
  --surface2:  #F7F8FA;   /* 테이블 헤더, hover, 비활성 영역 */

  /* 텍스트 */
  --text:      #1A1A2E;   /* 본문 기본 */
  --text2:     #4A5568;   /* 보조 텍스트 */
  --text3:     #9AA0B4;   /* 플레이스홀더, 레이블, 비활성 */

  /* 테두리 */
  --border:    #E2E8F0;   /* 기본 테두리 */
  --border2:   #EDF2F7;   /* 테이블 행 구분선 */

  /* 액션 컬러 */
  --blue:      #3B5BDB;   /* 주요 액션, 링크, 활성 상태 */
  --blue-l:    #EEF2FF;   /* blue 배경 (배지, 하이라이트) */
  --blue-d:    #2C46C3;   /* blue hover */

  --green:     #2F9E44;   /* 성공, 정상, 완료 */
  --green-l:   #EBFBEE;

  --orange:    #E8590C;   /* 경고, 승인대기, 처리필요 */
  --orange-l:  #FFF4E6;

  --red:       #C92A2A;   /* 오류, 실패, 반려 */
  --red-l:     #FFF5F5;

  --yellow:    #F08C00;   /* 주의, 정지 */
  --yellow-l:  #FFF9DB;

  /* 사이드바 전용 */
  --sb-bg:         #0F1420;              /* 사이드바 배경 */
  --sb-text:       rgba(255,255,255,0.5); /* 비활성 메뉴 텍스트 */
  --sb-text-active:#FFFFFF;              /* 활성 메뉴 텍스트 */
  --sb-active-bg:  rgba(59,91,219,0.15); /* 활성 메뉴 배경 */
  --sb-section:    rgba(255,255,255,0.25);/* 섹션 레이블 */
}
```

### 서비스별 색상 매핑
| 서비스 | 주색 | 배지 배경 |
|---|---|---|
| 마케팅 채널관리 | `#3B5BDB` | `#EEF2FF` |
| 비즈챗 | `#2F9E44` | `#EBFBEE` |
| AI 챗봇 | `#6B3FD4` | `#F0EBFE` |

---

## 2. 타이포그래피

> **폰트 단일 체계**: Noto Sans KR 하나만 사용 (Georgia 사용 안 함)

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600;700&display=swap" rel="stylesheet">
```

| 용도 | 굵기 | 크기 |
|---|---|---|
| 페이지 제목 | 700 | 18px |
| 카드/섹션 제목 | 700 | 13px |
| 테이블 헤더 | 700 | 11px |
| 테이블 본문 | 400 | 12px |
| 배지 | 600 | 11px |
| 보조/메타 텍스트 | 400 | 11px |
| KPI 숫자 | 700 | 22px |
| 버튼 | 600 | 12px |
| 섹션 레이블 (uppercase) | 700 | 10px |

---

## 3. 레이아웃

```
┌─────────────────────────────────────────────────────────┐
│  사이드바 (200px, 고정, 다크)  │  Topbar (50px, 고정)   │
│                               │─────────────────────────│
│  좌측 네비게이션               │  Main 콘텐츠            │
│  배경: #0F1420                │  배경: #F5F6FA          │
│                               │  패딩: 24px             │
└─────────────────────────────────────────────────────────┘
```

- 사이드바 너비: `200px` 고정, `position: fixed`, `height: 100vh`
- Topbar 높이: `50px`, 배경 `#FFFFFF`, 하단 border `1px solid #E2E8F0`
- 콘텐츠 영역: `margin-left: 200px`, `padding: 24px`, `background: #F5F6FA`

---

## 4. 사이드바

```css
.sidebar {
  width: 200px;
  background: #0F1420;
  border-right: none;
  position: fixed;
  height: 100vh;
  overflow-y: auto;
}

/* 로고 */
.sb-logo {
  padding: 18px 18px 14px;
  font-size: 16px;
  font-weight: 700;
  color: #FFFFFF;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}
.sb-logo em { color: #6B8FFF; font-style: normal; }

/* 섹션 레이블 */
.sb-section {
  padding: 16px 18px 4px;
  font-size: 10px;
  font-weight: 700;
  color: rgba(255,255,255,0.25);
  text-transform: uppercase;
  letter-spacing: .6px;
}

/* 메뉴 아이템 */
.sb-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 18px;
  font-size: 12px;
  color: rgba(255,255,255,0.5);
  border-left: 2px solid transparent;
  cursor: pointer;
  text-decoration: none;
}
.sb-item:hover {
  background: rgba(255,255,255,0.05);
  color: rgba(255,255,255,0.8);
}
.sb-item.active {
  background: rgba(59,91,219,0.2);
  color: #FFFFFF;
  font-weight: 600;
  border-left-color: #3B5BDB;
}

/* 하위 메뉴 */
.sb-sub {
  padding-left: 34px;
  font-size: 11px;
}
.sb-sub.active {
  background: rgba(59,91,219,0.15);
  color: #FFFFFF;
  font-weight: 600;
  border-left-color: #3B5BDB;
}

/* 하단 사용자 정보 */
.sb-footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 14px 18px;
  border-top: 1px solid rgba(255,255,255,0.08);
  font-size: 11px;
  color: rgba(255,255,255,0.4);
}
```

---

## 5. Topbar

```css
.topbar {
  position: fixed;
  top: 0;
  left: 200px;
  right: 0;
  height: 50px;
  background: #FFFFFF;
  border-bottom: 1px solid #E2E8F0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
  z-index: 100;
}
.topbar-left {
  font-size: 12px;
  color: #9AA0B4;  /* breadcrumb */
}
.topbar-right {
  display: flex;
  align-items: center;
  gap: 10px;
}
```

---

## 6. 컴포넌트

### 버튼

```css
.btn {
  height: 32px;
  padding: 0 14px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  border: none;
}
.btn-sm { height: 28px; padding: 0 10px; font-size: 11px; }

/* Primary */
.btn-primary { background: #3B5BDB; color: #FFFFFF; }
.btn-primary:hover { background: #2C46C3; }

/* Ghost */
.btn-ghost { background: #FFFFFF; color: #4A5568; border: 1px solid #E2E8F0; }
.btn-ghost:hover { background: #F7F8FA; }

/* Danger */
.btn-danger { background: #FFF5F5; color: #C92A2A; border: 1px solid #FFC9C9; }
.btn-danger:hover { background: #FFE8E8; }
```

---

### 배지

```css
.badge {
  padding: 2px 8px;
  border-radius: 12px;
  font-size: 11px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  white-space: nowrap;
}

.b-green  { background: #EBFBEE; color: #2F9E44; }  /* 완료, 정상, 발행완료 */
.b-blue   { background: #EEF2FF; color: #3B5BDB; }  /* AI 자동, 진행중 */
.b-orange { background: #FFF4E6; color: #E8590C; }  /* 승인대기, 처리필요 */
.b-red    { background: #FFF5F5; color: #C92A2A; }  /* 오류, 실패 */
.b-yellow { background: #FFF9DB; color: #F08C00; }  /* 주의, 발행예약 */
.b-gray   { background: #F1F3F5; color: #868E96; border: 1px solid #E2E8F0; } /* 비활성, 취소, 직접등록 */
```

---

### 입력 요소

```css
input, select, textarea {
  height: 32px;
  padding: 0 10px;
  border: 1px solid #E2E8F0;
  border-radius: 6px;
  font-size: 12px;
  font-family: 'Noto Sans KR', sans-serif;
  background: #FFFFFF;
  color: #1A1A2E;
}
input:focus, select:focus {
  outline: none;
  border-color: #3B5BDB;
  box-shadow: 0 0 0 3px rgba(59,91,219,0.1);
}
textarea { height: auto; padding: 8px 10px; resize: vertical; }
```

---

### 필터 바

```css
.filter-bar {
  background: #FFFFFF;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  padding: 12px 16px;
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 16px;
}
.f-label {
  font-size: 11px;
  font-weight: 700;
  color: #9AA0B4;
}
```

---

### 테이블

```css
.tbl-wrap {
  background: #FFFFFF;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  overflow: hidden;
}
thead tr { background: #F7F8FA; }
th {
  padding: 10px 12px;
  font-size: 11px;
  font-weight: 700;
  color: #9AA0B4;
  border-bottom: 1px solid #E2E8F0;
  text-align: left;
  white-space: nowrap;
}
td {
  padding: 11px 12px;
  font-size: 12px;
  color: #1A1A2E;
  border-bottom: 1px solid #EDF2F7;
  vertical-align: middle;
}
tbody tr:hover { background: #F7F8FA; cursor: pointer; }
tbody tr:last-child td { border-bottom: none; }

/* 클릭 가능한 텍스트 */
.td-link { color: #3B5BDB; font-weight: 500; }
/* 비활성/없음 값 */
.td-empty { color: #9AA0B4; }
/* 오류 행 강조 */
tbody tr.row-error { background: #FFF5F5; }
tbody tr.row-warn  { background: #FFF9DB; }
```

---

### KPI 카드

```css
.kpi-card {
  background: #FFFFFF;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  padding: 14px 16px;
}
.kpi-label { font-size: 11px; color: #9AA0B4; margin-bottom: 4px; }
.kpi-val   { font-size: 22px; font-weight: 700; color: #1A1A2E; }
.kpi-sub   { font-size: 11px; color: #9AA0B4; margin-top: 4px; }
.kpi-sub.up   { color: #2F9E44; }
.kpi-sub.down { color: #C92A2A; }

/* 액션 필요 강조 */
.kpi-card.alert {
  border-color: #FFA94D;
  background: #FFF9F0;
}
.kpi-card.alert .kpi-label,
.kpi-card.alert .kpi-val { color: #E8590C; }
```

---

### 폼 섹션

```css
.form-section {
  background: #FFFFFF;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 16px;
}
.form-section-title {
  padding: 12px 16px;
  border-bottom: 1px solid #E2E8F0;
  font-size: 13px;
  font-weight: 700;
  color: #1A1A2E;
  background: #F7F8FA;
}
.form-body    { padding: 16px; }
.form-actions {
  padding: 12px 16px;
  border-top: 1px solid #E2E8F0;
  background: #F7F8FA;
  display: flex;
  justify-content: flex-end;
  gap: 8px;
}
.form-row {
  display: flex;
  gap: 8px;
  align-items: flex-start;
  margin-bottom: 12px;
}
.form-row:last-child { margin-bottom: 0; }
.form-label {
  font-size: 11px;
  font-weight: 700;
  color: #4A5568;
  min-width: 80px;
  padding-top: 8px;
}
.form-label.req::after { content: '*'; color: #C92A2A; margin-left: 2px; }
.form-hint { font-size: 11px; color: #9AA0B4; margin-top: 4px; }
```

---

### 탭

```css
.tab-row {
  display: flex;
  border-bottom: 1px solid #E2E8F0;
  margin-bottom: 16px;
  background: #FFFFFF;
}
.tab-item {
  padding: 10px 16px;
  font-size: 13px;
  color: #9AA0B4;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  font-weight: 400;
}
.tab-item:hover { color: #4A5568; }
.tab-item.active {
  color: #3B5BDB;
  font-weight: 600;
  border-bottom-color: #3B5BDB;
}

/* 카운트 뱃지 (탭 내) */
.tab-count {
  font-size: 11px;
  color: #9AA0B4;
  margin-left: 4px;
}
.tab-item.active .tab-count { color: #3B5BDB; }
```

---

### 모달

```css
.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(15,20,32,0.45);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}
.modal {
  background: #FFFFFF;
  border-radius: 10px;
  padding: 24px;
  width: 400px;
  max-width: calc(100vw - 48px);
  box-shadow: 0 4px 16px rgba(40,50,100,0.12);
}
.modal-title {
  font-size: 15px;
  font-weight: 700;
  color: #1A1A2E;
  margin: 0 0 8px;
}
.modal-desc {
  font-size: 13px;
  color: #4A5568;
  margin: 0 0 20px;
  line-height: 1.6;
}
.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 8px;
}

/* 소형 확인 모달 */
.modal.modal-sm { width: 320px; }

/* 입력 포함 모달 */
.modal-field { margin-bottom: 16px; }
.modal-field label {
  display: block;
  font-size: 11px;
  font-weight: 700;
  color: #4A5568;
  margin-bottom: 6px;
}
```

---

### 진행 상태 (수집/학습 중)

```css
/* 진행 카드 */
.progress-card {
  background: #F7F8FA;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
}
.progress-title {
  font-size: 13px;
  font-weight: 700;
  color: #1A1A2E;
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 12px;
}
.progress-meta {
  font-size: 11px;
  color: #9AA0B4;
  font-weight: 400;
  margin-left: auto;
}

/* 스피너 */
.spinner {
  width: 14px;
  height: 14px;
  border: 2px solid #E2E8F0;
  border-top-color: #3B5BDB;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
  flex-shrink: 0;
}
@keyframes spin { to { transform: rotate(360deg); } }

/* 채널별 진행 행 */
.prog-ch-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 12px;
  padding: 7px 10px;
  border-radius: 6px;
  background: #FFFFFF;
  margin-bottom: 6px;
  border: 1px solid #E2E8F0;
}
.prog-ch-row:last-child { margin-bottom: 0; }
.prog-ch-name {
  display: flex;
  align-items: center;
  gap: 6px;
  color: #1A1A2E;
}

/* 상태 텍스트 */
.s-done { font-size: 11px; color: #2F9E44; display: flex; align-items: center; gap: 4px; }
.s-ing  { font-size: 11px; color: #3B5BDB; display: flex; align-items: center; gap: 4px; }
.s-wait { font-size: 11px; color: #9AA0B4; }
```

---

### 빈 상태 (Empty State)

```css
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 24px;
  text-align: center;
  background: #FFFFFF;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
}
.empty-icon {
  width: 48px;
  height: 48px;
  background: #EEF2FF;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 16px;
}
.empty-title {
  font-size: 14px;
  font-weight: 700;
  color: #1A1A2E;
  margin: 0 0 6px;
}
.empty-desc {
  font-size: 13px;
  color: #9AA0B4;
  margin: 0 0 20px;
  line-height: 1.6;
  max-width: 280px;
}
```

---

### 오류 배너

```css
.err-banner {
  border-radius: 8px;
  padding: 14px 16px;
  margin-bottom: 16px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.err-banner.danger {
  background: #FFF5F5;
  border: 1px solid #FFC9C9;
}
.err-banner.warning {
  background: #FFF9DB;
  border: 1px solid #FFD43B;
}
.err-title {
  font-size: 13px;
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 6px;
}
.err-banner.danger .err-title { color: #C92A2A; }
.err-banner.warning .err-title { color: #F08C00; }
.err-desc {
  font-size: 12px;
  line-height: 1.6;
  margin: 0;
}
.err-banner.danger .err-desc { color: #C92A2A; opacity: 0.85; }
.err-banner.warning .err-desc { color: #F08C00; opacity: 0.85; }
```

---

### 페이지네이션

```css
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  margin-top: 16px;
}
.pg-btn {
  width: 28px;
  height: 28px;
  border: 1px solid #E2E8F0;
  border-radius: 5px;
  font-size: 12px;
  background: #FFFFFF;
  color: #4A5568;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}
.pg-btn:hover { background: #F7F8FA; }
.pg-btn.active {
  background: #3B5BDB;
  color: #FFFFFF;
  border-color: #3B5BDB;
  font-weight: 700;
}
.pg-btn.disabled { opacity: 0.4; cursor: default; }
```

---

### 키워드 태그 입력

```css
.tag-input-wrap {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  padding: 8px;
  border: 1px solid #E2E8F0;
  border-radius: 6px;
  background: #FFFFFF;
  min-height: 40px;
  align-items: center;
}
.tag-item {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 3px 10px;
  border-radius: 20px;
  border: 1px solid #E2E8F0;
  font-size: 12px;
  color: #1A1A2E;
  background: #FFFFFF;
}
.tag-remove {
  font-size: 11px;
  color: #9AA0B4;
  cursor: pointer;
  line-height: 1;
}
.tag-remove:hover { color: #C92A2A; }
```

---

### 채널 블록 (URL 입력)

```css
.channel-block {
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  margin-bottom: 10px;
  overflow: hidden;
}
.channel-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 14px;
  background: #F7F8FA;
  border-bottom: 1px solid #E2E8F0;
}
.channel-name {
  font-size: 13px;
  font-weight: 600;
  color: #1A1A2E;
  display: flex;
  align-items: center;
  gap: 6px;
}
.channel-body { padding: 12px 14px; }
.channel-url-row {
  display: flex;
  gap: 8px;
  align-items: center;
  margin-bottom: 8px;
}
.channel-url-row:last-child { margin-bottom: 0; }
.channel-note {
  font-size: 11px;
  color: #4A5568;
  background: #F7F8FA;
  border-radius: 6px;
  padding: 7px 10px;
  display: flex;
  align-items: flex-start;
  gap: 6px;
  line-height: 1.5;
}
```

---

### 룰셋 필드 (조회/수정)

```css
.ruleset-field { margin-bottom: 14px; }
.ruleset-field:last-child { margin-bottom: 0; }
.ruleset-label {
  font-size: 11px;
  font-weight: 700;
  color: #4A5568;
  margin-bottom: 5px;
  display: flex;
  align-items: center;
  gap: 6px;
}
.ruleset-val {
  font-size: 12px;
  color: #1A1A2E;
  background: #F7F8FA;
  border: 1px solid #E2E8F0;
  border-radius: 6px;
  padding: 8px 10px;
  line-height: 1.6;
}
.ruleset-val.edited {
  border-color: #3B5BDB;
  background: #EEF2FF;
}
.ruleset-hint { font-size: 11px; color: #9AA0B4; margin-top: 4px; }

/* 출처 배지 */
.src-ai     { background: #EEF2FF; color: #3B5BDB; font-size: 10px; padding: 1px 6px; border-radius: 10px; font-weight: 600; }
.src-edited { background: #EEF2FF; color: #3B5BDB; font-size: 10px; padding: 1px 6px; border-radius: 10px; font-weight: 600; border: 1px solid #3B5BDB; }
```

---

## 7. 아이콘

```
라이브러리: Lucide Icons (CDN)
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
사용법: <i data-lucide="아이콘명"></i> 후 lucide.createIcons() 호출

크기: 컨텐츠 내 14–16px / 사이드바 14px
stroke-width: 1.8 (모든 아이콘 동일)
색상: 부모 color 상속 (currentColor)

자주 쓰는 아이콘:
- 채널: globe, rss, map-pin, instagram
- 액션: refresh-cw, plus, trash-2, edit-2, external-link, chevron-down
- 상태: check, alert-circle, alert-triangle, x-circle, clock
- UI: chevron-left, chevron-right, search, filter, settings
```

---

## 8. 그림자

```
기본 카드:   border 1px #E2E8F0 만 사용 (shadow 없음)
드롭다운:   0 2px 10px rgba(40,50,100,0.08)
모달:       0 4px 16px rgba(40,50,100,0.12)
```

---

## 9. HTML 파일 기본 구조

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BizPlanet — 페이지명</title>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Noto Sans KR', sans-serif; font-size: 13px; color: #1A1A2E; background: #F5F6FA; }
    /* 공통 CSS 변수 및 컴포넌트 스타일 */
  </style>
</head>
<body>
  <!-- 사이드바 -->
  <aside class="sidebar">...</aside>

  <!-- 메인 영역 -->
  <div style="margin-left:200px; padding-top:50px;">
    <!-- Topbar -->
    <header class="topbar">...</header>
    <!-- 콘텐츠 -->
    <main style="padding:24px; background:#F5F6FA; min-height:calc(100vh - 50px);">
      ...
    </main>
  </div>

  <script>lucide.createIcons();</script>
</body>
</html>
```

---

## 10. 프레임 구조 (다중 화면 시안용)

여러 화면을 하나의 파일에서 메뉴 링크로 이동하며 볼 수 있게 iframe 구조를 활용한다.

```html
<!-- index.html (네비게이션 프레임) -->
<frameset cols="200,*">
  <frame src="nav.html" name="nav">
  <frame src="01_대시보드.html" name="main">
</frameset>

<!-- 또는 iframe 방식 -->
<aside class="sidebar">
  <a href="01_대시보드.html" target="main">대시보드</a>
</aside>
<iframe name="main" src="01_대시보드.html"></iframe>
```

---

## 11. 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026.05 | 최초 작성. bizplanet_admin_ui_guide 기반으로 PC 웹 소호용으로 분리 |
| 2026.05 | 사이드바 다크 네이비(#0F1420) 적용 |
| 2026.05 | 탭, 모달, 진행상태, 빈상태, 오류배너, 채널블록, 룰셋필드, 키워드태그 컴포넌트 추가 |
