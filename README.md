# Portfolio

정적 HTML. 빌드 도구 없음. `index.html`을 브라우저로 열면 그대로 동작하고, GitHub Pages에도 그대로 올라간다.

## 구조

```
index.html        작업 인덱스. 분야가 뼈대, 연도는 서브필터
case.html         케이스 뷰. #cheongun 처럼 해시로 작업을 지정
tokens.css        색·타이포·간격 토큰 (두 페이지가 공유)

assets/
  cheongun/       청운문학도서관   p04–p18, eaves, motion-1·2
  turnbler/       턴블러          01–26, hero, motion
  clap/           클랩            ux-01–29 (UX/UI), brand-p42–p61 (브랜딩)
  wholesome/      홀썸라이프       p62–p76, motion-1·2·3
  moonlight/      문라이트 로고    intro-1·2·3, mockup-1, mockup-right
  signifier/      익스플레인 실험  group-a·b·c
  growth/         실시간 나눔 보드 board-1
  gimhae/         김해 건강도시    emblem, logo-old/new
  kkol/           꼴 레터링       a1–a3, b1–b3, c1–c3
  thonik/          토닉 강연 포스터 thonik-lecture-poster
  frankfurt/       아토 한국어 도서 ato-book-cover, ato-four-seasons-spreads
  rural/           금왕 관광 기획   finding-geumwang-map-thumbnail
  incoming/       ← 새 파일은 여기에 던져두면 정리해서 붙임

_archive/
  prototypes/     확정 전 시안 10개 + 그 시안들이 쓰던 자산 (그대로 열림)
  framer-raw/     Framer에서 받은 조각 자산 91개 (대부분 레이아웃 파편)
```

## 케이스 데이터

전부 `case.html` 안의 `WORK` 객체 하나에 들어 있다. 프레임은 네 형태를 받는다.

| 형태 | 뜻 |
|---|---|
| `"clap/ux-01.jpg"` | 이미지 한 장 |
| `"turnbler/motion.mp4"` | 영상. 자동재생·무음·루프 |
| `{row: ["a.mp4", "b.jpg"]}` | 좌우로 나란히. 간격 없이 한 장처럼 |
| `{fit: "gimhae/emblem.png"}` | 16:9 아닌 그림을 흰 프레임 안 가운데 |

한 작업이 관점을 여러 개 가질 수 있다.

```js
tracks: [
  { label: "Brand",  frames: [...] },
  { label: "Motion", lead: "이 트랙 위에 붙는 설명", frames: [...] }
]
```

탭을 바꿔도 **좌측 설명은 그대로 있다.** 바뀌는 건 릴뿐이다.

## 규칙

- **경로는 항상 상대.** `besoluble.github.io/<repo>/` 아래 놓이므로 `/assets/…` 는 404가 난다
- **프레임에 hover하면 우하단에 확대 아이콘이 뜬다.** 눌러 전체화면. 예전에는 파일 경로도 같이 떴는데, 사진마다 이름을 짓기 번거로워 아이콘만 남겼다
- **PDF에서 페이지를 뽑을 때는 RGB를 거쳐 크롭한다.** `pdftoppm` 이 윗줄에 흰 1px을 남기는데, JPEG는 크로마 서브샘플링 때문에 홀수 오프셋 크롭이 조용히 무시된다

```bash
pdftoppm -jpeg -scale-to-x 1920 -f N -l N in.pdf tmp
ffmpeg -i tmp-NN.jpg -vf "format=rgb24,crop=1920:1080:0:1" -q:v 2 out.jpg
```

## 남은 일

[PENDING.md](PENDING.md) 참고. 꼴·김해시·그로스 이미지가 들어오면 붙인다.
