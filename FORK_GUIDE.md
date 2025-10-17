# 🍴 Fork 방식 완벽 가이드

## 🎯 Fork 방식을 선택한 이유

### 장점
1. **독립적인 작업 환경**
   - 각자 자유롭게 커밋하고 실험 가능
   - 브랜치 관리 불필요 (각자 main 사용)

2. **실제 오픈소스 기여 경험**
   - 면접에서 어필 가능한 협업 경험
   - PR 기반 코드 리뷰 프로세스

3. **깔끔한 저장소 관리**
   - 원본 저장소는 검증된 내용만 포함
   - 개인 저장소에 자유로운 실험 가능

4. **포트폴리오 효과**
   - 개인 GitHub에 학습 기록이 남음
   - Contribution 그래프에 반영

---

## 📋 초기 설정 (최초 1회)

### 1단계: Fork 하기
```
1. https://github.com/study-four-career/CS-study 접속
2. 우측 상단 "Fork" 버튼 클릭
3. 본인 계정으로 Fork 생성 완료!
```

### 2단계: Clone 하기
```bash
# 본인의 Fork 저장소 클론
git clone https://github.com/본인계정/CS-study.git
cd CS-study
```

### 3단계: upstream 설정
```bash
# 원본 저장소를 upstream으로 추가
git remote add upstream https://github.com/study-four-career/CS-study.git

# 확인
git remote -v
# origin    https://github.com/본인계정/CS-study.git
# upstream  https://github.com/study-four-career/CS-study.git
```

### 4단계: 개인 폴더 생성
```bash
# 본인 이름의 폴더 생성
mkdir 본인이름
cd 본인이름
mkdir week01
```

---

## 🔄 일주일 워크플로우

### 월요일
```bash
# 1. upstream 최신 내용 가져오기
git pull upstream main
git push origin main

# 2. 새 주차 시작
mkdir week02
cd week02
```

### 화~목요일
```bash
# 매일 반복
# 1. 학습 & 마크다운 작성
day01_주제.md

# 2. 커밋 & 푸시 (본인 Fork에)
git add .
git commit -m "docs(week01): day01 - 주제명"
git push origin main
```

### 금요일
```bash
# 1. 마지막 학습 완료
git add .
git commit -m "docs(week01): day05 - 주제명"
git push origin main

# 2. GitHub 웹에서 PR 생성
# - 본인 Fork → 원본 저장소로 PR
# - base: study-four-career/CS-study (main)
# - head: 본인계정/CS-study (main)
```

### 주말
```bash
# 1. 원본 저장소에서 팀원 PR 리뷰
# 2. 내 PR 피드백 확인 & 수정
# 3. Approve 받으면 관리자가 Merge
```

---

## 🔀 Git 명령어 정리

### 기본 작업 흐름
```bash
# 1. upstream 동기화 (주 1회, 월요일)
git pull upstream main
git push origin main

# 2. 매일 작업 (월~금)
git add .
git commit -m "docs(weekN): dayN - 주제"
git push origin main

# 3. PR 생성 (금요일, GitHub 웹에서)
```

### 트러블슈팅

#### upstream 동기화 시 충돌
```bash
git pull upstream main

# 충돌 발생 시
# 1. 충돌 파일 확인
git status

# 2. 파일 열어서 수동 해결
# 3. 충돌 해결 후
git add .
git commit -m "chore: upstream 동기화"
git push origin main
```

---

## 🎯 PR 생성 방법 (상세)

### 1단계: GitHub 웹 접속
```
본인 Fork 저장소 접속:
https://github.com/본인계정/CS-study
```

### 2단계: PR 생성 버튼 클릭
```
"Pull request" 탭 → "New pull request" 버튼
또는
"Contribute" → "Open pull request"
```

### 3단계: Base와 Head 설정
```
base repository: study-four-career/CS-study
base: main

head repository: 본인계정/CS-study  
compare: main
```

### 4단계: PR 작성
```
제목: [Week N] 이름 - 한 주 학습 정리
내용: 자동 템플릿 활용
```

### 5단계: 리뷰어 지정
```
우측 "Reviewers" 에서 팀원 선택
```

---

## 💡 Issue 연결하기

### PR에서 원본 저장소 Issue 연결
Fork에서 PR을 생성할 때 원본 저장소의 Issue를 연결하려면:

```markdown
# ❌ 작동 안 함
- 관련 Issue: #1

# ✅ 올바른 방법
- 관련 Issue: study-four-career/CS-study#1
```

### 자동으로 Issue 닫기
```markdown
Closes study-four-career/CS-study#1
Fixes study-four-career/CS-study#1
Resolves study-four-career/CS-study#1
```

> 💡 PR이 merge되면 연결된 Issue가 자동으로 닫힙니다!

---

## 🆘 문제 해결

### Q. origin과 upstream이 헷갈려요!
```bash
# 간단하게 기억하기
origin   = 내 저장소 (내가 푸시)
upstream = 원본 저장소 (동기화만)

# 확인 방법
git remote -v
```

### Q. 다른 팀원의 최신 학습 자료를 보고 싶어요!
```bash
# upstream에서 최신 내용 가져오기
git pull upstream main

# 이제 다른 팀원 폴더를 확인할 수 있습니다
ls -la
```

### Q. Fork가 원본보다 뒤처졌다는 메시지가 떠요!
```
A. 정상입니다! 매주 월요일에 git pull upstream main 하면 됩니다.

GitHub 웹에서 "Sync fork" 버튼을 눌러도 됩니다.
```


## 🎉 설정 완료 체크리스트

- [ ] 원본 저장소 Fork 완료
- [ ] 본인 Fork Clone 완료
- [ ] upstream 원격 저장소 추가 완료
- [ ] 본인 이름 폴더 생성 완료
- [ ] week01 폴더 생성 완료
- [ ] Git 명령어 이해 완료
- [ ] PR 생성 방법 이해 완료

모두 체크했다면 시작할 준비 완료! 🚀