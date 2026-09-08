# 강남구 공공데이터 활용 공모전

제1회 강남구 공공데이터 활용 공모전 참가작 — **🏆 Best Paper Award 수상 (ICEF2024)**

강남구의 견인(불법 주정차) 데이터와 기존 주차 데이터를 클러스터링하여, 견인이 집중되는 지역을 기준으로 새로운 공영주차장 후보지를 제안하는 프로젝트입니다.

## 분석 흐름

1. **인구 통계 분석** (`N_20s_person.ipynb`) — 행정동별 10·20대 거주 인구를 집계해 수요가 높은 지역을 파악
2. **주차구역 현황 분석** (`N_parking.ipynb`, `N_parking_addr.ipynb`, `N_parking_map.ipynb`) — 강남구 공용 주차구역 데이터를 정제하고 지오코딩·지도 시각화
3. **견인 데이터 클러스터링** (`N_fin_K-means(k_over_2).ipynb`) — 견인이 잦은 주소를 K-Means로 군집화해 신규 주차장 후보 좌표 도출 (최종 채택 모델)

## 노트북 목록

| 파일 | 내용 |
|---|---|
| `N_20s_person.ipynb` | 강남구 연령대별(10대/20대) 인구 분포 분석 |
| `N_parking.ipynb` | 강남구 공용 킥보드 주차구역 데이터 정제 |
| `N_parking_addr.ipynb` | 주차구역 주소 → 위경도 지오코딩 |
| `N_parking_map.ipynb` | 주차구역 지도 시각화 |
| `N_fin_K-means(k_over_2).ipynb` | **최종 채택 모델** — K-Means 클러스터링으로 신규 주차장 후보지 도출 |
| `archive/` | K-Means/DBSCAN 파라미터·전처리 비교 실험 노트북 (개발 과정 기록) |

## 실행 방법

### 1) 의존성 설치

```bash
pip install -r requirements.txt
```

### 2) API 키 설정

지오코딩·지도 API를 사용하는 노트북(`N_parking_addr.ipynb`, `N_parking_map.ipynb`, `N_fin_K-means(k_over_2).ipynb`)은 환경변수로 키를 읽습니다.

```bash
# Windows PowerShell
$env:GOOGLE_MAPS_API_KEY="..."
$env:KAKAO_API_KEY="..."

# macOS / Linux
export GOOGLE_MAPS_API_KEY="..."
export KAKAO_API_KEY="..."
```

### 3) 데이터

- 노트북들은 원래 Google Colab에서 개인 Google Drive의 `Colab Notebooks/gangnam/...` 경로 데이터(공공데이터포털 CSV/XLSX)를 로드하도록 작성되어 있습니다.
- 로컬 실행 시에는 각 노트북 상단의 `file = ...` 경로를 데이터가 있는 위치로 바꿔주세요.
- 데이터 파일은 저장소에 포함되지 않습니다 (`.gitignore`).

## 사용 라이브러리

`pandas`, `numpy`, `matplotlib`, `scikit-learn`(KMeans, DBSCAN, silhouette_score), `requests`, `openpyxl`

## 보안 관련 참고

과거 커밋 히스토리에 Google Maps / Kakao API 개인 키가 노출되어 있었으며, `git filter-repo`로 히스토리에서 제거했습니다. 그럼에도 이미 공개 노출되었던 이력이 있으므로 해당 키들은 재발급(rotate)된 상태여야 안전합니다.
