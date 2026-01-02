# 블로그 개선 및 수정 사항 정리 (Fix Log)

Chirpy 테마 기반의 Jekyll 블로그를 최적화하고 사용자 경험(UI/UX) 및 유지보수성을 높이기 위해 수행한 작업 내용입니다.

## 1. 코드 구조 및 유지보수 (Code Maintenance)
- **`_config.yml` 최적화**:
    - 불필요한 Analytics 및 Webmaster Verification 플레이스홀더 제거.
    - 네이버 서치 콘솔 인증(`naver`) 항목 추가.
    - **PWA 알림 수정**: "새 버전의 콘텐츠가 있습니다" 알림이 무한 반복되는 문제를 해결하기 위해 `pwa.cache.deny_paths`에 사이트 URL 추가.
- **불필요 파일 제거**:
    - 레포지토리 관리에 불필요한 `.devcontainer`, `.husky`, `.vscode`, `docs`, `tools` 디렉토리 및 관련 설정 파일(`.gitattributes`, `.gitmodules`, `.markdownlint.json` 등)을 제거하여 빌드 위험과 관리 부담을 줄임.
- **테마 커스터마이징 가이드 준수**:
    - Chirpy 테마의 권장 방식에 따라 `assets/css/jekyll-theme-chirpy.scss`와 `_sass/custom/` 폴더를 활용하여 스타일을 오버라이드함.

## 2. UI/UX 및 디자인 개선 (Design & UX)
- **홈 화면(`index.html`) 레이아웃 고도화**:
    - **Education, Research Experience, Publications, Award** 섹션을 Bootstrap Card 스타일로 재구성.
    - 카드에 그림자 효과(`shadow-sm`)와 호버 애니메이션을 추가하여 시각적 구분감 강화.
    - FontAwesome 아이콘을 활용하여 가독성 향상.
- **색상 대비 및 가독성 향상**:
    - **다크/라이트 모드 최적화**: `_sass/themes/`의 변수를 수정하여 텍스트와 배경 간의 대비를 WCAG 기준에 맞게 높임.
    - **다크 모드 버그 수정**: Award 섹션 등 일부 카드 내부 배경이 어두운 테마에서 올바르게 표시되지 않던 문제를 CSS 명시도 조정을 통해 해결.
- **반응형 대응**:
    - 코드 블록에 가로 스크롤(`overflow-x: auto`)을 허용하여 모바일 기기에서 레이아웃이 깨지지 않도록 수정.
    - 모든 이미지에 `max-width: 100%`를 적용하여 반응형 대응.

## 3. 콘텐츠 및 SEO 최적화 (Content & SEO)
- **About 페이지(`_tabs/about.md`) 업데이트**:
    - 기본 메시지를 제거하고, 국문/영문 혼용으로 본인 소개, 연구 관심사, 학력, 경력 및 연락처 정보를 전문적으로 작성.
- **카테고리 및 태그 정리**:
    - **Paper Review 카테고리 노출 수정**: 샘플 포스트의 카테고리명을 `Paper Review`로 통일하여 카테고리 탭에서 정상적으로 분류되도록 수정.
    - 각 포스트에 SEO를 위한 `description` 메타데이터 추가.
- **샘플 포스트 생성**:
    - 블로그의 각 구획(Notice, Paper Review, Life, Study)이 비어 보이지 않도록 각각의 성격에 맞는 샘플 포스트를 생성.

## 4. 성능 최적화 (Performance)
- **CDN 교체**:
    - 국내 접속 속도와 안정성을 고려하여 정적 자산(JS/CSS 라이브러리)의 출처를 `jsDelivr`에서 **`cdnjs`**로 변경 (`_data/origin/cors.yml`).
- **이미지 최적화**:
    - 홈 화면의 이미지들에 `loading="lazy"` 속성을 확인 및 적용하여 초기 로딩 속도 개선.

## 5. 미적용 및 추후 권장 사항 (Pending / Not Implemented)
요청 사항 중 기술적 제약이나 사용자 선택이 필요한 부분은 아래와 같이 정리하였습니다.

- **이미지 포맷 변환 (WebP/AVIF)**: 기존 이미지들을 WebP나 AVIF로 변환하는 작업은 별도의 이미지 처리 도구가 필요하여 수행하지 않았습니다. 향후 새 이미지를 업로드할 때 해당 포맷을 사용하시길 권장합니다.
- **LQIP (Low Quality Image Placeholder)**: 이미지 로딩 전 저해상도 미리보기를 보여주는 기능은 각 이미지마다 Base64 문자열을 생성해야 하므로 자동화하지 않았습니다.
- **Gem 기반 테마 완전 전환**: 현재 블로그는 커스터마이징의 편의를 위해 테마 소스 파일이 포함된 'Starter' 형태를 유지하고 있습니다. 순수 Gem 의존 방식으로 전환할 경우 현재의 커스텀 레이아웃(`index.html` 등)을 다시 이식해야 하므로 유지하였습니다.
- **정기적 글쓰기 및 템플릿 운영**: 논문 리뷰 등 정기적인 콘텐츠 업로드는 사용자의 운영 영역이므로, 제공된 샘플 포스트 형식을 참고하여 꾸준히 관리하시길 권장합니다.
- **이미지 대체 텍스트(alt text) 일괄 적용**: 기존 포스트의 이미지들에 대한 구체적인 대체 텍스트는 각 이미지의 내용을 정확히 파악해야 하므로, 홈 화면 레이아웃을 제외한 개별 포스트 내부 이미지는 수동 확인이 필요합니다.
- **영문 Slug(permalink) 일괄 적용**: 한글 제목 포스트의 URL 가독성을 위한 영문 slug 지정은 각 포스트의 주제에 맞춰 수동으로 `slug: 영문명`을 추가하시길 권장합니다. (예: `2025-06-25-award-ksbe.md` 등)

## 6. 빌드 오류 수정 (Build Fix)
- **GitHub Actions 서브모듈 오류 해결**: `assets/lib` 경로에 잘못 포함되어 있던 서브모듈 참조(`.git` 파일)를 제거하여 GitHub Actions 빌드 시 발생하던 `fatal: No url found for submodule path 'assets/lib' in .gitmodules` 오류를 해결하였습니다.

---
**Woo SungHyeon (우성현)**  
*Computer Science and Engineering, Dong-A University*
