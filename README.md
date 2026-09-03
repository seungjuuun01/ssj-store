# SSJ Store (자체 F-Droid 저장소)

내가 만든 안드로이드 앱을 배포/업데이트하는 개인 앱스토어입니다.
`repo/`에 서명된 APK를 넣고 push 하면, GitHub Actions가 F-Droid 인덱스를 만들어
GitHub Pages로 배포합니다. 사용자는 F-Droid 클라이언트에 저장소 주소만 추가하면
이후 업데이트를 자동으로 받습니다.

## 최초 1회 설정

1. **GitHub 저장소 생성**: `seungjuuun01/ssj-store` (public) 로 빈 저장소를 만든다.
2. **push**:
   ```bash
   cd /c/dev/ssj-store
   git add -A && git commit -m "init: hackmin fdroid store"
   git branch -M main
   git remote add origin https://github.com/seungjuuun01/ssj-store.git
   git push -u origin main
   ```
3. **Secrets 등록** (Settings → Secrets and variables → Actions → New repository secret):
   `.secrets.local.txt` 에 있는 3개 값을 그대로 등록.
   - `KEYSTORE_BASE64`
   - `KEYSTORE_PASS`
   - `KEY_PASS`
4. **Pages 활성화**: Settings → Pages → Source = **GitHub Actions**.
5. Actions 탭에서 워크플로우가 성공하면 완료.
   저장소 주소: `https://seungjuuun01.github.io/ssj-store/repo`

> ⚠️ `keystore.p12` 와 `.secrets.local.txt` 는 절대 커밋하지 말 것(.gitignore 처리됨).
> 이 키를 잃어버리면 기존 사용자에게 업데이트를 내보낼 수 없습니다. 안전하게 백업하세요.

## 앱 추가 / 업데이트 하는 법

1. 새로/업데이트된 **서명된 릴리스 APK**를 `repo/` 에 넣는다.
   - 업데이트로 인식되려면 앱의 `versionCode`가 이전보다 커야 한다.
   - 같은 앱은 반드시 **같은 서명키**로 서명해야 F-Droid가 업데이트로 받아들인다.
2. commit & push → Actions가 자동으로 인덱스 재생성 & 배포.
3. 사용자 폰에서 F-Droid가 새 버전 알림 표시.

## 사용자 안내

F-Droid 설치 후 저장소 주소 추가:
```
https://seungjuuun01.github.io/ssj-store/repo
```
(랜딩 페이지: `https://seungjuuun01.github.io/ssj-store/`)
