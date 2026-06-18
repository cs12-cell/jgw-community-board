# 실시간 동기화 (Firebase) 설정

게시판·그림판을 여러 기기에서 실시간으로 공유하려면 Firebase Realtime Database가 필요합니다.

## 1. Firebase 프로젝트 만들기

1. [Firebase 콘솔](https://console.firebase.google.com/) 접속 (Google 계정)
2. **프로젝트 추가** → 이름 예: `jgw-community`
3. **Realtime Database** 메뉴 → **데이터베이스 만들기**
4. 위치: `asia-southeast1` (싱가포르) 또는 가까운 지역
5. 보안 규칙: **테스트 모드**로 시작 (학교 내부용. 공개 사이트면 규칙을 나중에 조정하세요)

## 2. 웹 앱 설정 복사

1. 프로젝트 설정(톱니바퀴) → **일반** → **내 앱** → **웹** `</>` 추가
2. 표시되는 `firebaseConfig` 값을 `good.html`의 `FIREBASE_CONFIG`에 붙여넣기

```javascript
const FIREBASE_CONFIG = {
  apiKey: "…",
  authDomain: "….firebaseapp.com",
  databaseURL: "https://….firebasio.com",  // 또는 asia-southeast1.firebasedatabase.app
  projectId: "…",
  storageBucket: "….appspot.com",
  messagingSenderId: "…",
  appId: "…"
};
```

`databaseURL`만 채워도 실시간 동기화가 켜집니다.

## 3. 배포

```powershell
cd "d:\코딩\jgw-board"
Copy-Item "d:\코딩\good.html" "index.html" -Force
git add index.html
git commit -m "Firebase 설정 반영"
git push
```

## 4. 확인

사이트를 두 브라우저(또는 폰·PC)에서 열고, 한쪽에서 글을 쓰거나 그림판에 그리면 다른 쪽에 바로 나타나야 합니다. 상단에 **실시간 연결됨** 배지가 보이면 정상입니다.

## 보안 규칙 (선택)

`database.rules.json`을 Firebase 콘솔 → Realtime Database → 규칙에 붙여 넣을 수 있습니다. 테스트 모드는 누구나 읽기/쓰기가 가능합니다.
