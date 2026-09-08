# 강남구 공공데이터 활용 공모전

제1회 강남구 공공데이터 활용 공모전 참가작 — **🏆 Best Paper Award 수상 (ICEF2024)**

강남구의 견인(불법 주정차) 데이터와 기존 주차 데이터를 클러스터링하여, 견인이 집중되는 지역을 기준으로 새로운 공영주차장 후보지를 제안하는 프로젝트입니다.

## 분석 흐름

1. **인구 통계 분석** (`N_20s_person.ipynb`) — 행정동별 10·20대 거주 인구를 집계해 수요가 높은 지역을 파악
2. **주차구역 현황 분석** (`N_parking.ipynb`, `N_parking_addr.ipynb`, `N_parking_map.ipynb`) — 강남구 공용 주차구역 데이터를 정제하고 지도에 시각화
3. **견인 데이터 클러스터링** (`N_DBSCAN+K-MEANS.ipynb`, `N_K-means*.ipynb`, `N_K-Means*.ipynb`) — 견인이 잦은 주소를 DBSCAN·K-Means로 군집화해 신규 주차장 후보 좌표 도출
4. **최종 결과** (`N_fin_K-means(k_over_2).ipynb`) — 견인 데이터·기존 주차 데이터·신규 후보지를 함께 시각화한 최종 산출물

## 노트북 목록

| 파일 | 내용 |
|---|---|
| `N_20s_person.ipynb` | 강남구 연령대별(10대/20대) 인구 분포 분석 |
| `N_parking.ipynb` | 강남구 공용 킥보드 주차구역 데이터 정제 |
| `N_parking_addr.ipynb` | 주차구역 주소 → 위경도 지오코딩 |
| `N_parking_map.ipynb` | 주차구역 지도 시각화 |
| `N_DBSCAN+K-MEANS.ipynb` | 견인 데이터 DBSCAN/K-Means 비교 실험 |
| `N_K-Means (grouping x).ipynb` / `N_K-Means(grouping O).ipynb` | 행정동 그룹화 여부에 따른 클러스터링 비교 |
| `N_K-means(k_over_2).ipynb` / `N_K-means(k_over_6).ipynb` | 견인 최소 횟수(k) 기준별 클러스터링 |
| `N_fin_K-means(k_over_2).ipynb` | **최종 채택 모델** — 신규 주차장 후보지 도출 |

## 데이터 & 실행 환경

- Google Colab (`google.colab.drive`)에서 실행하도록 작성되어 있으며, 개인 Google Drive의 `Colab Notebooks/gangnam/...` 경로에 있는 원본 데이터(CSV/XLSX, 공공데이터포털 제공)를 불러옵니다. 데이터 파일은 저장소에 포함되어 있지 않습니다.
- 사용 라이브러리: `pandas`, `numpy`, `matplotlib`, `scikit-learn`(KMeans, DBSCAN, silhouette_score)
- 지오코딩 및 지도 시각화에 Google Maps API, 좌표-주소 변환에 Kakao Local API를 사용합니다. 노트북 내 `YOUR_GOOGLE_MAPS_API_KEY` / `YOUR_KAKAO_API_KEY` 자리에 본인 키를 넣어 실행하세요.

> ⚠️ 과거 커밋 히스토리에 개인 API 키가 노출된 적이 있습니다. 저장소를 공개로 유지한다면 해당 키들은 이미 유출된 것으로 보고 재발급(rotate)하는 것을 권장합니다.
