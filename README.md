# 제주 멍때리기 좋은 명소

제주대 바이브코딩 3일차 과제. 주제는 **제주 관광지·명소**(`jeju_spots.json`) 중 "멍때리기 좋은 곳"이에요.

## 구성
- `jeju_spots.json`: 68곳 (바다멍 17 · 오름멍 18 · 숲멍 10 · 물멍 9 · 문화멍 14)
- `index.html`: 사이트 본체 (day1·day2 강의 내용을 반영)
- `api/pixabay.js`: Pixabay 사진 검색용 서버리스 함수 (day2 방식)

## 강의 내용을 반영한 부분
| 강의 | 반영한 내용 |
| --- | --- |
| day2 레이아웃 | `grid-template-areas`로 header · nav · section · article · aside · footer 배치, 태블릿·모바일 반응형 |
| day2 탭 | 명소 목록 / 사진 검색 / 멍 뽑기 탭 (메뉴 링크와 방향키로 전환) |
| day2 Pixabay | 검색어로 사진을 0.5초마다 한 장씩 넘기는 슬라이드. API key는 서버 환경변수로만 사용 |
| day2 좋아요 | 버튼을 누를 때마다 숫자가 올라가는 카운터 |
| day1 뽑기 | "멍 뽑기" 버튼으로 장소 하나를 무작위로 뽑는 카드 |
| 애니메이션 | 숨 쉬는 원(`@keyframes breath`), 카드 등장(`rise`), 뽑기 카드(`pop`), 카운터(`bump`), 분류 막대(`transition`), 사진 전환(`fade`) |

## 데이터 구조
```json
{ "region": "제주특별자치도", "topic": "제주 멍때리기 좋은 명소",
  "items": [ { "name", "category", "area", "description", "score", "selected", "source" } ] }
```

## 어떻게 모았나
- 모든 항목의 `source`는 Visit Jeju(공식 관광 정보) 상세 페이지예요.
- `description`은 그 페이지 본문에 있는 내용만 바탕으로 썼고, 본문에 없는 숫자·유래·요금은 뺐어요.
- `area`는 페이지에 적힌 주소를 그대로 썼어요. 주소에 읍·면·동이 없으면 시 단위(또는 `제주도`)만 적었어요.
- `score`는 설명 속 '조용·한산·여유·잔잔' 같은 표현의 개수로 만든 임의 점수이고, `selected`는 제작자가 고른 값이에요. 실제 평점이 아니에요.
- 사진 검색은 장소 자체의 사진이 아니라 `jeju sea` 같은 분위기 사진을 보여 줘요.

## Pixabay 사진 검색 설정 (배포할 때)
API key는 코드나 저장소에 넣지 않아요. Vercel 프로젝트의 **Settings → Environment Variables**에
`PIXABAY_API_KEY`라는 이름으로 직접 등록하고 다시 배포해야 사진 탭이 동작해요.
등록하지 않으면 사진 탭에 안내 문구만 나오고 나머지 기능은 그대로 동작해요.

## 로컬에서 보기
`fetch`로 JSON을 읽기 때문에 서버로 열어야 해요. (사진 검색은 배포 환경에서만 동작)
```bash
python -m http.server 8000
```
