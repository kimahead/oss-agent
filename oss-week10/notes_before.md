# oss-week09/tools.py 분석 노트

## 파일 개요

`tools.py`는 **영화진흥위원회(KOBIS) 오픈 API**를 사용해 박스오피스 정보를 가져오는 도구 모음이다.

- 사용 라이브러리: `requests` (HTTP 요청)
- API 키: `secret.py` 파일의 `API_KEY`에서 불러온다 (저장소에는 포함되지 않음)
- 요청 주소(`BASE_URL`): KOBIS 일별 박스오피스 조회 API
  `https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`

## 함수 목록

현재 파일에는 함수가 **1개** 있다.

### `get_bpxoffice_rank_1(date)`

특정 날짜의 박스오피스 **1위 영화 제목**을 돌려준다.

| 구분 | 내용 |
|------|------|
| 매개변수 | `date` (문자열) — 8자리 날짜, 예: `"20260824"` |
| 반환값 | (문자열) 1위 영화 제목, 예: `"오디세이"` |

**동작 순서**

1. `key`(API 키)와 `targetDt`(날짜)를 요청 파라미터로 만든다.
2. `requests.get()`으로 KOBIS API에 요청한다 (타임아웃 10초).
3. 응답을 JSON으로 변환한다.
4. `boxOfficeResult` → `dailyBoxOfficeList`에서 영화 목록을 꺼낸다.
5. 목록의 첫 번째 항목(1위)의 `movieNm`(영화 이름)을 반환한다.

## 참고 사항

- 함수 이름의 `bpxoffice`는 `boxoffice`의 오타로 보인다.
- 독스트링에는 매개변수 이름이 `data`로 적혀 있지만, 실제 매개변수 이름은 `date`이다.
- 오류 처리가 없다. API 키가 잘못되었거나, 날짜 형식이 틀렸거나, 결과 목록이 비어 있으면 `KeyError`나 `IndexError`가 날 수 있다.
