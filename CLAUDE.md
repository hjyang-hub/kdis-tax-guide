# KDI 전문가 용역비 원천징수·비과세 안내 — GitHub Pages 배포

## 프로젝트 개요

`index.html` 하나로 이루어진 단일 페이지 웹앱. KDI 국제정책대학원 재무회계팀이 전문가 용역비
지급 시 원천징수/비과세 여부를 판단할 수 있도록 돕는 국영문 인터랙티브 안내 도구.
민감 정보나 개인정보는 포함하지 않음 (일반적인 세법 안내 내용만 포함) — **공개(Public) 저장소로
운영해도 무방함**.

기존에는 Send(send.co) 무료 플랜으로 배포했으나, 링크가 24시간마다 만료되는 문제가 반복되어
**GitHub Pages로 이전, 영구 무료 링크를 확보하는 것이 목표**.

## 할 일 (이 순서로 진행)

1. **GitHub 인증 확인**
   ```
   gh auth status
   ```
   로그인 안 되어 있으면:
   ```
   gh auth login
   ```
   (브라우저로 GitHub 계정 인증. `gh` CLI가 없으면 먼저 설치: https://cli.github.com/ 또는
   `winget install --id GitHub.cli`)

2. **저장소 생성 및 푸시** (이 폴더에서 실행)
   ```
   git init
   git add index.html CLAUDE.md
   git commit -m "Initial commit: KDI tax withholding guide"
   gh repo create kdi-tax-guide --public --source=. --remote=origin --push
   ```

3. **GitHub Pages 활성화**
   ```
   gh api -X POST repos/{owner}/kdi-tax-guide/pages -f "source[branch]=main" -f "source[path]=/"
   ```
   ({owner}는 실제 GitHub 사용자명으로 자동 치환되거나, 안 되면 사용자명 직접 입력)

   또는 API 호출이 안 되면 브라우저에서:
   - 저장소 페이지 → Settings → Pages
   - Source: `Deploy from a branch`, Branch: `main` / `/ (root)` → Save

4. **결과 확인**
   1~2분 후 아래 URL이 살아있는지 확인:
   ```
   https://{사용자명}.github.io/kdi-tax-guide/
   ```

## 향후 유지보수

`index.html`의 내용(안내 문구, 세율/과세최저한 설명, 링크 등)을 수정할 일이 생기면:
1. 이 폴더에서 `index.html` 직접 수정
2. `git add index.html && git commit -m "설명" && git push`
3. GitHub Pages가 자동으로 몇 분 내 재배포함 (별도 재배포 명령 불필요)

## 참고

- 이 프로젝트는 KDI의 다른 프로젝트인 "해외송금신청서 자동작성 웹앱"(Render 배포 예정, 별도
  저장소)과는 무관한 별개 산출물입니다.
- 콘텐츠 로직(원천징수 22%/8.8%, 과세최저한 12.5만원/5만원, 조세조약 비과세 신청서류 3종 등)은
  이미 완성되어 있으므로, 특별한 요청이 없는 한 로직을 임의로 변경하지 마세요.
