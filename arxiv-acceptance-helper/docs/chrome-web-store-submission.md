# Chrome Web Store 제출 문안

## 제품명 변경 시 확인

- 스토어 표시 이름은 `PaperGlint`로 맞추고 설명, 스크린샷, 홍보 이미지에도 같은 이름을 사용합니다.
- 기존 스토어 항목이 있다면 해당 항목을 업데이트하고, 업로드 전 `manifest.json`,
  `package.json`, `package-lock.json`의 버전을 기존 게시 버전보다 높게 맞춥니다.
- README와 개인정보처리방침을 GitHub에도 반영해야 공개 문서가 새 이름으로 표시됩니다.
  저장소명 `paper_Lens`와 하위 폴더명은 실제 경로이므로 URL을 임의로 바꾸지 않습니다.
- `Report issue`가 여는 Google Form의 제목과 설명은 폼 소유자 화면에서 별도로 확인합니다.
  로컬 코드의 이름 변경은 외부 폼 내용을 바꾸지 않습니다.
- 개발자 모드에서는 기존 설치 폴더에서 업데이트하고 확장 프로그램과 arXiv 탭을
  새로고침합니다. 기존 설정을 유지하려면 확장 프로그램을 제거 후 재설치하지 않습니다.

## Single purpose

PaperGlint is an arXiv research companion that shows publication evidence and
relevant code links and helps users save the current paper with a meaningful
PDF filename.

## 설치 전 데이터 공개 문안

PaperGlint는 지원되는 arXiv abstract 페이지에서 UI를 표시하기 위해 논문 ID, URL,
제목, 저자, Comments, DOI와 버전을 브라우저 안에서 읽습니다. 외부 조회는 사용자가
`Open PaperGlint` 또는 `Code & evidence`를 누른 뒤에만 시작합니다. 논문 게재 근거와
코드 저장소를 찾기 위해 필요한 최소 논문 정보를 DBLP, Crossref, Semantic Scholar,
OpenReview, 공식 proceedings 및 사용자가 권한을 허용한 경우 GitHub API에 HTTPS로
전송합니다. PDF 링크·텍스트는 `Code & evidence`를 누른 경우에만 브라우저 메모리에서
처리합니다. 분석 결과는 반복 요청을 줄이기 위해 최대 24시간 로컬 캐시되며, 원격
분석·광고·판매에는 사용되지 않습니다.

## Privacy practices

- Website content: 사용함
- Web browsing activity: 현재 지원 arXiv 논문 페이지에 한해 사용함
- Authentication information: OpenReview 세션 재시도에서 브라우저가 기존 쿠키를
  OpenReview로 직접 보낼 수 있으므로 보수적으로 신고
- Remote code: 사용하지 않음. PDF.js를 확장 패키지 안에 포함하며 외부 응답은
  데이터로만 처리함
- Limited Use certification: 모두 확인
- Privacy policy URL:
  `https://github.com/nuIw/paper_Lens/blob/main/arxiv-acceptance-helper/PRIVACY.md`

## 권한 설명

- `storage`: PDF 파일명 설정, 짧은 분석 캐시와 세션 내 GitHub 요청 제한을 저장
- `arxiv.org`: 논문 페이지 UI, 최신 버전 metadata 및 사용자가 요청한 PDF 처리
- `dblp.org`, `api.crossref.org`, `api.semanticscholar.org`: publication metadata 조회
- `api.openreview.net`, `api2.openreview.net`: OpenReview submission과 decision 조회
- CVF, ACL Anthology, PMLR, NeurIPS Proceedings: 강한 metadata 후보의 공식 근거 확인
- 선택적 `api.github.com`: 사용자가 `Code & evidence`를 눌러 권한을 허용했을 때만
  관련 코드 후보 검색
- 선택적 `downloads`: 사용자가 `Download PDF`를 눌러 권한을 허용했을 때만 지정한
  파일명으로 arXiv PDF 저장

## 제출 패키지

```sh
npm run package:extension
```

생성된 `dist/paperglint-<version>.zip`만 업로드합니다. ZIP 루트에는
`manifest.json`, `src/`, `vendor/`, `icons/`만 포함됩니다.
