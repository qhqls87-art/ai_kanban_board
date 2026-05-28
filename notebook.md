# 칸반보드 업무관리 · 프로젝트 노트북

> 개발 기록, 기능 명세, 배포 정보를 정리한 프로젝트 노트입니다.

---

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 프로젝트명 | 칸반보드 업무관리 시스템 |
| 배포 URL | https://qhqls87-art.github.io/ai_kanban_board/ |
| 저장소 | https://github.com/qhqls87-art/ai_kanban_board |
| 기술 스택 | HTML5 · CSS3 · Vanilla JavaScript |
| 외부 의존성 | 없음 (단일 파일 실행) |

---

## ✅ 기능 명세

### 컬럼 구조
- **To Do** — 예정된 업무
- **진행 중** — 현재 처리 중인 업무
- **완료** — 완료된 업무 (카드 제목에 취소선 적용)

### 카드 기능
- [x] 카드 추가 (컬럼별 버튼 / 우측 상단 버튼)
- [x] 카드 편집 (마우스 호버 → 연필 아이콘)
- [x] 카드 삭제 (마우스 호버 → 휴지통 아이콘)
- [x] 드래그 앤 드롭 (컬럼 간 이동)
- [x] localStorage 자동 저장 (새로고침 후 유지)

### 카드 데이터 필드
| 필드 | 타입 | 설명 |
|------|------|------|
| 제목 | string | 업무명 (필수, 최대 80자) |
| 설명 | string | 상세 내용 (선택) |
| 담당자 | string | 담당자 이름 → 아바타 자동 생성 |
| 마감일 | date | 날짜 선택 → 기한 초과 시 빨간색 표시 |
| 우선순위 | high / medium / low | 배지 색상으로 구분 |
| 라벨 | array | 개발, 디자인, 마케팅, 버그, 기능, 검토 |

### 우선순위 색상 코드
| 레벨 | 배경색 | 텍스트색 |
|------|--------|---------|
| 높음 | `#ffebe6` | `#de350b` |
| 보통 | `#fff8e6` | `#ff991f` |
| 낮음 | `#e3fcef` | `#36b37e` |

---

## 🗂 파일 구조

```
ai_kanban_board/
├── index.html                   ← 단일 파일 앱 (HTML + CSS + JS 통합)
├── notebook.md                  ← 프로젝트 노트북 (이 파일)
├── .gitignore
└── .github/
    └── workflows/
        └── deploy.yml           ← GitHub Actions 자동 배포
```

---

## 🚀 배포 방법

### GitHub Pages (자동 배포)
`main` 브랜치에 push하면 GitHub Actions가 자동으로 배포합니다.

```bash
git add index.html
git commit -m "feat: 변경 내용 설명"
git push origin main
```

### 로컬 실행
별도 서버 없이 `index.html`을 브라우저로 열면 바로 실행됩니다.

```
파일 탐색기 → index.html 더블클릭
또는
브라우저 주소창: file:///C:/work/ai_kanban_board/index.html
```

---

## 🎨 디자인 시스템

### 색상 팔레트
| 변수 | 값 | 용도 |
|------|----|------|
| `--header-bg` | `#172b4d` | 상단 헤더 |
| `--accent` | `#0052cc` | 버튼, 링크, 진행중 컬럼 |
| `--col-bg` | `#ebecf0` | 컬럼 배경 |
| `--card-bg` | `#ffffff` | 카드 배경 |
| `--ind-todo` | `#6b778c` | To Do 컬럼 인디케이터 |
| `--ind-doing` | `#0052cc` | 진행중 컬럼 인디케이터 |
| `--ind-done` | `#00875a` | 완료 컬럼 인디케이터 |

### 폰트
- `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, `Malgun Gothic`
- 외부 폰트 로드 없음

---

## 🔧 기술 노트

### localStorage 구조
```json
{
  "kanban_v1": [
    {
      "id": "abc12345",
      "title": "업무 제목",
      "desc": "설명",
      "assignee": "홍길동",
      "due": "2026-06-30",
      "priority": "high",
      "status": "todo",
      "labels": ["dev", "feature"],
      "createdAt": 1748000000000
    }
  ]
}
```

### 드래그 앤 드롭 구현
- HTML5 Drag and Drop API 사용
- `ondragstart` → `ondragover` → `ondrop` 이벤트 체인
- 드래그 중 카드에 `.is-dragging` 클래스 적용 (반투명 + 회전 효과)
- 드롭 존 진입 시 컬럼에 `.drop-active` 클래스 적용

### 아바타 색상 생성 로직
담당자 이름의 첫 글자 `charCode`를 8가지 색상 배열의 인덱스로 사용하여 일관된 아바타 색상을 자동 생성합니다.

---

## 📅 변경 이력

| 날짜 | 버전 | 내용 |
|------|------|------|
| 2026-05-28 | v1.0 | 초기 릴리즈 — 3컬럼 칸반보드, 드래그&드롭, localStorage 저장 |

---

## 🗺 향후 계획 (Backlog)

- [ ] 카드 검색 / 필터 기능
- [ ] 카드 순서 변경 (같은 컬럼 내 드래그)
- [ ] 마감일 캘린더 뷰
- [ ] 다크 모드 지원
- [ ] 멤버별 필터링
- [ ] 프린트 / PDF 내보내기
