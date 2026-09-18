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
