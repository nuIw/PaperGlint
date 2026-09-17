# Chrome Web Store 제출 문안

## 제품명 변경 시 확인

- 스토어 표시 이름은 `PaperGlint`로 맞추고 설명, 스크린샷, 홍보 이미지에도 같은 이름을 사용합니다.
- 기존 스토어 항목이 있다면 해당 항목을 업데이트하고, 업로드 전 `manifest.json`,
  `package.json`, `package-lock.json`의 버전을 기존 게시 버전보다 높게 맞춥니다.
- README와 개인정보처리방침을 GitHub에도 반영해야 공개 문서가 새 이름으로 표시됩니다.
  공개 저장소는 `nuIw/PaperGlint`이며, 확장 프로그램 경로는 `arxiv-acceptance-helper`입니다.
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
`Report issue`를 열면 현재 논문 URL이 Google Forms에 전달되며, 폼을 제출한
신고 내용은 개발자가 오류 재현과 지원을 위해 열람합니다. 신고 응답은 확장 프로그램
제거로 삭제되지 않으며, 개인정보처리방침의 문의 경로로 삭제를 요청할 수 있습니다.

## Privacy practices

- Website content: 사용함
- Web browsing activity: 현재 지원 arXiv 논문 페이지에 한해 사용함
- Authentication information: OpenReview 세션 재시도에서 브라우저가 기존 쿠키를
  OpenReview로 직접 보낼 수 있으므로 보수적으로 신고
- Remote code: 사용하지 않음. PDF.js를 확장 패키지 안에 포함하며 외부 응답은
  데이터로만 처리함
- 신고 폼의 이메일 수집 여부와 신고 내용에 해당하는 데이터 유형은 실제 폼 설정을
  확인한 뒤 신고합니다. 현재 저장소만으로 대시보드 체크박스의 최종 값을 확정하지 않습니다.
- Limited Use certification: 실제 데이터 처리와 위 문안을 대조한 뒤 개발자가 확인
- Privacy policy URL:
  `https://github.com/nuIw/PaperGlint/blob/main/arxiv-acceptance-helper/PRIVACY.md`

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

## 제출 전 남은 확인

- Google Form 제목을 `PaperGlint Issue Report`로 변경합니다. 로그인 요구 여부,
  이메일 수집 여부, 응답 접근자와 삭제 방법도 폼 소유자가 확인해야 합니다.
- 폼 설명에 다음 문안을 추가합니다: "이 폼을 열면 논문 URL이 Google에 전달됩니다.
  제출한 내용은 PaperGlint 개발자가 오류 확인을 위해 읽습니다. 민감한 정보는 입력하지
  마세요. 신고 삭제 요청과 자세한 내용은 PaperGlint 개인정보처리방침을 확인하세요."
- `store/promo-440x280.png`는 홍보 이미지입니다. 실제 작동 화면을 나타내는 스크린샷이 아닙니다.
- 실제 Chrome에서 설치한 뒤 1280×800 또는 640×400 스크린샷을 최소 1장 준비합니다.
- 신규 설치에서 외부 조회 전/후, 권한 허용·거절, PDF 스캔·다운로드,
  OpenReview 오류·세션 재시도, 키보드 조작을 확인합니다.
- 대시보드의 개인정보 URL, 데이터 신고, 권한 사유와 설명을 실제 동작과 일치시킵니다.

## 심사자 테스트 안내

설치 후 `https://arxiv.org/abs/1706.03762`를 열고 논문 제목 아래의
`Open PaperGlint`를 누릅니다. `Code & evidence`는 PDF 분석과 선택적 GitHub 검색을
시작합니다. PDF 다운로드 시에만 다운로드 권한을 요청합니다. 별도 계정은 필요하지
않으며, 외부 API 제한은 오류와 수동 확인 링크로 표시됩니다. 이 안내는 테스트 절차이며
현재 외부 API의 성공이나 실제 Chrome 테스트 완료를 보장하지 않습니다.
