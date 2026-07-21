# Nongak Formations — 한국 전통 대형의 디지털 기록 시스템

> A digital recording system for Korean traditional percussion (Nongak / Pungmul) formations.

**고창농악(Gochang Nongak)**의 진형(陣形, formations)을 시각적으로 기록하고 재생할 수 있는 브라우저 도구. 원진(circle), 태극진(yin-yang S-curve), 11자진(two-line) 같은 전통 대형을 디지털로 보존하고 가르치는 것을 목표로 한다.

This is a browser-based tool for visualizing, editing, and replaying the formations used in **Gochang Nongak**, a regional style of Korean traditional percussion ensemble performance. It captures formations like the circle (wonjin), the yin-yang S-curve (taegukjin), and the two-line formation (shibiljajin) as editable, replayable keyframes.

🔗 **Live demo:** [https://limdoyun0603.github.io/nongak-formations/](https://limdoyun0603.github.io/nongak-formations/)

---

## 왜 만들었나 / Background

전통 풍물패에서 진형을 가르치고 기억하는 도구는 대부분 종이 도해, 구전, 또는 영상이다. 영상은 한 시점만 보여주고, 종이 도해는 시간에 따른 변화를 담지 못한다. 일부 안무용 디지털 도구(예: arrangeUs)도 있지만 대부분 무용·치어리딩·드릴팀에 맞춰져 있어 풍물패의 핵심 원리인 **상쇠가 머리이고 나머지가 뱀처럼 따라간다**는 동작을 자연스럽게 표현하지 못한다.

이 도구는 그 한계를 해결하기 위해 만들어졌다:

- **상쇠(head)를 끌면 체인 전체가 따라옴** — 각 노드를 일일이 옮기지 않아도 됨
- **진형 변화를 키프레임으로 저장** — 가락에 맞춘 시간 흐름 기록
- **재생/가속 재생** — 안무를 영상처럼 검토 가능

장기적으로는 자연어 입력("3분짜리 판굿, 점점 빨라지는 흐름")만으로 진형 시퀀스를 자동 생성하는 **AI 상쇠** 시스템의 기반이 되는 것을 목표로 한다.

Traditional teaching of these formations relies on paper diagrams, oral transmission, or video — none of which capture both spatial structure and temporal change well. Existing choreography tools (e.g., arrangeUs) target dance and drill teams, and don't model the core principle of Korean percussion ensembles: the lead percussionist (sangsoe) is the "head" of a chain, and everyone else follows snake-like. This tool is built around that principle.

---

## 주요 기능 / Features

- **체인 기반 편집** — 선두 또는 후미만 드래그하면 나머지가 자동으로 따라옴 (뱀 따라가기)
- **키프레임 기록** — 한 진형 상태를 저장하고 사이드바에서 클릭으로 재생
- **재생 / 가속 재생** — 키프레임들을 영상처럼 재생, 가속 재생으로 흐름 검토
- **진형 프리셋**
  - 원진 (Wonjin) — 기본 원
  - 겹원진 (Double circle) — 안원+바깥원
  - 난진 (Nanjin) — 어름굿 워밍업용 (매번 다른 모양)
  - 180° 회전 — 진행 방향 반전
- **노드 분리/재결합** — 일부 노드만 자유 위치로 떼어 놓을 수 있음
- **좌표 내보내기** — 클립보드 복사 또는 JSON 다운로드
- **23명 기본** (꽹과리 5, 징 3, 장구 5, 북 5, 소고 5)
- **모든 한국어 UI** — 풍물패 사용자 친화적

---

## 사용법 / Usage

브라우저에서 [index.html](./index.html)을 열면 바로 사용 가능. 별도 설치/서버 필요 없음.

1. **드래그로 동선 만들기**: 1번 노드(상쇠) 또는 마지막 노드를 드래그하면 체인 전체가 뱀처럼 따라옴
2. **진형 만들기**: 상단의 ⊙ 원진 / ◎ 겹원진 / ⁂ 난진 버튼 클릭
3. **키프레임 저장**: 💾 키프레임 저장 → 사이드바에 추가됨
4. **재생**: ▶ 재생 또는 ▶▶ 가속으로 키프레임 시퀀스 재생
5. **내보내기**: 📥 JSON 내보내기로 좌표 데이터 다운로드

상세한 사용법과 도메인 지식은 [고창농악_진형_프로젝트_Overview.md](./고창농악_진형_프로젝트_Overview.md) 참조.

---

## 구현된 진형 / Implemented Formations

| 진형 | 영문 | 상태 | 출처 |
|------|------|------|------|
| 원진 | Wonjin | ✅ 구현 | 모든 마당의 기본 |
| 겹원진 | Double Wonjin | ✅ 구현 | — |
| 태극진 | Taegukjin | ✅ 구현 | 1마당, 2마당, 3마당 |
| 난진 | Nanjin | ✅ 구현 | 어름굿 |
| 11자진 | Shibiljajin | ⚡ 부분 구현 (방법 1 정적) | 2마당, 3마당 |
| 달팽이진 | Dalpaengyijin | 📝 명문화만 | 2마당 |
| 장사진 | Jangsajin | ☑ snake-follow로 본질 구현 | 3마당, 입장굿 |

각 진형의 상세 정의는 [formations/](./formations/) 폴더의 JSON 파일 참조.

---

## 폴더 구조 / Structure

```
nongak-formations/
├── README.md                          (이 파일)
├── index.html                         (도구 본체, 단일 HTML 파일)
├── LICENSE                            (MIT)
├── 고창농악_진형_프로젝트_Overview.md   (도메인 지식 + 기술 명세)
└── formations/                        (진형 사전 — JSON)
    ├── index.json                     (전체 진형 인덱스)
    ├── wonjin.json
    ├── taegukjin.json
    ├── nanjin.json
    ├── shibiljajin.json
    ├── dalpaengyijin.json
    └── jangsajin.json
```

---

## 향후 계획 / Roadmap

**단기 (Short-term)**
- 11자진, 달팽이진을 도구에 구현
- 4마당 (구정놀이마당) 명문화
- 도둑잽이굿 (선택적 삽입 연극) 명문화
- 이채덩더쿵(이덩) 개인 기량 부분 상세 명문화

**중기 (Mid-term)**
- 가락(음악) 트랙 동기화 — 키프레임에 가락 이름·박자 메타데이터 부여
- 진형 시퀀스 DSL 정의 — `won_jin(direction: ccw, laps: 2) → taegeuk_jin() → ...` 형태로 판굿 전체를 코드로 표현
- 노드 상태 확장: `sitting`, `partnership`, `role` (잡색·대포수 등)

**장기 (Long-term) — "AI 상쇠"**
- 자연어 입력 → 진형 시퀀스 자동 생성 (Claude API 등 LLM을 자연어→DSL 번역기로 활용)
- 음악 파일 입력 → 가락 인식 → 진형 시퀀스 자동 생성
- 다른 지역 풍물(이리농악·진주삼천포농악 등)으로 확장

---

## 기술적 원칙 / Design Principles

- **단일 HTML 파일** — 빌드 도구·프레임워크 없음. 브라우저 열면 즉시 실행
- **No localStorage / sessionStorage** — 모든 상태는 메모리에. 명시적 export/import만
- **No `prompt()`** — 모달 UI로 입력 받음
- **최소 노드 간 거리 32px** — 노드끼리 절대 겹치지 않음
- **뱀 따라가기 (snake-follow)** — 노드를 일일이 옮기지 않고 체인 단위로 편집

---

## 라이선스 / License

MIT License — [LICENSE](./LICENSE) 참조.

Copyright (c) 2026 limdoyun0603

자유롭게 사용·수정·재배포 가능. 풍물패와 농악 교육에 기여하기를 바라며 만든 도구입니다.
