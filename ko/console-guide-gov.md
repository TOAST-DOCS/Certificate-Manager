## Management > Certificate Manager > 콘솔 사용 가이드
콘솔 사용 가이드에서는 Certificate Manager를 사용하는 데 필요한 기본적인 내용을 설명합니다.
* 알림 그룹
* 인증서
* 도메인
* 사용자 데이터
* 인증서 조회/다운로드 API 자격 관련

## 알림 그룹

Certificate Manager는 알림 그룹 단위로 만료 일자의 알림 주기를 설정하고 알림을 받을 대상자를 관리합니다.

![alarmgroup-1.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-1.png)

### 알림 그룹 생성

1. 알림 그룹 메인 화면에서 **+ 그룹 만들기** 버튼을 클릭합니다.
![alarmgroup-2.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-2.png)
2. **그룹 만들기** 창에서 그룹 이름을 입력합니다. 이미 있는 이름은 지정할 수 없습니다.
3. 알림 사용 여부를 선택합니다. 알림 그룹에 속한 사용자에게 만료 일자 알림을 포함한 모든 알림을 발송할지 여부를 선택할 수 있습니다.
4. **추가** 버튼을 클릭합니다.

### 상세 정보

1. 알림 그룹 메인 화면에서 **상세 정보** 버튼을 클릭하면 알림 그룹 이름과 알림 사용 여부, 관리 데이터가 표시됩니다. **관리 data**는 해당 알림 그룹에 연동되어 있는 인증서, 도메인, 사용자 데이터를 의미합니다.
2. **수정** 버튼을 클릭하여 알림 그룹의 이름 및 알림 사용 여부를 변경할 수 있습니다.

![alarmgroup-3.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-3.png)

### 알림 설정

1. 알림 그룹 메인 화면에서 **알림 설정** 버튼을 클릭합니다.
2. 기본으로 설정된 알림 정책이 없으므로 **알림 설정** 창에서 알림 정책을 추가해야 만료일 알림을 받을 수 있습니다.![alarmgroup-4.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-4.png)

### 알림 추가

1. **알림 설정** 창 왼쪽 하단의 **+** 버튼을 클릭합니다.![alarmgroup-5.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-5.png)
2. **알림 시작 D-day**에서 인증서, 도메인, 데이터 만료일 며칠 전부터 알림을 발송할지를 지정합니다.
3. **알림 주기**에서 며칠 간격으로 알림을 발송할지를 지정합니다.
4. **Email 발송 여부**와 **SMS 발송 여부**에서 알림 발송 시 이메일, SMS를 사용할지를 선택합니다. 둘 다 선택돼 있지 않으면 알림을 발송하지 않습니다.
5. **삭제** 열에서 **-** 버튼을 클릭하여 알림 정책을 삭제할 수 있습니다.
6. **알림 시작 D-day**와 **알림 주기**는 중복 설정할 수 없습니다.
7. **완료** 버튼을 클릭합니다.
![alarmgroup-6.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-6.png)

### 수신 그룹 연동 화면

알림 그룹 메인 화면에서 **사용자 그룹 연동** 버튼을 클릭하면 알림 그룹에 연동되어 있는 사용자가 표시됩니다.
기본값으로는 알림 그룹을 생성한 사용자가 추가되어 있습니다.

NHN Cloud 프로젝트에 속한 멤버가 알림 그룹의 사용자로 연동될 수 있습니다.![alarmgroup-7.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-7.png)

### 사용자 추가

상단의 사용자 연동 검색 창에서 NHN Cloud 프로젝트에 속한 멤버를 검색하여 추가할 수 있습니다.

![alarmgroup-8.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-8.png)
![alarmgroup-9.png](http://static.toastoven.net/prod_certificate_manager/202002/alarmgroup-9.png)

* **Type**은 해당 사용자가 지닌 NHN Cloud 프로젝트 권한(ADMIN/MEMBER)을 의미합니다.
* 멤버의 **이름**, **Email** 및 **Phone**을 확인할 수 있습니다.
* 등록된 휴대폰 번호가 없다면 **Phone**에 '-'로 표시됩니다. 이 경우 SMS 알림 발송에 실패하며, 알림 발송 실패 시 알림 그룹에 속한 ADMIN에게 '알림 발송 실패' 알림이 발송됩니다.

## 인증서

인증서의 도메인 이름(예: \*.toast.com)과 만료일을 입력하면 연동한 알림 그룹의 알림 정책에 맞춰 사용자에게 알림을 발송합니다.

인증서 파일(.pem)을 업로드하는 경우, 인증서 파일로부터 아래 항목을 자동으로 수집합니다.
* 생성일
* 만료일
* 인증서의 서명 방식(예: sha256RSA)
* 인증 기관(예: Digicert)

인증서의 설치 정보를 등록하는 경우, 인증서 설치 정보의 IP 와 포트로부터 인증서를 가져와, Certificate Manager에 등록한 인증서와 만료일을 비교합니다.
Certificate Manager에 등록한 인증서의 만료일보다 자동 수집한 인증서 설치 정보의 만료일이 앞선 경우, 인증서 교체가 필요하다는 알림을 발송합니다.

### 메인 화면
메인 화면에서는 인증서 목록이나 만료일까지 남은 날짜 등을 확인할 수 있습니다.

![certificate-1.png](http://static.toastoven.net/prod_certificate_manager/202302/certificate-1.png)

* 기존에 등록한 인증서의 목록을 확인 및 검색할 수 있습니다.
* 만료일까지 남은 날짜를 확인할 수 있습니다.
* 오늘 날짜 기준으로 만료일이 지난 데이터는 빨간색으로, 만료일까지 남은 날짜가 30일 이하인 데이터는 주황색으로 표시됩니다.

### 인증서 생성

1. 인증서 메인 화면에서 **+ 인증서 추가** 버튼을 클릭하면 **인증서 추가** 창이 나타납니다.
![certificate-2.png](http://static.toastoven.net/prod_certificate_manager/202302/certificate-2.png)
2. **알림 그룹**에서 연동할 알림 그룹을 선택합니다. 생성된 알림 그룹이 없을 때는 목록에 표시되지 않으며, 인증서를 생성할 수 없습니다.
3. **이름**에 인증서 이름(CommonName, CN)을 입력합니다. 인증서 이름은 중복으로 등록할 수 없습니다. <br>
   * SAN 인증서의 경우 인증서 파일을 업로드하면 인증서 이름과 서브 인증서 이름이 자동으로 입력됩니다. 인증서의 이름은 임의로 변경할 수 없습니다.
4. **유형**에서 원하는 항목을 선택합니다.
   * Single은 단일 인증서입니다.
   * Wildcard는 \*(asterisk)로 시작하는 범용 인증서(여러 호스트에서 사용할 수 있는 인증서)를 뜻합니다.
   * SAN은 1개의 인증서로 여러 개의 도메인에 SSL을 적용할 수 있는 인증서입니다.
5. **인증서 등록** 아래 **인증서**에서 인증서 파일을 등록합니다.<br>
   인증서는 필수값이 아니며, 추후에 등록할 수도 있습니다.
    * 인증서는 개인 키와 인증서로 구성된 .pem 형식의 파일입니다.
    * 지원하는 인증서 파일(.pem) 형식은 [**문제 해결 가이드 > 인증서 파일 포맷 변환**](http://gov-docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)을 참고하십시오.
    * 인증서 파일은 최대 512KB까지 업로드할 수 있습니다.
6. **패스프레이즈**(passphrase, 비밀 문구)에 인증서 파일 내에 포함된 개인 키의 **패스프레이즈**를 입력합니다.
7. **추가** 버튼을 클릭합니다.
   * Single과 Wildcard의 경우는 1개의 인증서가 생성됩니다.
   * SAN의 경우 대표 인증서와 서브 인증서가 모두 생성됩니다. 예를 들어 대표 인증서가 1개이고, 서브 인증서가 3개인 경우 총 4개의 인증서가 생성됩니다.
8. [Network > Load Balancer](https://gov.toast.com/kr/service/network/load-balancer) 서비스와 연동해야 할 때는 인증서 파일의 **패스프레이즈**를 삭제해야 합니다.
    * **패스프레이즈**는 다음 명령을 사용해 삭제할 수 있습니다.
    ```bash
    openssl rsa -in my_private_input.key -out my_private_output.key
    ``` 



### 상세 화면

1. 인증서 메인 화면에서 **상세 정보** 버튼을 클릭하면 인증서 파일 정보를 확인할 수 있습니다.
    * **(자동 수집)**이 표시된 필드는 인증서 파일로부터 자동 수집된 항목을 의미합니다. 인증서 파일이 등록되지 않은 경우 '-'로 표시됩니다.
2. **수정** 버튼을 클릭하여 인증서 정보를 수정하거나, 인증서 파일을 업로드할 수 있습니다.
    * 인증서 이름은 수정할 수 없습니다. 인증서 이름을 수정하려면 기존에 등록한 인증서를 삭제하고 새로 생성해야 합니다.
      ![certificate-3.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-3.png)

### 인증서 사용 정보, 설치 정보 생성

1. 인증서 메인 화면에서 **인증서 사용 정보** 버튼을 클릭하면 인증서 사용 및 설치 정보를 확인할 수 있습니다. 기본값으로는 아무것도 등록되어 있지 않습니다.
![certificate-4.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-4.png)
2. **수정** 버튼을 클릭하면 다음과 같은 화면을 확인할 수 있습니다.
![certificate-5.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-5.png)
3. 오른쪽 상단의 **+ 추가** 버튼을 클릭하면 정보를 입력할 수 있는 필드가 나타납니다.
![certificate-6.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-6.png)
4. 인증서 사용 정보의 이름을 입력합니다.
    * 인증서 유형이 **Single**인 경우 인증서 이름과 동일해야 합니다.
    * 인증서 유형이 **Wildcard**인 경우 '\*'(asterisk)를 제외한 인증서 이름과 동일하거나 '\*'(asterisk)를 제외한 '.[인증서 이름]'으로 끝나야 합니다.
    * 인증서 유형이 **SAN**인 경우
      * 인증서 이름이 Single 형태인 경우 인증서 이름과 동일해야 합니다.
      * 인증서 이름이 Wildcard 형태인 경우 '\*'(asterisk)를 제외한 인증서 이름과 동일하거나 '\*'(asterisk)를 제외한 '.[인증서 이름]'으로 끝나야 합니다.
5. **알림 사용 여부**에서 인증서 사용 정보의 알림 사용 여부를 선택합니다.
6. 인증서 설치 정보를 입력하려면 인증서 설치 정보 옆의 **+추가** 버튼을 클릭합니다. 
![certificate-7.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-7.png)
    * **IP 주소**와 **포트 번호**를 입력합니다. 인증서의 자동 수집을 사용하는 경우, 입력한 IP 주소와 포트 번호로 인증서를 다운로드해 만료 일자를 비교합니다.
    * IP 주소가 사설 IP(예: 192.168.0.1, 172.20.0.1, 10.0.0.1)인 경우 인증서를 다운로드하지 못해 자동 수집 실패 알림이 발송될 수 있습니다.
7. **완료** 버튼을 클릭하면 설정한 인증서의 사용 및 설치 정보가 저장됩니다.

### 인증서 사용 정보 화면
인증서 메인 화면에서 **인증서 사용 정보** 버튼을 클릭하면 인증서 사용 및 설치 정보를 확인할 수 있습니다.
오른쪽 상단의 전체/사용/미사용으로 인증서 사용 정보의 알림 사용 여부를 선택해서 볼 수 있습니다.

![certificate-8.png](http://static.toastoven.net/prod_certificate_manager/202002/certificate-8.png)

## 도메인
DNS의 최상위 도메인 이름(예: toast.com)과 만료일을 입력하면 연동한 알림 그룹의 알림 정책에 맞춰 사용자에게 알림을 발송합니다.

도메인의 '자동 수집' 기능을 사용하는 경우, whois 서버로부터 도메인의 정보를 자동 수집합니다.
자동 수집하는 항목은 다음과 같습니다.
* 생성일
* 만료일
* 등록자(registrar)(예: Gabia, Inc.)
* 등록 기관(registrant, 도메인의 실 소유자)
* 네임 서버

### 메인 화면

기존에 등록한 도메인의 목록을 확인하거나 검색할 수 있습니다.

![domain-1.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-1.png)

만료일까지 며칠이 남았는지 확인할 수 있습니다.

오늘 날짜 기준으로 만료일이 지난 데이터는 빨간색으로, 만료일까지 남은 날짜가 30일 이하인 데이터는 주황색으로 표시됩니다.

### 도메인 생성

1. 도메인 메인 화면에서 **+ 도메인 추가** 버튼을 클릭합니다.
![domain-2.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-2.png)
2. **도메인 추가** 창에서 연동할 알림 그룹을 선택합니다. 알림 그룹이 없으면 목록에 나타나지 않으며 도메인을 생성할 수 없습니다.
3. **상위 도메인 정보** 아래 **이름**에 상위 도메인 이름을 입력합니다. 상위 도메인 이름은 중복으로 등록할 수 없습니다.
4. **만료일**에 도메인의 만료일을 입력합니다.
5. **유형**에서 원하는 유형을 선택합니다. 
    * **서비스용**은 DNS 서버에 도메인을 등록해 서비스에서 사용하는 경우입니다. 
    * **방어용**은 실 서비스에서 사용하진 않지만 서비스의 신뢰성 등의 목적으로 도메인을 구매하여 확보하는 경우입니다.
6. **알림 사용 여부**를 선택합니다. 해당 도메인에 대한 알림을 발송할지 선택합니다. **미사용**을 선택하면 해당 도메인에 대한 알림이 모두 발송되지 않습니다.
7. **자동 수집**에서 항목을 자동으로 수집할지 선택합니다. **사용**을 선택하면 whois 서버로부터 아래 항목들을 수집합니다.
    * 생성일
    * 만료일
    * 등록자(registrar, 예: Gabia, Inc.)
    * 등록 기관(registrant, 도메인의 실 소유자)
    * 네임 서버
8. **하위 도메인 정보**에서 하위 도메인의 자동 수집 여부 및 하위 도메인 이름을 입력합니다.
    * 하위 도메인의 자동 수집을 사용할 경우, 해당 도메인으로 ping을 호출해 응답이 성공하는지 확인합니다.
    * 하위 도메인 이름은 상위 도메인에 속해야 합니다.
        * 하위 도메인 이름은 상위 도메인과 같거나, '.[상위 도메인 이름]'으로 끝나야 합니다.
        * 예: 상위 도메인 이름이 'toast.com'인 경우, 하위 도메인 이름으로는 'toast.com' 및 'www.toast.com', 'www2.toast.com' 등을 입력할 수 있습니다.
9. **추가** 버튼을 클릭하면 설정하신 도메인 정보를 저장할 수 있습니다.

### 상세 화면

1. 도메인 메인 화면에서 **상세 정보** 버튼을 클릭하면 도메인과 하위 도메인의 정보 및 자동 수집된 정보가 표시됩니다.
2. 필드 이름 뒤에 **(자동 수집)**으로 표시된 필드는 자동 수집된 항목을 의미합니다. 자동 수집된 정보가 없을 경우 **-**로 표시됩니다.
3. **수정** 버튼을 클릭하여 상위 도메인 정보를 수정하시거나, 등록된 하위 도메인을 삭제 혹은 하위 도메인을 추가할 수 있습니다.
    * 상위 도메인 이름은 수정할 수 없습니다. 상위 도메인 이름을 수정해야 하면 기존에 등록한 도메인을 삭제하고 신규로 생성해야 합니다.

![domain-3.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-3.png)

## 사용자 데이터

만료일이 있는 데이터(예: 라이선스 키)를 입력하면 연동한 알림 그룹의 알림 정책에 따라 사용자에게 알림을 발송합니다.
특정 사용자 그룹에게 주기적으로 알림을 발송할 때 활용할 수 있습니다.

### 메인 화면

기존에 등록한 사용자 데이터의 목록을 확인하거나 검색할 수 있습니다. 만료일까지 남은 날짜를 확인할 수 있습니다.
오늘 날짜 기준으로 만료일이 지난 데이터는 빨간색으로, 만료일까지 남은 날짜가 30일 이하인 데이터는 주황색으로 표시됩니다. 

![userdata-1.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-1.png)

### 사용자 데이터 생성

사용자 데이터 메인 화면에서 **+ 사용자 데이터 추가** 버튼을 클릭하면 다음과 같은 화면이 나옵니다.

![userdata-2.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-2.png)

* 연동할 알림 그룹을 선택합니다. 알림 그룹이 생성되어 있지 않은 경우 선택 가능한 알림 그룹이 표시되지 않으며, 사용자 데이터를 생성할 수 없습니다.
* 사용자 데이터 이름을 입력합니다. 사용자 데이터 이름은 중복으로 등록할 수 없습니다.
* 알림 발송 여부를 선택합니다. 해당 사용자 데이터에 대한 알림을 발송할지 여부이며, 해당 필드를 **미사용**으로 선택하는 경우 해당 사용자 데이터에 대한 알림이 모두 발송되지 않습니다.
* 사용자 데이터의 만료일을 입력합니다.
* **추가** 버튼을 클릭하면 사용자 데이터 정보가 저장됩니다.

### 상세 화면

사용자 데이터 메인 화면에서 **상세 정보** 버튼을 클릭하면 저장했던 사용자 데이터의 정보가 표시됩니다.

**수정** 버튼을 클릭하여 사용자 데이터의 정보를 수정할 수 있습니다.

![userdata-3.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-3.png)

## 인증서 조회/다운로드 API 자격 관련

### User Access Key ID, Secret Access Key 생성

콘솔 우측 상단의 ID 영역을 클릭하면 다음과 같은 **API 보안 설정** 메뉴를 확인할 수 있습니다.

![console-guide-api1](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403/console-guide-api1.png)

**API 보안 설정**에서 **User Access Key ID 생성**을 클릭하여 CertificateManager API 헤더에 입력해야 하는 **User Access Key ID**와 **Secret Access Key**를 생성할 수 있습니다.

![console-guide-api2](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403/console-guide-api2.png)

![console-guide-api3](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403/console-guide-api3.png)

**User Access Key ID**, **Secret Access Key**를 생성하면 아래와 같이 **비밀 키 발급 완료** 화면이 표시됩니다. 비밀 키는 해당 팝업 화면에서 한 번만 알려주므로 이 값을 잘 기록하여 사용합니다.

![console-guide-api4](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403/console-guide-api4.png)

API 요청 시 필요한 **User Access Key ID**는 비밀 키 발급 완료 팝업을 닫으면 확인할 수 있습니다.

![console-guide-api5](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_certificate_manager/202403/console-guide-api5.png)

