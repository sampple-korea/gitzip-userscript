이 유저스크립트는 GitHub 저장소 페이지에서 직접 하위 폴더나 개별 파일을 ZIP 아카이브 형태로 다운로드할 수 있도록 기능을 추가합니다. 기존 GitZip 웹 애플리케이션의 기능을 GitHub 페이지 내에서 바로 사용할 수 있도록 변형한 버전입니다.

AdGuard, Tampermonkey, Violentmonkey 등 다양한 유저스크립트 매니저와 호환됩니다.

## 주요 기능

*   **다운로드 버튼 추가:** GitHub 저장소의 파일 및 폴더 목록 옆에 해당 항목을 다운로드할 수 있는 `Zip` (폴더) 또는 `File` (파일) 버튼을 추가합니다.
*   **폴더/파일 다운로드:** 버튼 클릭 한 번으로 특정 폴더 전체를 ZIP 압축하여 다운로드하거나, 개별 파일을 직접 다운로드할 수 있습니다.
*   **GitHub 토큰 지원:**
    *   비공개(Private) 저장소의 폴더/파일 다운로드를 지원합니다.
    *   GitHub API 요청 제한(Rate Limit)을 늘려 대용량 폴더 다운로드 시 발생할 수 있는 오류를 줄여줍니다.
*   **UI 통합:** GitHub 페이지 상단 액션 바 영역에 토큰 설정을 위한 🔑 아이콘 버튼과 설정 패널을 추가합니다.
*   **자동 라이브러리 로드:** 스크립트 실행에 필요한 JSZip, FileSaver 라이브러리를 `@require` 메타데이터를 통해 자동으로 로드합니다.

## 설치 방법

1.  **유저스크립트 매니저 설치:** 사용 중인 브라우저에 맞는 유저스크립트 매니저 확장 프로그램(예: [Tampermonkey](https://www.tampermonkey.net/), [Violentmonkey](https://violentmonkey.github.io/))을 설치합니다. AdGuard 사용자의 경우, 설정 내 유저스크립트 관리 기능을 이용할 수 있습니다.
2.  **새 스크립트 만들기:** 유저스크립트 매니저 대시보드에서 '새 스크립트 만들기' 또는 유사한 메뉴를 선택합니다.
3.  **코드 붙여넣기:** 위 유저스크립트 코드 전체를 복사하여 에디터에 붙여넣습니다. (기존 템플릿 코드는 삭제합니다.)
4.  **저장:** 스크립트를 저장합니다. 매니저가 스크립트를 자동으로 활성화합니다.

## 사용 방법

1.  **GitHub 저장소 방문:** 스크립트가 실행될 GitHub 저장소 페이지 (루트, 특정 폴더 경로 등)로 이동합니다.
2.  **버튼 확인:**
    *   페이지 상단 액션 바 (보통 'Code' 버튼 근처)에 🔑 아이콘과 "GitZip" 텍스트가 있는 작은 버튼이 추가된 것을 확인합니다. 이 버튼으로 토큰 설정을 할 수 있습니다.
    *   파일/폴더 목록의 각 항목 옆에 `Zip` 또는 `File` 버튼이 추가된 것을 확인합니다.
3.  **다운로드:** 다운로드하려는 폴더 옆의 `Zip` 버튼 또는 파일 옆의 `File` 버튼을 클릭합니다. 버튼에 로딩 아이콘이 표시되며 다운로드가 진행됩니다.

## GitHub 개인 접근 토큰 (Personal Access Token - PAT) 설정 (권장)

GitHub API는 익명 사용자의 시간당 요청 횟수(Rate Limit)를 제한합니다. 큰 폴더를 다운로드하거나 비공개 저장소에 접근하려면 **개인 접근 토큰(PAT)** 사용이 강력히 권장됩니다.

**토큰 생성 방법:**

1.  **GitHub 토큰 설정 페이지 이동:** [GitHub Tokens (classic)](https://github.com/settings/tokens/new?scopes=repo&description=GitZip%20UserScript) 페이지로 이동합니다. (또는 스크립트 UI의 'Create Private/Public' 링크 클릭)
2.  **토큰 생성:**
    *   `Note`: 토큰의 용도를 알아볼 수 있는 이름(예: GitZip UserScript)을 입력합니다.
    *   `Expiration`: 토큰 만료 기간을 설정합니다. (보안을 위해 적절한 기간 설정 권장)
    *   **`Select scopes` (스코프 설정):**
        *   **비공개 저장소 포함:** `repo` 스코프 전체를 체크합니다.
        *   **공개 저장소만:** `public_repo` 스코프만 체크합니다. (더 안전한 옵션)
    *   `Generate token` 버튼을 클릭합니다.
3.  **토큰 복사:** 생성된 토큰 문자열이 화면에 표시됩니다. **이 토큰은 다시 표시되지 않으므로 반드시 즉시 복사하여 안전한 곳에 임시 보관하세요.**

**스크립트에 토큰 추가 방법:**

1.  GitHub 저장소 페이지에서 🔑 **GitZip** 버튼을 클릭하여 설정 패널을 엽니다.
2.  복사해 둔 개인 접근 토큰(PAT)을 입력 필드에 붙여넣습니다. (비밀번호 형태처럼 보입니다)
3.  `Save Token` 버튼을 클릭합니다. "Token saved!" 메시지가 잠시 표시됩니다.

이제부터 스크립트는 저장된 토큰을 사용하여 GitHub API에 요청을 보냅니다.

## 주의사항

*   **GitHub UI 변경:** GitHub 웹사이트의 디자인이나 구조가 변경되면 스크립트가 버튼을 삽입하는 위치나 방식이 달라져 버튼이 보이지 않거나 제대로 작동하지 않을 수 있습니다. 이 경우 스크립트 내의 CSS 셀렉터 수정이 필요할 수 있습니다.
*   **대용량 저장소:** 매우 큰 폴더를 ZIP으로 압축하는 작업은 브라우저의 메모리와 CPU를 많이 사용할 수 있으며, 경우에 따라 브라우저 탭이 느려지거나 응답하지 않을 수 있습니다.
*   **토큰 보안:** 토큰은 유저스크립트 매니저의 저장 공간 (`GM_setValue`)에 로컬로 저장됩니다. 개인 PC에서는 비교적 안전하지만, 공용 PC 등에서는 사용에 주의하고 사용 후에는 토큰을 삭제하거나 만료시키는 것이 좋습니다.
*   **외부 라이브러리:** 이 스크립트는 작동을 위해 jQuery, JSZip, FileSaver.js 라이브러리를 사용하며, 이는 유저스크립트 매니저의 `@require` 기능을 통해 외부 CDN에서 로드됩니다. 네트워크 상태나 CDN 문제 발생 시 스크립트 작동에 영향을 줄 수 있습니다.

## 라이선스

*   MIT License (원본 GitZip 및 Bootstrap 기반)

## 원본 및 개조

*   이 유저스크립트는 KinoLien의 [GitZip 웹 애플리케이션](https://github.com/KinoLien/gitzip)을 기반으로 GitHub 페이지에 직접 적용 가능하도록 개조되었습니다.
