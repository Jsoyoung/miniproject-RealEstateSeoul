# 부동산 적정가격책정 프로젝트 [부동산 트래커: 서울]
-------

## 기획 배경
- 기획시점일 기준 국토교통부와 한국부동산원이 발표하는 주택 거래량은 거래 당사자가 시·군·구청에 거래신고를 한 '신고일' 기준으로 수치가 집계되지만, 서울시가 서울부동산정보광장에 공개하는 통계는 매일 갱신되는 국토부 실거래가신고 자료를 '계약일' 기준으로 따로 분류한 수치로 제공되고 있습니다. 즉 아직 통계 정보에 혼란이 존재합니다. 
- 정확한 부동산 실거래가 자료 파악은 시장가격 형성에 필수적인 절차입니다.
- 따라서 지역별/건물용도별로 서울시 부동산 거래 동향을 파악할 수 있는 사이트에 대한 수요가 높아질 것으로 예상하게 되었습니다.
- 이러한 현황에 대한 자료조사를 바탕으로 사용자가 서울시의 전반적인 부동산 상황을 확인하고, 필요한 정보를 카테고리별로 분류해 확인할 수 있는 대시보드를 기획하게 되었습니다.


## 프로젝트 목적
- 본 프로젝트의 목적은 서울시 부동산 실거래가 데이터를 바탕으로 개발된 대시보드를 통해 부동산 가격을 책정하는 판매자가 유의미한 정보를 얻도록 하는 것입니다.
- 이를 위해 구/동 단위별 지역에 대한 거래금액, 월별 거래 건수 추이, 선택한 키워드별 세부 데이터, 타 법정동과의 비교 등의 기능을 제공합니다.


## 팀원 소개
- 팀장 [나한울](https://github.com/ghkstod/streamlit_minimi)
- 팀원 [김영환](https://github.com/younghwangit/mulcamp-mini-project)
- 팀원 [양인선](https://github.com/swflora/miniproject_2024) 
- 팀원 [이상훈](https://github.com/less927/mp240208) 
- 팀원 [정소영](https://github.com/Jsoyoung/miniproject-RealEstateSeoul.git)
- 팀원 [황유진](https://github.com/yellayujin/RealEstateTrackerSeoul)



## 본 프로젝트에서 사용한 주요 개발환경 요약
  + Programming Languages : Python(ver. 3.12.1)
  + Web Framework : Streamlit (ver. 1.31.0)

## 주요 라이브러리 버전
  + [requirements.txt](requirements.txt) 파일 참조

## 테스트 준비 및 방법
- 원격 저장소의 주소를 복사한 다음 로컬 환경에 복제합니다.

```bash
git clone https://github.com/Jsoyoung/miniproject-RealEstateSeoul.git
```

- 폴더 최상위 경로에서 가상환경을 설치합니다.

```bash
pip install virtualenv  #기존에 설치한 가상환경이 있다면 생략 가능
virtualenv venv
```

- 가상환경에 접속합니다.
```bash
source venv/Scripts/activate
```

- 라이브러리를 설치합니다.
```bash
pip install -r requirements.txt
```

- 일반적인 파이썬 `.py` 파일을 실행할 경우
```bash
python a.py
```

- Streamlit 파일 `.py` 파일을 실행할 경우
```bash
streamlit run app.py
```

## 데모페이지
- Streamlit에서 구현한 Demo는 다음과 같습니다.
  + [https://miniproject-realestateseoul.streamlit.app/](https://miniproject-realestateseoul.streamlit.app/)

### 주요 기능
 - 본 프로젝트에서 자체 개발 및 활용한 주요 메서드는 다음과 같습니다.

| Functions | Location | Description |
|---|---|---|
| main | app.py  | for deploy |
| load_data | data_collect.py | for loading dataset and creating new columns |
| theme | config.toml | for customizing theme |


### main()
- [app.py](app.py) 파일 참조
- 첫 페이지에서는 서울시 전체 부동산 실거래 데이터를 분석한 결과를 보여줍니다.
- 사이드바에서 원하는 자치구와 법정동을 선택하면 분석 페이지가 나타납니다. 선택 지역에 대한 데이터를 보여줍니다.
  - 분석 페이지 구성 : 한눈에 보기/키워드 상세 조회/타 법정동 비교
    - 한눈에 보기 : 거래금액 분석, 월별 거래 건수 추이, 건물용도별 거래건 시각화
    - 키워드 상세 조회 : 물건금액/건물유형/지번구분명/거래연도/건축연도 키워드 선택하여 데이터 조회 가능
    - 타 법정동 비교 : 선택한 지역과 동일한 자치구내 다른 동과 거래정보 비교(옵션: 건물 정보/건물 가격)
- `sgg_nm_sort` : 자치구
- `selected_sgg_nm` : 선택된 자치구
- `selected_bjdong_nm` : 선택된 법정동
- `filtered_data` : 선택된 자치구와 법정동 데이터

- 결과 이미지
<p align = "center" width = "150%">
  <img src = "./image/image1.png" width = "20%">
  <img src = "./image/image2.png" width = "20%">
  <img src = "./image/image3.png" width = "20%">
  <img src = "./image/image4.png" width = "20%">
</p>


### load_data():
- [data_collect.py](data_collect.py) 파일 참조
- `load_data()` 함수는 데이터를 불러와 전처리하는 함수입니다.
- `DEAL_YMD` 컬럼의 데이터를 문자열 데이터로 변환하여 형식을 통일했습니다.
- `BLDG_AREA` 데이터를 활용하여 `Pyeong` 데이터를 생성하고 `Range()` 함수를 통해 범주화했습니다.
- `df`: csv파일의 형태로 출력한 데이터셋
- `DEAL_YMD`: 계약일
- `Pyeong`: 평수 (BLDG_AREA/3.3)
- `Pyeong_range`: 평수를 10평 단위로 범주화


## 코드 에러 문의 
- 메뉴 `Issues`-`New Issues`-`메모 남기기`-`Submit new issue`
- email : sspkl124@gmail.com


## 발표자료 PDF 
 + [발표 PDF](발표자료.pdf)


## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
