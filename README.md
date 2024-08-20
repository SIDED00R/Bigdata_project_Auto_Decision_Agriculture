# 2024-1 Bigdata Project

Analysis of the optimized environment in which tomatoes and strawberries grow and price prediction based on yield

## Authors

- 홍민기 [@Mario76-soldier](https://github.com/Mario76-soldier)
- 우성현 [@samuel426](https://github.com/samuel426)
- 이재호 [@SIDED00R](https://github.com/SIDED00R)
- JIN LI [@LJ2021105555](https://github.com/LJ2021105555)
- 이의준 [@Euijune](https://github.com/Euijune)

## Data

[스마트팜 빅데이터 플랫폼](https://www.n-farm.kr/dataproduct?page=0&sort=issued&limit=15&category=[%2233%22])
660MB of data on strawberry and tomato crops was obtained from the site.

The remaining 90MB of data
[도매시장 통합 홈페이지](https://at.agromarket.kr/domeinfo/smallTrade.do) 
Imported via Crwaling.

### Crwaling

Data was retrieved from the following site using python chrome web driver Selenium.
[도매시장 통합 홈페이지](https://at.agromarket.kr/domeinfo/smallTrade.do)
Brought data on wholesale market transaction details from 2019 to 2023.

### Analyze

Analysis was performed using Spark.

## Data Consolidation

### Consolidated wholesale market transaction details file

Combining all Excel files
Exclude crop data rows that do not correspond to tomatoes and strawberries
Insert data by adding a new column in N-won format per kg

### Data consolidation by crop

Combine separated and stored strawberry and tomato data by row and column

### Data consolidation by crop

1. Strawberry data date, category, type, item, market, corporation, weight, price, price per kilogram included
2. Total 90899 lines of tomato data date, category, type, item, market, corporation, weight, price, price per kilogram
3. Merge data total 187369 lines, including data date, category, type, item, market, corporation, weight, price, price per kilogram

## Data Analysis

### Key Column

**Input environment column :**:
- PFBS_NTRO_CBDX_CTRN: Observation Point Indoor Carbon Dioxide Concentration
- EXTN_TPRT: External Temperature 
- STRTN_WATER: saturated moisture (water content when saturated)
- WATER_LACK_VL: underwater value (how much less than saturation)
- EXTN_SRQT: External Daylight (Replaced by Accumulated Light)
- EXTN_ACCMLT_QOFLG: External Accumulated Light Volume
- NTSLT_SPL_PH_LVL: Positive Solution Supply Acid Level
- NTSLT_SPL_ELCDT: Positive Liquid Supply Electrical Conductivity
- AVE_INNER_TPRT_1_2: Average internal temperature
- AVE_INNER_HMDT_1_2: Average Internal Humidity

**Output column :**:
- Tomato
  - BLMNG_CLUSTER: Blooming Group
  - FRT_LENGTH: Fruit Length
  - YIELD_CLUSTER: Harvest Group
  - FRST_TREE_CNT: Accumulation
  - FWRCT_HGHT: height of the room
  - LAST_FWRCT_NO: Final Picture Number
  - FRST_CLUSTER: Arrival Group
  - FLWR_CNT: Flower Water
  - YIELD_CNT: Harvesting Water
  - STEM_THNS: Stem Thickness
  - FRT_WDTH: Fruit Width
  - FRT_WT: Fruit Weight
  - LEAF_LNGTH: Leaf Length
  - LEAF_WDTH: leaf width
  - LEAF_CNT: Foliage
  - GRTH_LNGTH: Growth Length
  - PLT_LNGTH: Plant Length

- Strawberry
  - SHPMN_QTY: Shipments
  - PH_LVL: acidity level
  - SGCN sugar: content
  - FRT_WDTH: overwidth
  - FRT_LNGTH: Fruit Length
  - FRST_RATE: attachment ratio
  - FRT_WT_WDTH_RATE: Overweight and Overweight
  - SGCN_PH_RATE: sugar content acidity ratio
  - FRT_WT Fruit: Weight
  - FRST_TREE_CNT: Accumulation
  - NOT_BLMNG_CNT: Unopened Water
  - BLMNG_CNT: Blooming Water
  - BLPRD_TPCD: flowering period classification code
  - FLWRCLSTR_FLWR_NBR: Flower Water
  - FLWRCLSTR_BDDG_TPCD: Fire Extinguisher Classification Code
  - GRTH_SPD: Growth Rate
  - LEAF_LNGTH_LEAF_WDTH_RATE: Leaf width ratio
  - ACCMLT_LEAF_CNT: cumulative foliage
  - LEAF_CNT_INCR_SPD: Foliage Acceleration
  - AXLRBD_OCRN_TPCD: Grooming Classification Code
  - GRTH_LNGTH: Growth Length
  - CRN_DIAM: pipe diameter
  - LEAF_CNT: Foliage
  - PTL_LNGTH: Sargeant
  - LEAF_WDTH: leaf width
  - LEAF_LNGTH: Chapter 11
  - PLT_LNGTH: Plant Length



### Gaussian
**Use Scoring**
- To predict similar environment status, calculate some env factors with weight, gaussian method.

**Why gaussian?**
- environment factors follows the gaussian distribution, and all of that factors need appropriate amount, neither too much nor too little.

**Why did we choose this weight?**
- Gaussian distribution mean probability normalization to 1
  - To calculate all of factors under equal conditions


## Visualization

Django's framework was used.

![readme](https://github.com/philip-lee-khu/2024-BIGDATA-PROJECT-4/assets/49184956/684d1e76-11d4-4050-951c-4c6bfb735481)


## Demo

```
ssh -L 50077:localhost:50077 hadoop@133.186.215.216
cd django
python manage.py runserver 50077
```

## Project Significance

Through this project, we systematically collected and analyzed data and went through the management of smart farms and optimization of crop productivity.
Through weekly Scrum meetings, members were able to work together with reasonable division of labor and successfully achieved the project objectives they had initially set.
About 752MB of valid data was collected and integrated, and analysis was conducted using the appropriate spark.
Using Django, we developed an api that predicts the expected yield and sales accordingly by entering the current situation on the homepage.

### Forward-looking:

Improve data precision and analysis efficiency by continuously optimizing data collection and analysis methods.
Expand to a variety of crop types to expand the versatility of production management on smart farms.
We study the effects of different environmental variables on crop growth by subdividing them and develop a farm management system with increased accuracy.
