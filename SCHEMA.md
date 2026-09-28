# 진형 데이터 스펙 (formations/*.json)

`formations/` 폴더의 진형 파일 6개(`wonjin`, `taegukjin`, `nanjin`, `shibiljajin`, `dalpaengyijin`, `jangsajin`)와 목록 파일 `index.json`의 구조를 설명한다. 이 문서에 적힌 필드는 모두 실제 파일에 있는 것이다.

---

## 1. 진형 파일의 최상위 필드

| 필드 | 타입 | 설명 | 예시 |
|------|------|------|------|
| `name` | string | 진형 이름 (한글) | `"원진"` |
| `name_en` | string | 영문 이름. 괄호로 뜻을 덧붙이기도 함 | `"Nanjin (Loose formation)"` |
| `name_romanized` | string | 로마자 표기 | `"Shibiljajin"` |
| `description` | string | 진형 설명 (한글) | `"치배들이 둥근 원으로 늘어선 가장 기본적인 진형. …"` |
| `description_en` | string | 진형 설명 (영문) | `"The most fundamental formation: …"` |
| `source` | string | 판굿에서 쓰이는 곳 | `"고창농악 2마당 (진오방진)"` |
| `parameters` | object | 진형을 정하는 값들. 키는 진형마다 다름 (아래 표) | `{"person_count": 23, "radius_px": 216, …}` |
| `rules` | string[] | 좌표로 나타나지 않는 규칙 | `["한 번의 태극진은 원진의 회전 방향을 뒤집는다", …]` |
| `algorithm` | object | 배치 절차. `type`(string)과 `steps`(string[]). 난진에만 있음 | `{"type": "stochastic_placement", "steps": ["1. 상쇠(id=1)를 무대 중앙 …", …]}` |
| `variants` | object[] | 변형. 각 항목은 `name`, `description`(모두 string). 없으면 빈 배열 | `[{"name": "겹원진", "description": "…"}]` |
| `implementation_status` | string | 도구(index.html)에 구현된 정도. 값은 §4 | `"algorithm_only"` |
| `notes` | string | 좌표 데이터나 진형에 대한 보충 설명. 일부 파일에만 있음 | `"좌표 데이터는 생성 방법 1(원진에서 접기) 기준의 참고용 정적 스냅숏."` |
| `implementation_notes` | string | 도구에서 실제로 어떻게 동작하는지, 무엇이 미구현인지 | `"‖ 11자진 버튼(진풀이 탭). …"` |
| `nodes` | object[] \| null | 사람별 좌표 (§2). 정적 좌표로 나타낼 수 없는 진형은 `null` | 난진·장사진은 `null` |
| `node_roster` | object[] | `nodes`가 `null`인 파일에만 있는 편성표. 각 항목은 `id`, `instrument`, `role` | `[{"id": 1, "instrument": "꽹과리", "role": "상쇠"}, …]` |

### `parameters` 키 (파일별)

| 파일 | 키 |
|------|----|
| 공통 | `person_count` (number, 인원) |
| wonjin | `radius_px`, `stage_size` {`w`, `h`}, `center` {`x`, `y`}, `direction`, `min_node_gap_px` |
| taegukjin | `enclosing_circle_radius_px`, `s_curve_half_radius_px`, `stage_size`, `center`, `entry_point`, `exit_point`, `lower_bulge`, `upper_bulge` |
| nanjin | `cluster_radius_ratio`, `same_instrument_min_distance_px`, `any_node_min_distance_px`, `placement_attempts_per_node` |
| shibiljajin | `line_gap_px`, `same_line_spacing_px`, `stage_size`, `person_distribution` |
| dalpaengyijin | `direction`, `tightness_px`, `typical_count_per_madang` |
| jangsajin | `shape`, `spacing_px` |

값은 숫자일 수도, 설명 문자열일 수도 있다 (예: 11자진 `line_gap_px`는 `"variable (맨 앞 사람이 자율 결정)"`).

---

## 2. `nodes` 항목

| 필드 | 타입 | 설명 | 예시 |
|------|------|------|------|
| `id` | number | 1부터 시작하는 번호. 체인(대열) 순서이자 편성 순서 | `1` |
| `instrument` | string | 악기군: `꽹과리`, `징`, `장구`, `북`, `소고`, `잡색` (잡색은 악기가 아니지만 같은 필드에 둠) | `"장구"` |
| `role` | string | index.html `INSTRUMENTS`의 이름 그대로 | `"상쇠"`, `"부쇠"`, `"장구1"` |
| `x` | number | 가로 좌표 (px) | `474.1` |
| `y` | number | 세로 좌표 (px) | `97.1` |
| `heading` | number | 바라보는 방향 (라디안) | `0.35` |

**좌표계**
- 무대 크기 800 × 600 px, 원점 (0, 0)은 **왼쪽 위**. x는 오른쪽, y는 아래로 증가
- 무대 아래쪽이 관객(청중) 쪽, 위쪽이 무대 뒤
- `heading`은 도구와 같은 규약: 0 = 오른쪽(+x), π/2 = 아래쪽(관객 쪽). −π~π로 정규화되어 있지 않은 값도 있음 (예: 원진 최대 6.36, 달팽이진 최소 −12.57). 방향은 2π로 나눈 나머지로 읽으면 됨
- `id`는 1부터 시작하고, index.html 안의 노드 배열 인덱스는 0부터 시작함 (`id` = 인덱스 + 1)

**기본 편성 (23명, index.html `INSTRUMENTS`와 같음)**

| id | instrument | role |
|----|-----------|------|
| 1–2 | 꽹과리 | 상쇠, 부쇠 |
| 3–4 | 징 | 징1, 징2 |
| 5–10 | 장구 | 장구1 ~ 장구6 |
| 11–14 | 북 | 북1 ~ 북4 |
| 15–20 | 소고 | 소고1 ~ 소고6 |
| 21–23 | 잡색 | 잡색1 ~ 잡색3 |

---

## 3. `index.json`

| 필드 | 타입 | 설명 |
|------|------|------|
| `name` | string | 사전 이름 (`"Nongak Formations Dictionary"`) |
| `description` | string | 사전 설명 |
| `count` | number | 진형 파일 수 (`6`) |
| `formations` | object[] | 진형 목록. 각 항목은 `file`, `name`, `name_en`, `source`, `status` |

`formations[].status`는 해당 파일의 `implementation_status`와 같은 값이다.

---

## 4. `implementation_status` 값

| 값 | 뜻 | 해당 진형 |
|----|----|----------|
| `implemented` | 도구에서 버튼이나 자동 동작으로 만들 수 있음 | 원진 (자동 정리), 난진 (버튼) |
| `partially_implemented` | 일부 생성 방법만 도구에 있음 | 11자진 (방법 1만) |
| `algorithm_only` | index.html에 알고리즘 코드는 있으나 화면에서 쓸 수 없음 | 태극진 |
| `documented_only` | 정의만 문서화됨. 도구에 생성 기능 없음 | 달팽이진 |
| `inherent` | 도구의 기본 동작 자체가 그 진형이라 별도 구현이 없음 | 장사진 (뱀 따라가기) |

---

## 5. 설계 시 고려한 것

1. **좌표만으로는 부족하다.** 태극진의 "회전 방향이 뒤집힌다"는 규칙은 좌표에 나타나지 않지만 다음 진형을 결정한다. 그래서 `rules`를 별도 필드로 뒀다.
2. **정적으로 표현할 수 없는 진형이 있다.** 장사진은 상쇠의 즉흥 동선이라 좌표가 무의미하고, 난진은 매번 달라야 한다. 이들은 `nodes`를 `null`로 두고 규칙이나 알고리즘을 기술했다.
3. **구현 상태를 데이터에 포함했다.** 문서와 도구가 어긋나는 것을 막기 위해서다.
