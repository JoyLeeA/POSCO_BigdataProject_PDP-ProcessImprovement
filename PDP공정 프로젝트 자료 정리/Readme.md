# PDF 공정 프로젝트 자료 정리

## 데이터
	->Another
	DE.csv: 필요한 데이터만 합쳐서 사용
	mc.csv: MFG_MACHINE_NULL_COL_OUT.csv 와 동일
	pro.csv: MFG_PROCESS_NULL_COL_OUT.csv 와 동일

	->기본 데이터(가공전): 처음에 받은 그대로의 파일
	MFG_MACHINE.csv: 처음에 받은 머신 파일
	MFG_PROCESS.csv: 처음에 받은 프로세스 파일
	MFG_TAT.csv: 처음에 받은 타임 파일
	MFG_PROCESS_DIELEC.csv: 다른 열을 제거하고 DIELEC 열만 남긴 것(결측치 처리는 안됨)
	
	->결측치 제거 데이터: 결측치만 제거한 파일
	MFG_MACHINE_NULL.csv: 기본 데이터(가공전)에서 결측치만 처리한 머신 파일
	MFG_PROCESS_NULL.csv: 기본 데이터(가공전)에서 결측치만 처리한 프로세스 파일
	MFG_TAT_NULL.csv: 기본 데이터(가공전)에서 결측치만 처리한 타임 파일

	->결측치 + 불필요한 열 제거 데이터
	MFG_MACHINE_NULL_COL.csv: 결측치 제거 데이터에서 불필요한 열을 제거한 머신 파일
	MFG_PROCESS_NULL_COL.csv: 결측치 제거 데이터에서 불필요한 열을 제거한 프로세스 파일
	MFG_TAT_NULL_COL.csv: 결측치 제거 데이터에서 불필요한 열을 제거한 타임 파일

	->PDP이론에 따른 이상치 제거 데이터
	MFG_MACHINE_NULL_COL_OUT.csv: 결측치 + 불필요한 열 제거 데이터에서 이상치를 제거한 머신 파일
	MFG_PROCESS_NULL_COL_OUT.csv: 결측치 + 불필요한 열 제거 데이터에서 이상치를 제거한 프로세스 파일
	MFG_TATNULL_COL_OUT.csv: 결측치 + 불필요한 열 제거 데이터에서 이상치를 제거한 타임 파일
	*tat_4dielec_fire.csv: (TAT_4DIELEC_FIRE변수 - TAT_4DIELEC_FIRE변수의 평균) / TAT_4DIELEC_FIRE변수의 평균 * 100 이 4 이상인 것들
	삭제한 이상치 정보: 삭제한 이상치의 정보를 담은 이미지 파일

	->LOT 단위로 묶은 데이터 (결측치 + 불필요한 열 제거 데이터 기반)
	MFG_PROCESS_NULL_COL_OUT_LOT.csv: PDP이론에 따른 이상치 제거 데이터를 로트 단위로 묶은 프로세스 파일(평균으로)
	MFG_TAT_NULL_COL_OUT_LOT.csv: PDP이론에 따른 이상치 제거 데이터를 로트 단위로 묶은 타임 파일(평균으로)

	->MERGE 데이터
	MERGE_STD.csv: 로트별로 갖고 있는 값을 표준 편차 낸 것
	MERGE_STD+MEAN.csv: 로트별로 갖고 있는 값을 표준 편차 값 내고, 뒷 부분에는 평균 값을 낸 것
	MERGE_FULL.csv: 기본 데이터(가공전)의 머신, 프로세스, 타임 파일을 한 개로 병합한 것
	MFG_MERGE.csv: 중요 변수만 묶고 나머지 컬럼은 삭제 (처음 데이터 상태에서)

## PDP공정 부가 정보
	제조_평판TV(PDP) 경쟁력 향상_Data Dictionary.xlsx : 데이터에 대한 설명
	GI@PDP공정순서-참조용.xlsx: 공정 순서에 대한 설명

## CODE
후진제거법 코드: 말 그래도 후진제거법 코드임
scale 점수 코드: 말 그대로 스케일 점수 코드임
scale 후진제거법 코드: 말그래로 스케일 후진제거법 코드임

	->RAW Data 이용 분석: 기본 데이터(가공전)으로 분석한 코드 모음
	PROCESS.ipynb - 기본 PROCESS.csv로 히스토그램 형식 분석
	Profiling MERGE.ipynb: Machine + TAT & Process + TAT 병합 후, 프로파일링 하는 코드
	Profiling MFG-MACHINE.ipynb: Machine 프로파일링 코드
	Profiling MFG-PROCESS.ipynb:  Process 프로파일링 코드
	Profiling MFG-TAT.ipynb: TAT 프로파일링 코드
	TAT.ipynb : 기본 TAT.csv로 히스토그램 + 상관 계수 분석
	TAT 공정별 소요시간 merge.ipynb: 공정별 소요시간(이름이 같은 과정)을 합치고, 이를 트리 분석한 코드 - TAT 공정별 소요시간 merge.dot 산출

	->MERGE DATA 이용 분석: MERGE 데이터로 분석한 코드 모음
	MERGE_STD - 회귀 분석.ipynb: MERGE_STD.csv를 활용하여 변수 상관 관계 분석, 회귀 분석 실행, 후진 제거법 실행
	MERGE_FULL - StdMerge.ipynb: MERGE_FULL.csv를 활용하여 LOT_ID를 기준으로 데이터를 병합(기준은 편차)

	->최종 Data이용 분석: PDP이론에 따른 이상치 제거 데이터로 분석한 코드 모음
	빅데이터 프로젝트(PDP) - 나무기본.ipynb :트리 방식으로 변수 중요도 분석한 코드
	빅데이터 프로젝트(PDP) - 로지스틱_수정본.ipynb : 로지스틱 방식으로 변수 중요도 분석한 코드
	빅데이터 프로젝트(PDP) - PCA.ipynb : 주성분 분석 방식으로 변수 중요도 분석한 코드
	설비와 작업시간의 관계.ipynb: Machine과 TAT로 AG_RTD호기 간 작업시간 편차
				   	MC_4DIELEC_1FIRE호기 간 작업시간 편차
				   	MC_6PHOS_2G_2DRY호기 간 작업시간 편차를 분석한 코드
	tat_4dielec_fire.csv: tat_4dielec변수와 tat_4dielec_fire.csv변수의 평균을 비교함
	[로지스틱] PROCESS Vital Few.ipynb: MFG_PROCESS_NULL_COL_OUT.csv를 이용한 로지스틱 회귀
	BUS DEVELOP 호기와 작업소요시간.ipynb: _OUT 데이터 세개를 활용하여 호기와 작업 소요시간 분석(평균과 편차로서)
	*MACHINE_카이제곱.ipynb: 트리로 분석했던 머신 변수를 카이제곱으로 검정
	공정작업시간의 편차와 불량.ipynb: 
	빅데이터 프로젝트(PDP) - 로지스틱.ipynb: OUT 데이터 세개랄 활용하여 로지스틱 회귀 분석(노스케일/ 스케일)
	공정작업시간의 편차와 불량.ipynb: tat_4dielec_fire.csv를 뽑아내는 코드
	빅데이터 프로젝트(PDP) - 유전체_로지스틱.ipynb: 유전체 변수만 뽑아내어, 로지스틱 회귀 분석(노스케일/스케일)
	DT 모델링.ipynb: AG_FTD의 설비 작업 조건 주요 변수 도출 - A.dot 산출
				DIELEC_FIRE의 설비 작업 조건 주요 변수 도출 -B.dot  산출
				BLACK_RTD의 설비 작업 조건 주요 변수 도출 - block.dot 산출 (중복)
				BUS_DEVELOP의 설비 작업 조건 주요 변수 도출 - BUS_DEVELOP.dot 산출
				BUS_FIRE의 설비 작업 조건 주요 변수 도출 - BUS_FIRE.dot 산출(중복)
				PHOS_R_DRY의 설비 작업 조건 주요 변수 도출 - PHOS_R_DRY.dot 산출 (중복)
				PHOS_G_DRY의 설비 작업 조건 주요 변수 도출 - PHOS_G_DRY.dot 산출(중복)
				PHOS_FIRE의 설비 작업 조건 주요 변수 도출 - PHOS_FIRE.dot 산출
				이 모든 것들은 의사결정나무 방식으로 분석이 진행됨.

	RF 모델링.ipynb: AG_RTD의 설비 작업 조건 주요 변수 도출 - rf_af_rtd.dot 산출
				BLACK_RTD의 설비 작업 조건 주요 변수 도출 - black.dot 산출(중복)
				BUS_FIRE의 설비 작업 조건 주요 변수 도출 -BUS_FIRE.dot 산출(중복)
				PHOS_R_DRY의 설비 작업 조건 주요 변수 도출 -  PHOS_R_DRY.dot 산출 (중복)
				PHOS_G_DRY의 설비 작업 조건 주요 변수 도출 - PHOS_G_DRY.dot 산출 (중복)
				PHOS설비 작업 조건 주요 변수 도출 - PHOS.dot
	유전체 배기량:ipynb: 배기량과 배기온도 간의 관계 분석 (상관계수 이용)

## CODE 산출물
	->DT 모델링 산출물: DT모델링.ipynb에서 산출된 산출물 모음
	->RF 모델링 산출물: RF모델링.ipynb에서 산출된 산출물 모음
TAT 공정별 소요시간 merge.dot: TAT 공정별 소요시간 merge.ipynb에서 산출된 산출물

-3가지 분류 분석: 주요 변수 3가지를 집중적으로 분석

