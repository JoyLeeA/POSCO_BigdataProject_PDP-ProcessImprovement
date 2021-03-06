# POSCO_BigdataProject_PDP-ProcessImprovement
 포스코 청년 AI Bigdata에서 진행한 빅데이터 프로젝트
 

## PDP 공정 프로세스 개선
- 보통 5%미만인 명점 불량률 수준이 10% 수준으로 급증했고, 최근에는 12% 수준이 되었다.
- 명점 불량 1%는 생산량에 따른 편차는 있지만 약 10억 원의 품질 비용이 요구된다.
- 명점 불량 문제를 해결하고자, 불량 발생의 근본원인을 도출하고 신속한 개선조치 방안을 수립
 하고자 한다.

## 개선 계획
1. 불량 발생 영향의 분석과 개선
- 제조 과정에서 발생하는 불량은 설비 기인성이 매우 높음
- 공정 설비, 공정 작업시간의 차이에 의한 불량 발생 가능성 확인 및 개선 필요

2. 핵심 근본 원인자 및 최적 조건 도출
- 불량은 공정의 설비 작업 조건에 따라 많은 영향을 받음
- 다양한 모델 활용 및 기술적인 검토를 거쳐 불량 영향 인자 도출 및 종합적인 최적조건 도출 가능

3. 최적 설비조합 및 작업 조건
- 설비 진행 결로에 따른 불량률 발생 차이의 확인
- 최적/최악 설비 경로 분석
- 전 공정의 진행 설비 및 작업 조건에 따른 후 공정의 불량률 예측과 최적 설비 조합 및 작업 조건

수행 단계: 불량 패턴 분석 -> 유의차 분석 -> 영향인자 선정 -> 경로 탐색 -> 파라미터 분석

## 데이터 셋
[Raw Data(원천 데이터)]
- MFG_MACHINE: 공정이 이루어지는 설비 (ex> 1호기, 2호기) 
- MFG_PROCESS: 공정이 이루어지는 조건 (ex> 온도, 배기량)
- MFG_TAT: 공정별 소요 시간

[전처리 데이터]
- MFG_MACHINE_NULL_COL_OUT: MFG_MACHINE에서 결측치(NULL)와 불필요한 열(COL), 
				 그리고, 이상치(OUT)을 제거한 데이터
- MFG_PROCESS_NULL_COL_OUT: MFG_PROCESS 에서 결측치(NULL)와 불필요한 열(COL), 
				 그리고, 이상치(OUT)을 제거한 데이터
- MFG_TAT_NULL_COL_OUT: MFG_TAT에서 결측치(NULL)와 불필요한 열(COL), 
				 그리고, 이상치(OUT)을 제거한 데이터

[MERGE 데이터]
MFG_PROCESS_NULL_COL_OUT 과 MFG_TAT_NULL_COL_OUT 파일의 모든 열을 결합하고,
같은 LOT_ID값을 갖는 행끼리 결합한 데이터. (ex> Lot101을 가진 값 20개를 한개로 결합)
- MERGE_STD: LOT_ID 결합 시 , 표준 편차를 기준으로 결합한 파일
- MERGE_MEAN: LOT_ID 결합 시 , 평균을 기준으로 결합한 파일

