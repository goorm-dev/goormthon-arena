# 구름톤 아레나 2026 소개 사이트

구름톤 아레나 전국 프로그래밍 챔피언십(2026.11.21) 참가자 모집 페이지입니다.
빌드 도구 없이 정적 파일만으로 동작합니다.

## 구조

```
index.html            # 페이지 전체 (HTML + CSS + JS 한 파일)
assets/
  goormthon-arena-logo.webp
  lang-*.svg          # C / C++ / Java / Python 아이콘
  logos/lg01~lg52.webp # 고객사 로고 (무한 스크롤용, 배경 투명)
  proctor-*.webp      # 응시 환경 화면
  photo-*.webp        # 개최 이력 사진
  report-preview.webp # 역량 리포트 미리보기
  apply-qr.png        # 참가 신청 QR
```

외부 의존성은 Pretendard 웹폰트(jsDelivr CDN) 하나뿐입니다.

## 로컬 확인

```bash
python3 -m http.server 8080
# 또는
npx serve .
```

`index.html`을 브라우저로 바로 열어도 되지만, 정적 서버로 띄우는 쪽이 실제 배포와 같습니다.

## 컨테이너 배포

```bash
docker build -t goormthon-arena .
docker run -p 8080:80 goormthon-arena
```

nginx 이미지에 정적 파일만 복사하는 구성이라, 컨테이너 안에서 바로 실행해도 되고
`python3 -m http.server`로 포트만 열어도 동일하게 동작합니다.

## GitHub Pages로 바로 띄우려면

1. 이 디렉터리를 저장소 루트로 푸시
2. Settings → Pages → Source를 `main` 브랜치 `/ (root)`로 지정

빌드 단계가 없어 별도 워크플로가 필요 없습니다.

## 수정이 잦은 곳

- **참가 신청 링크**: `index.html`에서 `goor.me/qFQjM` 검색 (헤더·히어로·신청 카드 3곳)
- **대회 일시/카운트다운**: 하단 스크립트의 `2026-11-21T14:00:00+09:00`
- **채용 평가 추이 차트**: `class="chart"` SVG의 `polyline points` 세 줄
  (2021~2025 값은 제안서 그래프에서 읽은 추정치, 2026년 70/20/10%만 확정치)
- **문의처**: 푸터 및 신청 카드의 `platform-biz-division@goorm.io`
