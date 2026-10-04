# book

우리동네 AI클럽 책 뼈대 펼침면 입력 — Firebase 실시간 저장 + Vercel 배포 버전.

## 파일

- `index.html` — 본 파일 (Vercel이 서빙). 원본 `책뼈대_펼침면입력_v1.html`에서 복사 후 Firebase 코드 주입됨.
- `firestore.rules` — Firestore 보안 규칙 (구글 로그인 사용자만 읽기/쓰기).

## Firebase 설정 (최초 1회, 약 10분)

1. https://console.firebase.google.com → 새 프로젝트 생성.
2. Firestore Database → 데이터베이스 만들기 → 리전 `asia-northeast3(서울)` → 프로덕션 모드.
3. Authentication → 시작하기 → Google 공급업체 사용 설정.
4. 웹앱 추가(`</>`) → `firebaseConfig` 발급 → `index.html` 상단의 `FIREBASE_CONFIG` 3줄(apiKey/authDomain/projectId)에 붙여넣기.
5. Firestore 규칙 탭에 `firestore.rules` 내용 붙여넣고 게시.
6. Authentication → 설정 → 승인된 도메인에 Vercel 주소(`xxx.vercel.app`) 추가.

`FIREBASE_CONFIG`를 안 넣으면 "로컬 모드(파일 저장)"로 동작하고, 넣고 재배포하면 실시간 저장이 켜집니다.

## Vercel 배포

1. 이 폴더를 GitHub `jejuailabs/book`에 push.
2. https://vercel.com → Add New Project → 해당 repo import → Framework Preset: `Other` → Deploy.
3. 나온 주소(`https://book-xxx.vercel.app`)를 모두에게 공유. 각자 구글 로그인 후 입력하면 `bookData/main` 문서에 자동 저장되고, 새로고침해도 유지됩니다.

## 사용법

- 툴바 우측 `로그인` → 구글 로그인 → 입력하면 0.8초 뒤 클라우드에 자동 저장.
- `md로 내보내기` / `인쇄 / PDF`는 그대로 유지. 기존 `나눠서 따로 저장 / 합치기`는 백업용으로만 남기고, 평소엔 쓸 필요 없음.

## 수정 로그 (📜 메뉴 맨 끝)

- 칸을 고치고 빠져나오면 `언제 · 누가 · 어디를 · 추가/수정/삭제`가 한 줄씩 기록된다. 의견 추가·삭제, 추가 항목 삭제도 기록.
- 저장 위치: Firestore `bookData/log-YYYY-MM` (월별 문서의 `e` 배열). 기존 규칙(`bookData/{docId}`) 그대로 사용.
- `로그 직접 남기기`: 메모 / 구조(사이트 수정) / 검토(검토 완료 기준점).
- `Claude용 보기`: 마지막 '검토' 기록 이후 바뀐 칸만, 칸마다 최신 값 하나. 콘솔에서 `claudeView()`로도 읽을 수 있다.
- 주소 뒤에 `?by=Claude`를 붙여 연 탭은 그 탭에서 남는 기록의 작성자가 `Claude`로 표시된다 (탭을 닫으면 해제).

## 수정 이력 · 되돌리기

- 칸을 고치면 수정 전·후 **전체 내용**이 `bookData/v-…` 문서에 버전 하나로 저장된다 (깃 커밋처럼).
- 수정 로그의 [비교] → 바뀐 부분(빨강=지운 글, 초록=넣은 글) + [수정 전 내용으로 되돌리기]. 되돌림도 버전으로 남아 다시 되돌릴 수 있다.
- 각 칸 오른쪽 위 [이력] → 그 칸의 모든 버전 목록.
- 칸에 커서를 둔 채 창을 닫거나 탭을 옮겨도 버전이 저장된다.
- 날짜별 전체 백업: 그날 처음 접속한 사람의 접속 시점 상태를 `bookData/snap-YYYY-MM-DD`에 저장. 로그 페이지에서 날짜별 md로 받을 수 있다.
- Claude용 보기: 고친 칸은 검토 시점 대비 바뀐 부분만 `[-지운 글-] {+넣은 글+}`로 보여 준다.
