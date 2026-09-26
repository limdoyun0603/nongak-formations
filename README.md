# Nongak Formations — 한국 전통 대형의 디지털 기록 시스템

> A digital recording system for Korean traditional percussion (Nongak / Pungmul) formations.

**고창농악(Gochang Nongak)**의 진형(陣形, formations)과 그 사이의 움직임을 기록하고 재생하는 브라우저 도구. 원진(circle), 11자진(two-line), 난진(scatter) 같은 전통 대형과, 대형이 바뀌는 동작 자체를 디지털로 보존하고 가르치는 것을 목표로 한다.

This is a browser-based tool for recording and replaying the formations of **Gochang Nongak**, a regional style of Korean traditional percussion ensemble performance — both the formations themselves (circle, two-line, scatter) and the movement between them.

🔗 **Live demo:** [https://limdoyun0603.github.io/nongak-formations/](https://limdoyun0603.github.io/nongak-formations/)

---

## 왜 만들었나 / Background

전통 풍물패에서 진형을 가르치고 기억하는 도구는 대부분 종이 도해, 구전, 또는 영상이다. 영상은 한 시점만 보여주고, 종이 도해는 시간에 따른 변화를 담지 못한다. 일부 안무용 디지털 도구(예: arrangeUs)도 있지만 대부분 무용·치어리딩·드릴팀에 맞춰져 있어 풍물패의 핵심 원리인 **상쇠가 머리이고 나머지가 뱀처럼 따라간다**는 동작을 자연스럽게 표현하지 못한다.

이 도구는 그 원리를 중심에 두고 만들었다: 상쇠(머리)를 끌면 체인 전체가 따라오고, 그 움직임을 그대로 녹화해 파일로 남길 수 있다.

장기적으로는 자연어 입력("3분짜리 판굿, 점점 빨라지는 흐름")만으로 진형 시퀀스를 자동 생성하는 **AI 상쇠** 시스템의 기반이 되는 것을 목표로 한다.

Traditional teaching relies on paper diagrams, oral transmission, or video — none of which capture both spatial structure and temporal change well. Existing choreography tools target dance and drill teams and don't model the core principle of Korean percussion ensembles: the lead percussionist (sangsoe) is the "head" of a chain, and everyone else follows snake-like.

---

## 주요 기능 / Features

**편집**
- **뱀 따라가기 (snake-follow)** — 체인의 머리나 꼬리만 끌면 나머지가 따라옴
- **원진 자동 스냅** — 원 모양으로 돌리고 손을 떼면 균등한 원진으로 정리. 원진 상태에서는 궤도를 따라 끌면 회전, 바깥으로 크게 벗어나면 풀림
- **11자진** — 버튼을 누른 뒤 화살표(두 점)로 방향을 지정하면, 상쇠 위치는 그대로 두고 두 줄로 접힘
- **난진** — 같은 악기끼리 붙지 않게 흩어짐. 3명 이상 선택하면 선택한 사람만
- **반연풍 / 180° / 앉기** — 제자리 회전, 방향 반전, 앉음·일어섬
- **진 끊기·합치기** — 이웃한 두 사람을 골라 ✂ 분리하면 체인이 둘로 나뉘고(각 조각의 앞사람이 새 머리), 🔗 연결로 다시 합침
- **연결 시 순서 정리** — 같은 악기 안에서만 위치 순으로 재배열. 악기 순서와 상치배·말치배·부쇠·말쇠 자리는 고정

**선택**
- 클릭: 한 사람 · 더블클릭: 선택하며 체인에서 떼어내기 · 우클릭: 메뉴(체인 전체 선택, 방향 돌리기, 떼기, 앉기)
- Ctrl+클릭: 여러 명 · Ctrl+A: 전체 · 빈 곳 드래그: 영역 선택 · Esc: 해제

**기록**
- **동작 녹화** — ⏺ 녹화 중 드래그한 움직임이 실제 속도 그대로 기록됨. 드래그 한 번이 동작 하나
- **키프레임** — 특정 진형 상태를 저장하고 클릭으로 불러오기
- **파일로 저장 / 열기** — 녹화한 동작, 키프레임, 현재 진형, 끊은 체인을 `.json` 파일 하나로 저장하고 다시 열기
- **재생 / 가속 재생**, 좌표 복사

**가락** — 마당별 가락과 BPM 사전

**23명 기본 편성** — 꽹과리 2(상쇠·부쇠), 징 2, 장구 6, 북 4, 소고 6, 잡색 3. 노드 수는 조절 가능

---

## 사용법 / Usage

브라우저에서 [index.html](./index.html)을 열면 바로 사용 가능. 설치나 서버가 필요 없다.

1. **동선 만들기** — 1번(상쇠) 또는 마지막 사람을 드래그. 원을 그리면 원진으로 정리됨
2. **진형 버튼** — 진풀이 탭의 ⁂ 난진, ‖ 11자진, ↻ 반연풍 등
3. **녹화** — 애니메이션 탭의 ⏺ 녹화를 누르고 드래그. 다시 누르면 중지
4. **저장** — 오른쪽 아래 💾 파일로 저장. 나중에 📂 파일 열기로 이어서 작업
5. **재생** — ▶ 재생 (녹화한 동작이 있으면 동작을, 없으면 키프레임을 재생)

도메인 지식(판굿 구조, 마당별 진형·가락, 용어)은 [OVERVIEW.md](./OVERVIEW.md) 참조.

---

## 진형 현황 / Formations

| 진형 | 영문 | 도구 | 출처 |
|------|------|------|------|
| 원진 | Wonjin | ✅ 자동 스냅 | 모든 마당의 기본 |
| 11자진 | Shibiljajin | ✅ 방향 지정 | 2마당, 3마당 |
| 난진 | Nanjin | ✅ 버튼 | 어름굿 |
| 장사진 | Jangsajin | ✅ 뱀 따라가기로 표현 | 3마당, 입장굿 |
| 태극진 | Taegukjin | 🔧 알고리즘만 보존 (버튼 없음) | 1·2·3마당 |
| 달팽이진 | Dalpaengyijin | 📝 명문화만 | 2마당 |

각 진형의 정의는 [formations/](./formations/) 폴더의 JSON 파일 참조.

---

## 기록 파일 형식 / Record File

💾 파일로 저장이 만드는 `.json` 파일 (`format: "gochang-nongak-record"`, `version: 1`):

| 필드 | 내용 |
|------|------|
| `stage` | 저장 당시 캔버스 크기 (불러올 때 중심을 맞춤) |
| `nodeCount`, `instruments` | 인원과 각자의 악기 |
| `current` | 현재 진형 |
| `clips[]` | 녹화한 동작. `frames`(프레임별 전원 상태)와 `times`(각 프레임의 경과 ms) |
| `keyframes[]` | 저장한 키프레임 |
| `brokenLinks` | 끊어 둔 체인 지점 |
| `spacing` | 간격 설정 |

한 사람의 상태는 `[x, y, 방향(라디안), 떨어짐(0/1), 앉음(0/1)]` 배열로 압축 저장한다.

---

## 폴더 구조 / Structure

```
nongak-formations/
├── README.md          (이 파일)
├── index.html         (도구 본체, 단일 HTML 파일)
├── OVERVIEW.md        (도메인 지식 + 기술 명세)
├── LICENSE            (MIT)
└── formations/        (진형 사전 — JSON)
    ├── index.json
    ├── wonjin.json
    ├── taegukjin.json
    ├── nanjin.json
    ├── shibiljajin.json
    ├── dalpaengyijin.json
    └── jangsajin.json
```

---

## 향후 계획 / Roadmap

**단기**
- 2마당 삼채굿, 3마당, 4마당(구정놀이마당) 명문화
- 빈 BPM 채우기 (일채, 반굿거리, 된굿거리, 된이채)
- 실제 한 마당을 처음부터 끝까지 이 도구로 기보해 보기

**중기**
- 진형 시퀀스 DSL — `won_jin(direction: ccw, laps: 2) → taegeuk_jin() → ...` 처럼 판굿 전체를 코드로 표현
- 가락과 동작의 박자 동기화

**장기 — "AI 상쇠"**
- 자연어 입력 → 진형 시퀀스 자동 생성 (LLM을 자연어→DSL 번역기로 활용)
- 다른 지역 풍물(이리농악·진주삼천포농악 등)로 확장

---

## 기술적 원칙 / Design Principles

- **단일 HTML 파일** — 빌드 도구·프레임워크 없음. 브라우저로 열면 즉시 실행
- **브라우저 저장소 안 씀** — 작업 내용은 메모리에만 있고, 남기려면 파일로 저장
- **체인 단위 편집** — 사람을 일일이 옮기지 않고 머리를 끌어 움직임

---

## 라이선스 / License

MIT License — [LICENSE](./LICENSE) 참조.

Copyright (c) 2026 limdoyun0603

자유롭게 사용·수정·재배포 가능. 풍물패와 농악 교육에 기여하기를 바라며 만든 도구입니다.
