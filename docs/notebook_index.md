# Notebook Index

이 문서는 저장소에 있는 17개 노트북의 역할과 연결 관계를 정리합니다. 표의 분류는 노트북의 연구상 역할을 뜻하며, 현재 환경에서의 실행 보장 여부를 의미하지는 않습니다.

## 먼저 읽을 노트북

WEMIX 캡스톤의 핵심 흐름은 다음 세 노트북에 담겨 있습니다.

1. [`wemix_dynamic_network.ipynb`](../notebooks/capstone/visualization/wemix_dynamic_network.ipynb): 이벤트 구간별 동적 네트워크 시각화
2. [`wemix_daily_centrality.ipynb`](../notebooks/capstone/network_analysis/wemix_daily_centrality.ipynb): 일별 지갑 중앙성 계산
3. [`wemix_network_metrics.ipynb`](../notebooks/capstone/network_analysis/wemix_network_metrics.ipynb): 네트워크 지표와 이벤트 비교

## 캡스톤

| 노트북 | 역할 | 주요 입력 | 주요 출력 | 분류 |
| --- | --- | --- | --- | --- |
| [`sol_bitquery_extraction.ipynb`](../notebooks/capstone/data_collection/sol_bitquery_extraction.ipynb) | Bitquery에서 SOL 트랜스퍼를 페이지 단위로 수집하고 CSV로 통합 | Bitquery API | `data/raw/solana`, `data/processed/solana` | 수집 보조 |
| [`toncenter_extraction_experiment.ipynb`](../notebooks/capstone/data_collection/toncenter_extraction_experiment.ipynb) | Toncenter API로 TON 일별 거래 수집 가능성 시험 | Toncenter API | `data/raw/ton` | 실험 |
| [`wemix_daily_centrality.ipynb`](../notebooks/capstone/network_analysis/wemix_daily_centrality.ipynb) | WEMIX 지갑별 일간 중앙성과 PageRank 계산 | 정제된 WEMIX 트랜스퍼 | `results/wemix/network_metrics` | 발표 핵심 |
| [`wemix_network_metrics.ipynb`](../notebooks/capstone/network_analysis/wemix_network_metrics.ipynb) | 연결요소·밀도 계열 지표와 주요 이벤트를 시계열로 비교 | WEMIX 지표 CSV, 이벤트 CSV | 네트워크 지표 HTML | 발표 핵심 |
| [`wemix_dynamic_network.ipynb`](../notebooks/capstone/visualization/wemix_dynamic_network.ipynb) | 거래금액 또는 이웃 수로 노드 크기를 표현한 일별 애니메이션 생성 | WEMIX 트랜스퍼, 지갑 라벨 | `results/wemix/dynamic_network`, 상위 지갑 CSV | 발표 핵심 |

## 논문 작성 보조

2024년 9월부터 10월까지 약 2개월간 [**가상자산 온체인 데이터 분석을 통한내부자 거래 규제 가능성에 대한 연구**](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART003144407)의 작성을 지원하기 위해 데이터 수집·정제와 분석 보조를 수행했습니다. 아래 노트북은 주된 논문 집필이 아니라 그 기술 지원 과정에서 작성된 작업 기록입니다.

### 데이터 수집과 전처리

| 노트북 | 역할 | 주요 입력 | 주요 출력 | 분류 |
| --- | --- | --- | --- | --- |
| [`sol_bitquery_filtered_extraction.ipynb`](../notebooks/thesis/data_collection/sol_bitquery_filtered_extraction.ipynb) | `amount >= 100` 조건으로 SOL 트랜스퍼 수집 | Bitquery API | SOL JSON 페이지, 통합 CSV | 후속 수집 |
| [`avail_block_extraction.ipynb`](../notebooks/thesis/data_collection/avail_block_extraction.ipynb) | Subscan API에서 AVAIL 블록을 묶음 단위로 수집 | Subscan API | `data/raw/avail/blocks` | 후속 수집 |
| [`avail_blocks_to_events.ipynb`](../notebooks/thesis/preprocessing/avail_blocks_to_events.ipynb) | AVAIL 블록 JSON에서 이벤트를 추출해 CSV로 변환 | AVAIL 블록 JSON | `data/interim/avail/events` | 후속 전처리 |

### SOL 네트워크 분석

권장 순서는 `데이터 수집 → 중앙성·구조 지표 계산 → 주요 지갑 추출 → 지갑 흐름 정리`입니다.

| 노트북 | 역할 | 주요 입력 | 주요 출력 | 분류 |
| --- | --- | --- | --- | --- |
| [`sol_daily_centrality.ipynb`](../notebooks/thesis/network_analysis/sol_daily_centrality.ipynb) | SOL 일별 Degree·Betweenness·Closeness·PageRank 계산 | SOL 트랜스퍼 CSV | 일별 중앙성 CSV | 후속 분석 |
| [`sol_weighted_centrality.ipynb`](../notebooks/thesis/network_analysis/sol_weighted_centrality.ipynb) | 거래금액을 가중치로 사용한 일별 중앙성 계산 | 기간별 SOL 트랜스퍼 CSV | 가중 중앙성 CSV | 후속 분석 |
| [`sol_network_components.ipynb`](../notebooks/thesis/network_analysis/sol_network_components.ipynb) | SCC·WCC, Reciprocity, Assortativity, Transitivity 등 계산 | SOL 트랜스퍼 CSV | 연결요소 지표 CSV | 후속 분석 |
| [`sol_network_connectivity.ipynb`](../notebooks/thesis/network_analysis/sol_network_connectivity.ipynb) | Core number, Edge connectivity, Node connectivity 계산 | SOL 트랜스퍼 CSV | 연결성 지표 CSV | 후속 분석 |
| [`sol_top_wallets.ipynb`](../notebooks/thesis/wallet_analysis/sol_top_wallets.ipynb) | 일별 PageRank·Betweenness 상위 지갑을 합쳐 중복 제거 | 중앙성 CSV | 일반·가중 상위 지갑 CSV | 후속 지갑 분석 |
| [`sol_combined_wallets.ipynb`](../notebooks/thesis/wallet_analysis/sol_combined_wallets.ipynb) | 일반·가중 중앙성에서 추출한 지갑 목록 통합 | 상위 지갑 CSV | 통합 상위 지갑 CSV | 후속 지갑 분석 |
| [`sol_wallet_flows.ipynb`](../notebooks/thesis/wallet_analysis/sol_wallet_flows.ipynb) | 지갑별 전체 송신량과 수신량 집계 | 기간별 SOL 트랜스퍼 CSV | 지갑별 송수신 집계 CSV | 후속 지갑 분석 |

## 실험 노트북

두 AVAX 노트북은 중간발표 단계의 탐색을 보여주는 기록입니다. WEMIX 중심의 최종 분석 파이프라인과는 직접 연결되지 않습니다.

| 노트북 | 역할 | 주요 입력 | 주요 출력 | 분류 |
| --- | --- | --- | --- | --- |
| [`avax_transaction_eda.ipynb`](../notebooks/experiments/avax_transaction_eda.ipynb) | AVAX 거래금액과 가격의 추세·계절성·변동성 탐색 | AVAX 가격 XLSX, 거래량 CSV | 노트북 내 표·그래프 | 중간발표 실험 |
| [`avax_granger_causality.ipynb`](../notebooks/experiments/avax_granger_causality.ipynb) | 거래금액 변화가 가격 차분값 예측에 정보를 더하는지 시험 | AVAX 가격 XLSX, 거래량 CSV | Granger 인과관계 검정 결과 | 중간발표 실험 |

## 데이터 경로

- 수집 원본: `data/raw/`
- 전처리 중간 산출물: `data/interim/`
- 분석용 정제 데이터: `data/processed/`
- 저장 가능한 분석 결과: `results/`

원본 데이터는 저장소에 포함되지 않습니다. 자세한 내용은 [`data/README.md`](../data/README.md)를 참고하세요.
