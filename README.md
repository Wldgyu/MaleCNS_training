# MaleCNS: Fly·RNN·GRU 기초 비교 실험

초파리 연결망을 활용한 Fly 모델과 일반 RNN·GRU가 작은 게임에서 기억과 선택을 어떻게 학습하는지 살펴본 연구 기록입니다. 카드 기억 게임, 방·복도 미로 과제, 다중 단서 기억, 초기 오목 실험의 코드와 결과를 모았습니다.

이 폴더는 기초 비교 실험을 보존합니다. 이후의 오목 학습 개선과 성장 과정은 별도 `Gomoku_training` 깃 저장소 에서 계속 정리합니다.

**후속 요약 (2026-10-19):** 15×15 렌주에서 같은 자료와 같은 학습 횟수로 실제 Fly·재배열 Fly·RNN을 처음부터 학습해 비교했지만 구조 간 일관된 우열은 확인되지 않았습니다. 기초 과제부터 15×15까지를 원래 연구 질문(RQ1~4)에 맞춰 정리한 [통합 연구 보고서](https://github.com/Wldgyu/Gomoku_training/blob/main/docs/RESEARCH_REPORT_20261019.md)는 `Gomoku_training` 저장소에 있습니다.

## 초파리 연결 데이터 출처

Fly 모델은 [MaleCNS v1.0 공식 공개 데이터](https://male-cns.janelia.org/download/)의 뉴런 주석과 시냅스 연결을 가공해 사용합니다. 원자료는 FlyEM (HHMI Janelia)·University of Cambridge·MRC LMB·Google Research 공동 프로젝트에서 제공하며, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)으로 배포됩니다. 실제 연결 구조를 인공 순환망에 적용하고 간단한 게임 과제들은 별도 학습했습니다. [사용 파일·가공 내용·출처 상세](docs/DATA_SOURCES.md)를 참고하세요.

## 비교한 모델

| 모델 | 비교 목적 |
|---|---|
| Fly | 실제 초파리 연결 부분 그래프를 사용한 순환망의 학습 특성 확인 |
| 재배열 Fly | 연결 차수를 보존하고 배치를 바꿔 실제 연결 구조의 효과 비교 |
| RNN | 일반적인 순환 신경망 기준선 |
| GRU | 게이트를 사용하는 순환 신경망 기준선 |

Fly는 생물의 뇌 전체를 재현한 모델이 아니라, 실측 연결 부분 그래프를 이용하는 학습 가능한 순환망입니다.

## 실험 내용

| 과제 | 확인한 내용 | 자료 |
|---|---|---|
| 카드 기억 게임 | 관측한 정보를 지연 뒤 기억하고 선택하는 능력 | [보고서](previous_research/reports/card_game/) · [웹게임](previous_research/games/card_memory/index.html) |
| 방·복도 / MiniGrid | 단서 기억, 이동, 목표 선택과 새로운 조건으로의 전이 | [보고서](previous_research/reports/minigrid/) |
| 다중 단서 기억 | 여러 단서의 결합, 방해 입력과 출력 선택의 안정성 | [보고서](previous_research/reports/memory/) |
| 초기 오목 | 9×9·12×12 자유 오목의 기본 경기·전술·방어 학습 | [보고서](gomoku/reports/) |

## 지금까지 확인한 점

모델의 성적은 과제·입력 방식·학습 조건·시드에 따라 달랐습니다. 일부 조건에서 Fly의 이점이 나타났지만, 실제 연결 구조의 일관된 우월성은 확인하지 못했습니다. RNN·GRU도 성공과 실패가 조건별로 달라 하나의 고정된 순위로 정리하기 어렵습니다.

기억 정보가 내부에 남아 있는지, 질문에 맞게 출력할 수 있는지, 화면을 인식하고 행동으로 연결하는지는 따로 확인해야 했습니다. 초기 오목에서도 전술 문제 정답률이 높아지는 것만으로 실제 경기 승률이 충분히 높아지지는 않았습니다.

세부 수치와 실험 한계는 각 보고서에 있습니다. [기초 연구 질문 종합 기록](previous_research/reports/foundation/core_research_questions_report.txt)과 [날짜별 연구 기록](docs/README_HISTORY.md)을 함께 참고하세요.

## 코드와 실행 안내

- [이전 과제 코드·실행 안내](previous_research/README.md)
- [오목 코드·실행 안내](gomoku/README.md)
- [연구 기획서](drosophila_project_plan_flow.txt) · [실행 계획](RESEARCH_PROTOCOL.md)
- [의존성](requirements.txt) · [업로드 안내](docs/GITHUB_UPLOAD.md)

코드·보고서·작은 재현 자료를 포함하며, 가상환경·대형 원자료·학습 가중치는 제외했습니다. 일부 재현과 체크포인트 평가에는 별도 데이터 또는 가중치가 필요합니다.
