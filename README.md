# OSS Week 13 — React Mini Dashboard (Student Starter)
## 황예찬 
> **강의 중 연습용 프로젝트입니다. 제출하지 않습니다.** 이 LAB의 GitHub URL, Vercel URL, 스크린샷 및 결과 보고서를 LMS에 제출할 필요가 없습니다. **실제 평가 대상은 각 팀이 선정한 오픈소스 프로젝트와 팀 프로젝트 과제 결과물입니다.**

## 1. 학습 목표

하나의 React + Vite 프로젝트로 다음 흐름을 연습합니다.

**GitHub 협업 → 설치·실행·빌드 → 컴포넌트 분석 → Vercel 배포 → Axios GET → useEffect·Loading/Error → Open-Meteo API**

현재 Starter에는 다음이 구현되어 있습니다.

- `Header`, `StatCard`, `UserList` 컴포넌트
- `users.js`의 **정적** 사용자 4명 표시
- `useState` 기반 검색 및 `useRef` 기반 입력창 Focus
- `WeatherPlaceholder`: LAB 7에서 WeatherCard로 교체할 위치
- 반응형 CSS, Vite 빌드 설정

**구현되지 않은 것:** Axios, 외부 API 호출, 로딩·오류 처리, 날씨 표시. 직접 LAB에서 만들어야 합니다.

## 2. 실행 방법

요구 환경: Node.js **20.19+ 또는 22.12+** 권장 (Vite 요구사항을 충족하는 버전).

```bash
npm install
npm run dev
```

터미널에 표시되는 로컬 주소(일반적으로 `http://localhost:5173`)를 브라우저에서 엽니다.

배포용 빌드와 미리보기:

```bash
npm run build
npm run preview
```

## 3. 프로젝트 구조

```text
src/
├── main.jsx                    # React 시작
├── App.jsx                     # 화면 결합, Props 전달
├── App.css                     # 스타일
├── components/
│   ├── Header.jsx              # Props
│   ├── StatCard.jsx            # Props
│   ├── UserList.jsx            # useState, Event, useRef, Array.filter/map
│   └── WeatherPlaceholder.jsx  # LAB 7의 자리
└── data/
    └── users.js                # 정적 샘플 데이터 (LAB 6에서 교체)
```

`package.json`의 `scripts`, `dependencies`, `devDependencies`를 먼저 분석하세요.

## 4. LAB 안내

모든 단계는 **[LAB_GUIDE.md](./LAB_GUIDE.md)** 에 정리되어 있습니다.

| LAB | 핵심 활동 | 완성 조건 |
|---|---|---|
| 1 | Fork/Clone/Branch/PR/Merge | PR 및 Merge를 한 번 수행 |
| 2 | npm install/dev/build | 로컬 화면과 dist 확인 |
| 3 | Props/State/Hooks 분석 | UserList 데이터 흐름 설명 |
| 4 | Vercel 배포/자동 배포 | Preview와 Production 차이 확인 |
| 5 | Axios GET | Console에서 API 사용자 확인 |
| 6 | useEffect·State·Loading/Error | 정적 데이터 대신 API 사용자 출력 |
| 7 | Open-Meteo API | 도시별 날씨 화면 표시 |

## 5. 제출·평가 정책

**이 Starter 프로젝트는 제출하지 않습니다. 별도 LAB 점수나 결과물 제출도 없습니다.** GitHub/Vercel 실습은 강의 중 연습을 위한 것입니다. 팀 프로젝트는 **각 팀이 12주차에 선정한 별도의 오픈소스 저장소**에서 진행하고, 해당 과제 지침에 맞춰 제출하세요.

## 6. API / 환경변수 유의사항

- LAB 5~6: [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — 공개 테스트 REST API
- LAB 7: [Open-Meteo](https://open-meteo.com/en/docs) — 현재 날씨 API
- 이 연습에서 사용하는 두 API는 기본 실습에 비밀 API Key가 필요하지 않습니다.
- `.env.example`은 선택적 설정 예시입니다. `VITE_`로 시작하는 값은 **브라우저에서 공개**되므로 비밀 API Key를 넣지 마세요.
- 외부 API 응답은 네트워크 및 제공 서비스 상태에 따라 달라집니다.
