# 📚 CS 스터디 운영 요약

## 🎯 핵심 목표
**"내 포트폴리오 프로젝트를 완벽하게 설명할 수 있는 개발자 되기"**

---

## 🔄 주간 사이클

```
월요일 (또는 주말)
  └─ Issue 생성: 주간 학습 계획 5가지 선정
       ↓
월~금 (매일)
  └─ 1개 주제씩 학습 & 커밋
       ↓
금요일
  └─ 한 주의 학습을 모아서 PR 생성
       ↓
주말
  └─ 팀원들 리뷰 & 피드백
       ↓
일요일 밤 or 월요일
  └─ Merge → 다음 주 시작!
```

---

## 📂 폴더 구조

```
CS-study/
├── 본인이름/
│   └── weekNN/
│       ├── day01_주제.md
│       ├── day02_주제.md
│       ├── day03_주제.md
│       ├── day04_주제.md
│       └── day05_주제.md
├── README.md
├── GETTING_STARTED.md
└── CHECKLIST.md
```

---

## 📝 학습 노트 필수 구성

1. **🤔 학습 배경** - 왜 이 주제를?
2. **📚 핵심 개념** - 주요 개념 설명
3. **🔍 깊이 파기** - 내부 동작, 장단점
4. **💼 프로젝트 적용** - 실제 코드 예시
5. **🎤 면접 Q&A** - 최소 1개 이상
6. **🔗 참고 자료** - 학습 자료

---

## 🔀 Git 워크플로우 (Fork 방식)

### 저장소 구조
- **upstream**: 원본 저장소 (study-four-career/CS-study)
- **origin**: 개인 Fork 저장소 (본인계정/CS-study)

### 커밋 & 푸시
```bash
# 커밋 규칙
docs(weekNN): day0N - 주제명

# 본인 Fork에 푸시
git push origin main

예시:
git commit -m "docs(week01): day01 - React Virtual DOM"
git push origin main
```

### PR 규칙
```
본인 Fork → 원본 저장소(upstream)로 PR

base: study-four-career/CS-study (main)
head: 본인계정/CS-study (main)

제목: [Week N] 이름 - 00월 0주차 학습 정리
예시: [Week 1] 홍길동 - 10월 1주차 학습 정리
```

### 동기화
```bash
# 매주 월요일: upstream 최신 내용 가져오기
git pull upstream main
git push origin main
```

---

## 🏆 참여 규칙

✅ 주 5회 (월~금) 학습 & 커밋
✅ 금요일 PR 제출
✅ 주말 팀원 PR 리뷰 (최소 1개)

---

## 📊 진행 현황 관리

매주 README.md의 진행 현황 테이블 업데이트:
- ✅ = PR Merged
- ⏸️ = 휴식
- ❌ = 불참