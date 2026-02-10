# **튜토리얼 C: AI로 동적 웹 애플리케이션 만들기 (중급)**

**Claude Code**를 활용하여 데이터를 관리하고 사용자와 상호작용하는 동적 웹 애플리케이션을 제작합니다. React 기반의 할 일 관리(To-Do) 앱을 만들고, 외부 API 연동과 로컬 스토리지 저장까지 구현한 뒤 Vercel로 배포합니다.

**사용 도구**: Claude Code, VS Code, Node.js, React, Vercel

**사전 조건**: [튜토리얼 A](A.firstWebpageWithAI.md), [튜토리얼 B](B.landingPageWithAI.md)를 완료했거나, HTML/CSS/JavaScript 기본 개념을 이해하고 있는 상태

---

## **1. 사전 준비**

### **1-1. Node.js 설치**

React 프로젝트 생성과 실행에 Node.js가 필요합니다.

1. [Node.js 공식 사이트](https://nodejs.org/)에서 **LTS** 버전을 다운로드하여 설치합니다.
2. 설치 확인:

   ```bash
   node --version
   npm --version
   ```

### **1-2. VS Code 설치**

1. [Visual Studio Code 공식 사이트](https://code.visualstudio.com/)에서 다운로드하여 설치합니다.

### **1-3. Git 설치**

1. [Git 공식 사이트](https://git-scm.com/)에서 다운로드 후 설치합니다.
2. 설치 확인:

   ```bash
   git --version
   ```

3. 사용자 정보 설정 (처음인 경우):

   ```bash
   git config --global user.name "본인이름"
   git config --global user.email "본인이메일@example.com"
   ```

---

## **2. Claude Code 세팅**

### **2-1. Claude Code란?**

Claude Code는 Anthropic에서 만든 **터미널 기반 AI 코딩 어시스턴트**입니다. 터미널에서 직접 대화하며 파일 생성, 코드 작성, 디버깅, Git 작업까지 수행할 수 있습니다.

**GitHub Copilot과의 차이점**:

| 항목 | GitHub Copilot | Claude Code |
|---|---|---|
| 동작 방식 | VS Code 에디터 내 자동 완성/채팅 | 터미널에서 대화형으로 작업 |
| 파일 생성 | 코드를 복사하여 직접 붙여넣기 | AI가 직접 파일을 생성/수정 |
| 프로젝트 이해 | 열린 파일 중심 | 프로젝트 전체 구조를 파악 |
| 적합한 작업 | 코드 자동 완성, 부분 수정 | 프로젝트 생성, 대규모 작업, 디버깅 |

### **2-2. Claude Code 설치**

Claude Code는 npm을 통해 설치합니다:

```bash
npm install -g @anthropic-ai/claude-code
```

설치 확인:

```bash
claude --version
```

### **2-3. Anthropic 계정 연동**

1. 처음 실행 시 인증이 필요합니다:

   ```bash
   claude
   ```

2. 브라우저가 열리면 **Anthropic 계정으로 로그인**합니다.
   - 계정이 없다면 [Anthropic Console](https://console.anthropic.com/)에서 생성합니다.

3. 인증이 완료되면 터미널에 Claude Code 대화창이 나타납니다.

### **2-4. 기본 사용법**

Claude Code는 프로젝트 폴더에서 실행하면 해당 폴더 전체를 이해합니다:

```bash
cd my-project
claude
```

주요 명령어:

| 동작 | 방법 |
|---|---|
| AI에게 질문/요청 | 대화창에 자연어로 입력 |
| 파일 생성 요청 | `"index.html 파일을 만들어줘"` |
| 코드 수정 요청 | `"App.jsx에서 버튼 색상을 파란색으로 바꿔줘"` |
| 에러 디버깅 | `"이 에러를 해결해줘"` (에러 메시지 붙여넣기) |
| 대화 종료 | `/exit` 또는 `Ctrl+C` |

### **2-5. 정상 동작 확인**

```bash
mkdir test-claude && cd test-claude
claude
```

대화창에 다음과 같이 입력합니다:

```
"Hello World"를 출력하는 index.html 파일을 만들어줘
```

프로젝트 폴더에 `index.html` 파일이 생성되면 정상입니다. 확인 후 테스트 폴더를 삭제합니다:

```bash
cd .. && rm -rf test-claude
```

---

## **3. React 프로젝트 생성**

### **3-1. Claude Code로 프로젝트 생성**

프로젝트 폴더를 만들고 Claude Code를 실행합니다:

```bash
mkdir todo-app && cd todo-app
claude
```

Claude Code에 다음과 같이 요청합니다:

```
Vite를 사용해서 React 프로젝트를 초기화해줘.
프로젝트 이름은 현재 폴더에 바로 생성해줘.
```

Claude Code가 다음 명령어를 실행합니다:

```bash
npm create vite@latest . -- --template react
npm install
```

### **3-2. 프로젝트 구조 확인**

생성된 프로젝트 구조:

```
todo-app/
├── public/
├── src/
│   ├── App.jsx         ← 메인 컴포넌트
│   ├── App.css         ← 앱 스타일
│   ├── main.jsx        ← 진입점
│   └── index.css       ← 전역 스타일
├── index.html
├── package.json
└── vite.config.js
```

### **3-3. 개발 서버 실행 확인**

Claude Code에 요청:

```
개발 서버를 실행해줘
```

또는 직접 실행:

```bash
npm run dev
```

브라우저에서 `http://localhost:5173`에 접속하여 React 기본 페이지가 표시되면 준비 완료입니다.

---

## **4. 할 일 관리(To-Do) 앱 제작**

### **4-1. 기본 To-Do 기능 요청**

Claude Code에 다음과 같이 요청합니다:

```
할 일 관리(To-Do) 앱을 만들어줘.
기능:
1. 할 일 추가 (텍스트 입력 + 추가 버튼)
2. 할 일 목록 표시
3. 완료 체크 (체크하면 취소선)
4. 할 일 삭제
5. 남은 할 일 개수 표시

App.jsx에 작성하고, App.css에 깔끔한 스타일을 적용해줘.
색상 테마는 흰색 배경에 파란색(#2563eb) 포인트로 해줘.
```

Claude Code가 `App.jsx`와 `App.css`를 직접 수정합니다.

### **4-2. 생성되는 코드 예시**

**App.jsx**:

```jsx
import { useState } from 'react';
import './App.css';

function App() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState('');

  const addTodo = () => {
    if (input.trim() === '') return;
    setTodos([...todos, { id: Date.now(), text: input, completed: false }]);
    setInput('');
  };

  const toggleTodo = (id) => {
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  };

  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };

  const handleKeyPress = (e) => {
    if (e.key === 'Enter') addTodo();
  };

  const remainingCount = todos.filter(todo => !todo.completed).length;

  return (
    <div className="app">
      <h1>To-Do List</h1>
      <div className="input-area">
        <input
          type="text"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          onKeyPress={handleKeyPress}
          placeholder="할 일을 입력하세요"
        />
        <button onClick={addTodo}>추가</button>
      </div>
      <p className="remaining">남은 할 일: {remainingCount}개</p>
      <ul className="todo-list">
        {todos.map(todo => (
          <li key={todo.id} className={todo.completed ? 'completed' : ''}>
            <span onClick={() => toggleTodo(todo.id)}>{todo.text}</span>
            <button className="delete-btn" onClick={() => deleteTodo(todo.id)}>삭제</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

**App.css**:

```css
.app {
  max-width: 500px;
  margin: 60px auto;
  padding: 30px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
  text-align: center;
  color: #1a1a2e;
  margin-bottom: 30px;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

.input-area input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s;
}

.input-area input:focus {
  border-color: #2563eb;
}

.input-area button {
  padding: 12px 24px;
  background-color: #2563eb;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.input-area button:hover {
  background-color: #1e40af;
}

.remaining {
  color: #888;
  font-size: 0.9rem;
  margin-bottom: 10px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 16px;
  border-bottom: 1px solid #f0f0f0;
  transition: background-color 0.2s;
}

.todo-list li:hover {
  background-color: #f8fafc;
}

.todo-list li span {
  cursor: pointer;
  flex: 1;
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: #aaa;
}

.delete-btn {
  background: none;
  border: none;
  color: #ef4444;
  cursor: pointer;
  font-size: 0.9rem;
  padding: 4px 8px;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.delete-btn:hover {
  background-color: #fef2f2;
}
```

### **4-3. 브라우저에서 확인**

개발 서버(`npm run dev`)가 실행 중이면 저장 즉시 브라우저에 반영됩니다. 할 일 추가, 체크, 삭제가 정상 동작하는지 확인합니다.

---

## **5. 로컬 스토리지로 데이터 저장**

현재 상태에서는 페이지를 새로고침하면 할 일 목록이 사라집니다. **로컬 스토리지**를 활용하여 데이터를 브라우저에 영구 저장합니다.

### **5-1. Claude Code에 요청**

```
할 일 데이터를 브라우저 로컬 스토리지에 저장해줘.
- 페이지를 새로고침해도 데이터가 유지되도록
- 할 일이 추가/수정/삭제될 때마다 자동 저장
- 처음 로딩 시 로컬 스토리지에서 데이터를 불러오기
```

### **5-2. Claude Code가 수정하는 코드**

Claude Code가 `App.jsx`의 상태 관리 부분을 수정합니다:

```jsx
import { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [todos, setTodos] = useState(() => {
    const saved = localStorage.getItem('todos');
    return saved ? JSON.parse(saved) : [];
  });
  const [input, setInput] = useState('');

  // todos가 변경될 때마다 로컬 스토리지에 저장
  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos));
  }, [todos]);

  // ... 나머지 함수들은 동일
}
```

### **5-3. 확인**

1. 할 일을 몇 개 추가합니다.
2. 브라우저를 새로고침(`F5`)합니다.
3. 할 일 목록이 그대로 유지되면 성공입니다.

---

## **6. 외부 API 연동 - 날씨 정보 표시**

할 일 앱 상단에 현재 날씨 정보를 표시하는 기능을 추가합니다. 무료 공개 API인 **Open-Meteo**를 사용합니다 (API 키 불필요).

### **6-1. Claude Code에 요청**

```
할 일 앱 상단에 현재 서울 날씨를 표시하는 기능을 추가해줘.
조건:
- Open-Meteo API 사용 (https://api.open-meteo.com)
- 서울 좌표: 위도 37.5665, 경도 126.9780
- 현재 기온과 날씨 상태를 표시
- 컴포넌트를 별도 파일(Weather.jsx)로 분리
- 로딩 중 상태와 에러 처리 포함
```

### **6-2. Claude Code가 생성하는 파일**

**src/Weather.jsx**:

```jsx
import { useState, useEffect } from 'react';

// 날씨 코드를 한글 설명으로 변환
const weatherDescriptions = {
  0: '맑음 ☀️',
  1: '대체로 맑음 🌤️',
  2: '부분적으로 흐림 ⛅',
  3: '흐림 ☁️',
  51: '가벼운 이슬비 🌦️',
  61: '약한 비 🌧️',
  71: '약한 눈 🌨️',
  95: '뇌우 ⛈️',
};

function Weather() {
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(
      'https://api.open-meteo.com/v1/forecast?latitude=37.5665&longitude=126.9780&current_weather=true&timezone=Asia/Seoul'
    )
      .then((res) => res.json())
      .then((data) => {
        setWeather(data.current_weather);
        setLoading(false);
      })
      .catch((err) => {
        setError('날씨 정보를 가져올 수 없습니다.');
        setLoading(false);
      });
  }, []);

  if (loading) return <div className="weather">날씨 정보 로딩 중...</div>;
  if (error) return <div className="weather">{error}</div>;

  const description = weatherDescriptions[weather.weathercode] || '알 수 없음';

  return (
    <div className="weather">
      <span>서울 {weather.temperature}°C</span>
      <span>{description}</span>
    </div>
  );
}

export default Weather;
```

**App.jsx** 상단에 Weather 컴포넌트를 추가:

```jsx
import Weather from './Weather';

// return 내부, h1 위에 추가
<Weather />
<h1>To-Do List</h1>
```

**App.css**에 날씨 스타일 추가:

```css
.weather {
  display: flex;
  justify-content: center;
  gap: 15px;
  padding: 10px;
  background-color: #eff6ff;
  border-radius: 8px;
  margin-bottom: 20px;
  font-size: 0.95rem;
  color: #1e40af;
}
```

### **6-3. 확인**

브라우저에서 앱 상단에 서울의 현재 기온과 날씨 상태가 표시되면 성공입니다.

---

## **7. 에러 발생 시 Claude Code와 디버깅하기**

개발 중 에러가 발생하면 Claude Code와 함께 해결할 수 있습니다.

### **7-1. 에러 디버깅 워크플로우**

1. **에러 메시지 확인**: 터미널 또는 브라우저 콘솔(`F12` > Console)에서 에러 메시지를 확인합니다.

2. **Claude Code에 에러 전달**:

   ```
   다음 에러가 발생했어. 해결해줘:

   [에러 메시지를 그대로 붙여넣기]
   ```

3. **Claude Code가 원인을 분석하고 수정 사항을 적용합니다.**

### **7-2. 흔한 에러와 요청 예시**

| 에러 상황 | Claude Code에 요청할 내용 |
|---|---|
| 모듈 import 에러 | `"Cannot find module 에러가 나. 확인해줘"` |
| 화면이 안 나옴 | `"화면이 빈 페이지로 나와. 콘솔에 이런 에러가 있어: [에러메시지]"` |
| 스타일 깨짐 | `"카드 레이아웃이 세로로 쌓여. 가로 3열로 배치해줘"` |
| API 호출 실패 | `"날씨 API 호출 시 CORS 에러가 발생해. 해결해줘"` |
| 빌드 실패 | `"npm run build 하면 이런 에러가 나: [에러메시지]"` |

### **7-3. 프로젝트 전체를 파악한 디버깅**

Claude Code의 장점은 프로젝트 전체 구조를 이해한다는 점입니다:

```
현재 프로젝트 구조를 분석하고, 문제가 있는 부분이 있으면 알려줘
```

```
코드에서 개선할 부분이 있으면 알려줘
```

---

## **8. 추가 기능 구현**

기본 To-Do 앱이 완성되면 Claude Code에 추가 기능을 요청하여 앱을 확장합니다.

### **8-1. 카테고리 필터 추가**

```
할 일에 카테고리 기능을 추가해줘.
- 카테고리: 전체, 업무, 개인, 학습
- 할 일 추가 시 카테고리 선택 드롭다운
- 상단에 카테고리 필터 탭 (클릭하면 해당 카테고리만 표시)
```

### **8-2. 마감일 설정**

```
할 일에 마감일 기능을 추가해줘.
- 날짜 선택 input 추가
- 마감일이 지난 항목은 빨간색으로 표시
- 마감일 기준으로 정렬 옵션 추가
```

### **8-3. 다크 모드**

```
다크 모드 토글 버튼을 추가해줘.
- 상단에 해/달 아이콘 토글 버튼
- 다크 모드 설정을 로컬 스토리지에 저장
- 부드러운 전환 애니메이션
```

---

## **9. Vercel로 배포**

### **9-1. 빌드 확인**

배포 전 빌드가 정상적으로 되는지 확인합니다:

```bash
npm run build
```

`dist` 폴더가 생성되면 성공입니다. 에러가 발생하면 Claude Code에 에러 메시지를 전달하여 해결합니다.

### **9-2. Git 저장소 준비**

```bash
git init
git add .
git commit -m "할 일 관리 앱 제작"
```

### **9-3. GitHub 원격 저장소 생성 및 업로드**

1. [GitHub](https://github.com/)에서 **New repository**를 생성합니다.
   - Repository name: `todo-app`
   - **Public** 선택

2. 코드 업로드:

   ```bash
   git remote add origin https://github.com/본인아이디/todo-app.git
   git branch -M main
   git push -u origin main
   ```

### **9-4. Vercel 연동 및 배포**

1. [Vercel](https://vercel.com/)에 접속하여 **GitHub 계정으로 로그인**합니다.
2. **Add New Project** > `todo-app` 저장소를 선택합니다.
3. Vercel이 Vite 프로젝트를 자동 감지합니다. 설정은 기본값 그대로 두고 **Deploy**를 클릭합니다.
4. 약 1분 후 배포가 완료되고 URL이 생성됩니다.
   - 예: `https://todo-app-username.vercel.app`

### **9-5. 커스텀 도메인 연결 (선택)**

1. Vercel 프로젝트 대시보드에서 **Settings > Domains**로 이동합니다.
2. 보유한 도메인을 입력하고 **Add**를 클릭합니다.
3. Vercel이 안내하는 DNS 레코드를 도메인 관리 사이트에서 설정합니다.
4. DNS 전파 후 (최대 48시간, 보통 수 분) 커스텀 도메인으로 접속할 수 있습니다.

### **9-6. 이후 업데이트**

코드를 수정한 후 push하면 Vercel이 자동으로 재배포합니다:

```bash
git add .
git commit -m "기능 업데이트"
git push
```

---

## **주의 사항**

- **Claude Code 사용량**: Claude Code는 Anthropic 계정의 사용량 정책에 따라 제한이 있을 수 있습니다. 사용 전 [Anthropic Console](https://console.anthropic.com/)에서 플랜을 확인하세요.
- **API 키 관리**: 외부 API 키가 필요한 경우(예: 유료 날씨 API), 코드에 직접 입력하지 말고 `.env` 파일을 사용하고 `.gitignore`에 추가하세요.
- **코드 검토**: Claude Code가 생성/수정한 코드는 반드시 동작을 확인하고, 의도와 다른 부분은 추가 요청으로 수정하세요.
- **Git 커밋 습관**: 기능 하나가 완성될 때마다 커밋하는 습관을 들이면, 문제가 발생했을 때 이전 상태로 되돌리기 쉽습니다.

---

이 튜토리얼을 완료하면 React 기반의 동적 웹 애플리케이션을 Claude Code와 함께 제작하고, 외부 API 연동, 데이터 저장, 배포까지 전 과정을 경험하게 됩니다. 이 경험을 바탕으로 더 복잡한 웹 애플리케이션 개발에 도전해보세요.
