---
title: "배포 PKI 인증서 | System Center Configuration Manager"
description: "단계별 예제에 따라 System Center Configuration Manager에서 사용하는 PKI 인증서를 만들고 배포하는 프로세스를 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49dfa303453b26a64c1495a1259674e0d8a6bde2


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>System Center Configuration Manager용 PKI 인증서의 단계별 배포 예제: Windows Server 2008 인증 기관

*적용 대상: System Center Configuration Manager(현재 분기)*

Windows Server 2008 CA(인증 기관)를 사용하는 이 단계별 배포 예에서는 System Center Configuration Manager에서 사용하는 PKI(공개 키 인프라) 인증서를 만들고 배포하는 프로세스를 안내하는 절차를 제공합니다. 이러한 절차에서는 엔터프라이즈 CA(인증 기관)와 인증서 템플릿을 사용합니다. 이러한 단계는 개념 증명으로 테스트 네트워크에만 사용하는 것이 적절합니다.  

 필요한 인증서를 배포하는 방법에는 여러 가지가 있으므로 해당 PKI 배포 문서에서 프로덕션 환경의 필수 인증서를 배포하는 데 필요한 절차와 모범 사례를 참조해야 합니다. 인증서 요구 사항에 대한 자세한 내용은 [System Center Configuration Manager를 위한 PKI 인증서 요구 사항](../../../core/plan-design/network/pki-certificate-requirements.md)을 참조하세요.  

> [!TIP]  
>  이 항목의 지침은 테스트 네트워크 요구 사항 섹션에 설명된 지침보다 운영 체제에 쉽게 적용할 수 있습니다. 그러나 Windows Server 2012에서 발급 CA를 실행하는 경우 인증서 템플릿 버전을 묻는 메시지가 나타나지 않을 수 있습니다. 대신 템플릿 속성의 **호환성** 탭에서 이 버전을 다음과 같이 지정하세요.  
>   
>  -   **인증 기관**: **Windows Server 2003**  
> -   **인증서 받는 사람**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>이 섹션의 내용  
 다음 섹션에는 System Center Configuration Manager와 함께 사용할 수 있는 다음과 같은 인증서를 만들어 배포하기 위한 단계별 지침 예가 나와 있습니다.  

 [테스트 네트워크 요구 사항](#BKMK_testnetworkenvironment)  

 [인증서 개요](#BKMK_overview2008)  

 [IIS를 실행하는 사이트 시스템용 웹 서버 인증서 배포](#BKMK_webserver2008_cm2012)  

 [클라우드 기반 배포 지점용 서비스 인증서 배포](#BKMK_clouddp2008_cm2012)  

 [Windows 컴퓨터용 클라이언트 인증서 배포](#BKMK_client2008_cm2012)  

 [배포 지점용 클라이언트 인증서 배포](#BKMK_clientdistributionpoint2008_cm2012)  

 [모바일 장치용 등록 인증서 배포](#BKMK_mobiledevices2008_cm2012)  

 [AMT용 인증서 배포](#BKMK_AMT2008_cm2012)  

 [Mac 컴퓨터용 클라이언트 인증서 배포](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> 테스트 네트워크 요구 사항  
 이 단계별 지침은 다음과 같은 요구 사항을 갖습니다.  

-   테스트 네트워크가 Windows Server 2008과 Active Directory Domain Services를 실행하고 있고 단일 도메인, 단일 포리스트로 설치되어 있습니다.  

-   Active Directory 인증서 서비스 역할이 설치된 Certificate Services Windows Server 2008 Enterprise Edition을 실행하는 구성원 서버가 있고 이 서버가 엔터프라이즈 루트 CA(인증 기관)로 구성되어 있습니다.  

-   Windows Server 2008(Standard Edition 또는 Enterprise Edition R2 이상)이 설치되고 구성원 서버로 지정된 컴퓨터가 있으며, 이 컴퓨터에 IIS(인터넷 정보 서비스)가 설치되어 있습니다. 인터넷에서 System Center Configuration Manager 및 클라이언트에 의해 등록된 모바일 장치를 지원해야 하는 경우 이 컴퓨터는 인트라넷 FQDN(인트라넷에서 클라이언트 연결 지원)과 인터넷 FQDN으로 구성할 System Center Configuration Manager 사이트 시스템 서버가 됩니다.  

-   최신 서비스 팩이 설치된 Windows Vista 클라이언트가 있으며 이 컴퓨터가 ASCII 문자로 이루어진 컴퓨터 이름으로 구성되어 있고 도메인에 가입되어 있습니다. 이 컴퓨터가 System Center Configuration Manager 클라이언트 컴퓨터가 됩니다.  

-   루트 도메인 관리자 계정이나 엔터프라이즈 도메인 관리자 계정으로 로그인하고 이 배포 예의 모든 절차에 이 계정을 사용할 수 있습니다.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> 인증서 개요  
 다음 표에서 System Center Configuration Manager에 필요할 수 있는 PKI 인증서의 유형을 나열하고 사용 방법을 설명합니다.  

|인증서 요구 사항|인증서 설명|  
|-----------------------------|-----------------------------|  
|IIS를 실행하는 사이트 시스템용 웹 서버 인증서|이 인증서는 데이터를 암호화하고 클라이언트에 대해 서버를 인증하는 데 사용됩니다. 이는 IIS를 실행하고 HTTPS를 사용하도록 System Center Configuration Manager에서 구성된 사이트 시스템 서버에서 System Center Configuration Manager의 외부에 설치해야 합니다.<br /><br /> 이 인증서를 구성하고 설치하는 단계에 대한 자세한 내용은 이 항목의 [IIS를 실행하는 사이트 시스템용 웹 서버 인증서 배포](#BKMK_webserver2008_cm2012) 섹션을 참조하세요.|  
|클라이언트에서 클라우드 기반 배포 지점에 연결하기 위한 서비스 인증서|이 인증서를 구성하고 설치하는 단계는 이 항목에서 [클라우드 기반 배포 지점용 서비스 인증서 배포](#BKMK_clouddp2008_cm2012) 를 참조하세요.<br /><br /> **중요** : 이 인증서는 Microsoft Azure 관리 인증서와 함께 사용됩니다. 관리 인증서에 대한 자세한 내용은 MSDN 라이브러리의 Windows Azure 플랫폼 섹션에서 [관리 인증서를 만드는 방법](http://go.microsoft.com/fwlink/p/?LinkId=220281) 및 [Windows Azure 구독에 관리 인증서를 추가하는 방법](http://go.microsoft.com/fwlink/?LinkId=241722) 을 참조하세요.|  
|Windows 컴퓨터용 클라이언트 인증서|이 인증서는 HTTPS를 사용하도록 구성된 사이트 시스템에 대해 System Center Configuration Manager 클라이언트 컴퓨터를 인증하는 데 사용됩니다. 또한 HTTPS를 사용하도록 구성된 관리 지점과 상태 마이그레이션 지점에서 작업 상태를 모니터링하는 데 사용할 수 있습니다. 컴퓨터에 있는 System Center Configuration Manager의 외부에 설치해야 합니다.<br /><br /> 이 인증서를 구성하고 설치하는 단계는 이 항목에서 [Windows 컴퓨터용 클라이언트 인증서 배포](#BKMK_client2008_cm2012) 를 참조하세요.|  
|배포 지점용 클라이언트 인증서|이 인증서는 다음 두 가지 용도로 사용됩니다.<br /><br /> 이 인증서는 배포 지점에서 상태 메시지를 전송하기 전에 HTTPS 사용 관리 지점에 대해 배포 지점을 인증하는 데 사용됩니다.<br /><br /> **클라이언트에 대해 PXE 지원 사용** 배포 지점 옵션을 선택할 경우 인증서가 PXE 부팅을 수행하는 컴퓨터로 전송되어 이러한 컴퓨터에서 운영 체제 배포 시 HTTPS 사용 관리 지점에 연결할 수 있습니다.<br /><br /> 이 인증서를 구성하고 설치하는 단계에 대한 자세한 내용은 이 항목의 [배포 지점용 클라이언트 인증서 배포](#BKMK_clientdistributionpoint2008_cm2012) 섹션을 참조하세요.|  
|모바일 장치용 인증서 등록|이 인증서는 HTTPS를 사용하도록 구성된 사이트 시스템에 대해 System Center Configuration Manager 모바일 장치 클라이언트를 인증하는 데 사용됩니다. 이것은 System Center Configuration Manager에서 모바일 장치를 등록하는 과정에서 설치해야 하며 구성된 인증서 템플릿을 모바일 장치 클라이언트 설정으로 선택해야 합니다.<br /><br /> 이러한 인증서를 구성하는 단계는 이 항목에서 [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) 를 참조하세요.|  
|Intel AMT용 인증서|Intel AMT 기반 컴퓨터의 대역 외 관리와 관련된 세 가지 인증서, 즉 AMT 프로비전 인증서, AMT 웹 서버 인증서, 802.1X 무선 또는 유선 네트워크용 클라이언트 인증 인증서가 있습니다.<br /><br /> AMT 프로비전 인증서는 대역 외 서비스 지점 컴퓨터에서 System Center Configuration Manager 외부에 설치해야 하며 대역 외 서비스 지점 속성에서 설치된 인증서를 선택해야 합니다. AMT 웹 서버 인증서와 클라이언트 인증 인증서는 AMT 프로비전 및 관리 시 설치되며 대역 외 관리 구성 요소 속성에서 구성된 인증서 템플릿을 선택해야 합니다.<br /><br /> 이러한 인증서를 구성하는 단계에 대한 자세한 내용은 이 항목의 [AMT용 인증서 배포](#BKMK_AMT2008_cm2012) 섹션을 참조하세요.|  
|Mac 컴퓨터용 클라이언트 인증서|System Center Configuration Manager 등록을 사용할 때 Mac 컴퓨터에서 이 인증서를 요청하고 설치할 수 있으며 구성된 인증서 템플릿을 모바일 장치 클라이언트 설정으로 선택할 수 있습니다.<br /><br /> 이러한 인증서를 구성하는 단계는 이 항목에서 [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) 를 참조하세요.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> IIS를 실행하는 사이트 시스템용 웹 서버 인증서 배포  
 이 인증서 배포 절차는 다음과 같습니다.  

-   인증 기관에서 웹 서버 인증서 템플릿 만들기 및 발급  

-   웹 서버 인증서 요청  

-   웹 서버 인증서를 사용하도록 IIS 구성  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> 인증 기관에서 웹 서버 인증서 템플릿 만들기 및 발급  
 이 절차는 System Center Configuration Manager 사이트 시스템용 인증서 템플릿을 만들고 이를 인증 기관에 추가합니다.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>인증 기관에서 웹 서버 인증서 템플릿을 만들고 발급하려면  

1.  IIS를 실행할 System Center Configuration Manager 사이트 시스템을 설치할 구성원 서버가 포함된 **ConfigMgr IIS Servers**라는 보안 그룹을 만듭니다.  

2.  인증 서비스가 설치된 구성원 서버에서, 인증 기관 콘솔에서 **인증서 템플릿** 을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 **인증서 템플릿** 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **웹 서버**가 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 Configuration Manager 사이트 시스템에서 사용할 인증서를 생성할 웹 인증서(예: **ConfigMgr Client Certificate**)를 생성하기 위한 템플릿 이름을 입력합니다.  

6.  **주체 이름** 탭을 클릭하고 **요청에서 제공** 이 선택되어 있는지 확인합니다.  

7.  **보안** 탭을 클릭하고 **Domain Admins** 및 **Enterprise Admins** 보안 그룹에서 **등록**권한을 제거합니다.  

8.  **추가**를 클릭하고 텍스트 상자에 **ConfigMgr IIS Servers** 를 입력한 후 **확인**을 클릭합니다.  

9. 이 그룹에 대한 **등록** 권한을 선택하고, **읽기** 권한을 해제하지 않습니다.  

10. **확인**을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

11. 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

12. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Web Server Certificate**를 선택하고 **확인**을 클릭합니다.  

13. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> 웹 서버 인증서 요청  
 이 절차를 통해 사이트 시스템 서버 속성에서 구성할 인트라넷 및 인터넷 FQDN을 지정하고 IIS를 실행하는 구성원 서버에 웹 서버 인증서를 설치할 수 있습니다.  

##### <a name="to-request-the-web-server-certificate"></a>웹 서버 인증서를 요청하려면  

1.  IIS를 실행하는 웹 서버를 다시 시작하여, 컴퓨터에서 구성된 **읽기** 및 **등록** 권한을 사용하여 만들어진 인증서 템플릿에 액세스할 수 있는지 확인합니다.  

2.   **시작**, **실행**을 차례로 클릭한 다음 **mmc.exe**를 입력합니다. 비어 있는 콘솔에서 **파일**을 클릭한 후 **스냅인 추가/제거**를 클릭합니다.  

3.  **스냅인 추가/제거** 대화 상자의 **사용 가능한 스냅인** 목록에서 **인증서**를 선택하고 **추가**를 클릭합니다.  

4.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 선택한 후에 **다음**을 클릭합니다.  

5.  **컴퓨터 선택** 대화 상자에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 가 선택되어 있는지 확인한 다음 **마침**을 클릭합니다.  

6.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  

7.  콘솔에서 **인증서(로컬 컴퓨터)**를 확장하고 **개인**을 클릭합니다.  

8.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 후에 **새 인증서 요청**을 클릭합니다.  

9. **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

10. **인증서 등록 정책 선택** 페이지가 표시되면 **다음**을 클릭합니다.  

11. **인증서 요청** 페이지에 표시된 인증서 목록에서 **ConfigMgr Web Server Certificate**를 확인한 후 **이 인증서를 등록하려면 추가 정보가 필요합니다. 설정을 구성하려면 여기를 클릭 하십시오**를 클릭합니다.  

12. **인증서 속성** 대화 상자의 **주체** 탭에서 **주체 이름**에 대해 아무 것도 변경하지 않고 그대로 둡니다. 즉, **주체 이름** 섹션의 **값** 상자가 비어 있는 채로 둡니다. 대신 **대체 이름** 섹션에서 **유형** 드롭다운 목록을 클릭하고 **DNS**를 선택합니다.  

13. **값** 상자에 System Center Configuration Manager 사이트 시스템 속성에서 지정할 FQDN 값을 지정하고 **확인**을 클릭하여 **인증서 속성** 대화 상자를 닫습니다.  

     예제:  

    -   사이트 시스템이 인트라넷에서만 클라이언트 연결을 수락하고 사이트 시스템 서버의 FQDN이 **server1.internal.contoso.com**일 경우: **server1.internal.contoso.com**을 입력하고 **추가**를 클릭합니다.  

    -   사이트 시스템이 인트라넷과 인터넷에서 클라이언트 연결을 수락하며 사이트 시스템 서버의 인트라넷 FQDN이 **server1.internal.contoso.com** 이고 사이트 시스템 서버의 인터넷 FQDN이 **server.contoso.com**일 경우:  

        1.  **server1.internal.contoso.com**을 입력하고 **추가**를 클릭합니다.  

        2.  **server.contoso.com**을 입력하고 **추가**를 클릭합니다.  

        > [!NOTE]  
        >  System Center Configuration Manager에 대한 FQDN 지정 순서는 중요하지 않습니다. 그러나 모바일 장치와 프록시 웹 서버를 비롯한 인증서를 사용할 모든 장치에서 인증서 SAN을 사용하고 SAN에 여러 값을 사용할 수 있는지 확인해야 합니다. 장치가 인증서에서 SAN 값을 제한적으로 지원할 경우 FQDN의 순서를 변경하거나 대신 주체 값을 사용해야 할 수 있습니다.  

14. **인증서 요청** 페이지의 표시된 인증서 목록에서 **ConfigMgr Web Server Certificate** 를 확인하고 **등록**을 클릭합니다.  

15. **인증서 설치 결과** 페이지에서 인증서가 설치될 때까지 기다렸다가 **마침**을 클릭합니다.  

16. **인증서(로컬 컴퓨터)**를 닫습니다.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> 웹 서버 인증서를 사용하도록 IIS 구성  
 이 절차는 설치된 인증서를 IIS **기본 웹 사이트**에 바인딩합니다.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>웹 서버 인증서를 사용하도록 IIS를 구성하려면  

1.  IIS가 설치된 구성원 서버에서 **시작**, **프로그램**, **관리 도구**, **IIS(인터넷 정보 서비스) 관리자**를 차례로 클릭합니다.  

2.  **사이트**를 확장하고 **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭한 후에 **바인딩 편집**을 선택합니다.  

3.  **https** 항목을 클릭하고 **편집**을 클릭합니다.  

4.  **사이트 바인딩 편집** 대화 상자에서 ConfigMgr 웹 서버 인증서 템플릿을 사용하여 요청한 인증서를 선택하고 **확인**을 클릭합니다.  

    > [!NOTE]  
    >  올바른 인증서가 어느 것인지 확실하지 않은 경우 인증서를 하나 선택하고 **보기**를 클릭합니다. 그러면 인증서 스냅인에서 표시되는 인증서와 선택한 인증서 정보를 비교할 수 있습니다. 예를 들어 인증서 스냅인에는 인증서를 요청하는 데 사용된 인증서 템플릿이 표시됩니다. 그런 다음 ConfigMgr 웹 서버 인증서 템플릿을 사용하여 요청된 인증서의 인증서 지문을 **사이트 바인딩 편집** 대화 상자에서 현재 선택된 인증서의 인증서 지문과 비교할 수 있습니다.  

5.  **사이트 바인딩 편집** 대화 상자에서 **확인** 을 클릭하고 **닫기**를 클릭합니다.  

6.  **IIS(인터넷 정보 서비스) 관리자**를 닫습니다.  

 이제 구성원 서버가 System Center Configuration Manager 웹 서버 인증서를 사용하여 프로비전됩니다.  

> [!IMPORTANT]  
>  이 컴퓨터에 System Center Configuration Manager 사이트 시스템을 설치하는 경우 인증서를 요청할 때 지정한 것과 동일한 FQDN을 사이트 시스템 속성에 지정해야 합니다.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> 클라우드 기반 배포 지점용 서비스 인증서 배포  

> [!NOTE]  
>  클라우드 기반 배포 지점용 서비스 인증서는 System Center Configuration Manager SP1 이상에 적용됩니다.  

 이 인증서 배포 절차는 다음과 같습니다.  

-   [인증 기관에서 사용자 지정 웹 서버 인증서 템플릿 만들기 및 발급](#BKMK_clouddpcreating2008)  

-   [사용자 지정 웹 서버 인증서 요청](#BKMK_clouddprequesting2008)  

-   [클라우드 기반 배포 지점용 사용자 지정 웹 서버 인증서 내보내기](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> 인증 기관에서 사용자 지정 웹 서버 인증서 템플릿 만들기 및 발급  
 이 절차는 웹 서버 인증서 템플릿을 기반으로 사용자 지정 인증서 템플릿을 만듭니다. 인증서는 System Center Configuration Manager 클라우드 기반 배포 지점용이며 개인 키를 내보낼 수 있어야 합니다. 인증서 템플릿이 만들어진 후에는 인증 기관에 추가됩니다.  

> [!NOTE]  
>  이 절차는 IIS를 실행하는 사이트 시스템을 위해 만든 웹 서버 인증서 템플릿과는 다른 인증서 템플릿을 사용합니다. 두 인증서에 서버 인증 기능이 필요하지만 클라우드 기반 배포 지점용 인증서의 경우 주체 이름에 사용자 정의 값을 입력해야 하고 개인 키를 내보내야 하기 때문입니다. 이 구성이 필요한 경우를 제외하고 개인 키를 내보낼 수 있도록 인증서 템플릿을 구성하지 않는 것이 보안상 좋습니다. 클라우드 기반 배포 지점의 경우 인증서를 인증서 저장소에서 선택하지 않고 파일로 가져와야 하므로 이 구성이 필요합니다.  
>   
>  이 인증서에 대한 새 인증서 템플릿을 만들면 개인 키를 내보낼 수 있도록 허용하는 인증서를 특정 컴퓨터에서만 요청할 수 있게 제한할 수 있습니다. 프로덕션 네트워크에서는 이 인증서를 다음과 같이 수정하는 것을 고려해야 할 수 있습니다.  
>   
>  -   승인이 있어야 인증서를 설치할 수 있도록 하여 보안 강화  
> -   인증서 유효 기간 연장. 만료 전에 매번 인증서를 내보내고 가져와야 하므로 유효 기간을 늘리면 이 절차를 반복하는 횟수가 줄어듭니다. 그러나 유효 기간을 늘리면 공격자가 개인 키를 해독하여 인증서를 도용할 수 있는 시간이 늘어나므로 인증서 보안이 약화됩니다.  
> -   인증서 SAN(주체 대체 이름)에 사용자 지정 값을 사용하여 IIS를 통해 사용하는 표준 웹 서버 인증서에서 이 인증서를 식별할 수 있도록 합니다.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>인증 기관에서 사용자 지정 웹 서버 인증서 템플릿을 만들고 발급하려면  

1.  구성원 서버가 포함된 **ConfigMgr Site Servers**라는 보안 그룹을 만들어 클라우드 기반 배포 지점을 관리할 System Center Configuration Manager 기본 사이트 서버를 설치합니다.  

2.  인증 기관을 실행하는 구성원 서버에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 인증서 템플릿 관리 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **웹 서버**가 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 클라우드 기반 배포 지점용 웹 서버 인증서를 생성할 템플릿 이름(예: **ConfigMgr Cloud-Based Distribution Point Certificate**)을 입력합니다.  

6.  **요청 처리** 탭을 클릭하고 **개인 키를 내보낼 수 있음**을 선택합니다.  

7.  **보안** 탭을 클릭하고 **Enterprise Admins** 보안 그룹에서 **등록** 을 제거합니다.  

8.  **추가**를 클릭하고 텍스트 상자에 **ConfigMgr Site Servers** 를 입력한 후 **확인**을 클릭합니다.  

9. 이 그룹에 대한 **등록** 권한을 선택하고, **읽기** 권한을 해제하지 않습니다.  

10. **확인** 을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

11. 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

12. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Cloud-Based Distribution Point Certificate**을 선택하고 **확인**을 클릭합니다.  

13. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> 사용자 지정 웹 서버 인증서 요청  
 이 절차는 사용자 지정 웹 서버 인증서를 요청하고 사이트 서버를 실행하는 구성원 서버에 설치합니다.  

##### <a name="to-request-the-custom-web-server-certificate"></a>사용자 지정 웹 서버 인증서를 요청하려면  

1.  컴퓨터에서 구성된 **읽기** 및 **등록** 권한을 사용하여 만들어진 인증서 템플릿에 액세스할 수 있도록 **ConfigMgr Site Servers** 보안 그룹을 만들고 구성한 후에 구성원 서버를 다시 시작합니다.  

2.   **시작**, **실행**을 차례로 클릭한 다음 **mmc.exe**를 입력합니다. 비어 있는 콘솔에서 **파일**을 클릭한 후 **스냅인 추가/제거**를 클릭합니다.  

3.  **스냅인 추가/제거** 대화 상자의 **사용 가능한 스냅인** 목록에서 **인증서**를 선택하고 **추가**를 클릭합니다.  

4.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 선택한 후에 **다음**을 클릭합니다.  

5.  **컴퓨터 선택** 대화 상자에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 가 선택되어 있는지 확인한 다음 **마침**을 클릭합니다.  

6.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  

7.  콘솔에서 **인증서(로컬 컴퓨터)**를 확장하고 **개인**을 클릭합니다.  

8.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 후에 **새 인증서 요청**을 클릭합니다.  

9. **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

10. **인증서 등록 정책 선택** 페이지가 표시되면 **다음**을 클릭합니다.  

11. **인증서 요청** 페이지에 표시된 인증서 목록에서 **ConfigMgr Cloud-Based Distribution Point Certificate**를 확인한 후 **이 인증서를 등록하려면 추가 정보가 필요합니다. 설정을 구성하려면 여기를 클릭 하십시오**를 클릭합니다.  

12. **인증서 속성** 대화 상자의 **주체** 탭에서 **주체 이름**의 **유형** 으로 **일반 이름**을 선택합니다.  

13. **값** 상자에서 FQDN 형식을 사용하여 원하는 서비스 이름과 도메인 이름을 지정합니다. **clouddp1.contoso.com**등을 지정할 수 있습니다.  

    > [!NOTE]  
    >  네임스페이스에서 고유하기만 하다면 어떤 서비스 이름을 지정하든지 관계 없습니다. DNS를 사용하여 별칭(CNAME 레코드)을 만들고 이 서비스 이름을 자동으로 생성된 식별자(GUID)와 Windows Azure IP 주소에 매핑하게 됩니다.  

14. **추가**를 클릭하고 **확인** 을 클릭하여 **인증서 속성** 대화 상자를 닫습니다.  

15. **인증서 요청** 페이지의 표시된 인증서 목록에서 **ConfigMgr Cloud-Based Distribution Point Certificate** 를 확인하고 **등록**을 클릭합니다.  

16. **인증서 설치 결과** 페이지에서 인증서가 설치될 때까지 기다렸다가 **마침**을 클릭합니다.  

17. **인증서(로컬 컴퓨터)**를 닫습니다.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> 클라우드 기반 배포 지점용 사용자 지정 웹 서버 인증서 내보내기  
 이 절차는 클라우드 기반 배포 지점을 만들 때 가져올 수 있도록 사용자 지정 웹 서버 인증서를 파일로 내보냅니다.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>클라우드 기반 배포 지점용 사용자 지정 웹 서버 인증서를 내보내려면  

1.  **인증서(로컬 컴퓨터)** 콘솔에서 방금 설치한 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 선택한 후에 **내보내기**를 클릭합니다.  

2.  인증서 내보내기 마법사에서 **다음**을 클릭합니다.  

3.  **개인 키 내보내기** 페이지에서 **예, 개인 키를 내보냅니다**를 클릭하고 **다음**을 클릭합니다.  

    > [!NOTE]  
    >  이 옵션을 사용할 수 없는 경우 개인 키를 내보내는 옵션 없이 인증서가 만들어진 것입니다. 이 시나리오에서는 필요한 형식으로 인증서를 내보낼 수 없습니다. 개인 키를 내보낼 수 있도록 인증서 템플릿을 다시 구성한 후에 다시 인증서를 요청해야 합니다.  

4.  **파일 내보내기 형식** 페이지에서 **개인 정보 교환 - PKCS #12(.PFX)** 가 선택되어 있는지 확인합니다.  

5.  **암호** 페이지에서 개인 키를 사용하는 내보내는 인증서를 보호하도록 강력한 암호를 지정하고 **다음**을 클릭합니다.  

6.  **내보낼 파일** 페이지에서 내보낼 파일의 이름을 지정하고 **다음**을 클릭합니다.  

7.  마법사를 닫으려면 **인증서 내보내기 마법사** 에서 **마침** 을 클릭하고 확인 대화 상자에서 **확인** 을 클릭합니다.  

8.  **인증서(로컬 컴퓨터)**를 닫습니다.  

9. 파일을 안전하게 저장하고 System Center Configuration Manager 콘솔에서 액세스할 수 있는지 확인합니다.  

 이제 클라우드 기반 배포 지점을 만들 때 인증서를 가져올 수 있습니다.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Windows 컴퓨터용 클라이언트 인증서 배포  
 이 인증서 배포 절차는 다음과 같습니다.  

-   인증 기관에서 워크스테이션 인증 인증서 템플릿 만들기 및 발급  

-   그룹 정책을 사용하여 워크스테이션 인증 템플릿의 자동 등록 구성  

-   워크스테이션 인증 인증서 자동 등록 및 컴퓨터에서 설치 확인  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> 인증 기관에서 워크스테이션 인증 인증서 템플릿 만들기 및 발급  
 이 절차에서는 System Center Configuration Manager 클라이언트 컴퓨터용 인증서 템플릿을 만들고 이를 인증 기관에 추가합니다.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>인증 기관에서 워크스테이션 인증 인증서 템플릿을 만들고 발급하려면  

1.  인증 기관을 실행하는 구성원 서버에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 인증서 템플릿 관리 콘솔을 로드합니다.  

2.  결과 창에서 **템플릿 표시 이름** 열의 **워크스테이션 인증**이 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

3.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

4.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 Configuration Manager 클라이언트 컴퓨터에서 사용할 인증서를 생성할 템플릿 이름(예: **ConfigMgr Client Certificate**)을 입력합니다.  

5.  **보안** 탭을 클릭하고 **도메인 컴퓨터** 그룹을 선택한 후에 추가 권한으로 **읽기** 및 **자동 등록**을 선택합니다. **등록**을 선택 취소하지 마십시오.  

6.  **확인** 을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

7.  인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

8.  **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Client Certificate**를 선택하고 **확인**을 클릭합니다.  

9. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> 그룹 정책을 사용하여 워크스테이션 인증 템플릿의 자동 등록 구성  
 이 절차는 컴퓨터에서 클라이언트 인증서를 자동으로 등록하도록 그룹 정책을 구성합니다.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>그룹 정책을 사용하여 워크스테이션 인증 템플릿의 자동 등록을 구성하려면  

1.  도메인 컨트롤러에서 **시작**, **관리 도구**, **그룹 정책 관리**를 차례로 클릭합니다.  

2.  도메인을 찾아 마우스 오른쪽 단추로 클릭하고 **이 도메인에서 GPO를 만들어 여기에 연결**을 선택합니다.  

    > [!NOTE]  
    >  이 단계는 Active Directory Domain Services와 함께 설치되는 기본 도메인 정책을 편집하지 않고 사용자 지정 설정을 위한 새 그룹 정책을 만드는 모범 사례를 사용합니다. 도메인 수준에서 이 그룹 정책을 할당함으로써 도메인의 모든 컴퓨터에 그룹 정책을 적용하게 됩니다. 그러나 프로덕션 환경에서는 조직 구성 단위 수준에서 그룹 정책을 할당하여 선택한 컴퓨터에서만 등록되도록 자동 등록을 제한하거나 보안 그룹으로 도메인 그룹 정책을 필터링하여 보안 그룹의 컴퓨터에만 적용할 수 있습니다. 자동 등록을 제한하는 경우 관리 지점으로 구성된 서버는 포함해야 합니다.  

3.  **새 GPO** 대화 상자에 새 그룹 정책의 이름(예: **Autoenroll Certificates**)을 입력하고 **확인**을 클릭합니다.  

4.  결과 창의 **연결된 그룹 정책 개체** 탭에서 새 그룹 정책을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  

5.  **그룹 정책 관리 편집기**에서 **컴퓨터 구성** 아래의 **정책**을 확장한 다음 **Windows 설정** / **보안 설정** / **공개 키 정책**으로 이동합니다.  

6.  **인증서 서비스 클라이언트 – 자동 등록**이라는 개체 형식을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  

7.  **구성 모델** 드롭다운 목록에서 **사용**, **만료된 인증서 갱신, 보류 중인 인증서 업데이트, 해지된 인증서 제거**, **인증서 템플릿을 사용하는 인증서 업데이트**를 차례로 선택한 후에 **확인**을 클릭합니다.  

8.  **그룹 정책 관리**를 닫습니다.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> 워크스테이션 인증 인증서 자동 등록 및 컴퓨터에서 설치 확인  
 이 절차는 컴퓨터에 클라이언트 인증서를 설치하고 설치를 확인합니다.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>워크스테이션 인증 인증서를 자동으로 등록하고 클라이언트 컴퓨터에서 설치를 확인하려면  

1.  워크스테이션 컴퓨터를 다시 시작하고 몇 분 기다렸다가 다시 로그온합니다.  

    > [!NOTE]  
    >  컴퓨터를 다시 시작하는 것이 인증서를 자동으로 등록하기 위한 가장 안정적인 방법입니다.  

2.  관리자 권한을 가진 계정으로 로그온합니다.  

3.  검색 상자에 **mmc.exe**를 입력한 후 **Enter**키를 누릅니다.  

4.  비어 있는 관리 콘솔에서 **파일**을 클릭한 후 **스냅인 추가/제거**를 클릭합니다.  

5.  **스냅인 추가/제거** 대화 상자의 **사용 가능한 스냅인** 목록에서 **인증서**를 선택하고 **추가**를 클릭합니다.  

6.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 선택한 후에 **다음**을 클릭합니다.  

7.  **컴퓨터 선택** 대화 상자에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 가 선택되어 있는지 확인한 다음 **마침**을 클릭합니다.  

8.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  

9. 콘솔에서 **인증서(로컬 컴퓨터)**를 확장하고 **개인**을 확장한 후에 **인증서**를 클릭합니다.  

10. 결과 창에 인증서가 표시되며, **용도** 열에 **클라이언트 인증** 이 표시되고, **인증서 템플릿** 열에 **ConfigMgr Client Certificate** 가 표시되는지 확인합니다.  

11. **인증서(로컬 컴퓨터)**를 닫습니다.  

12. 구성원 서버에 대해 1~11단계를 반복하여 관리 지점으로 구성될 서버에도 클라이언트 인증서가 있는지 확인합니다.  

 이제 컴퓨터는 System Center Configuration Manager 클라이언트 인증서를 사용하여 프로비전됩니다.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> 배포 지점용 클라이언트 인증서 배포  

> [!NOTE]  
>  인증서 요구 사항이 동일하기 때문에 PXE 부팅을 사용하지 않는 미디어 이미지에도 이 인증서를 사용할 수 있습니다.  

 이 인증서 배포 절차는 다음과 같습니다.  

-   인증 기관에서 사용자 지정 워크스테이션 인증 인증서 템플릿 만들기 및 발급  

-   사용자 지정 워크스테이션 인증 인증서 요청  

-   배포 지점용 클라이언트 인증서 내보내기  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> 인증 기관에서 사용자 지정 워크스테이션 인증 인증서 템플릿 만들기 및 발급  
 이 절차는 개인 키를 내보낼 수 있도록 하는 System Center Configuration Manager 배포 지점용 사용자 지정 인증서 템플릿을 만들고 인증 기관에 인증서 템플릿을 추가합니다.  

> [!NOTE]  
>  이 절차는 클라이언트 컴퓨터용으로 만든 인증서 템플릿과 다른 인증서 템플릿을 사용합니다. 두 인증서에 모두 클라이언트 인증 기능이 필요하지만 배포 지점용 인증서의 경우 개인 키를 내보내야 하기 때문입니다. 이 구성이 필요한 경우를 제외하고 개인 키를 내보낼 수 있도록 인증서 템플릿을 구성하지 않는 것이 보안상 좋습니다. 배포 지점의 경우 인증서를 인증서 저장소에서 선택하지 않고 파일로 가져와야 하므로 이 구성이 필요합니다.  
>   
>  이 인증서에 대한 새 인증서 템플릿을 만들면 개인 키를 내보낼 수 있도록 허용하는 인증서를 특정 컴퓨터에서만 요청할 수 있게 제한할 수 있습니다. 이 배포 예에서는 이것이 IIS를 실행하는 System Center Configuration Manager 사이트 시스템 서버에 대해 이전에 만든 보안 그룹이 됩니다. IIS 사이트 시스템 역할을 배포하는 프로덕션 네트워크에서는 이러한 사이트 시스템 서버로만 인증서를 제한할 수 있도록 배포 지점을 실행하는 서버에 대한 새 보안 그룹을 만들어 보십시오. 또한 이 인증서를 다음과 같이 수정하는 것을 고려해야 할 수 있습니다.  
>   
>  -   승인이 있어야 인증서를 설치할 수 있도록 하여 보안 강화  
> -   인증서 유효 기간 연장. 만료 전에 매번 인증서를 내보내고 가져와야 하므로 유효 기간을 늘리면 이 절차를 반복하는 횟수가 줄어듭니다. 그러나 유효 기간을 늘리면 공격자가 개인 키를 해독하여 인증서를 도용할 수 있는 시간이 늘어나므로 인증서 보안이 약화됩니다.  
> -   표준 클라이언트 인증서에서 이 인증서를 식별할 수 있도록 인증서 주체 필드 또는 주체 대체 이름에 사용자 지정 값 사용. 여러 배포 지점에 대해 동일한 인증서를 사용할 경우 이것이 특히 유용할 수 있습니다.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>인증 기관에서 사용자 지정 워크스테이션 인증 인증서 템플릿을 만들고 발급하려면  

1.  인증 기관을 실행하는 구성원 서버에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 인증서 템플릿 관리 콘솔을 로드합니다.  

2.  결과 창에서 **템플릿 표시 이름** 열의 **워크스테이션 인증**이 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

3.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

4.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 배포 지점용 클라이언트 인증 인증서를 생성할 템플릿 이름(예: **ConfigMgr Client Distribution Point Certificate**)을 입력합니다.  

5.  **요청 처리** 탭을 클릭하고 **개인 키를 내보낼 수 있음**을 선택합니다.  

6.  **보안** 탭을 클릭하고 **Enterprise Admins** 보안 그룹에서 **등록** 을 제거합니다.  

7.  **추가**를 클릭하고 텍스트 상자에 **ConfigMgr IIS Servers** 를 입력한 후 **확인**을 클릭합니다.  

8.  이 그룹에 대한 **등록** 권한을 선택하고, **읽기** 권한을 해제하지 않습니다.  

9. **확인** 을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

10. 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

11. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Client Distribution Point Certificate**를 선택하고 **확인**을 클릭합니다.  

12. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> 사용자 지정 워크스테이션 인증 인증서 요청  
 이 절차는 IIS를 실행하며 배포 지점으로 구성될 구성원 서버에 사용자 지정 클라이언트 인증서를 요청하고 설치합니다.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>사용자 지정 워크스테이션 인증 인증서를 요청하려면  

1.   **시작**, **실행**을 차례로 클릭한 다음 **mmc.exe**를 입력합니다. 비어 있는 콘솔에서 **파일**을 클릭한 후 **스냅인 추가/제거**를 클릭합니다.  

2.  **스냅인 추가/제거** 대화 상자의 **사용 가능한 스냅인** 목록에서 **인증서**를 선택하고 **추가**를 클릭합니다.  

3.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 선택한 후에 **다음**을 클릭합니다.  

4.  **컴퓨터 선택** 대화 상자에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 가 선택되어 있는지 확인한 다음 **마침**을 클릭합니다.  

5.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  

6.  콘솔에서 **인증서(로컬 컴퓨터)**를 확장하고 **개인**을 클릭합니다.  

7.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 후에 **새 인증서 요청**을 클릭합니다.  

8.  **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

9. **인증서 등록 정책 선택** 페이지가 표시되면 **다음**을 클릭합니다.  

10. **인증서 요청** 페이지에서, 표시된 인증서 목록에서 **ConfigMgr Client Distribution Point Certificate** 를 확인하고 **등록**을 클릭합니다.  

11. **인증서 설치 결과** 페이지에서 인증서가 설치될 때까지 기다렸다가 **마침**을 클릭합니다.  

12. 결과 창에 인증서가 표시되며, **용도** 열에 **클라이언트 인증** 이 표시되고, **인증서 템플릿** 열에 **ConfigMgr Client Distribution Point Certificate** 가 표시되는지 확인합니다.  

13. **인증서(로컬 컴퓨터)**를 닫지 마십시오.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> 배포 지점용 클라이언트 인증서 내보내기  
 이 절차는 배포 지점 속성에서 가져올 수 있도록 사용자 지정 워크스테이션 인증 인증서를 파일로 내보냅니다.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>배포 지점에 대한 클라이언트 인증서를 내보내려면  

1.  **인증서(로컬 컴퓨터)** 콘솔에서 방금 설치한 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 선택한 후에 **내보내기**를 클릭합니다.  

2.  인증서 내보내기 마법사에서 **다음**을 클릭합니다.  

3.  **개인 키 내보내기** 페이지에서 **예, 개인 키를 내보냅니다**를 클릭하고 **다음**을 클릭합니다.  

    > [!NOTE]  
    >  이 옵션을 사용할 수 없는 경우 개인 키를 내보내는 옵션 없이 인증서가 만들어진 것입니다. 이 시나리오에서는 필요한 형식으로 인증서를 내보낼 수 없습니다. 개인 키를 내보낼 수 있도록 인증서 템플릿을 다시 구성한 후에 다시 인증서를 요청해야 합니다.  

4.  **파일 내보내기 형식** 페이지에서 **개인 정보 교환 - PKCS #12(.PFX)** 가 선택되어 있는지 확인합니다.  

5.  **암호** 페이지에서 개인 키를 사용하는 내보내는 인증서를 보호하도록 강력한 암호를 지정하고 **다음**을 클릭합니다.  

6.  **내보낼 파일** 페이지에서 내보낼 파일의 이름을 지정하고 **다음**을 클릭합니다.  

7.  마법사를 닫으려면 **인증서 내보내기 마법사** 에서 **마침** 을 클릭하고 확인 대화 상자에서 **확인** 을 클릭합니다.  

8.  **인증서(로컬 컴퓨터)**를 닫습니다.  

9. 파일을 안전하게 저장하고 System Center Configuration Manager 콘솔에서 액세스할 수 있는지 확인합니다.  

 이제 배포 지점을 구성할 때 이 인증서를 가져올 수 있습니다.  

> [!TIP]  
>  이제 PXE 부팅을 사용하지 않는 운영 체제 배포에 대해 미디어 이미지를 구성할 때 동일한 인증서 파일을 사용할 수 있으며, 이미지를 설치하기 위한 작업 순서가 HTTPS 클라이언트 연결이 필요한 관리 지점에 연결해야 합니다.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> 모바일 장치용 등록 인증서 배포  
 이 인증서 배포는 단일 절차로 인증 기관에서 등록 인증서 템플릿을 만들고 발급합니다.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>인증 기관에서 등록 인증서 템플릿 만들기 및 발급  
 이 절차에서는 System Center Configuration Manager 모바일 장치용 등록 인증서 템플릿을 만들고 인증 기관에 추가합니다.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>인증 기관에서 등록 인증서 템플릿을 만들고 발급하려면  

1.  System Center Configuration Manager에 모바일 장치를 등록할 사용자를 포함하는 보안 그룹을 만듭니다.  

2.  인증 서비스가 설치된 구성원 서버에서, 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 인증서 템플릿 관리 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **인증된 세션**이 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 System Center Configuration Manager로 관리할 모바일 장치용 등록 인증서를 생성하기 위한 템플릿 이름(예: **ConfigMgr Mobile Device Enrollment Certificate**)을 입력합니다.  

6.  **주체 이름** 탭에서 **이 Active Directory 정보로 만듦** 이 선택되어 있는지 확인하고 **주체 이름 형식:** 으로 **일반 이름** 을 선택한 후에 **대체 주체 이름에 이 정보 포함** 에서 **UPN(사용자 계정 이름)**의 선택을 취소합니다.  

7.  **보안** 탭을 클릭하고 등록할 모바일 장치의 사용자가 포함된 보안 그룹을 선택한 후에 추가 권한으로 **등록**을 선택합니다. **읽기**의 선택을 취소하지 마십시오.  

8.  **확인** 을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

9. 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

10. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Mobile Device Enrollment Certificate**를 선택하고 **확인**을 클릭합니다.  

11. 인증서를 더 만들고 발급할 필요가 없으면 인증 기관 콘솔을 닫습니다.  

 이제 클라이언트 설정에서 모바일 장치 등록 프로필을 구성할 때 모바일 장치 등록 인증서 템플릿을 선택할 수 있습니다.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> AMT용 인증서 배포  
 이 인증서 배포 절차는 다음과 같습니다.  

-   AMT 프로비전 인증서 만들기, 발급 및 설치  

-   AMT 기반 컴퓨터용 웹 서버 인증서 만들기 및 발급  

-   802.1X AMT 기반 컴퓨터용 클라이언트 인증 인증서 만들기 및 발급  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> AMT 프로비전 인증서 만들기, 발급 및 설치  
 내부 루트 CA의 인증서 지문을 사용하여 AMT 기반 컴퓨터를 구성한 경우 내부 CA를 사용하여 프로비전 인증서를 만듭니다. 이 경우가 아니고 외부 인증 기관을 사용해야 하는 경우, AMT 프로비전 인증서를 발급하는 회사의 지침을 따릅니다. 대개 회사의 공공 웹 사이트에서 인증서를 요청해야 합니다. Intel vPro Expert Center: Microsoft vPro Manageability 웹 사이트([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001))에서 선택한 외부 CA에 대한 자세한 지침을 찾을 수도 있습니다.  

> [!IMPORTANT]  
>  외부 CA가 Intel AMT 프로비전 개체 식별자를 지원하지 않을 수도 있습니다. 이 경우 **Intel(R) 클라이언트 설치 인증서**의 OU 특성을 제공하는 대체 방법을 사용합니다.  

 외부 CA에서 AMT 프로비전 인증서를 요청하는 경우 대역 외 서비스 지점을 호스팅하는 구성원 서버의 컴퓨터 개인 인증서 저장소에 인증서를 설치합니다.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>AMT 프로비전 인증서를 요청 및 발급하려면  

1.  대역 외 서비스 지점을 실행하는 사이트 시스템 서버의 컴퓨터 계정이 포함된 보안 그룹을 만듭니다.  

2.  인증 서비스가 설치된 구성원 서버에서, 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 **인증서 템플릿** 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **웹 서버** 가 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에 AMT 프로비전 인증서 템플릿의 템플릿 이름(예: **ConfigMgr AMT Provisioning**)을 입력합니다.  

6.  **주체 이름** 탭을 클릭하고 **이 Active Directory 정보로 만듦**을 선택하고 **일반 이름**을 선택합니다.  

7.  **확장** 탭에서 **응용 프로그램 정책** 을 선택하고 **편집**을 클릭합니다.  

8.  **응용 프로그램 정책 확장 편집** 대화 상자에서 **추가**를 클릭합니다.  

9. **응용 프로그램 정책 추가** 대화 상자에서 **새로 만들기**를 클릭합니다.  

10. **새 응용 프로그램 정책** 대화 상자에서 **이름** 필드에 **AMT Provisioning** 을 입력하고 **개체 식별자**:에 다음 숫자를 입력합니다. **2.16.840.1.113741.1.2.3**을 포함해야 합니다.  

11. **확인**을 클릭한 후에 **응용 프로그램 정책 추가** 대화 상자에서 **확인** 을 클릭합니다.  

12. **응용 프로그램 정책 확장 편집** 대화 상자에서 **확인** 을 클릭합니다.  

13. 이제 **새 템플릿의 속성** 대화 상자에 **응용 프로그램 정책** 설명으로 **서버 인증** 및 **AMT Provisioning**이 표시되어 있습니다.  

14. **보안** 탭을 클릭하고 **Domain Admins** 및 **Enterprise Admins** 보안 그룹에서 **등록**권한을 제거합니다.  

15. **추가**를 클릭하고 대역 외 서비스 지점 사이트 시스템 역할의 컴퓨터 계정이 포함된 보안 그룹의 이름을 입력한 후에 **확인**을 클릭합니다.  

16. 이 그룹에 대한 **등록** 권한을 선택하고, **읽기** 권한을 해제하지 않습니다.  

17. **확인**을 클릭하여 **인증서 템플릿** 콘솔을 닫습니다.  

18. **인증 기관**에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

19. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr AMT Provisioning**을 선택하고 **확인**을 클릭합니다.  

    > [!NOTE]  
    >  18단계 또는 19단계를 완료할 수 없으면 Windows Server 2008 Enterprise Edition을 사용 중인지 확인합니다. Windows Server Standard Edition 및 인증서 서비스를 사용하여 템플릿을 구성할 수는 있지만, Windows Server 2008 Enterprise Edition을 사용하지 않는 경우 수정된 인증서 템플릿을 사용하여 인증서를 배포할 수 없습니다.  

20. **인증 기관**을 닫지 마십시오.  

 이제 내부 CA의 AMT 프로비전 인증서를 대역 서비스 지점 컴퓨터에 설치할 수 있습니다.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>AMT 프로비전 인증서를 설치하려면  

1.  IIS를 실행하는 구성원 서버를 다시 시작하여 구성된 권한으로 인증서 템플릿에 액세스할 수 있는지 확인합니다.  

2.   **시작**, **실행**을 차례로 클릭한 다음 **mmc.exe**를 입력합니다. 비어 있는 콘솔에서 **파일**을 클릭한 후 **스냅인 추가/제거**를 클릭합니다.  

3.  **스냅인 추가/제거** 대화 상자의 **사용 가능한 스냅인** 목록에서 **인증서**를 선택하고 **추가**를 클릭합니다.  

4.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 선택한 후에 **다음**을 클릭합니다.  

5.  **컴퓨터 선택** 대화 상자에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 가 선택되어 있는지 확인한 다음 **마침**을 클릭합니다.  

6.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  

7.  콘솔에서 **인증서(로컬 컴퓨터)**를 확장하고 **개인**을 클릭합니다.  

8.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 후에 **새 인증서 요청**을 클릭합니다.  

9. **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

10. **인증서 등록 정책 선택** 페이지가 표시되면 **다음**을 클릭합니다.  

11. **인증서 요청** 페이지에서, 표시된 인증서 목록에서 **AMT Provisioning** 을 선택하고 **등록**을 클릭합니다.  

12. **인증서 설치 결과** 페이지에서 인증서가 설치될 때까지 기다렸다가 **마침**을 클릭합니다.  

13. **인증서(로컬 컴퓨터)**를 닫습니다.  

 이제 내부 CA의 AMT 프로비전 인증서를 대역 외 서비스 지점 속성에서 선택할 수 있습니다.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>AMT 기반 컴퓨터용 웹 서버 인증서 만들기 및 발급  
 AMT 기반 컴퓨터용 웹 서버 인증서를 준비하려면 다음 절차를 따르십시오.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>웹 서버 인증서 템플릿을 만들고 발급하려면  

1.  System Center Configuration Manager에서 AMT 프로비전 중 만드는 AMT 컴퓨터 계정을 포함하도록 빈 보안 그룹을 만듭니다.  

2.  인증 서비스가 설치된 구성원 서버에서, 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 **인증서 템플릿** 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **웹 서버**가 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition.**  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 AMT 컴퓨터의 대역 외 관리에 사용할 웹 인증서를 생성하기 위한 템플릿 이름(예: **ConfigMgr AMT Web Server Certificate**)을 입력합니다.  

6.  **주체 이름** 탭에서 **이 Active Directory 정보로 만듦**을 클릭하고 **주체 이름 형식** 에 **일반 이름**을 선택한 후에 대체 주체 이름에서 **UPN(사용자 계정 이름)** 의 선택을 취소합니다.  

7.  **보안** 탭을 클릭하고 **Domain Admins** 및 **Enterprise Admins** 보안 그룹에서 **등록**권한을 제거합니다.  

8.  **추가** 를 클릭하고 AMT 프로비전을 위해 만든 보안 그룹의 이름을 입력합니다. 그런 다음 **확인**을 클릭합니다.  

9. 이 보안 그룹에 대해 다음과 같은 **허용** 권한을 선택합니다. **읽기** 및 **등록**  

10. **확인**을 클릭하여 **인증서 템플릿** 콘솔을 닫습니다.  

11. **인증 기관** 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

12. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr AMT Web Server Certificate**를 선택하고 **확인**을 클릭합니다.  

13. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

 이제 AMT 웹 서버 템플릿에서 웹 서버 인증서를 사용하여 AMT 기반 컴퓨터를 프로비전할 수 있습니다. 대역 외 관리 구성 요소 속성에서 이 인증서 템플릿을 선택합니다.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>802.1X AMT 기반 컴퓨터용 클라이언트 인증 인증서 만들기 및 발급  
 AMT 기반 컴퓨터가 802.1X 인증 유/무선 네트워크에 클라이언트 인증서를 사용하는 경우 다음 절차를 따르십시오.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>CA에서 클라이언트 인증 인증서 템플릿을 만들고 발급하려면  

1.  인증 서비스가 설치된 구성원 서버에서, 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 **인증서 템플릿** 콘솔을 로드합니다.  

2.  결과 창에서 **템플릿 표시 이름** 열의 **워크스테이션 인증**이 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition.**  

3.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에서 AMT 컴퓨터의 대역 외 관리에 사용할 클라이언트 인증서를 생성하기 위한 템플릿 이름(예: **ConfigMgr AMT 802.1X Client Authentication Certificate**)을 입력합니다.  

4.  **주체 이름** 탭을 클릭하고 **이 Active Directory 정보로 만듦** 을 클릭한 후에 **주체 이름 형식** 에 **일반 이름**을 선택합니다. 대체 주체 이름에서 **DNS 이름** 의 선택을 취소하고 **UPN(사용자 계정 이름)**을 선택합니다.  

5.  **보안** 탭을 클릭하고 **Domain Admins** 및 **Enterprise Admins** 보안 그룹에서 **등록**권한을 제거합니다.  

6.  **추가** 를 클릭하고 대역 외 관리 구성 요소 속성에서 AMT 기반 컴퓨터의 컴퓨터 계정을 포함하도록 지정할 보안 그룹의 이름을 입력합니다. 그런 다음 **확인**을 클릭합니다.  

7.  이 보안 그룹에 대해 다음과 같은 **허용** 권한을 선택합니다. **읽기** 및 **등록**  

8.  **확인**을 클릭하여 **인증서 템플릿** 관리 콘솔, **certtmpl – [인증서 템플릿]**을 닫습니다.  

9. **인증 기관** 관리 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

10. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr AMT 802.1X Client Authentication Certificate**를 선택하고 **확인**을 클릭합니다.  

11. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

 이제 클라이언트 인증 인증서 템플릿으로 802.1X 클라이언트 인증에 사용할 수 있는 AMT 기반 컴퓨터에 대한 인증서를 발급할 수 있습니다. 대역 외 관리 구성 요소 속성에서 이 인증서 템플릿을 선택합니다.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Mac 컴퓨터용 클라이언트 인증서 배포  

> [!NOTE]  
>  Mac 컴퓨터용 클라이언트 인증서는 System Center Configuration Manager SP1 이상에 적용됩니다.  

 이 인증서 배포는 단일 절차로 인증 기관에서 등록 인증서 템플릿을 만들고 발급합니다.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> 인증 기관에서 Mac 클라이언트 인증서 템플릿 만들기 및 발급  
 이 절차는 System Center Configuration Manager Mac 컴퓨터용 사용자 지정 인증서 템플릿을 만들고 인증 기관에 인증서 템플릿을 추가합니다.  

> [!NOTE]  
>  이 인증서는 Windows 클라이언트 컴퓨터 또는 배포 지점용으로 만든 인증서 템플릿과 다른 인증서 템플릿을 사용합니다.  
>   
>  이 인증서에 대한 새 인증서 템플릿을 만듦으로써 인증서 요청을 인증된 사용자로 제한할 수 있습니다.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>인증 기관에서 Mac 클라이언트 인증서 템플릿을 만들고 발급하려면  

1.  System Center Configuration Manager를 사용하여 Mac 컴퓨터에서 인증서를 등록할 관리자의 사용자 계정이 포함된 보안 그룹을 만듭니다.  

2.  인증 기관을 실행하는 구성원 서버에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭하여 인증서 템플릿 관리 콘솔을 로드합니다.  

3.  결과 창에서 **템플릿 표시 이름** 열의 **인증된 세션**이 표시된 항목을 마우스 오른쪽 단추로 클릭하고 **중복된 템플릿**을 클릭합니다.  

4.  **중복된 템플릿** 대화 상자에서 **Windows 2003 Server, Enterprise Edition** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition**은 선택하지 마십시오.  

5.  **새 템플릿의 속성** 대화 상자의 **일반** 탭에 Mac 클라이언트 인증서를 생성하기 위한 템플릿 이름(예: **ConfigMgr Mac Client Certificate**)을 입력합니다.  

6.  **주체 이름** 탭에서 **이 Active Directory 정보로 만듦** 이 선택되어 있는지 확인하고 **주체 이름 형식:** 으로 **일반 이름** 을 선택한 후에 **대체 주체 이름에 이 정보 포함** 에서 **UPN(사용자 계정 이름)**의 선택을 취소합니다.  

7.  **보안** 탭을 클릭하고 **Domain Admins** 및 **Enterprise Admins** 보안 그룹에서 **등록** 권한을 제거합니다.  

8.  **추가**를 클릭하고 1단계에서 만든 보안 그룹을 지정한 후에 **확인**을 클릭합니다.  

9. 이 그룹에 대한 **등록** 권한을 선택하고, **읽기** 권한을 해제하지 않습니다.  

10. **확인** 을 클릭하여 **인증서 템플릿 콘솔**을 닫습니다.  

11. 인증 기관 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **발급할 인증서 템플릿**을 클릭합니다.  

12. **인증서 템플릿 사용** 대화 상자에서 방금 만든 새 템플릿 **ConfigMgr Mac Client Certificate**를 선택하고 **확인**을 클릭합니다.  

13. 인증서를 더 만들고 발급할 필요가 없으면 **인증 기관**을 닫습니다.  

 이제 등록을 위한 클라이언트 설정을 구성할 때 Mac 클라이언트 인증서 템플릿을 선택할 수 있습니다.



<!--HONumber=Nov16_HO1-->

