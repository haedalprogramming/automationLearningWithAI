# **튜토리얼 B: AI로 랜딩페이지 제작하기 (초급)**

제품 또는 서비스를 소개하는 **랜딩페이지**를 **GitHub Copilot**과 함께 제작합니다. 실제 비즈니스에서 활용할 수 있는 수준의 페이지를 만들며, 고객 문의 폼을 **Google Apps Script**와 연동하여 데이터를 자동 수집하는 것까지 다룹니다.

**사용 도구**: GitHub Copilot, VS Code, Git, Google Sheets, Google Apps Script

**사전 조건**: [튜토리얼 A](A.firstWebpageWithAI.md)를 완료했거나, VS Code와 GitHub Copilot이 세팅된 상태

---

## **1. 사전 준비**

### **1-1. VS Code 설치**

1. [Visual Studio Code 공식 사이트](https://code.visualstudio.com/)에서 본인 운영체제에 맞는 버전을 다운로드합니다.
2. 설치 파일을 실행하여 설치를 완료합니다.

### **1-2. Git 설치**

1. [Git 공식 사이트](https://git-scm.com/)에서 다운로드 후 설치합니다.
2. 설치 확인:

   ```bash
   git --version
   ```

3. 처음 사용하는 경우 사용자 정보를 설정합니다:

   ```bash
   git config --global user.name "본인이름"
   git config --global user.email "본인이메일@example.com"
   ```

### **1-3. Node.js 설치**

Vercel 배포를 위해 Node.js가 필요합니다.

1. [Node.js 공식 사이트](https://nodejs.org/)에서 **LTS** 버전을 다운로드하여 설치합니다.
2. 설치 확인:

   ```bash
   node --version
   npm --version
   ```

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
2. 왼쪽 사이드바에서 **확장(Extensions)** 아이콘을 클릭합니다.
3. 검색창에 `GitHub Copilot`을 입력합니다.
4. **GitHub Copilot**과 **GitHub Copilot Chat**을 모두 설치합니다.

### **2-3. GitHub 계정 연동**

1. 확장 설치 후 VS Code 우측 하단에 GitHub 로그인 알림이 나타납니다.
2. **Sign in to GitHub**를 클릭합니다.
3. 브라우저에서 GitHub 계정으로 로그인하고 **Authorize**를 클릭합니다.
4. VS Code로 돌아오면 연동이 완료됩니다.

### **2-4. Copilot 정상 동작 확인**

1. VS Code에서 새 파일을 만들고 (`Ctrl+N` 또는 `Cmd+N`), 언어를 **HTML**로 설정합니다.
2. `<!`를 입력하면 Copilot이 자동으로 HTML 기본 구조를 제안합니다.
3. `Ctrl+Shift+I` (Mac: `Cmd+Shift+I`)로 Copilot Chat 패널이 열리는지 확인합니다.

---

## **3. 프로젝트 구조 설정**

### **3-1. 프로젝트 폴더 생성**

```bash
mkdir my-landing-page
cd my-landing-page
code .
```

### **3-2. 파일 구조**

VS Code에서 다음 파일을 생성합니다:

```
my-landing-page/
├── index.html      ← 메인 페이지
├── style.css       ← 스타일
└── script.js       ← 문의 폼 전송 스크립트
```

---

## **4. 랜딩페이지 구조 이해**

코드를 작성하기 전에 랜딩페이지의 핵심 구성 요소를 이해합니다. Copilot에게 **섹션별로 나누어 요청**하면 더 정확한 결과를 얻을 수 있습니다.

| 순서 | 섹션 | 역할 |
|---|---|---|
| 1 | 네비게이션 바 | 로고, 메뉴 링크, CTA 버튼 |
| 2 | 히어로 섹션 | 핵심 메시지, 서브 타이틀, 행동 유도 버튼 |
| 3 | 서비스 소개 | 제공하는 서비스/기능을 카드 형태로 소개 |
| 4 | 특장점(Why Us) | 경쟁 우위 또는 핵심 가치 강조 |
| 5 | 고객 후기 | 신뢰도 확보를 위한 사회적 증거 |
| 6 | 문의 폼 | 고객 리드 수집 (이름, 이메일, 메시지) |
| 7 | 푸터 | 회사 정보, 링크, 저작권 표시 |

> **프롬프트 전략**: 전체를 한 번에 요청하기보다, 위 표 순서대로 섹션 하나씩 요청하면 품질이 높아집니다.

---

## **5. 섹션별 코드 작성**

### **5-1. HTML 기본 뼈대 + 외부 라이브러리 연결**

`index.html`을 열고 Copilot Chat에 다음과 같이 요청합니다:

```
랜딩페이지의 HTML 기본 뼈대를 만들어줘.
조건:
- Google Fonts에서 Noto Sans KR 폰트 연결
- Font Awesome 아이콘 CDN 연결
- 외부 CSS(style.css)와 JS(script.js) 파일 연결
- 한국어 설정
```

결과 예시:

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>서비스명 | 비즈니스 솔루션</title>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&display=swap" rel="stylesheet">

  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- 여기에 섹션별 코드를 추가합니다 -->

  <script src="script.js"></script>
</body>
</html>
```

### **5-2. 네비게이션 바**

Copilot Chat에 요청:

```
랜딩페이지 네비게이션 바 HTML을 작성해줘.
- 왼쪽에 로고(텍스트)
- 오른쪽에 메뉴: 서비스, 특장점, 후기, 문의
- 맨 오른쪽에 "무료 상담" CTA 버튼
```

결과 예시:

```html
<nav class="navbar">
  <div class="nav-container">
    <a href="#" class="nav-logo">BizSolution</a>
    <ul class="nav-links">
      <li><a href="#services">서비스</a></li>
      <li><a href="#why-us">특장점</a></li>
      <li><a href="#reviews">후기</a></li>
      <li><a href="#contact">문의</a></li>
    </ul>
    <a href="#contact" class="nav-cta">무료 상담</a>
  </div>
</nav>
```

### **5-3. 히어로 섹션**

Copilot Chat에 요청:

```
히어로 섹션 HTML을 작성해줘.
- 큰 제목: "비즈니스 성장을 위한 자동화 솔루션"
- 서브 타이틀: 간단한 설명 문구
- CTA 버튼 2개: "무료 체험 시작" (강조), "자세히 알아보기" (보조)
```

결과 예시:

```html
<section class="hero" id="hero">
  <div class="hero-content">
    <h1>비즈니스 성장을 위한<br>자동화 솔루션</h1>
    <p>반복 업무를 자동화하여 팀의 생산성을 높이고,<br>핵심 업무에 집중할 수 있도록 도와드립니다.</p>
    <div class="hero-buttons">
      <a href="#contact" class="btn btn-primary">무료 체험 시작</a>
      <a href="#services" class="btn btn-secondary">자세히 알아보기</a>
    </div>
  </div>
</section>
```

### **5-4. 서비스 소개 섹션**

Copilot Chat에 요청:

```
서비스 소개 섹션 HTML을 작성해줘.
- 섹션 제목: "제공 서비스"
- 카드 3개, 각 카드에 Font Awesome 아이콘, 제목, 설명 포함
- 서비스 예시: 업무 자동화, 데이터 분석, 고객 관리
```

결과 예시:

```html
<section class="services" id="services">
  <h2>제공 서비스</h2>
  <p class="section-subtitle">비즈니스에 필요한 핵심 솔루션을 제공합니다</p>
  <div class="services-grid">
    <div class="service-card">
      <i class="fas fa-cogs"></i>
      <h3>업무 자동화</h3>
      <p>반복적인 업무를 자동화하여 시간과 비용을 절감합니다. 이메일 발송, 데이터 입력, 보고서 생성을 자동으로 처리합니다.</p>
    </div>
    <div class="service-card">
      <i class="fas fa-chart-line"></i>
      <h3>데이터 분석</h3>
      <p>수집된 데이터를 분석하여 비즈니스 인사이트를 제공합니다. 실시간 대시보드로 핵심 지표를 한눈에 파악할 수 있습니다.</p>
    </div>
    <div class="service-card">
      <i class="fas fa-users"></i>
      <h3>고객 관리</h3>
      <p>고객 리드를 체계적으로 관리하고, 자동 후속 조치를 통해 전환율을 높입니다.</p>
    </div>
  </div>
</section>
```

### **5-5. 특장점(Why Us) 섹션**

Copilot Chat에 요청:

```
특장점 섹션 HTML을 작성해줘.
- 섹션 제목: "왜 BizSolution인가요?"
- 왼쪽에 특장점 리스트 3개 (아이콘 + 제목 + 설명)
- 숫자 강조 포함 (예: 도입 기업 500+, 업무 시간 70% 절감)
```

결과 예시:

```html
<section class="why-us" id="why-us">
  <h2>왜 BizSolution인가요?</h2>
  <div class="stats-grid">
    <div class="stat-item">
      <span class="stat-number">500+</span>
      <span class="stat-label">도입 기업</span>
    </div>
    <div class="stat-item">
      <span class="stat-number">70%</span>
      <span class="stat-label">업무 시간 절감</span>
    </div>
    <div class="stat-item">
      <span class="stat-number">98%</span>
      <span class="stat-label">고객 만족도</span>
    </div>
  </div>
  <div class="features-list">
    <div class="feature-item">
      <i class="fas fa-check-circle"></i>
      <div>
        <h3>코딩 없이 설정</h3>
        <p>개발자 없이도 누구나 쉽게 자동화를 설정할 수 있습니다.</p>
      </div>
    </div>
    <div class="feature-item">
      <i class="fas fa-check-circle"></i>
      <div>
        <h3>실시간 모니터링</h3>
        <p>자동화 현황을 실시간으로 확인하고 관리할 수 있습니다.</p>
      </div>
    </div>
    <div class="feature-item">
      <i class="fas fa-check-circle"></i>
      <div>
        <h3>전담 지원팀</h3>
        <p>도입부터 운영까지 전담 매니저가 함께합니다.</p>
      </div>
    </div>
  </div>
</section>
```

### **5-6. 고객 후기 섹션**

Copilot Chat에 요청:

```
고객 후기 섹션 HTML을 작성해줘.
- 섹션 제목: "고객 후기"
- 후기 카드 3개 (후기 내용, 고객 이름, 직책/회사)
- 별점 아이콘 포함
```

결과 예시:

```html
<section class="reviews" id="reviews">
  <h2>고객 후기</h2>
  <div class="reviews-grid">
    <div class="review-card">
      <div class="review-stars">
        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
      </div>
      <p>"업무 자동화 도입 후 팀의 생산성이 눈에 띄게 향상되었습니다. 매일 2시간씩 절약하고 있어요."</p>
      <div class="review-author">
        <strong>김영희</strong>
        <span>마케팅 팀장, ABC 주식회사</span>
      </div>
    </div>
    <div class="review-card">
      <div class="review-stars">
        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
      </div>
      <p>"고객 리드 관리가 체계적으로 바뀌면서 전환율이 30% 이상 올랐습니다."</p>
      <div class="review-author">
        <strong>박철수</strong>
        <span>영업 이사, XYZ 테크</span>
      </div>
    </div>
    <div class="review-card">
      <div class="review-stars">
        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
      </div>
      <p>"비개발자인 저도 쉽게 설정할 수 있었습니다. 지원팀의 도움이 정말 컸어요."</p>
      <div class="review-author">
        <strong>이지은</strong>
        <span>대표, 스타트업 DEF</span>
      </div>
    </div>
  </div>
</section>
```

### **5-7. 문의 폼 섹션**

Copilot Chat에 요청:

```
고객 문의 폼 섹션 HTML을 작성해줘.
- 섹션 제목: "무료 상담 신청"
- 입력 필드: 이름, 이메일, 회사명, 문의 내용(textarea)
- 제출 버튼
- 폼 제출은 JavaScript에서 처리 (action 없이)
```

결과 예시:

```html
<section class="contact" id="contact">
  <h2>무료 상담 신청</h2>
  <p class="section-subtitle">아래 양식을 작성해주시면 담당자가 빠르게 연락드리겠습니다</p>
  <form id="contactForm" class="contact-form">
    <div class="form-row">
      <div class="form-group">
        <label for="name">이름 *</label>
        <input type="text" id="name" name="name" required>
      </div>
      <div class="form-group">
        <label for="email">이메일 *</label>
        <input type="email" id="email" name="email" required>
      </div>
    </div>
    <div class="form-group">
      <label for="company">회사명</label>
      <input type="text" id="company" name="company">
    </div>
    <div class="form-group">
      <label for="message">문의 내용 *</label>
      <textarea id="message" name="message" rows="5" required></textarea>
    </div>
    <button type="submit" id="submitBtn">상담 신청하기</button>
  </form>
  <div id="successMessage" class="success-message">
    신청이 완료되었습니다. 빠른 시일 내에 연락드리겠습니다!
  </div>
</section>
```

### **5-8. 푸터**

```html
<footer>
  <div class="footer-content">
    <div class="footer-logo">BizSolution</div>
    <p>비즈니스 자동화의 시작</p>
    <div class="footer-links">
      <a href="#">이용약관</a>
      <a href="#">개인정보처리방침</a>
      <a href="#">고객센터</a>
    </div>
    <p class="footer-copyright">&copy; 2025 BizSolution. All rights reserved.</p>
  </div>
</footer>
```

---

## **6. CSS 스타일링**

### **6-1. Copilot Chat에 전체 CSS 요청**

`style.css`를 열고 Copilot Chat에 요청합니다:

```
위 랜딩페이지 HTML에 맞는 CSS를 작성해줘.
조건:
- 폰트: Noto Sans KR
- 메인 컬러: #2563eb (파란색), 보조 컬러: #1e40af
- 네비게이션 상단 고정, 스크롤 시 그림자 효과
- 히어로 섹션 전체 화면, 그라데이션 배경
- 서비스 카드, 후기 카드에 hover 효과
- 문의 폼은 중앙 정렬, 최대 너비 700px
- 반응형: 768px 이하에서 1열 레이아웃
- 부드러운 스크롤
```

### **6-2. 생성된 CSS 적용**

결과 예시:

```css
/* 기본 설정 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Noto Sans KR', sans-serif;
  color: #333;
  line-height: 1.7;
}

/* 네비게이션 */
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 100;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
}

.nav-logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: #2563eb;
  text-decoration: none;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 30px;
}

.nav-links a {
  color: #555;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #2563eb;
}

.nav-cta {
  background-color: #2563eb;
  color: white;
  padding: 10px 24px;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 500;
  transition: background-color 0.3s;
}

.nav-cta:hover {
  background-color: #1e40af;
}

/* 히어로 */
.hero {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: linear-gradient(135deg, #1e3a5f, #2563eb);
  color: white;
  padding: 0 20px;
}

.hero h1 {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 20px;
  line-height: 1.3;
}

.hero p {
  font-size: 1.2rem;
  color: #d1d5db;
  margin-bottom: 35px;
}

.hero-buttons {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.btn {
  padding: 14px 32px;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.3s;
}

.btn-primary {
  background-color: white;
  color: #2563eb;
}

.btn-primary:hover {
  background-color: #f0f0f0;
}

.btn-secondary {
  border: 2px solid white;
  color: white;
}

.btn-secondary:hover {
  background-color: white;
  color: #2563eb;
}

/* 공통 섹션 */
section {
  padding: 100px 30px;
}

section h2 {
  font-size: 2.2rem;
  text-align: center;
  margin-bottom: 10px;
  color: #1a1a2e;
}

.section-subtitle {
  text-align: center;
  color: #777;
  margin-bottom: 50px;
  font-size: 1.05rem;
}

/* 서비스 카드 */
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  max-width: 1100px;
  margin: 0 auto;
}

.service-card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 40px 30px;
  text-align: center;
  transition: transform 0.3s, box-shadow 0.3s;
}

.service-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.service-card i {
  font-size: 2.5rem;
  color: #2563eb;
  margin-bottom: 20px;
}

.service-card h3 {
  font-size: 1.3rem;
  margin-bottom: 12px;
}

.service-card p {
  color: #666;
  font-size: 0.95rem;
}

/* 특장점 */
.why-us {
  background-color: #f8fafc;
}

.stats-grid {
  display: flex;
  justify-content: center;
  gap: 60px;
  margin: 40px 0 50px;
}

.stat-item {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  color: #2563eb;
}

.stat-label {
  color: #666;
  font-size: 1rem;
}

.features-list {
  max-width: 700px;
  margin: 0 auto;
}

.feature-item {
  display: flex;
  align-items: flex-start;
  gap: 15px;
  margin-bottom: 25px;
}

.feature-item i {
  color: #2563eb;
  font-size: 1.4rem;
  margin-top: 3px;
}

.feature-item h3 {
  font-size: 1.1rem;
  margin-bottom: 5px;
}

.feature-item p {
  color: #666;
  font-size: 0.95rem;
}

/* 고객 후기 */
.reviews-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  max-width: 1100px;
  margin: 0 auto;
}

.review-card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 30px;
  transition: transform 0.3s, box-shadow 0.3s;
}

.review-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
}

.review-stars {
  color: #f59e0b;
  margin-bottom: 15px;
}

.review-stars i {
  margin-right: 2px;
}

.review-card p {
  color: #555;
  font-size: 0.95rem;
  margin-bottom: 20px;
  line-height: 1.6;
}

.review-author strong {
  display: block;
  font-size: 1rem;
}

.review-author span {
  color: #888;
  font-size: 0.85rem;
}

/* 문의 폼 */
.contact {
  background-color: #f8fafc;
}

.contact-form {
  max-width: 700px;
  margin: 0 auto;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 6px;
  font-weight: 500;
  color: #444;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 1rem;
  font-family: 'Noto Sans KR', sans-serif;
  transition: border-color 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #2563eb;
}

#submitBtn {
  width: 100%;
  padding: 14px;
  background-color: #2563eb;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.3s;
}

#submitBtn:hover {
  background-color: #1e40af;
}

#submitBtn:disabled {
  background-color: #9ca3af;
  cursor: not-allowed;
}

.success-message {
  display: none;
  text-align: center;
  color: #16a34a;
  font-size: 1.2rem;
  margin-top: 30px;
  padding: 20px;
  background-color: #f0fdf4;
  border-radius: 8px;
}

/* 푸터 */
footer {
  background-color: #1a1a2e;
  color: #aaa;
  padding: 50px 30px;
  text-align: center;
}

.footer-logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  margin-bottom: 8px;
}

.footer-links {
  margin: 20px 0;
}

.footer-links a {
  color: #aaa;
  text-decoration: none;
  margin: 0 12px;
  font-size: 0.9rem;
  transition: color 0.3s;
}

.footer-links a:hover {
  color: white;
}

.footer-copyright {
  margin-top: 15px;
  font-size: 0.85rem;
}

/* 반응형 */
@media (max-width: 768px) {
  .nav-container {
    flex-direction: column;
    gap: 10px;
  }

  .nav-links {
    gap: 15px;
  }

  .hero h1 {
    font-size: 2rem;
  }

  .hero p {
    font-size: 1rem;
  }

  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }

  .services-grid,
  .reviews-grid {
    grid-template-columns: 1fr;
  }

  .stats-grid {
    flex-direction: column;
    gap: 25px;
  }

  .form-row {
    grid-template-columns: 1fr;
  }

  section {
    padding: 60px 20px;
  }
}
```

---

## **7. 문의 폼과 Google Apps Script 연동**

문의 폼 데이터를 **Google Sheets**에 자동 저장되도록 연동합니다. ([실습 8](8.webLeadCollection.md) 응용)

### **7-1. Google Sheets 준비**

1. [Google Sheets](https://docs.google.com/spreadsheets/)에서 새 스프레드시트를 생성합니다.
2. 첫 번째 행에 헤더를 추가합니다:

   | A | B | C | D | E |
   |---|---|---|---|---|
   | 접수일시 | 이름 | 이메일 | 회사명 | 문의내용 |

3. 스프레드시트 ID를 확인합니다 (URL의 `/d/` 뒤 문자열).

### **7-2. Google Apps Script 작성**

1. [Google Apps Script](https://script.google.com/)에서 새 프로젝트를 생성합니다.
2. `Code.gs`에 다음 코드를 작성합니다:

```javascript
var SPREADSHEET_ID = 'YOUR_SPREADSHEET_ID';
var SHEET_NAME = 'Sheet1';

function doPost(e) {
  try {
    var data = JSON.parse(e.postData.contents);

    if (!data.name || !data.email || !data.message) {
      return ContentService.createTextOutput(
        JSON.stringify({ status: 'error', message: '필수 필드가 누락되었습니다.' })
      ).setMimeType(ContentService.MimeType.JSON);
    }

    var sheet = SpreadsheetApp.openById(SPREADSHEET_ID).getSheetByName(SHEET_NAME);
    var timestamp = Utilities.formatDate(new Date(), 'Asia/Seoul', 'yyyy-MM-dd HH:mm:ss');

    sheet.appendRow([
      timestamp,
      data.name,
      data.email,
      data.company || '',
      data.message
    ]);

    return ContentService.createTextOutput(
      JSON.stringify({ status: 'success', message: '문의가 접수되었습니다.' })
    ).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    return ContentService.createTextOutput(
      JSON.stringify({ status: 'error', message: error.message })
    ).setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet() {
  return ContentService.createTextOutput(
    JSON.stringify({ status: 'ok', message: 'Contact API is running.' })
  ).setMimeType(ContentService.MimeType.JSON);
}
```

> `YOUR_SPREADSHEET_ID`를 실제 스프레드시트 ID로 교체합니다.

### **7-3. Apps Script 배포**

1. **배포 > 새 배포**를 클릭합니다.
2. 유형: **웹 앱**, 실행 사용자: **나**, 액세스: **모든 사용자**
3. **배포**를 클릭하고 생성된 URL을 복사합니다.

### **7-4. script.js 작성**

`script.js` 파일에 폼 전송 로직을 작성합니다:

```javascript
// Apps Script 웹 앱 URL (배포 시 생성된 URL로 교체)
var APPS_SCRIPT_URL = 'https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec';

document.getElementById('contactForm').addEventListener('submit', function(e) {
  e.preventDefault();

  var submitBtn = document.getElementById('submitBtn');
  submitBtn.disabled = true;
  submitBtn.textContent = '전송 중...';

  var formData = {
    name: document.getElementById('name').value.trim(),
    email: document.getElementById('email').value.trim(),
    company: document.getElementById('company').value.trim(),
    message: document.getElementById('message').value.trim()
  };

  fetch(APPS_SCRIPT_URL, {
    method: 'POST',
    mode: 'no-cors',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(formData)
  })
  .then(function() {
    document.getElementById('contactForm').style.display = 'none';
    document.getElementById('successMessage').style.display = 'block';
  })
  .catch(function() {
    alert('전송 중 오류가 발생했습니다. 다시 시도해주세요.');
    submitBtn.disabled = false;
    submitBtn.textContent = '상담 신청하기';
  });
});
```

> `YOUR_DEPLOYMENT_ID`를 실제 배포 URL로 교체합니다.

---

## **8. 테스트**

### **8-1. 로컬에서 확인**

1. VS Code에서 `index.html`을 마우스 오른쪽 클릭 > **Open with Live Server**
2. 각 섹션이 정상적으로 표시되는지 확인합니다.
3. `F12` > 기기 전환 아이콘으로 모바일 레이아웃도 확인합니다.

### **8-2. 문의 폼 테스트**

1. 문의 폼에 테스트 데이터를 입력하고 **상담 신청하기**를 클릭합니다.
2. Google Sheets에 데이터가 저장되었는지 확인합니다.

---

## **9. Vercel로 배포**

### **9-1. Git 저장소 준비**

```bash
git init
git add index.html style.css script.js
git commit -m "랜딩페이지 제작"
```

### **9-2. GitHub 원격 저장소 생성 및 업로드**

1. [GitHub](https://github.com/)에서 **New repository**를 생성합니다.
   - Repository name: `my-landing-page`
   - **Public** 선택

2. 코드 업로드:

   ```bash
   git remote add origin https://github.com/본인아이디/my-landing-page.git
   git branch -M main
   git push -u origin main
   ```

### **9-3. Vercel 연동 및 배포**

1. [Vercel](https://vercel.com/)에 접속하여 **GitHub 계정으로 로그인**합니다.
2. **Add New Project**를 클릭합니다.
3. **Import Git Repository**에서 `my-landing-page` 저장소를 선택합니다.
4. 설정은 기본값 그대로 두고 **Deploy**를 클릭합니다.
5. 약 30초~1분 후 배포가 완료되고 URL이 생성됩니다.
   - 예: `https://my-landing-page.vercel.app`

### **9-4. 이후 업데이트**

코드를 수정한 후 push하면 Vercel이 자동으로 재배포합니다:

```bash
git add .
git commit -m "랜딩페이지 수정"
git push
```

---

## **주의 사항**

- **Copilot 코드 검토**: AI가 생성한 코드는 반드시 브라우저에서 결과를 확인하고, 의도와 다른 부분은 추가 수정을 요청하세요.
- **이미지 저작권**: 랜딩페이지에 이미지를 사용할 경우 [Unsplash](https://unsplash.com/), [Pexels](https://www.pexels.com/) 등 무료 라이선스 이미지를 활용하세요.
- **개인정보 수집 동의**: 문의 폼에서 개인정보를 수집하는 경우, 개인정보 처리방침 링크와 수집 동의 체크박스를 추가하는 것을 권장합니다.
- **Apps Script URL 노출**: `script.js`에 포함된 Apps Script URL은 브라우저에서 노출됩니다. 스팸 방지를 위해 reCAPTCHA 등을 추가로 고려할 수 있습니다.

---

이 튜토리얼을 완료하면 실제 비즈니스에 활용 가능한 랜딩페이지를 제작하고 배포하는 전체 과정을 경험하게 됩니다. 다음 단계인 **튜토리얼 C**에서는 React를 활용한 동적 웹 애플리케이션을 제작해봅니다.
