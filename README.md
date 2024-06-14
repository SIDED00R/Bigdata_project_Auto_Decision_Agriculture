# 2024-1 Bigdata Project

토마토, 딸기가 자라는 최적화된 환경에 대한 분석 및 수확량에 따른 가격 예측

## Authors

- 홍민기 [@Mario76-soldier](https://github.com/Mario76-soldier)
- 우성현 [@samuel426](https://github.com/samuel426)
- 이재호 [@SIDED00R](https://github.com/SIDED00R)
- JIN LI [@LJ2021105555](https://github.com/LJ2021105555)
- 이의준 [@Euijune](https://github.com/Euijune)

## Data

[스마트팜 빅데이터 플랫폼](https://www.n-farm.kr/dataproduct?page=0&sort=issued&limit=15&category=[%2233%22])
해당 사이트에서 딸기, 토마토 작물에 대한 데이터를 660MB 확보하였습니다.

나머지 데이터 90MB는
[도매시장 통합 홈페이지](https://at.agromarket.kr/domeinfo/smallTrade.do) 에서
Crwaling을 통해 가져왔습니다.

### Crwaling

python 크롬 웹드라이버 Selenium을 이용하여 아래 사이트에서 데이터를 가져왔습니다.
[도매시장 통합 홈페이지](https://at.agromarket.kr/domeinfo/smallTrade.do)
2019~2023년 도매시장 거래내역 데이터를 가져왔습니다.

### Analyze

Spark를 사용하여 분석을 진행하였습니다.

## 데이터 통합

### 도매시장 거래내역 파일 통합

전체 엑셀 파일들 합치기
토마토, 딸기에 해당하지 않는 작물 데이터 행 제외하기
1kg당 N원 형식의 새로운 열을 추가해서 데이터 삽입

### 작물별 데이터 통합

분리되어 저장된 딸기, 토마토 데이터 종목별로 행과 열 맞춰서 합치기

### 작물별 데이터 통합

1. 딸기 총 96470줄 데이터 날짜, 범주, 종류, 품목, 시장, 법인, 무게, 가격, 킬로그램당 가격 포함 
2. 토마토 총 90899줄 데이터날짜, 범주, 종류, 품목, 시장, 법인, 무게, 가격, 킬로그램당 가격 포함 
3. 데이터 병합 총 187369줄 데이터날짜, 범주, 종류, 품목, 시장, 법인, 무게, 가격, 킬로그램당 가격 포함

## 데이터 분석

### Key Column

**Input environment column :**
PFBS_NTRO_CBDX_CTRN 관측지점실내이산화탄소농도
EXTN_TPRT 외부온도 
STRTN_WATER 포화수분(포화 상태일 때 수분량)
WATER_LACK_VL 수분부족값(포화에서 얼마나 못미치는지)
EXTN_SRQT 외부일사량(누적광량으로 대체)
EXTN_ACCMLT_QOFLG 외부누적광량
NTSLT_SPL_PH_LVL 양액공급산도레벨
NTSLT_SPL_ELCDT 양액공급전기전도도
AVE_INNER_TPRT_1_2 평균내부온도
AVE_INNER_HMDT_1_2 평균내부습도

**Output column :**
- Tomato 
    BLMNG_CLUSTER 개화군
    FRT_LENGTH 과일길이
    YIELD_CLUSTER 수확군
    FRST_TREE_CNT 착과수
    FWRCT_HGHT 화방높이
    LAST_FWRCT_NO 최종화방번호
    FRST_CLUSTER 착과군
    FLWR_CNT 꽃수
    YIELD_CNT 수확수
    STEM_THNS 줄기굵기
    FRT_WDTH 과일폭
    FRT_WT 과일무게
    LEAF_LNGTH 잎 길이
    LEAF_WDTH 엽폭
    LEAF_CNT 엽수
    GRTH_LNGTH 생장길이
    PLT_LNGTH 식물길이

- Strawberry
    SHPMN_QTY 출하량
    PH_LVL 산도레벨
    SGCN 당도
    FRT_WDTH 과폭
    FRT_LNGTH 과일길이
    FRST_RATE 착과비율
    FRT_WT_WDTH_RATE 과중과폭비
    SGCN_PH_RATE 당도산도비
    FRT_WT 과일무게
    FRST_TREE_CNT 착과수
    NOT_BLMNG_CNT 미개화수
    BLMNG_CNT 개화수
    BLPRD_TPCD 개화기 구분코드
    FLWRCLSTR_FLWR_NBR 화방꽃수
    FLWRCLSTR_BDDG_TPCD 화방출뢰기구분코드
    GRTH_SPD 생장속도
    LEAF_LNGTH_LEAF_WDTH_RATE 엽장엽폭비
    ACCMLT_LEAF_CNT 누적엽수
    LEAF_CNT_INCR_SPD 엽수증가속도
    AXLRBD_OCRN_TPCD 액아발생구분코드
    GRTH_LNGTH 생장길이
    CRN_DIAM 관부직경
    LEAF_CNT 엽수
    PTL_LNGTH 엽병장
    LEAF_WDTH 엽폭
    LEAF_LNGTH 엽장
    PLT_LNGTH 식물길이



### Gaussian
**Use Scoring**
- To predict similar environment status, calculate some env factors with weight, gaussian method.
**Why gaussian?**
- environment factors follows the gaussian distribution, and all of that factors need appropriate amount, neither too much nor too little.
**Why did we choose this weight?**
- Gaussian distribution mean probability normalization to 1
  - To calculate all of factors under equal conditions


## Visualization

Django의 프레임워크를 사용하였습니다.

![readme](https://github.com/philip-lee-khu/2024-BIGDATA-PROJECT-4/assets/49184956/684d1e76-11d4-4050-951c-4c6bfb735481)


## Demo
데모 실행 방법

```
ssh -L 50077:localhost:50077 hadoop@133.186.215.216
cd django
python manage.py runserver 50077
```

## 프로젝트 의의

이번 프로젝트를 통해 체계적인 데이터 수집 및 분석을 하였고 스마트 팜의 관리 및 작물 생산성을 최적화하는 작업을 거쳤습니다.
매주 Scrum 회의를 통해 부원들이 합리적인 분업과 협력을 할 수 있었고 초기에 세웠던 프로젝트 목표를 성공적으로 달성하였습니다.
752MB 가량의 유효한 데이터를 수집하고 통합했으며 그에 맞는 spark를 사용한 분석을 진행하였습니다.
Django를 이용하여 홈페이지에 현재 상황을 입력하면 예상 수확량과 그에 따른 매출을 예측해주는 api를 개발하였습니다.

### 향후 전망:

데이터 수집 및 분석 방법을 지속적으로 최적화하여 데이터 정밀도 및 분석 효율성을 향상합니다.
다양한 작물 종류로 확장하여 스마트 농장의 생산 관리의 범용성을 넓힙니다.
서로 다른 환경 변수가 작물의 생장에 미치는 영향을 세분화하여 연구하고 정확도가 높아진 농장 관리 시스템을 개발합니다.
