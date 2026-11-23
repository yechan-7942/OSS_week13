# Week 13 LAB Guide — 학생용

> **연습 전용 / LMS 제출 없음.** 구현 결과는 각자의 학습에 활용하고, 실제 개발 및 평가는 별도 **2인 1팀 오픈소스 프로젝트**에서 진행합니다.

## LAB 1 — GitHub Collaboration (Fork / Clone / Branch / PR)

1. 교수자가 GitHub에 게시한 Starter 저장소를 Fork합니다. (교수자가 ZIP만 공유한 경우 먼저 GitHub에 연습용 저장소를 생성하도록 안내합니다.)
2. Fork한 저장소를 Clone합니다.
3. `feature/title-update` Branch를 만듭니다.
4. `src/App.jsx`의 헤더/제목 문구를 1곳 변경합니다.
5. Commit, Push 후 **자신의 Fork 안에서 `main`을 대상으로 PR**을 생성합니다. (원본 교수자 저장소로 PR을 보내지 않습니다.)
6. 변경 내용을 확인한 후 Merge하고 로컬 `main`에서 `git pull`을 실행합니다.

```bash
git clone https://github.com/<YOUR_ID>/<REPO>.git
cd <REPO>
git switch -c feature/title-update
# src/App.jsx 수정
git add src/App.jsx
git commit -m "feat: update dashboard title"
git push -u origin feature/title-update
# 웹에서 PR 및 Merge 수행
git switch main
git pull origin main
```

**확인:** Fork와 Branch 차이를 설명할 수 있고, 자신의 저장소에서 PR과 Merge를 완료합니다.

## LAB 2 — Install / Dev / Build

```bash
node -v
npm -v
npm install
npm run dev
```

로컬 화면을 확인한 다음 개발 서버를 멈추고:

```bash
npm run build
npm run preview
```

**확인:** `package.json`의 `scripts`를 읽고 `dist/`의 역할을 설명합니다.

## LAB 3 — React Source Analysis

1. `index.html` → `src/main.jsx` → `src/App.jsx`를 추적합니다.
2. `Header`, `StatCard`, `UserList`의 Props를 찾습니다.
3. `UserList.jsx`에서 다음을 찾아보세요.
   - `useState`가 관리하는 값은?
   - `useRef`가 가리키는 DOM은?
   - 어떤 이벤트가 `setKeyword`를 호출하는가?
   - `filter()`와 `map()`은 각각 무엇을 하는가?
4. `UserList`를 화면에 그리는 데이터 흐름을 말로 설명합니다.

```text
users.js → App.jsx → UserList(initialUsers Props)
                         └→ keyword State → filter() → map() → JSX
```

**확인:** 파일 이름과 코드 위치를 근거로 기능을 설명할 수 있습니다.

## LAB 4 — Vercel Deployment

1. 연습용 **개인 Fork 저장소**를 Vercel 프로젝트로 Import합니다.
2. Vite 빌드 설정(`npm run build`, 출력 폴더 `dist`)을 확인하고 최초 배포합니다.
3. `feature/deploy-test` Branch에서 텍스트를 수정하고 Push합니다.
4. **Preview Deployment**를 확인합니다.
5. PR을 `main`에 Merge하고 **Production Deployment**가 갱신되는지 확인합니다.

**확인:** Preview URL과 Production URL이 서로 다른 환경을 가리킨다는 것을 이해합니다.

## LAB 5 — Axios GET (Console)

아직 UI에 표시하지 않습니다. `UserList.jsx`에서 버튼을 클릭했을 때 API 응답을 Console에 출력해 보세요.

1. `npm install axios`
2. `import axios from 'axios';`
3. 아래 함수를 `UserList` 함수 안에 추가합니다.

```jsx
const loadUsers = async () => {
  try {
    const response = await axios.get(
      'https://jsonplaceholder.typicode.com/users'
    );
    console.log(response.status, response.data);
  } catch (error) {
    console.error('Axios request failed:', error);
  }
};
```

4. 검색 입력창 아래에 `<button onClick={loadUsers}>Load API Users</button>`를 추가하여 실행합니다.
5. `response.data`가 배열인지, 각 객체에 어떤 필드가 있는지 확인합니다.

**확인:** 버튼 클릭으로 실제 GET 요청을 실행하고 `response.data[0].name`을 확인합니다.

## LAB 6 — useEffect + Axios + Loading/Error

목표는 **정적 users.js 배열을 API 사용자 목록으로 교체**하는 것입니다.

1. `UserList`에서 `initialUsers` Props를 제거하고 `users` State를 만듭니다.
2. `loading`과 `error` State를 추가합니다.
3. `useEffect` 안에서 Axios GET을 호출하고 응답을 `setUsers(response.data)`로 저장합니다.
4. Loading / Error / Empty 상태를 조건부 렌더링합니다.
5. 기존 `filteredUsers = users.filter(...)`와 검색 UI는 유지합니다.
6. 요청이 진행 중일 때 컴포넌트가 언마운트되면 오래된 응답이 State를 갱신하지 않도록 Cleanup을 작성합니다. (`AbortController` 또는 `ignore` 패턴)
7. `App.jsx`의 `UserList initialUsers={sampleUsers}`를 `<UserList />`로 변경합니다.

권장 State:

```jsx
const [users, setUsers] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
```

요청 처리 개념:

```text
Mount → useEffect → Axios GET → response.data → setUsers → Re-render
                      ├─ Loading → 안내 메시지
                      └─ Failure → Error 메시지
```

**확인:** 사용자 목록이 API 응답값으로 바뀌고, Network Throttling 또는 잘못된 API URL에서 Loading/Error 메시지를 확인합니다.

참고: 개발 모드의 React StrictMode에서는 Effect의 추가 Setup/Cleanup 확인 때문에 요청이 중복되어 보일 수 있습니다.

## LAB 7 — Public API: Open-Meteo Weather

1. 공식 문서를 확인합니다: <https://open-meteo.com/en/docs>
2. 우선 브라우저 또는 Postman에서 다음 URL을 호출합니다.

```text
https://api.open-meteo.com/v1/forecast?latitude=37.5665&longitude=126.9780&current=temperature_2m,wind_speed_10m,relative_humidity_2m
```

3. 응답의 `current`, `current_units`를 확인합니다.
4. `src/components/WeatherCard.jsx`를 만들어 Axios GET을 구현합니다.
5. State에 응답을 저장하고 **온도·풍속·습도**를 표시합니다.
6. `App.jsx`의 `WeatherPlaceholder`를 `WeatherCard`로 교체합니다.
7. 여유가 있으면 `select`를 추가하여 서울/포항/부산 중 한 도시를 선택할 수 있게 합니다.

권장 Params:

```js
{
  latitude: 37.5665,
  longitude: 126.9780,
  current: 'temperature_2m,wind_speed_10m,relative_humidity_2m',
  timezone: 'Asia/Seoul'
}
```

**확인:** 실제 API 응답에서 온도와 풍속이 UI에 표시됩니다. 날짜나 숫자는 고정값이 아닌 API 데이터여야 합니다.

## 학습 후 팀 프로젝트에 적용할 점

이 연습에서 만든 Mini Dashboard를 **팀 프로젝트로 제출하지 않습니다.** 팀별로 선정한 오픈소스에 아래 경험을 적용합니다.

- 기존 소스를 분석하고 F1 핵심 기능 실행
- F3 기본 기능 구현 및 GitHub 협업·Vercel 배포
- 14주차 F2에 사용할 Open API를 직접 탐색·호출·테스트하여 선정
- 실제 팀 프로젝트 과제 지침에 따라 결과물 제출


