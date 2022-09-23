## Management > Certificate Manager > 릴리스 노트

### 2022. 10. 04.
#### 기능 개선
* 역할 그룹 관리를 통해 권한 부여시 부여한 권한이 제대로 적용되지 않던 점을 수정하였습니다

### 2022. 08. 23.
#### 기능 개선
* API 엔드포인트의 도메인이 api-certificate-manager.cloud.toast.com에서 certmanager.api.nhncloudservice.com으로 변경되었습니다.

### 2020. 03. 24.
#### 기능 추가
Certificate Manager에 추가한 인증서의 목록을 조회할 수 있는 API를 추가했습니다.
* [API] 인증서 목록 조회 API 추가

### 2020. 01. 21.
#### 신규 서비스 출시
Certificate Manager는 만료일 연장을 놓치지 않도록, 만료일이 가까워지면 알람(SMS, 이메일)을 발송하는 서비스입니다.
만료일이 존재하는 TLS 인증서, 도메인, 사용자 데이터(예: 라이선스)를 관리하고, 만료일에 따른 알람 발송 규칙과 알람을 받을 사용자를 정할 수 있습니다.
