# 이인직 포트폴리오 — GitHub Pages

정적 사이트(순수 HTML/CSS/JS, 빌드 과정 없음)이며, `public/` 폴더가 GitHub Actions를 통해
GitHub Pages로 배포됩니다.

## 구조

```
public/
  index.html              메인 페이지 (프로필 헤더 / About Me / Project / AI Utilization)
  assets/css/style.css    디자인 토큰 + 전체 스타일
  assets/js/main.js       content.json을 읽어와 화면을 렌더링, 탭 전환 처리
  assets/img/             사진·스크린샷
  content/content.json    실제 콘텐츠 데이터 (이름/경력/AI 도구 등)
  admin/                  관리자 페이지 — 브라우저에서 글/이미지 수정 → GitHub에 직접 커밋
img_src/                  원본 스크린샷 소스 (git에는 포함되지 않음, 로컬 참고용)
.github/workflows/pages.yml   public/ 폴더를 GitHub Pages로 배포하는 워크플로
```

## 처음 배포하기

```bash
git init
git branch -M main
git remote add origin <GitHub 저장소 URL>
git add .
git commit -m "init: portfolio site"
git push -u origin main
```

푸시 후 GitHub 저장소의 **Settings → Pages**에서 "Build and deployment" 소스를
**GitHub Actions**로 한 번 설정하세요. 이후 `main` 브랜치에 푸시할 때마다
`.github/workflows/pages.yml`이 실행되어 `public/`이 배포됩니다. 배포 URL도 같은 화면에서
확인할 수 있습니다.

### ⚠️ 저장소 공개 범위 설정 (중요)

GitHub는 GitLab과 달리 **무료 플랜에서는 Private 저장소에서 Pages 배포가 되지 않습니다**
(Private 저장소의 Pages는 GitHub Pro/Team/Enterprise 플랜에서만 지원됩니다). 이 프로젝트는
저장소를 **Public**으로 운영하는 것을 전제로 합니다.

따라서 `img_src/`(사내 IP, 다른 시스템 탭 등 민감 정보가 포함된 원본 스크린샷)는
**git에 올리지 않고 로컬에만 보관**하세요. `.gitignore`에 이미 `img_src/`가 등록되어 있습니다.
AI Utilization/Project에 쓸 스크린샷은 `/admin`에서 업로드하기 전에 직접 크롭·모자이크 처리한
뒤 올리세요 — `/admin`을 거쳐 커밋되는 이미지(`public/assets/img/...`)는 공개 저장소에 그대로
들어갑니다.

(Private 저장소 + 유료 플랜을 쓰는 경우에만 `img_src/`를 git에 포함해도 되지만, 이 저장소는
기본적으로 Public을 가정하고 구성되어 있습니다.)

## 콘텐츠 채우기

1. `public/assets/img/profile/me.jpg`를 실제 사진으로 교체하거나, `/admin` 페이지에서 업로드하세요.
2. `/admin` 접속 → GitHub 연결 설정(저장소 `owner/repo`, 브랜치, Personal Access Token 입력) →
   "저장소에서 불러오기"
3. About Me, Project(경력), AI Utilization 내용을 채우고 "변경사항 저장"을 누르면 GitHub에
   직접 커밋되고, 1~2분 뒤 Actions 워크플로가 끝나면 사이트에 반영됩니다.

### Personal Access Token 만들기

GitHub → **Settings → Developer settings → Personal access tokens**에서 발급하세요.

- Fine-grained token(권장): 이 저장소만 선택 → Repository permissions의 **Contents**를
  `Read and write`로 설정
- Classic token: `repo` 스코프

이 토큰은 **이 브라우저의 localStorage에만 저장**되며 다른 서버로 전송되지 않습니다. 공용 PC에서는
"토큰 지우기" 버튼으로 반드시 지우세요.

커밋 방식에 대한 참고: GitHub Contents API는 파일 하나당 커밋 하나씩 생성합니다(GitLab처럼
여러 파일을 한 번에 원자적으로 커밋하지 않음). 이미지 여러 장 + content.json을 한 번에 저장하면
그만큼 여러 커밋이 생깁니다.

## 디자인 메모

블랙 배경(`#0B0B0C`)에 오렌지 포인트 컬러(`#FF9900`) 한 가지만 구조적으로 사용한, AWS 콘솔
느낌의 다크 테마입니다. 상단에 사진·이름·한 줄 소개가 중앙 정렬로 오고, 그 아래 네비게이션
바(About Me / Project / AI Utilization)가 탭처럼 동작합니다 — 기본으로는 About Me만 보이고,
Project·AI Utilization은 스크린샷이 많아 클릭했을 때만 아래에 펼쳐집니다.
