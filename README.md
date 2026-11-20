# 이인직 포트폴리오 — GitLab Pages

정적 사이트(순수 HTML/CSS/JS, 빌드 과정 없음)이며, `public/` 폴더가 그대로 GitLab Pages로 배포됩니다.

## 구조

```
public/
  index.html              메인 페이지 (Hero / About / Changelog / AI Skill)
  assets/css/style.css    디자인 토큰 + 전체 스타일
  assets/js/main.js       content.json을 읽어와 화면을 렌더링
  assets/img/             사진·스크린샷
  content/content.json    실제 콘텐츠 데이터 (이름/경력/AI 도구 등)
  admin/                  관리자 페이지 — 브라우저에서 글/이미지 수정 → GitLab에 직접 커밋
img_src/                  원본 스크린샷 소스 (배포되지 않음, 참고용)
.gitlab-ci.yml            public/ 폴더를 그대로 Pages로 배포하는 파이프라인
```

## 처음 배포하기

```bash
git init
git branch -M main
git remote add origin <GitLab 저장소 URL>
git add .
git commit -m "init: portfolio site"
git push -u origin main
```

푸시하면 파이프라인이 자동 실행되어 `public/`이 Pages로 배포됩니다. GitLab 프로젝트의
**Settings → Pages**에서 배포 URL을 확인할 수 있습니다.

### ⚠️ 저장소 공개 범위 설정 (중요)

`img_src/`에는 아직 가공하지 않은 원본 스크린샷(사내 IP, 다른 시스템 탭 등 민감 정보 포함)이 들어 있습니다.
**이 저장소(Repository) 자체는 Private으로 유지**하고, Pages 사이트만 공개하세요:

- **Settings → General → Visibility**에서 Project visibility는 `Private`
- 같은 화면의 **Pages** 항목에서 "Pages visibility"만 `Everyone`으로 설정

이렇게 하면 배포된 사이트(`public/`)는 누구나 볼 수 있지만, 저장소 코드와 `img_src/` 원본은 비공개로 남습니다.
(반대로 저장소까지 Public으로 두면 `img_src/`의 원본 스크린샷도 그대로 노출되니 주의하세요.)

## 콘텐츠 채우기

1. `public/assets/img/profile/me.jpg`를 실제 사진으로 교체하거나, `/admin` 페이지에서 업로드하세요.
2. `/admin` 접속 → GitLab 연결 설정(주소/프로젝트 경로/브랜치/Personal Access Token 입력) → "저장소에서 불러오기"
3. About, Changelog(경력), AI Skill 내용을 채우고 "변경사항 저장"을 누르면 GitLab에 직접 커밋되고,
   1~2분 뒤 파이프라인이 끝나면 사이트에 반영됩니다.

### Personal Access Token 만들기

GitLab → **Settings → Access Tokens**에서 `api` 또는 `write_repository` 스코프로 토큰을 발급하세요.
이 토큰은 **이 브라우저의 localStorage에만 저장**되며 다른 서버로 전송되지 않습니다. 공용 PC에서는
"토큰 지우기" 버튼으로 반드시 지우세요.

### FSPM 스크린샷 업로드 전 확인

`img_src/pf/1. FSPM/` 원본에는 내부 IP, 다른 사내 시스템이 찍힌 브라우저 탭, 장비명 등이 포함되어
있습니다. `/admin`에서 AI Skill 스크린샷을 업로드하기 전에 **직접 크롭/모자이크 처리된 이미지로
바꿔서** 올리세요.

## 디자인 메모

방화벽 정책/변경 이력 관리 도구를 만드는 사람이라는 소재에서 출발해, 페이지 전체를 관통하는
세로선("spine")과 섹션마다 뻗는 분기 노드로 전체 구조를 "정책 트리"처럼 구성했습니다. 경력 섹션은
실제로 만든 도구의 "변경 이력(Changelog)" 개념을 그대로 빌려와 이름 붙였습니다. 다크 네이비
(`#0E1420`) 베이스에 시그널 틸(`#4FB8A6`) 한 가지 포인트 컬러만 구조적으로 사용했고, About 섹션은
key:value 구성 파일처럼 보이도록 모노스페이스를 의도적으로 썼습니다.
