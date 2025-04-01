# automationLearningWithAI
Zapier과 Google Apps Script를 활용해 자동화시스템을 학습 하기 위한 튜토리얼  

주니어 개발자를 위한 자동화 시스템 구축 튜토리얼 개요를 아래와 같이 정리하였습니다. 각 단계는 난이도에 따라 **초급**, **중급**, **고급**으로 구성되어 있으며, 실습을 통해 다양한 자동화 도구와 API 활용 방법을 익힐 수 있습니다.

---

## **[1. 초급: 기본 트리거 활용 - Zapier]**

### [**실습 1: 구글 폼 신청 시 이메일 자동 응답 시스템 구축**](1.formsToEmail.md)

- **설명**: 사용자가 Google Form을 제출하면 자동으로 회신 이메일을 발송하는 시스템을 구축합니다.

- **사용 도구**: Google Forms, Gmail, Zapier

- **추가 실습**:
  - **추가 실습 1**: 신청 내용에 `[대기 신청]` 키워드가 포함된 경우 별도의 이메일 템플릿으로 응답하기
  - **추가 실습 2**: 신청자 정보를 운영진의 Slack 채널로 자동 전송하기
  - **추가 실습 3**: Solapi를 연동하여 신청자에게 카카오톡 또는 문자 메시지 전송하기

## **[1-1. 초급: 기본 트리거 활용 - Make]**

### [**실습 1-1: 구글 폼 신청시 자동응답(메일, 문자, 카톡)**](1-1.formsResponse_Make.md)

- **설명**: Make.com을 활용하여 Google Forms 신청 시 참가자에게 이메일, 문자, 카카오톡으로 안내 메시지를 자동으로 발송하는 시스템을 구축

- **사용 도구**: Make, Google Forms, Gmail, Solapi

---

## **[2. 중급: API와 데이터 활용 - Google Apps Script]**

### [**실습 2: 스프레드시트에서 배송 메시지 보내기**](2.sheetsToMessage.md)

- **설명**: Google Sheets의 특정 칼럼이 체크되면 Slack으로 배송 관련 메시지를 자동 전송하는 기능을 구현합니다.

- **사용 도구**: Google Apps Script, Google Sheets, Slack API

- **추가 실습**:
  - **추가 실습 1**: 배송 완료 시 다른 스프레드시트에 자동으로 업데이트하기
  - **추가 실습 2**: 주문 금액이 10만 원 이상인 경우에만 메시지 전송하기

### [**실습 2-1: 스프레드시트에서 문자 발송하기**](2_1.sheetsToMMS.md)

### [**실습 3: 스프레드시트에서 수능 성적표 생성하기**](3.sheetsToDocs.md)

- **설명**: Google Sheets에서 특정 칼럼이 체크되면 Google Docs를 생성하여 수능 성적표를 자동으로 작성합니다.

- **성적표 데이터**: 이름, 출생년도, 과목별 성적 그래프(국어, 영어, 수학), 지원 가능 대학 목록

- **사용 도구**: Google Apps Script, Google Sheets, Google Docs

- **추가 실습**: 생성된 성적표 파일의 링크와 제작 완료 메시지를 Slack으로 전송하기

### [**실습 4: 스프레드시트에서 새내기 시간표 생성하기**](4.sheetsToCalendar.md)

- **설명**: Google Sheets에서 특정 칼럼이 체크되면 Google Calendar에 수업 일정을 자동으로 생성합니다.

- **시간표 데이터**: 교과목 이름, 교수님 이름 및 이메일, 본인 휴대폰 번호, 함께 듣는 친구 4명의 정보, 수업 시작 및 종료 시간, 강의실

- **사용 도구**: Google Apps Script, Google Sheets, Google Calendar

- **추가 실습**: 이벤트 생성 시 안내 메시지를 Slack으로 발송하기

### [**실습 5: 뉴스 요약 자동화**](5.newsSummary.md)

- **설명**: Google 알리미를 통해 수신된 이메일을 ChatGPT를 활용하여 뉴스 데이터를 개별로 추출한 후, 구글 스프레드시트에 작성하고 Slack에 공유합니다.

- **사용 도구**: Google 알리미, Zapier, Google Sheets, ChatGPT API, Slack

- **추가 실습**: 블로그 글을 자동으로 요약하여 이메일로 발송하기

---

## **[3. 고급: 외부 API 및 데이터 연동]**

### [**실습 6: 네이버 카페 API를 활용한 스프레드시트에서 자동 게시글 업로드**](6.sheetsToCafe.md)

- **설명**: Google Sheets에서 특정 칼럼이 체크되면 ChatGPT를 통해 내용을 요약하고, 이를 네이버 카페에 자동으로 게시합니다.

- **사용 도구**: Google Apps Script, ChatGPT API, 네이버 카페 API

- **추가 실습**: 게시글에 이미지 추가하기

### [**실습 7: 기업은행 Open API 연동하여 거래내역 자동 알림**](7.bankTransaction.md)

- **설명**: 기업은행 Open API를 통해 특정 조건(예: 입금액 100만 원 이상)이 충족되면 Slack으로 알림을 전송합니다.

- **사용 도구**: IBK 기업은행 Open API, Zapier, Slack

- **추가 실습**: 입출금 내역을 스프레드시트에 자동으로 저장하기

### [**실습 8: Google Forms API와 Apps Script를 활용한 웹 데이터 수집 자동화](8.formsApiToAppsScript.md)**

- **설명:** 이 실습에서는 Google Forms API와 Google Apps Script를 사용하여 웹페이지에서 직접 데이터를 수집하고, 이를 Google Forms에 자동으로 저장하는 시스템을 구축합니다.

- **사용 도구:** Google Forms, Google Apps Script, Google Cloud Platform

- **추가 실습:** 수집된 데이터를 Google Sheets에 자동으로 저장하여 데이터 분석 및 시각화에 활용하기, 특정 조건에 따라 수집된 데이터에 대한 알림 이메일 또는 Slack 메시지 자동 발송하기, 사용자 입력에 대한 실시간 검증 및 오류 처리 기능 추가하기

이 실습을 통해 웹페이지에서 수집한 데이터를 Google Forms와 연동하여 자동으로 처리하는 방법을 습득하게 됩니다. 이는 다양한 웹 기반 데이터 수집 및 자동화 프로젝트에 활용될 수 있습니다. 

---

이러한 튜토리얼을 통해 주니어 개발자들은 다양한 자동화 도구와 API를 활용하여 업무 효율을 높이는 방법을 체계적으로 학습할 수 있습니다. 각 실습은 단계별로 구성되어 있어 난이도에 따라 순차적으로 진행할 수 있으며, 추가 실습을 통해 응용 능력을 향상시킬 수 있습니다. 
