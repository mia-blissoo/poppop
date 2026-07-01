# POP POP · CORN-TROVERSY 랜딩페이지

핑크 VIP 파우치 디자인 기반 랜딩. 로고가 먼저 등장하고 팝콘/슈몬이 주변에 순차적으로 팝인한다.

## 집에서 이어서 작업하기

```bash
git clone https://github.com/mia-blissoo/poppop.git
cd poppop
python3 -m http.server 8000    # 미리보기: http://localhost:8000
```

편집 후:
```bash
git add -A && git commit -m "수정 내용" && git push
```
푸시하면 **GitHub Pages가 자동 배포** → 약 1분 뒤 반영: https://mia-blissoo.github.io/poppop/
(이 주소가 컨펌용 링크. noindex 처리돼 검색에는 안 잡힘)

## 구성

- `index.html` — 페이지 전체 (HTML + CSS + JS 한 파일). 아래 `ITEMS` 배열이 핵심.
- `assets/pk/` — 개별 벡터 에셋 (디자이너 제공)
  - `logo.svg` — POP POP CORN-TROVERSY 로고 (중앙, 맨 먼저 등장)
  - `popcon_01~13.svg` — 팝콘 13개
  - `shumon_01~03.svg` — 얼굴 슈몬 3종 (블러시 / 윙크 / 찡그림)
- `og.png` — 카톡/SNS 공유 썸네일 · `favicon-32.png` `apple-touch-icon.png` — 파비콘

## 위치·타이밍 수정 (index.html 안 `ITEMS` 배열)

각 줄이 에셋 하나. 좌표는 원본 아트 픽셀 기준(자동 매칭값), `d`는 등장 지연(초):
```js
{src:"pk/shumon_01.svg", cx:3160, cy:2275, w:984, d:0.42, fd:2.8, z:25},
//  파일            중심x   중심y   너비  등장시점  둥둥주기 레이어
{src:"pk/logo.svg", cx:2581, cy:4687, w:3187, d:.10, ..., z:40, logo:true}, // 로고=맨위, 먼저
```
- `d` 값을 바꾸면 등장 순서/타이밍 조절 (로고 `.10`이 가장 먼저, 팝콘들 `.42`부터 순차)
- `z` 는 레이어 순서 (팝콘 25 = 로고 40 뒤)
- 화면 아무 곳이나 클릭하면 애니메이션 재생

## 실제 라이브(poppop.com) 배포

poppop.com 은 별도로 **AWS(S3+CloudFront)** 로 배포한다 (GitHub Pages 아님).
사내 `~/claude-code/jisoo-landings/` 의 `deploy.sh poppop` 사용.
현재 poppop.com 은 **Coming Soon** 상태이고, 컨펌 완료 후 이 디자인으로 교체 예정.
