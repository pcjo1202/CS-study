# 🚀 시작 가이드

## 첫 주 준비 사항

### 1️⃣ 저장소 Fork하기
```bash
# 1. GitHub에서 원본 저장소 접속
https://github.com/study-four-career/CS-study

# 2. 우측 상단 "Fork" 버튼 클릭
# 3. 본인 계정으로 Fork 생성
```

### 2️⃣ Fork한 저장소 Clone
```bash
# 본인의 Fork 저장소 클론
git clone https://github.com/본인계정/CS-study.git
cd CS-study

# upstream 원격 저장소 추가 (원본 저장소)
git remote add upstream https://github.com/study-four-career/CS-study.git

# 원격 저장소 확인
git remote -v
# origin    https://github.com/본인계정/CS-study.git (fetch)
# origin    https://github.com/본인계정/CS-study.git (push)
# upstream  https://github.com/study-four-career/CS-study.git (fetch)
# upstream  https://github.com/study-four-career/CS-study.git (push)
```

### 3️⃣ 개인 폴더 생성
```bash
# 본인 이름의 폴더 생성
mkdir 본인이름
cd 본인이름

# 첫 주차 폴더 생성
mkdir week01
```

### 4️⃣ GitHub Issue로 학습 계획 세우기

> ⚠️ **중요**: Issue는 본인 Fork가 아닌 **원본 저장소**에 생성합니다!

1. **원본 저장소**로 이동 👉 https://github.com/study-four-career/CS-study
2. **Issues** 탭 클릭
3. **New Issue** 버튼 클릭
4. **주간 학습 계획** 템플릿 선택
5. 이번 주에 학습할 5가지 주제 작성
6. Issue 생성! (생성된 Issue 번호를 기억해두세요 - PR에서 사용)

---

## 📝 일주일 루틴

### 월요일 (또는 주말)
```bash
# 1. 주차 폴더 생성
mkdir week0N

# 2. GitHub Issue로 학습 계획 등록
# (웹에서 진행)

# 3. 첫 번째 주제 학습 시작
```

### 화~금요일
```bash
# 매일 반복
# 1. 학습 내용 정리 (마크다운 작성)
# 예: vim day02_상태관리_라이브러리.md

# 2. 커밋 & 푸시 (본인 Fork에)
git add .
git commit -m "docs(week01): day02 - 상태관리 라이브러리 비교"
git push origin main
```

### 금요일 저녁
```bash
# 1. GitHub에서 PR 생성
# - 본인 Fork → 원본 저장소(upstream)로 PR 생성
# - base repository: study-four-career/CS-study (base: main)
# - head repository: 본인계정/CS-study (compare: main)
# - 제목: [Week N] 이름 - 한 주 학습 정리

# 2. PR 설명 작성 (자동 템플릿 활용)

# 3. 팀원들에게 리뷰 요청
```

### 주말
```bash
# 1. 팀원들의 PR 리뷰
# - 원본 저장소의 PR 탭에서 확인
# - 최소 1개 이상 리뷰하기
# - 구체적인 피드백과 질문 남기기

# 2. 내 PR에 달린 리뷰 확인

# 3. 리뷰 반영 후 Merge (팀원이 승인하면 관리자가 Merge)
```

### 다음 주 월요일
```bash
# 1. upstream(원본 저장소)의 최신 내용 가져오기
git pull upstream main
git push origin main

# 2. 새로운 주차 시작!
mkdir week02
```

---

## 📋 마크다운 작성 팁

### 파일명 규칙
```
dayN_주제명.md

✅ 좋은 예:
- day01_React의Virtual_DOM.md
- day02_상태관리_라이브러리_비교.md
- day03_번들링_최적화.md

❌ 나쁜 예:
- 1일차.md
- react.md
- 20251021.md
```

### 필수 포함 내용
1. **🤔 학습 배경**: 왜 이 주제를 선택했나?
2. **📚 핵심 개념**: 주요 개념 설명
3. **💼 프로젝트 적용 사례**: 실제 코드와 함께
4. **🎤 면접 질문 & 답변**: 최소 3개 이상


## 💡 Issue 연결하기

PR을 작성할 때 원본 저장소의 Issue와 연결하는 방법:

```markdown
- **관련 Issue**: study-four-career/CS-study#1
```

> ⚠️ **주의**: 단순히 `#1`만 쓰면 본인 Fork의 Issue를 찾습니다!
> 
> 반드시 `저장소명#번호` 형식을 사용하세요.

### 자동으로 Issue 닫기
PR이 merge될 때 자동으로 Issue를 닫고 싶다면:

```markdown
Closes study-four-career/CS-study#1
Fixes study-four-career/CS-study#1
Resolves study-four-career/CS-study#1
```

---

## 🎉 준비 완료!

모든 설정이 끝났다면 바로 시작해봅시다!

```bash
# 1. Fork 및 Clone 완료
# 2. upstream 원격 저장소 추가 완료
# 3. 본인 폴더 및 week01 생성
# 4. 학습 계획 Issue 생성 (원본 저장소에)
# 5. day01 마크다운 작성
# 6. 커밋 & 푸시 (본인 Fork에)

git add .
git commit -m "docs(week01): day01 - [주제명]"
git push origin main
```

> 💡 **Fork 방식의 장점**
> - 각자 독립적으로 작업 가능
> - 실제 오픈소스 기여 경험
> - 본인 저장소에서 자유롭게 실험 가능
> - 원본 저장소는 검증된 내용만 Merge

**화이팅! 🔥**

