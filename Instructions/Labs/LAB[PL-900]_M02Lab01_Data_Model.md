---
lab:
    title: '랩 1: 데이터 모델링'
    module: '모듈 2: Common Data Service 소개'
---

# 모듈 2: Common Data Service 소개
## 랩: 데이터 모델링

### 중요 알림(2020년 11월 발효):
Common Data Service가 Microsoft Dataverse로 이름이 바뀌었습니다. Microsoft Dataverse의 일부 용어도 업데이트되었습니다. 예를 들어 엔터티는 이제 테이블입니다. Dataverse 데이터베이스의 필드와 레코드는 이제 열과 행을 나타냅니다.

애플리케이션의 사용자 환경이 업데이트되는 중인 경우 엔터티(현재 **테이블**), 필드(현재 **열**) 및 레코드(현재 **행**) 같은 Microsoft Dataverse 용어를 언급한 부분에서 최신 변경 내용이 반영되지 않을 수 있습니다. 랩을 진행하는 동안 이를 염두에 두시기 바랍니다. 최대한 빠른 시일 내에 콘텐츠를 완전히 최신 상태로 유지하도록 노력하겠습니다. 

자세한 내용 및 영향을 받는 용어의 전체 목록을 확인하려면 [Microsoft Dataverse란?](https://docs.microsoft.com/ko-kr/powerapps/maker/common-data-service/data-platform-intro#terminology-updates)을 참조하세요.

# 시나리오

Bellows College는 캠퍼스 내에 여러 건물이 있는 교육 기관입니다. 캠퍼스 방문은 현재 종이에 기록되어 있습니다. 이 정보는 일관되게 수집되지 않으며, 전체 캠퍼스 방문 데이터를 수집하고 분석할 방법이 없습니다. 

캠퍼스 관리부는 건물 액세스가 보안 요원에 의해 제어되고, 모든 방문이 반드시 호스트에 의해 사전 등록 및 기록되는 현대화된 방문자 등록 시스템을 원합니다.

이 과정 전반에 걸쳐 벨로즈 칼리지 관리 및 보안 담당자가 캠퍼스 내 건물에 대한 액세스를 관리하고 제어할 수 있도록 애플리케이션을 빌드하고 자동화를 수행합니다. 

이 랩에서는 환경에 액세스하고, CDS(Common Data Service) 데이터베이스를 만들고, 변경 내용을 추적할 수 있는 솔루션을 만듭니다. 또한 다음 요구 사항을 지원하는 데이터 모델을 만듭니다.

-   R1 - 캠퍼스 방문 위치(건물) 추적
-   R2 - 방문자를 식별하고 추적하기 위한 기본 정보 기록 
-   R3 – 방문의 일정, 기록 및 관리 

마지막으로 샘플 데이터를 Common Data Service로 가져옵니다.

# 고급 랩 단계

학습 환경을 준비하려면 다음을 수행합니다.

* 솔루션 및 게시자 만들기
* 애플리케이션 요구 사항을 충족하는 새 구성 요소와 기존 구성 요소를 모두 추가합니다. 메타데이터에 대한 설명(엔터티 및 관계)은 [데이터 모델 문서](../../Allfiles/Campus%20Management.png)를 참조하세요. CTRL 키를 누른 상태로 클릭하거나 링크를 마우스 오른쪽 단추로 클릭하여 새 창에서 데이터 모델 문서를 열 수 있습니다.

모든 사용자 지정이 완료되면 솔루션에는 여러 엔터티가 포함됩니다.

-   연락처
-   건물
-   방문

## 필수 구성 요소:

* **모듈 0 랩 0 - 랩 환경 검증** 완료

## 시작하기 전에 고려해야 할 사항:

* 명명 규칙

* 데이터 유형, 제한 사항(예: 이름의 최대 길이)

* 용이한 지역화를 지원하는 날짜 시간 서식 지정

# 연습 \#1: 솔루션을 만드세요

## 작업 \#1: 솔루션 및 게시자 만들기

1.  솔루션을 만드세요

    -   <https://make.powerapps.com>으로 이동합니다. 다시 인증해야 할 수도 있습니다. **로그인**을 클릭하고 필요한 경우 지침을 따르세요.

    -   화면 오른쪽 상단에 있는 **환경**을 클릭하고 드롭다운 메뉴에서 환경을 선택하여 해당 환경을 선택합니다.

    -   왼쪽 메뉴에서 **솔루션**을 선택하고 **새 솔루션**을 클릭합니다.

    -   **표시 이름**으로 **[사용자의 성] 캠퍼스 관리**를 입력합니다.

2.  게시자 만들기

    -   **게시자** 드롭다운을 클릭하고 **게시자**를 선택합니다.

    -   표시되는 창에서 **표시 이름**으로 **Bellows College**를 입력합니다. 
    
    -   **접두사**에 **bc**를 입력합니다.

    -   **저장 후 닫기**를 클릭합니다.
    
    -   팝업 창에서 **완료**를 클릭합니다.

3.  솔루션 만들기를 완료합니다.

    -   이제 **게시자** 드롭다운을 클릭하고 방금 만든 게시자인 **벨로즈 대학**을 선택합니다
        방금 만든 게시자.

    -   **버전**이 **1.0.0.0**으로 설정되어 있는지 확인합니다. 
    
    -   **만들기**를 클릭합니다.

## 작업 \#2: 기존 엔터티 추가

1.  방금 만든 **캠퍼스 관리** 솔루션을 클릭하여 엽니다.

2.  **기존 항목 추가**를 클릭하고 **엔터티**를 선택합니다.

3.  **연락처**를 찾아 선택합니다.

4.  **다음**을 클릭합니다.

5.  연락처에서 **구성 요소 선택**을 클릭합니다.

6.  **뷰** 탭을 선택하고 **활성 연락처** 뷰를 선택합니다. 클릭
    **추가**합니다.
    
7.  **구성 요소 선택**을 다시 클릭합니다.

8.  **양식** 탭을 선택하고 **연락처** 양식을 선택합니다.
    
9.  **추가**를 클릭합니다.

    > **뷰 1개**와 **양식 1개**가 선택되어 있어야 합니다. 
    
10.  **추가**를 다시 클릭합니다. 이렇게 하면 새로 만든 솔루션에 선택한 뷰 및 양식이 있는 연락처 엔터티가 추가됩니다. 
    
11.  이제 솔루션에 "연락처"라는 엔터티가 하나 있어야 합니다. 있어야 합니다.

# 연습 \#2: 엔터티 및 관계 만들기

**목표:** 이 연습에서는 엔터티를 만들고 엔터티 간에
관계를 추가합니다.

## 작업 #1: 건물 엔터티 및 필드 만들기

1.  브라우저에 캠퍼스 관리 솔루션이 열려 있어야 합니다. 그렇지 않은 경우 다음 단계를 수행하여 캠퍼스 관리 솔루션을 엽니다.

    * <https://make.powerapps.com>에 로그인 (아직 로그인하지 않은 경우)
    
    * **솔루션**을 선택하고 방금 만든 **[사용자의 성] 캠퍼스 관리** 솔루션을
          클릭하여 엽니다.
          
2.  건물 엔터티 만들기

    -   **새로 만들기**를 클릭하고 **엔터티**를 선택합니다.
    
    -   **표시 이름**에 **건물**을 입력합니다. 
    
    -   **완료**를 클릭합니다. 이렇게 하면 백그라운드에서 엔터티 프로비전을 시작하는 동시에 다른 엔터티 및 필드를 추가할 수 있습니다.

## 작업 #2: 방문 엔터티 및 필드 만들기

**방문** 엔터티는 건물, 방문자, 각 방문의 예약된 시간 및 실제 시간을 포함한 캠퍼스 방문 정보를 포함합니다. 

방문 체크인 과정에서 방문자가 쉽게 입력하고 해석할 수 있는 고유한 번호를 각 방문에 할당하려 합니다.

> 방문 시간은 항상 건물의 위치의 현지 시간이고 다른 표준 시간대에서 볼 때 변경되지 않아야 하기 때문에 **표준 시간대 독립** 동작을 사용하여 날짜 및 시간 정보를 기록합니다. 

1.  **캠퍼스 관리** 솔루션을 선택합니다.

2. 방문 엔터티 만들기

   * **새로 만들기**를 클릭하고 **엔터티**를 선택합니다.
   
   * **표시 이름**에 **방문**을 입력합니다. 
   
   * **완료**를 클릭합니다. 이렇게 하면 백그라운드에서 엔터티 프로비전을 시작하는 동시에 다른 필드 추가하기를 시작할 수 있습니다.

3. 예약된 시작 필드 만들기

   * **필드** 탭을 선택했는지 확인하고 **필드 추가**를 클릭합니다.
   
   * **표시 이름**에 대해 **예약된 시작**을 입력합니다.
   
   * **데이터 형식**에 대해 **날짜 및 시간**을 선택합니다.
   
   * **필수** 필드에서 **필수**를 선택합니다.
   
   * **고급 옵션** 섹션을 펼칩니다.
   
   * **동작** 필드에서 **표준 시간대 독립**을 선택합니다.
   
   * **완료**를 클릭합니다.

4.  예약된 끝 필드 만들기

    * **필드 추가**를 클릭합니다.
    
    * **표시 이름**에 **예약된 끝**을 입력합니다.
    
    * **데이터 형식**에 대해 **날짜 및 시간**을 선택합니다.
    
    * **필수** 필드에서 **필수**를 선택합니다.
    
    * **고급 옵션** 섹션을 펼칩니다.
    
    * **동작** 필드에서 **표준 시간대 독립**을 선택합니다.
    
    * **완료**를 클릭합니다.
    
5.  실제 시작 필드 만들기

    * **필드 추가**를 클릭합니다.
    
    * **표시 이름**에 **실제 시작**을 입력합니다.
    
    * **데이터 형식**에 대해 **날짜 및 시간**을 선택합니다.
    
    * **필수** 필드를 **선택 사항**으로 둡니다.
    
    * **고급 옵션** 섹션을 펼칩니다.
    
    * **동작** 필드에서 **표준 시간대 독립**을 선택합니다.
    
    * **완료**를 클릭합니다.
    
6.  실제 끝 필드 만들기

    * **필드 추가**를 클릭합니다.
    
    * **표시 이름**에 **실제 끝**을 입력합니다.
    
    * **데이터 형식**에 대해 **날짜 및 시간**을 선택합니다.
    
    * **필수** 필드를 **선택 사항**으로 둡니다.
    
    * **고급 옵션** 섹션을 펼칩니다.
    
    * **동작** 필드에서 **표준 시간대 독립**을 선택합니다.
    
    * **완료**를 클릭합니다.
    
7.  코드 만들기 필드

    * **필드 추가**를 클릭합니다.
    
    * **표시 이름**에 **코드**를 입력합니다.
    
    * **데이터 유형**에서 **일련 번호**를 선택합니다.
    
    * **일련 번호 유형**에 **날짜 접두사 번호**를 선택합니다.
    
    * **완료**를 클릭합니다.
    
8.  **엔터티 저장** 클릭

## 작업 #3: 관계 만들기

1.  **캠퍼스 관리** 솔루션의 **방문** 엔터티가 계속 표시되는지 확인합니다. 그렇지 않은 경우 이동합니다.

2.  연락처 방문 관계 만들기

    * **관계** 탭을 선택합니다.
    
    * **관계 추가** 클릭 및 **다대일** 선택
    
    * **관련 항목(1개)** 으로 **연락처**를 선택합니다. 
    
    * **조회 필드 표시 이름**에 **방문자** 입력 
    
    * **완료**를 클릭합니다.
    
3.  건물 방문 관계 만들기

    * **관계 추가** 클릭 및 **다대일** 선택
    
    * **관련 항목(1개)** 으로 **건물**을 선택합니다. 
    
    * **완료**를 클릭합니다.
    
4.  **엔터티 저장**을 클릭합니다.

5.  상단 메뉴에서 **솔루션**을 선택하고 **모든 사용자 지정 게시**를 클릭합니다.

# 연습 \#3: 데이터 가져오기

**목표:** 이 연습에서는 샘플 데이터를 Common Data Service 데이터베이스로 가져옵니다.

## 작업 #1: 솔루션 가져오기

이 작업에서는 데이터 가져오기를 완료하는 데 필요한 Power Automate 흐름이 포함된 솔루션을 가져옵니다.

1. 데스크톱에  파일 저장소 **DataImport_managed.zip**이 있어야 합니다. 그렇지 않은 경우 [데이터 가져오기 솔루션](../../Allfiles/DataImport_managed.zip)을 다운로드합니다.

2. <https://make.powerapps.com>에 로그인합니다.

3. 아직 선택되지 않은 경우, 오른쪽 상단에 있는 ***내 이니셜* 연습** 환경을 선택합니다.

4. 왼쪽 탐색 패널에서 **솔루션**을 선택합니다.

5. **가져오기**를 클릭한 다음, **찾아보기**를 클릭합니다. 데스크톱에서 **DataImport_managed.zip** 을 찾아 선택한 다음 **다음**을 누릅니다.

>   다음과 같은 메시지를 받을 수 있습니다.
>
>   종속성이 누락되었습니다. 이 솔루션을 설치하기 전에 다음 솔루션을 설치하세요...
>
>   이 메시지는 데이터 모델이 완전하지 않음을 의미합니다.
>   게시자 접두사는 **bc** 가 아니고 **건물** 및 **방문** 엔터티가 아닙니다.
>   이름은 위의 단계에 나열된 이름과 다릅니다.

6. **다음**을 누릅니다. 연결을 다시 설정하라는 메시지가 표시됩니다. 

7. **연결 선택** 드롭다운을 펼치고 **새 연결**을 선택합니다.

8. 새 브라우저 창 또는 탭이 열립니다. Common Data Service 연결을 만들라는 메시지가 표시될 때 **만들기**를 선택합니다. 연결을 만들기 위해 필요한 경우 로그인합니다.

9. 솔루션을 가져왔던 이전 탭으로 다시 전환합니다.

10. **새로 고침**을 클릭하여 연결 목록을 새로 고칩니다. 

11. 방금 만든 연결이 선택되었는지 확인합니다.

12. **가져오기**를 누릅니다.

13. 가져오기가 완료될 때까지 기다립니다.

## 작업 #2: 데이터 가져오기  

1. **데이터 가져오기** 솔루션을 엽니다.

2. **데이터 가져오기** 흐름의 **상태**를 확인합니다.

3. **상태**가 **꺼짐**인 경우, **데이터 가져오기** 옆의 **...** 를 선택하고 **켜기**를 선택합니다.

   > **중요:** 오류 메시지를 수신한 경우, 만들어진 엔터티 및 필드가 위의 지침과 일치하는지 확인합니다.

4. **데이터 가져오기** 구성 요소를 엽니다. 새 탭에서 Power Automate가 열립니다. 

5. 팝업이 나타나는 경우 **시작하기**를 클릭합니다. 

6. **실행**을 클릭한 다음 메시지가 표시되면 **흐름 실행**을 클릭합니다.

7. **완료**를 클릭합니다.

8. 흐름 인스턴스가 실행을 완료할 때까지 기다립니다. **28일간의 실행 기록** 테이블을 새로 고쳐 흐름이 실행된 시기를 확인할 수 있습니다. 

    > 이 흐름의 목적은 이후의 랩에 대한 예제 데이터를 생성하는 것이었습니다. 다음 작업에서는 데이터 가져오기가 성공했는지 확인합니다. 

## 작업 #3: 데이터 가져오기 확인

1. 이전 Power Apps 탭으로 다시 이동합니다. 팝업에서 **완료**를 클릭합니다. 왼쪽 탐색 표시줄에서 **솔루션**을 선택하고 **캠퍼스 관리** 솔루션을 엽니다.

2. **방문** 엔터티를 클릭하여 연 다음 **데이터** 탭을 선택합니다.

3. 오른쪽 상단 모서리에 있는 **활성 방문**을 클릭하여 뷰 선택기를 표시한 다음 **모든 필드**를 선택합니다. 이렇게 하면 방문 데이터를 표시하는 데 사용되는 뷰가 변경됩니다. 

    > 해상도가 낮아 **활성 방문수**가 표시되지 않는 경우, 같은 위치에 눈 모양 아이콘이 표시됩니다.

    > 가져오기에 성공하면 방문 항목 목록이 표시됩니다.

4. **건물** 열에서 값을 클릭하고 건물 양식이 별도 창에서 열리는지 확인합니다. 

5. 최근에 시작된 창을 닫습니다.

6. **방문자** 열에서 값을 클릭하고(뷰를 오른쪽으로 스크롤해야 할 수도 있음) 연락처 양식이 별도 창에서 열리는지 확인합니다.

7. 최근에 시작된 창을 닫습니다.

# 과제

* 솔루션의 일부로 *약속* 활동을 사용해 보시겠습니까? 무엇이 변경 되나요?
* 예약된 종료를 어떻게 예약된 시작 후로 적용할 수 있나요? 
* 단일 방문 동안 여러 회의에 대한 지원을 추가하려면 어떻게 해야 하나요?
* 외부 연락처뿐만 아니라 내부 직원에 대해서도 건물 액세스를 보호하려면 어떻게 해야 하나요?
* 특정 건물을 방문할 때 관리 승인이 필요하게 하려면 어떻게 해야 하나요? 데이터 모델의 승인 프로세스는 어떻게 변경되나요?

