# **튜토리얼 A: AI와 함께 첫 웹페이지 만들기 (입문)**

코딩 경험이 없어도 **GitHub Copilot**을 활용하면 자기소개 웹페이지를 직접 만들 수 있습니다. 이 튜토리얼에서는 GitHub Copilot 세팅부터 웹페이지 제작, GitHub Pages 배포까지 전 과정을 단계별로 안내합니다.

**사용 도구**: GitHub Copilot, VS Code, Git, 웹 브라우저

---

## **1. 사전 준비**

### **1-1. VS Code 설치**

1. [Visual Studio Code 공식 사이트](https://code.visualstudio.com/)에서 본인 운영체제에 맞는 버전을 다운로드합니다.
2. 설치 파일을 실행하여 설치를 완료합니다.

### **1-2. Git 설치**

GitHub Pages 배포를 위해 Git이 필요합니다.

1. [Git 공식 사이트](https://git-scm.com/)에서 다운로드 후 설치합니다.
2. 설치 확인 - 터미널(또는 명령 프롬프트)에서 다음 명령어를 실행합니다:

   ```bash
   git --version
   ```

3. 처음 사용하는 경우 사용자 정보를 설정합니다:

   ```bash
   git config --global user.name "본인이름"
   git config --global user.email "본인이메일@example.com"
   ```

### **1-3. GitHub 계정 생성**

1. [GitHub](https://github.com/)에 접속하여 계정을 생성합니다.
2. 이메일 인증을 완료합니다.

---

## **2. GitHub Copilot 세팅**

### **2-1. GitHub Copilot 구독**

1. [GitHub Copilot 페이지](https://github.com/features/copilot)에 접속합니다.
2. **플랜 선택**:
   - **Copilot Free**: 무료, 월 사용량 제한 있음 (시작하기에 충분)
   - **Copilot Pro**: 월 $10, 무제한 사용
3. 원하는 플랜을 선택하고 구독을 완료합니다.

### **2-2. VS Code에 GitHub Copilot 확장 설치**

1. VS Code를 실행합니다.
2. 왼쪽 사이드바에서 **확장(Extensions)** 아이콘(네모 4개 모양)을 클릭합니다.
3. 검색창에 `GitHub Copilot`을 입력합니다.
4. **GitHub Copilot** 확장을 찾아 **Install** 버튼을 클릭합니다.
5. 함께 **GitHub Copilot Chat**도 설치합니다 — 이것이 AI와 대화하며 코드를 작성하는 핵심 도구입니다.

### **2-3. GitHub 계정 연동**

1. 확장 설치 후 VS Code 우측 하단에 GitHub 로그인 알림이 나타납니다.
2. **Sign in to GitHub**를 클릭합니다.
3. 브라우저가 열리면 GitHub 계정으로 로그인하고 **Authorize** 버튼을 클릭합니다.
4. VS Code로 돌아오면 연동이 완료됩니다.

### **2-4. Copilot 정상 동작 확인**

1. VS Code에서 새 파일을 만들고 (`Ctrl+N` 또는 `Cmd+N`), 언어를 **HTML**로 설정합니다.
2. `<!` 를 입력하면 Copilot이 자동으로 HTML 기본 구조를 제안합니다.
3. 제안이 나타나면 `Tab` 키로 수락할 수 있습니다.
4. **Copilot Chat** 확인: `Ctrl+Shift+I` (Mac: `Cmd+Shift+I`)로 Copilot Chat 패널을 열 수 있는지 확인합니다.

> Copilot Chat이 열리지 않는 경우 VS Code를 재시작한 후 다시 시도합니다.

---

## **3. 프로젝트 폴더 생성**

### **3-1. 작업 폴더 만들기**

1. 원하는 위치에 프로젝트 폴더를 생성합니다:

   ```bash
   mkdir my-profile-page
   cd my-profile-page
   ```

2. VS Code에서 해당 폴더를 엽니다:

   ```bash
   code .
   ```

### **3-2. 기본 파일 생성**

VS Code에서 다음 파일을 생성합니다:
- `index.html` — 웹페이지 구조
- `style.css` — 디자인 스타일

> **파일 생성 방법**: 왼쪽 탐색기(Explorer)에서 마우스 오른쪽 클릭 > **New File** 클릭

---

## **4. Copilot Chat으로 자기소개 웹페이지 만들기**

### **4-1. Copilot Chat 열기**

1. `Ctrl+Shift+I` (Mac: `Cmd+Shift+I`)를 눌러 Copilot Chat을 엽니다.
2. 또는 왼쪽 사이드바의 **Copilot Chat 아이콘**을 클릭합니다.

### **4-2. HTML 구조 요청하기**

Copilot Chat에 다음과 같이 프롬프트를 입력합니다:

```
자기소개 원페이지 웹사이트의 HTML을 만들어줘.
다음 섹션들을 포함해줘:
1. 상단 네비게이션 바 (이름, 소개/기술/포트폴리오/연락처 메뉴)
2. 히어로 섹션 (이름, 한 줄 소개, 프로필 이미지 자리)
3. 소개 섹션 (자기소개 텍스트)
4. 기술 스택 섹션 (기술 목록을 카드 형태로)
5. 포트폴리오 섹션 (프로젝트 카드 3개)
6. 연락처 섹션 (이메일, GitHub 링크)
7. 푸터

외부 CSS 파일(style.css)을 연결하고, 한국어로 작성해줘.
```

### **4-3. 생성된 코드 적용하기**

1. Copilot이 생성한 HTML 코드를 확인합니다.
2. 코드 블록 상단의 **복사** 아이콘 또는 **Insert at Cursor** 버튼을 클릭하여 `index.html`에 적용합니다.
3. 결과 예시:

   ```html
   <!DOCTYPE html>
   <html lang="ko">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>홍길동 | 포트폴리오</title>
     <link rel="stylesheet" href="style.css">
   </head>
   <body>
     <nav class="navbar">
       <div class="nav-logo">홍길동</div>
       <ul class="nav-links">
         <li><a href="#about">소개</a></li>
         <li><a href="#skills">기술</a></li>
         <li><a href="#portfolio">포트폴리오</a></li>
         <li><a href="#contact">연락처</a></li>
       </ul>
     </nav>

     <section class="hero" id="hero">
       <div class="hero-content">
         <h1>안녕하세요, 홍길동입니다</h1>
         <p>주니어 웹 개발자를 꿈꾸는 대학생입니다</p>
       </div>
     </section>

     <section class="about" id="about">
       <h2>소개</h2>
       <p>자동화와 웹 개발에 관심이 많은 개발자입니다.
          새로운 기술을 배우고 실제 프로젝트에 적용하는 것을 좋아합니다.</p>
     </section>

     <section class="skills" id="skills">
       <h2>기술 스택</h2>
       <div class="skills-grid">
         <div class="skill-card">HTML/CSS</div>
         <div class="skill-card">JavaScript</div>
         <div class="skill-card">Google Apps Script</div>
         <div class="skill-card">Git/GitHub</div>
       </div>
     </section>

     <section class="portfolio" id="portfolio">
       <h2>포트폴리오</h2>
       <div class="portfolio-grid">
         <div class="portfolio-card">
           <h3>프로젝트 1</h3>
           <p>구글 폼 자동 응답 시스템</p>
         </div>
         <div class="portfolio-card">
           <h3>프로젝트 2</h3>
           <p>스프레드시트 배송 알림 자동화</p>
         </div>
         <div class="portfolio-card">
           <h3>프로젝트 3</h3>
           <p>고객 리드 수집 웹 앱</p>
         </div>
       </div>
     </section>

     <section class="contact" id="contact">
       <h2>연락처</h2>
       <p>이메일: hong@example.com</p>
       <p>GitHub: github.com/honggildong</p>
     </section>

     <footer>
       <p>&copy; 2025 홍길동. All rights reserved.</p>
     </footer>
   </body>
   </html>
   ```

### **4-4. 브라우저에서 확인하기**

1. `index.html` 파일을 마우스 오른쪽 버튼으로 클릭합니다.
2. **Open with Live Server**를 선택합니다.
   - Live Server가 없다면: 확장(Extensions)에서 `Live Server`를 검색하여 설치합니다.
3. 브라우저에 웹페이지가 표시됩니다. 아직 CSS가 없으므로 기본 스타일로 보입니다.

---

## **5. CSS 디자인 입히기**

### **5-1. Copilot Chat에 CSS 요청하기**

`style.css` 파일을 열고, Copilot Chat에 다음과 같이 요청합니다:

```
위 HTML에 어울리는 모던한 CSS를 작성해줘.
조건:
- 깔끔하고 미니멀한 디자인
- 색상 테마는 네이비(#1a1a2e)와 화이트 기반
- 네비게이션은 상단 고정
- 히어로 섹션은 전체 화면 높이
- 기술 카드와 포트폴리오 카드는 그리드 레이아웃
- 부드러운 스크롤과 hover 효과 포함
```

### **5-2. 생성된 CSS 적용**

Copilot이 생성한 CSS를 `style.css`에 적용합니다. 결과 예시:

```css
/* 기본 초기화 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
  line-height: 1.6;
}

/* 네비게이션 */
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 40px;
  background-color: #1a1a2e;
  color: white;
  z-index: 100;
}

.nav-logo {
  font-size: 1.4rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 25px;
}

.nav-links a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #e94560;
}

/* 히어로 섹션 */
.hero {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: linear-gradient(135deg, #1a1a2e, #16213e);
  color: white;
}

.hero h1 {
  font-size: 2.8rem;
  margin-bottom: 15px;
}

.hero p {
  font-size: 1.2rem;
  color: #ccc;
}

/* 공통 섹션 */
section {
  padding: 80px 40px;
  max-width: 1000px;
  margin: 0 auto;
}

section h2 {
  font-size: 2rem;
  margin-bottom: 30px;
  color: #1a1a2e;
  text-align: center;
}

/* 소개 섹션 */
.about p {
  font-size: 1.1rem;
  text-align: center;
  max-width: 700px;
  margin: 0 auto;
}

/* 기술 스택 */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 20px;
}

.skill-card {
  background-color: #f0f0f0;
  padding: 25px;
  text-align: center;
  border-radius: 8px;
  font-weight: bold;
  transition: transform 0.3s, box-shadow 0.3s;
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

/* 포트폴리오 */
.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
}

.portfolio-card {
  background-color: #fff;
  border: 1px solid #e0e0e0;
  padding: 30px;
  border-radius: 8px;
  transition: transform 0.3s, box-shadow 0.3s;
}

.portfolio-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.portfolio-card h3 {
  margin-bottom: 10px;
  color: #1a1a2e;
}

/* 연락처 */
.contact {
  text-align: center;
}

.contact p {
  font-size: 1.1rem;
  margin-bottom: 10px;
}

/* 푸터 */
footer {
  text-align: center;
  padding: 25px;
  background-color: #1a1a2e;
  color: #aaa;
}
```

### **5-3. 브라우저에서 확인**

Live Server가 실행 중이라면 저장 즉시 브라우저에 변경 사항이 반영됩니다. 네이비 색상 기반의 깔끔한 자기소개 페이지가 보일 것입니다.

---

## **6. AI에게 수정 요청하여 반복 개선하기**

웹페이지가 마음에 들지 않는 부분이 있다면 Copilot Chat에 자연어로 수정을 요청합니다.

### **6-1. 수정 요청 프롬프트 예시**

원하는 부분을 구체적으로 설명할수록 좋은 결과를 얻을 수 있습니다:

| 요청 | 프롬프트 예시 |
|---|---|
| 색상 변경 | `히어로 섹션 배경색을 파란색 그라데이션에서 진한 초록색 계열로 바꿔줘` |
| 폰트 변경 | `Google Fonts에서 Noto Sans KR 폰트를 적용해줘` |
| 프로필 이미지 추가 | `히어로 섹션에 둥근 프로필 이미지를 추가해줘. 이미지 파일명은 profile.jpg로 해줘` |
| 애니메이션 추가 | `각 섹션이 스크롤할 때 아래에서 위로 페이드인되는 애니메이션을 추가해줘` |
| 내용 수정 | `기술 스택에 Python과 React를 추가해줘` |

### **6-2. 수정 적용 워크플로우**

1. Copilot Chat에 수정 요청 입력
2. 생성된 코드를 확인
3. 기존 코드와 비교하여 변경 부분만 적용 (또는 전체 교체)
4. 브라우저에서 결과 확인
5. 만족할 때까지 반복

> **팁**: 한 번에 여러 가지를 요청하기보다, 하나씩 수정하며 결과를 확인하는 것이 더 정확합니다.

---

## **7. 반응형 레이아웃 적용**

모바일과 태블릿에서도 잘 보이도록 반응형 디자인을 추가합니다.

### **7-1. Copilot Chat에 반응형 CSS 요청**

```
현재 style.css에 모바일 반응형 디자인을 추가해줘.
조건:
- 768px 이하에서 네비게이션을 세로로 변경
- 기술 카드와 포트폴리오 카드를 1열로 변경
- 히어로 섹션 글자 크기 축소
- 전체적으로 모바일에서 여백 조정
```

### **7-2. 생성된 미디어 쿼리 적용**

`style.css` 하단에 추가합니다:

```css
/* 반응형 디자인 */
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    padding: 10px 20px;
  }

  .nav-links {
    margin-top: 10px;
    gap: 15px;
  }

  .hero h1 {
    font-size: 1.8rem;
  }

  .hero p {
    font-size: 1rem;
  }

  section {
    padding: 50px 20px;
  }

  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .portfolio-grid {
    grid-template-columns: 1fr;
  }
}
```

### **7-3. 반응형 확인 방법**

1. 브라우저에서 `F12`를 눌러 개발자 도구를 엽니다.
2. 상단의 **기기 전환 아이콘**(Toggle Device Toolbar)을 클릭합니다.
3. 다양한 기기 크기(iPhone, iPad 등)에서 레이아웃을 확인합니다.

---

## **8. GitHub Pages로 무료 배포**

### **8-1. Git 저장소 초기화**

프로젝트 폴더에서 터미널을 열고 다음 명령어를 실행합니다:

```bash
git init
git add index.html style.css
git commit -m "자기소개 웹페이지 제작"
```

### **8-2. GitHub 원격 저장소 생성**

1. [GitHub](https://github.com/)에 로그인합니다.
2. 우측 상단 **+** 버튼 > **New repository**를 클릭합니다.
3. 저장소 설정:
   - **Repository name**: `my-profile-page`
   - **Public** 선택 (GitHub Pages 무료 사용을 위해 필수)
4. **Create repository**를 클릭합니다.

### **8-3. 코드 업로드**

생성된 저장소 페이지에 표시된 명령어를 참고하여 실행합니다:

```bash
git remote add origin https://github.com/본인아이디/my-profile-page.git
git branch -M main
git push -u origin main
```

### **8-4. GitHub Pages 활성화**

1. GitHub 저장소 페이지에서 **Settings** 탭을 클릭합니다.
2. 왼쪽 메뉴에서 **Pages**를 클릭합니다.
3. **Source** 항목에서:
   - **Branch**: `main` 선택
   - **Folder**: `/ (root)` 선택
4. **Save** 버튼을 클릭합니다.

### **8-5. 배포 확인**

1. 약 1~2분 후 페이지 상단에 배포 URL이 표시됩니다.
2. URL 형식: `https://본인아이디.github.io/my-profile-page/`
3. 해당 URL에 접속하여 웹페이지가 정상적으로 표시되는지 확인합니다.

---

## **9. 이후 업데이트 방법**

내용을 수정한 후 다시 배포하려면 다음 명령어를 실행합니다:

```bash
git add .
git commit -m "웹페이지 내용 업데이트"
git push
```

push 후 1~2분 이내에 GitHub Pages에 변경 사항이 자동 반영됩니다.

---

## **주의 사항**

- **Copilot 코드 검토**: AI가 생성한 코드는 항상 브라우저에서 결과를 확인하고, 의도와 다른 부분이 있으면 추가 수정을 요청하세요.
- **개인정보**: 연락처, 이메일 등 민감한 정보를 Public 저장소에 올릴 때는 스팸 방지를 위해 이메일을 이미지로 대체하거나 문의 폼을 활용하는 것을 권장합니다.
- **이미지 파일**: 프로필 이미지 등을 추가할 경우 프로젝트 폴더에 이미지를 넣고 `git add`에 포함시켜야 배포 시 표시됩니다.

---

이 튜토리얼을 완료하면 GitHub Copilot을 활용하여 웹페이지를 제작하고 배포하는 전체 과정을 경험하게 됩니다. 다음 단계인 **튜토리얼 B**에서는 이 경험을 바탕으로 실제 비즈니스용 랜딩페이지를 제작해봅니다.
