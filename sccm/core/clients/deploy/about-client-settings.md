---
title: "클라이언트 설정 | Microsoft 문서"
description: "System Center Configuration Manager에서 관리 콘솔을 사용하여 클라이언트 설정을 선택합니다."
ms.custom: na
ms.date: 08/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a8233c361e1a78b14a02f328da445814624e38d8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager의 클라이언트 설정 정보

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager의 모든 클라이언트 설정은 **관리** 작업 영역에 있는 **클라이언트 설정** 노드의 Configuration Manager 콘솔에서 관리됩니다. Configuration Manager에는 기본 설정 집합이 포함되어 있습니다. 기본 클라이언트 설정을 변경하면 이러한 설정이 계층 구조의 모든 클라이언트에 적용됩니다. 또한 사용자 지정 클라이언트 설정을 구성할 수 있습니다. 사용자 지정 클라이언트 설정을 컬렉션에 할당하면 기본 클라이언트 설정이 재정의됩니다. 클라이언트 설정을 구성하는 방법에 대한 자세한 내용은 [System Center Configuration Manager에서 클라이언트 설정을 구성하는 방법](../../../core/clients/deploy/configure-client-settings.md)을 참조하세요.  

대부분의 클라이언트 설정은 별도의 설명이 필요 없습니다. 기타 설정은 여기서 설명합니다.  

## <a name="background-intelligent-transfer-service"></a>Background Intelligent Transfer Service  

-   **BITS 백그라운드 전송의 최대 네트워크 대역폭 제한**  

   이 옵션이 **True** 또는 **예**인 경우 클라이언트에서 BITS 대역폭 제한이 사용됩니다.  

-   **제한 기간 시작 시간**  

   BITS 제한 기간의 현지 시작 시간을 지정합니다.  

-   **제한 기간 끝 시간**  

   BITS 제한 기간의 현지 종료 시간을 지정합니다. **제한 기간 시작 시간**과 같을 경우 BITS 제한이 항상 사용됩니다.  

-   **제한 기간 내의 최대 전송 속도(Kbps)**  

   클라이언트가 해당 기간 동안 사용할 수 있는 최대 전송 속도를 지정합니다.  

-   **제한 기간 외에 BITS 다운로드 허용**  

   Configuration Manager 클라이언트가 지정된 기간 외에 별도의 BITS 설정을 사용하도록 허용하려면 이 옵션을 선택합니다.  

-   **제한 기간 외의 최대 전송 속도(Kbps)**  

   BITS 제한 기간 이외의 시간에 BITS 제한을 허용하도록 선택한 경우 해당 기간이 아닐 때 클라이언트가 사용할 최대 전송 속도를 지정합니다.  

## <a name="client-cache-settings"></a>클라이언트 캐시 설정

- **BranchCache 구성**

  버전 1606부터 [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache)를 사용하도록 클라이언트 컴퓨터를 설정하려면 이 설정을 사용합니다. 클라이언트에 대해 BranchCache 캐싱을 허용하려면 **BranchCache 사용**을 **예**로 설정합니다.

- **BranchCache 사용**

클라이언트 컴퓨터에서 BranchCache를 사용하도록 설정합니다.

- **최대 BranchCache 캐시 크기(디스크의 비율)**

- **클라이언트 캐시 크기 구성**

  Windows 컴퓨터의 클라이언트 캐시에서 응용 프로그램 및 프로그램 설치에 사용되는 임시 파일이 저장됩니다. **예**를 선택하고 다음을 지정합니다.
    - **최대 캐시 크기**(메가바이트) 
    - **최대 캐시 크기**(디스크의 비율)
클라이언트 캐시 크기는 MB 또는 디스크에 대한 백분율 최대값(**둘 중 더 작은 크기**)으로 확장될 수 있습니다. 이 옵션이 **아니요**인 경우 기본 크기는 5,120MB입니다.

- **콘텐츠를 공유하도록 정품 OS에서 Configuration Manager 클라이언트 사용**

Configuration Manager 클라이언트에 대한 피어 캐시를 사용하도록 설정합니다. 그런 다음 클라이언트가 피어 컴퓨터와 통신하는 데 사용하는 포트 정보를 지정합니다. Configuration Manager는 이 트래픽을 허용하도록 자동으로 Windows 방화벽 규칙을 구성합니다. 다른 방화벽을 사용하는 경우 이 트래픽을 허용하도록 수동으로 포트를 구성해야 합니다.




## <a name="client-policy"></a>클라이언트 정책  

-   **클라이언트 정책 폴링 간격(분)**  

   다음 Configuration Manager 클라이언트가 클라이언트 정책을 다운로드하는 빈도를 지정합니다.  

  -   Windows 컴퓨터(예: 데스크톱, 서버, 랩톱)  

  -   Configuration Manager에서 등록된 모바일 장치  

  -   Mac 컴퓨터  

  -   Linux 또는 UNIX를 실행하는 컴퓨터  

-   **클라이언트에서 사용자 정책 폴링 사용**  

   이 옵션을 **True** 또는 **예**로 구성한 상태에서 Configuration Manager가 [사용자를 검색](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)하면 컴퓨터의 클라이언트가 로그온한 사용자를 대상으로 하는 응용 프로그램과 프로그램을 받습니다.  

   응용 프로그램 카탈로그는 사이트 서버에서 사용자가 사용할 수 있는 소프트웨어 목록을 받기 때문에 응용 프로그램 카탈로그에서 응용 프로그램을 보고 요청하는 사용자에 대해서는 이 설정을 **True** 또는 **예**로 지정하지 않아도 됩니다. 그러나 이 설정이 **False** 또는 **아니요**인 경우 사용자가 응용 프로그램을 사용할 때 다음이 작동하지 않습니다.  

  -   사용자가 응용 프로그램 카탈로그에서 보는 응용 프로그램을 설치할 수 없습니다.  

  -   사용자에게 응용 프로그램 승인 요청에 대한 알림이 표시되지 않습니다. 대신 응용 프로그램 카탈로그를 새로 고치고 응용 프로그램 상태를 확인해야 합니다.  

  -   사용자가 응용 프로그램 카탈로그에 게시되는 응용 프로그램에 대한 수정 버전과 업데이트를 받지 않습니다. 그러나 응용 프로그램 카탈로그에서 응용 프로그램 정보에 대한 변경 내용을 볼 수 있습니다.  

  -   클라이언트가 응용 프로그램 카탈로그에서 응용 프로그램을 설치한 후에 응용 프로그램 배포를 제거할 경우 클라이언트는 최대 2일 동안 응용 프로그램이 설치되어 있는지를 계속 확인합니다.  

   또한 이 설정이 **False** 또는 **아니요**일 경우 사용자에게 배포한 필수 응용 프로그램 또는 사용자 정책에 포함된 기타 관리 작업을 사용자가 받지 않게 됩니다.  

   이 설정은 컴퓨터가 인트라넷 및 인터넷에 있는 경우 사용자에게 적용됩니다. 인터넷에도 사용자 정책을 사용하도록 설정하려는 경우 **True** 또는 **예**여야 합니다.  

-   **인터넷 클라이언트의 사용자 정책 요청 사용**  

   클라이언트와 사이트가 인터넷 기반 클라이언트 관리로 구성되어 있고 이 옵션을 **True** 또는 **예**로 설정했으며 다음 조건이 모두 해당되는 경우, 사용자 컴퓨터가 인터넷에 있을 때 사용자가 사용자 정책을 받게 됩니다.  

  -   **클라이언트에 대한 사용자 정책 폴링 사용** 클라이언트 설정이 **True**이거나 **클라이언트에 대한 사용자 정책 사용**이 **예**인 경우  

  -   인터넷 기반 관리 지점이 Windows 인증(Kerberos 또는 NTLM)을 사용하여 사용자를 성공적으로 인증함  

   이 옵션을 **거짓** 또는 **아니요**로 두거나 이러한 조건 중 하나를 만족하지 않을 경우 인터넷상의 컴퓨터가 컴퓨터 정책만 받게 됩니다. 이 시나리오에서 사용자는 여전히 인터넷 기반 응용 프로그램 카탈로그에서 응용 프로그램을 보고 요청하고 설치할 수 있습니다. 이 설정이 **False** 또는 **아니요**이지만 **클라이언트에 대한 사용자 정책 폴링 사용** 이 **True**이거나 **클라이언트에 대한 사용자 정책 사용**이 **예**인 경우 컴퓨터가 인트라넷에 연결될 때까지 사용자 정책을 받지 않게 됩니다.  

   인터넷상의 클라이언트 관리에 대한 자세한 내용은 [System Center Configuration Manager에서 끝점 간의 통신](../../../core/plan-design/hierarchy/communications-between-endpoints.md)의 [인터넷 또는 신뢰할 수 없는 포리스트에서의 클라이언트 통신에 대한 고려 사항](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)을 참조하세요.  

  > [!NOTE]  
  >  사용자의 응용 프로그램 승인 요청에는 사용자 정책이나 사용자 인증이 필요하지 않습니다.  

##  <a name="compliance-settings"></a>호환성 설정  

-   **호환성 평가의 일정**  

     사용자가 구성 기준을 배포할 때 사용자에게 표시되는 기본 일정을 만들려면 **일정**을 선택합니다. 이 값은 **구성 기준 배포** 대화 상자에서 각 기준에 대해 구성할 수 있습니다.  

-   **사용자 데이터 및 프로필 사용**  

     계층 구조의 Windows 8 컴퓨터에 [사용자 데이터 및 프로필](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) 구성 항목을 배포하려면 **예**를 선택합니다.  

## <a name="computer-agent"></a>컴퓨터 에이전트  

-   **기본 응용 프로그램 카탈로그 웹 사이트 지점**  

     Configuration Manager에서는 이 설정을 사용하여 소프트웨어 센터의 응용 프로그램 카탈로그에 사용자를 연결합니다. 응용 프로그램 카탈로그 웹 사이트 지점을 호스팅하는 서버를 NetBIOS 이름 또는 FQDN으로 지정하거나, 자동 검색을 지정하거나, 사용자 지정 배포의 URL을 지정합니다. 대부분의 경우 자동 검색이 다음과 같은 이점을 제공하므로 가장 좋은 방법입니다.  

    -   사이트에 응용 프로그램 카탈로그 웹 사이트 지점이 포함된 경우 사이트에서 응용 프로그램 카탈로그 웹 사이트 지점이 클라이언트에 자동으로 지정됩니다.  

    -   HTTPS용으로 구성된 인트라넷의 응용 프로그램 카탈로그 웹 사이트 지점이 HTTPS용으로 구성되지 않은 응용 프로그램 카탈로그 웹 사이트 지점보다 우선적으로 사용됩니다. 이렇게 하면 Rogue 서버로부터 보호됩니다.

    -   클라이언트가 인트라넷 기반 및 인터넷 기반 클라이언트 관리로 구성된 경우, 인터넷에 있으면 인터넷 기반의 응용 프로그램 카탈로그 웹 사이트 지점이 지정되고 인트라넷에 있으면 인트라넷 기반의 응용 프로그램 카탈로그 웹 사이트 지점이 지정됩니다.  

     자동 검색을 통해서는 클라이언트에 가장 가까운 응용 프로그램 카탈로그 웹 사이트 지점이 지정되는 것을 보장할 수 없습니다. 다음과 같은 이유로 **자동 검색** 을 사용하지 않을 수 있습니다.  

     -   클라이언트에 대한 가장 가까운 서버를 수동으로 구성하거나 느린 네트워크 연결을 사용하는 서버에 연결하지 않으려고 합니다.  

     -   각 서버에 연결되는 클라이언트를 제어하려고 합니다. 이 구성은 테스트, 성능 또는 비즈니스 사유로 사용할 수 있습니다.  

     -   최대 25시간을 기다리거나 다른 응용 프로그램 카탈로그 웹 사이트 지점을 사용하여 클라이언트에 대한 네트워크 변경이 구성되는 것을 기다리길 원하지 않습니다.  

     자동 검색을 사용하는 대신 응용 프로그램 카탈로그 웹 사이트 지점을 지정하는 경우 인트라넷 FQDN 대신 NetBIOS 이름을 지정합니다. 이렇게 하면 사용자가 인트라넷에서 응용 프로그램 카탈로그에 연결할 때 자격 증명을 입력해야 하는 가능성을 줄어듭니다. NetBIOS 이름을 사용하려면 다음 조건에 해당해야 합니다.  

     -   응용 프로그램 카탈로그 웹 사이트 지점 속성에 NetBIOS 이름이 지정되어 있어야 합니다.  

     -   WINS를 사용하거나 모든 클라이언트가 응용 프로그램 카탈로그 웹 사이트 지점과 같은 도메인에 있어야 합니다.  

     -   응용 프로그램 카탈로그 웹 사이트 지점이 HTTP 클라이언트 연결을 사용하도록 구성되어 있거나, HTTPS 클라이언트 연결을 사용하도록 구성되어 있고 웹 서버 인증서에 NetBIOS 이름이 포함되어 있어야 합니다.  

     일반적으로 URL에 FQDN이 포함된 경우 사용자가 자격 증명을 입력해야 하지만 URL이 NetBIOS 이름인 경우 그렇지 않습니다. 사용자가 인터넷에서 연결하는 경우 항상 자격 증명을 입력해야 합니다. 이 연결은 인터넷 FQDN을 사용하기 때문입니다. 사용자가 인터넷에 있을 때 자격 증명을 입력해야 하는 경우 Kerberos를 통해 사용자를 인증할 수 있도록 응용 프로그램 카탈로그 웹 사이트 지점을 실행하는 서버에서 사용자 계정의 도메인 컨트롤러에 연결할 수 있어야 합니다.  

    > [!NOTE]  
    >  자동 검색 작동 방식:  
    >   
    >  클라이언트가 관리 지점에 서비스 위치를 요청합니다. 응용 프로그램 카탈로그 웹 사이트 지점이 클라이언트와 같은 사이트에 있는 경우 이 서버가 클라이언트에서 사용할 응용 프로그램 서버로 주어집니다. 사이트에 사용 가능한 응용 프로그램 카탈로그 웹 사이트 지점이 둘 이상 있는 경우 HTTPS 사용 서버가 HTTPS를 사용하지 않는 서버보다 우선됩니다. 이 필터링 후에 모든 클라이언트에 응용 프로그램 카탈로그로 사용할 서버 중 하나가 지정됩니다. Configuration Manager에서는 여러 서버 간에 부하를 분산하지 않습니다. 클라이언트 사이트에 응용 프로그램 카탈로그 웹 사이트 지점이 포함되지 않은 경우 관리 지점이 해당 계층 구조에서 응용 프로그램 카탈로그 웹 사이트 지점을 임의로 반환합니다.  
    >   
    >  클라이언트가 인트라넷에 있는 경우 선택한 응용 프로그램 카탈로그 웹 사이트 지점이 응용 프로그램 카탈로그 URL에 NetBIOS 이름을 사용하여 구성되어 있으면 클라이언트에 인트라넷 FQDN 대신 이 NetBIOS 이름이 지정됩니다. 클라이언트가 인터넷에 있는 것으로 검색되면 클라이언트에 인터넷 FQDN만 지정됩니다.  
    >   
    >  클라이언트는 25시간마다 또는 네트워크 변경을 감지할 때마다 이 서비스 위치를 요청합니다. 예를 들어 클라이언트가 인트라넷에서 인터넷으로 이동되고 클라이언트가 인터넷 기반 관리 지점을 찾을 수 있는 경우 인터넷 기반 관리 지점에서 클라이언트에 인터넷 기반 응용 프로그램 카탈로그 웹 사이트 지점 서버를 지정합니다.  

-   **기본 응용 프로그램 카탈로그 웹 사이트를 Internet Explorer의 신뢰할 수 있는 사이트 영역에 추가**  

     이 옵션이 **True** 또는 **예**인 경우 현재 기본 응용 프로그램 카탈로그 웹 사이트 URL이 클라이언트에서 Internet Explorer의 신뢰할 수 있는 사이트 영역에 자동으로 추가됩니다.  

     이 설정은 Internet Explorer의 보호 모드 설정이 사용되지 않도록 보장합니다. 보호 모드가 사용될 경우 Configuration Manager 클라이언트가 응용 프로그램 카탈로그에서 응용 프로그램을 설치하지 못할 수 있습니다. 또한 신뢰할 수 있는 사이트 영역은 기본적으로 Windows 인증을 요구하는 응용 프로그램 카탈로그에 대한 사용자 로그온을 지원합니다.  

     이 옵션을 **False**로 둘 경우 클라이언트가 사용하는 응용 프로그램 카탈로그 URL의 다른 영역에 대해 이러한 Internet Explorer 설정이 구성되지 않으면 Configuration Manager 클라이언트가 응용 프로그램 카탈로그에서 응용 프로그램을 설치하지 못할 수 있습니다.  

    > [!NOTE]  
    >  Configuration Manager는 신뢰할 수 있는 사이트 영역에 기본 응용 프로그램 카탈로그를 추가할 때마다 Configuration Manager는 새 항목을 추가하기 전에 Configuration Manager가 추가한 이전 기본 응용 프로그램 카탈로그 URL을 제거합니다.  
    >   
    >  보안 영역 중 하나에 URL이 이미 지정된 경우 Configuration Manager에서 URL을 추가할 수 없습니다. 이 시나리오에서는 다른 영역에서 URL을 제거하거나 필요한 Internet Explorer 설정을 수동으로 구성해야 합니다.  

-   **Silverlight 응용 프로그램의 높은 권한 모드 실행을 허용합니다.**  

     사용자가 Configuration Manager 클라이언트를 실행하고 응용 프로그램 카탈로그를 사용하는 경우 이 설정을 **예**로 지정해야 합니다.  

     이 설정을 변경하면 사용자가 다음에 브라우저를 로드하거나 현재 열려 있는 브라우저 창을 새로 고칠 때 변경 내용이 적용됩니다.  

     이 설정에 대한 자세한 내용은 [System Center Configuration Manager에서 응용 프로그램 관리에 대한 보안 및 개인 정보](../../../apps/plan-design/security-and-privacy-for-application-management.md)의 [Microsoft Silverlight 5 인증서 및 응용 프로그램 카탈로그에 필요한 높은 권한 모드](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5)를 참조하세요.  

-   **소프트웨어 센터에 표시된 조직 이름**  

     소프트웨어 센터에서 사용자에게 표시되는 이름을 입력합니다. 사용자는 이러한 브랜드 정보를 통해 응용 프로그램을 신뢰할 수 있는 원본으로 확인할 수 있습니다.  

-   **새 소프트웨어 센터 사용**  

     사용되는 경우 이러한 클라이언트 설정에서 대상으로 지정된 모든 클라이언트 컴퓨터가 새로운 소프트웨어 센터를 사용합니다. 소프트웨어 센터는 이전에 Silverlight 종속 응용 프로그램 카탈로그에서만 액세스할 수 있었던 앱(사용자가 사용할 수 있는 앱)을 보여 줍니다.  

     사용자가 사용할 수 있는 앱이 소프트웨어 센터에 표시되려면 응용 프로그램 카탈로그 웹 사이트 지점 및 응용 프로그램 카탈로그 웹 서비스 지점 사이트 시스템 역할이 여전히 필요합니다.  

     자세한 내용은 [System Center Configuration Manager에서 응용 프로그램 관리 계획 및 구성](../../../apps/plan-design/plan-for-and-configure-application-management.md)을 참조하세요.  

-   **설치 권한**  

    > [!WARNING]  
    >  이 설정은 응용 프로그램 카탈로그와 소프트웨어 센터에 적용됩니다. 사용자가 회사 포털을 사용할 때는 이 설정이 적용되지 않습니다.  

     사용자가 소프트웨어, 소프트웨어 업데이트 및 작업 순서의 설치를 시작하는 방식을 구성합니다.  

    -   **모든 사용자**: 게스트 이외의 권한으로 클라이언트 컴퓨터에 로그온한 사용자는 소프트웨어, 소프트웨어 업데이트 및 작업 순서의 설치를 시작할 수 있습니다.  

    -   **관리자만**: 클라이언트 컴퓨터에 로그온한 사용자는 로컬 관리자 그룹의 멤버이어야만 소프트웨어, 소프트웨어 업데이트 및 작업 순서의 설치를 시작할 수 있습니다.  

    -   **관리자 및 기본 사용자만**: 클라이언트 컴퓨터에 로그온한 사용자는 로컬 관리자 그룹의 멤버 또는 컴퓨터의 기본 사용자여야만 소프트웨어, 소프트웨어 업데이트 및 작업 순서의 설치를 시작할 수 있습니다.  

    -   **사용자 없음**: 클라이언트 컴퓨터에 로그온한 모든 사용자는 소프트웨어, 소프트웨어 업데이트 및 작업 순서의 설치를 시작할 수 없습니다. 컴퓨터에 필요한 배포는 항상 최종 기한에 설치됩니다. 사용자는 응용 프로그램 카탈로그 또는 소프트웨어 센터에서 소프트웨어 설치를 시작할 수 없습니다.  

-   **다시 시작 시 BitLocker PIN 항목 일시 중단**  

     컴퓨터에 BitLocker PIN 항목이 구성된 경우 이 옵션을 사용하면 소프트웨어 설치 후 컴퓨터가 다시 시작할 때 PIN을 입력해야 하는 요구 사항을 무시할 수 있습니다.  

    -   **항상**: Configuration Manager는 다시 시작이 필요한 소프트웨어를 설치하고 컴퓨터를 다시 시작한 후 BitLocker 요구 사항을 일시적으로 중단합니다. 이 설정은 Configuration Manager에서 시작한 컴퓨터 다시 시작에만 적용되며 사용자가 컴퓨터를 다시 시작할 때 BitLocker PIN을 입력해야 하는 요구 사항은 일시 중단하지 않습니다. BitLocker PIN 항목 요구 사항은 Windows 시작 후 다시 시작됩니다.

    -   **안 함**: Configuration Manager는 다시 시작이 필요한 소프트웨어를 설치한 후 다음 컴퓨터 시작 시 BitLocker 요구 사항을 일시 중단하지 않습니다. 이 시나리오에서 소프트웨어 설치는 사용자가 PIN을 입력하여 표준 시작 프로세스를 완료하고 Windows를 로드할 때까지 완료되지 않습니다.

-   **추가 소프트웨어로 응용 프로그램 및 소프트웨어 업데이트 배포 관리**  

     이 옵션은 다음 조건 중 하나를 충족하는 경우에만 사용하세요.  

    -   이 설정이 필요한 공급업체 솔루션을 사용합니다.  

    -   Configuration Manager SDK(소프트웨어 개발 키트)를 사용하여 클라이언트 에이전트 알림과 응용 프로그램 및 소프트웨어 업데이트의 설치를 관리합니다.  

    > [!WARNING]  
    >  두 조건 중 어느 조건도 충족하지 않을 때 이 옵션을 선택하면 클라이언트에 소프트웨어 업데이트 및 필수 응용 프로그램은 설치되지 않습니다. 이 설정을 사용하더라도 사용자는 응용 프로그램 카탈로그에서 응용 프로그램을 설치할 수 있으며 패키지, 프로그램 및 작업 순서가 클라이언트 컴퓨터에 설치될 수 있습니다.  

-   **PowerShell 실행 정책**  

     Configuration Manager 클라이언트에서 Windows PowerShell 스크립트를 실행할 수 있는 방식을 구성합니다. 이러한 스크립트는 구성 항목에서 호환성 설정을 검색하는 데 자주 사용됩니다. 배포 시 표준 스크립트로 보낼 수도 있습니다.  

    -   **바이패스**: Configuration Manager 클라이언트는 서명되지 않은 스크립트가 실행될 수 있도록 클라이언트 컴퓨터에서 Windows PowerShell 구성을 바이패스합니다.  

    -   **제한**: Configuration Manager 클라이언트는 클라이언트 컴퓨터에서 현재 Windows PowerShell 구성을 사용합니다. 이 구성에 따라 서명되지 않은 스크립트 실행 가능 여부가 결정됩니다.  

    -   **서명된 전체**: Configuration Manager 클라이언트는 신뢰할 수 있는 게시자가 서명한 스크립트만 실행합니다. 이 제한은 클라이언트 컴퓨터의 현재 Windows PowerShell 구성과 별개로 적용됩니다.  

     이 옵션을 사용하려면 Windows PowerShell 버전 2.0 이상이 필요합니다. 기본값은 **서명된 전체**입니다.  

    > [!TIP]  
    >  서명되지 않은 스크립트가 이 클라이언트 설정으로 인해 실행되지 못한 경우 Configuration Manager는 다음 방법으로 이 오류를 보고합니다.  
    >   
    > -   Configuration Manager 콘솔의 **모니터링** 작업 영역에서 배포 상태 오류로 오류 ID **0X87D00327** 및 설명 **스크립트가 서명되지 않음**을 보고합니다.  
    > -   보고서에서 오류 코드 및 설명으로 **0X87D00327** 및 **스크립트가 서명되지 않음** 또는 **0X87D00320** 및 **스크립트 호스트가 아직 설치되지 않았습니다.**와 함께 오류 유형 **검색 오류**를 작성합니다. 예를 들면 **자산의 구성 기준에서 구성 항목의 자세한 오류 정보**입니다.  
    > -   **Script is not signed (Error: 87D00327; Source: CCM)** 파일에 **DcmWmiProvider.log** 메시지를 기록합니다.  

-   **새 배포에 대한 알림 표시**  

     1주 이내에 사용할 수 있던 배포에 대한 알림을 표시하려면 **예**를 선택합니다.  이 메시지는 클라이언트 에이전트가 시작될 때마다 표시됩니다.

-   **최종 기한 임의 설정 사용 안 함**  

     이 설정은 클라이언트에서 최종 기한에 도달할 때 필수 소프트웨어 업데이트를 설치하는 데 최대 2시간의 활성화 지연 시간을 사용할지 여부를 결정합니다. 기본적으로 활성화 지연 시간은 사용하지 않도록 설정되어 있습니다.  

     VDI(가상 데스크톱 인프라) 시나리오의 경우 이러한 지연 시간으로 Configuration Manager 클라이언트를 실행하는 여러 개의 가상 컴퓨터가 포함된 컴퓨터에 대해 CPU 처리 및 데이터 전송을 분산할 수 있습니다. VDI를 사용하지 않더라도 여러 클라이언트에서 동일한 업데이트를 동시에 설치할 경우, 사이트 서버의 CPU 사용량이 크게 늘어날 수 있습니다. 또한 배포 지점의 속도가 느려지며 사용 가능한 네트워크 대역폭이 대폭 감소할 수 있습니다.  

     구성된 최종 기한에 도달한 경우 필수 소프트웨어 업데이트를 지연 시간 없이 설치해야 하는 경우 이 설정에 대해 **예**를 선택하세요.  

-   **배포 최종 기한 이후 적용 유예 기간(시간)**

     간혹 구성한 기한 이후에도 필수 응용 프로그램 배포 또는 소프트웨어 업데이트를 설치할 수 있는 시간을 사용자에게 더 제공하려는 경우가 있습니다. 컴퓨터가 오랫동안 꺼져 있었거나 많은 응용 프로그램 또는 업데이트 배포를 설치해야 할 때 이런 경우가 필요할 수 있습니다. 예를 들어 사용자가 휴가에서 막 돌아온 경우 지연된 응용 프로그램 배포를 설치하는 데 너무 오래 기다려야 할 수 있습니다. 이 문제를 해결하기 위해 컬렉션에 Configuration Manager 클라이언트 설정을 배포하여 적용 유예 기간을 정의할 수 있습니다.

     유예 기간은 1~120시간 사이로 설정할 수 있습니다. 이 설정은 **이 배포의 적용을 사용자 기본 설정에 따라 연기** 배포 속성과 함께 사용됩니다. 자세한 내용은 [응용 프로그램 배포](/sccm/apps/deploy-use/deploy-applications)를 참조하세요.

##  <a name="computer-restart"></a>컴퓨터 다시 시작  
 이 컴퓨터 다시 시작 설정을 지정할 경우 다시 시작 임시 알림 간격의 값과 최종 카운트다운 간격의 값을 컴퓨터에 적용된 최단 유지 관리 기간보다 더 짧게 설정해야 합니다.  

 유지 관리 기간에 대한 자세한 내용은 [System Center Configuration Manager에서 유지 관리 기간을 사용하는 방법](../../../core/clients/manage/collections/use-maintenance-windows.md)을 참조하세요.  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **클라이언트 컴퓨터에서 Endpoint Protection 클라이언트 관리**  

     계층 구조의 컴퓨터에서 기존 Endpoint Protection 클라이언트를 관리하려면 **True** 또는 **예**를 선택합니다.  

     Endpoint Protection 클라이언트를 이미 설치했고 Configuration Manager를 사용하여 이를 관리하려는 경우 이 옵션을 선택합니다.  

     또한 기존 맬웨어 방지 솔루션을 제거하는 스크립트를 만들고, Endpoint Protection 클라이언트를 설치하고, Configuration Manager 응용 프로그램 또는 패키지 및 프로그램을 사용하여 이 스크립트를 배포하려면 이 옵션을 선택하세요.  

-   **클라이언트 컴퓨터에 Endpoint Protection 클라이언트 설치**  

     Endpoint Protection 클라이언트를 아직 설치하지 않은 클라이언트 컴퓨터에 설치하고 사용하도록 설정하려면 **True** 또는 **예**를 선택합니다.  

    > [!NOTE]  
    >  Endpoint Protection 클라이언트가 이미 설치된 경우 **False** 또는 **아니요** 를 선택해도 Endpoint Protection 클라이언트는 제거되지 않습니다. Endpoint Protection 클라이언트를 제거하려면 **클라이언트 컴퓨터에서 Endpoint Protection 클라이언트 관리** 클라이언트 설정을 **False** 또는 **아니요**로 설정합니다. 그런 다음 패키지 및 프로그램을 배포하여 Endpoint Protection 클라이언트를 제거합니다.  

-   **쓰기 필터를 지원하는 Windows Embedded 장치에 Endpoint Protection 클라이언트 설치 커밋(다시 시작 필요)**  

     Windows Embedded 장치에서 쓰기 필터를 사용하지 않도록 설정하려면 **예**를 선택하고 장치를 다시 시작합니다. 이렇게 하면 장치에서 설치가 커밋됩니다.  

     **아니요** 를 지정하면 클라이언트는 임시 오버레이에 설치되고 이 오버레이는 장치가 다시 시작될 때 삭제됩니다. 이 시나리오에서 Endpoint Protection 클라이언트는 다른 설치에서 장치 변경 내용을 커밋하기 전까지 커밋되지 않습니다. 이것이 기본 설정입니다.  

-   **Endpoint Protection 클라이언트 설치 후 필요한 컴퓨터 다시 시작 보류**  

     Endpoint Protection 클라이언트 설치 후 필요에 따라 컴퓨터 다시 시작을 보류하려면 **True** 또는 **예**를 선택합니다.  

    > [!IMPORTANT]  
    >  Endpoint Protection 클라이언트 설치를 위해 컴퓨터 다시 시작이 필요하고 이 설정이 **False**인 경우 구성된 유지 관리 기간에 관계없이 다시 시작됩니다.  

-   **Endpoint Protection 설치를 완료하는 데 필요한 다시 시작을 연기할 수 있도록 허용된 기간(시)**  

     Endpoint Protection 클라이언트 설치 후 필요한 컴퓨터 다시 시작을 연기할 수 있는 시간을 지정합니다. 이 옵션은 **Endpoint Protection 클라이언트 설치 후 필요한 컴퓨터 다시 시작 보류** 옵션이 **False**인 경우에만 구성할 수 있습니다.  

-   **클라이언트 컴퓨터의 초기 정의 업데이트에 대체 원본(예: Windows 업데이트, Microsoft Windows Server Update Services 또는 UNC 공유) 사용 안 함**  

     Configuration Manager에서 클라이언트 컴퓨터에 초기 정의 업데이트만 설치하도록 하려면 **True** 또는 **예**를 선택합니다. 이 설정은 정의 업데이트 초기 설치 중에 불필요한 네트워크 연결을 방지하고 네트워크 대역폭의 사용량을 줄이는 데 유용합니다.  

##  <a name="hardware-inventory"></a>하드웨어 인벤토리  

-   **최대 사용자 지정 MIF 파일 크기(KB)**  

     하드웨어 인벤토리 주기 중 클라이언트에서 수집할 각 사용자 지정 MIF(관리 정보 형식) 파일에 허용되는 최대 크기(KB)를 지정합니다. 이 크기를 초과하는 MIF 파일은 Configuration Manager 하드웨어 인벤토리에서 처리되지 않습니다. 1에서 5,000KB의 크기를 지정할 수 있습니다. 기본적으로 이 값은 250KB로 설정되어 있습니다. 이 설정은 정규 하드웨어 인벤토리 데이터 파일의 크기에 영향을 주지 않습니다.  

    > [!NOTE]  
    >  이 설정은 기본 클라이언트 설정에서만 사용할 수 있습니다.  

-   **하드웨어 인벤토리 클래스**  

     Configuration Manager를 사용할 때 클라이언트에서 수집하는 하드웨어 정보를 sms_def.mof 파일을 수동으로 편집하지 않고 확장할 수 있습니다. Configuration Manager 하드웨어 인벤토리를 확장하려는 경우 **클래스 설정**을 선택합니다. 자세한 내용은 [System Center Configuration Manager에서 하드웨어 인벤토리를 구성하는 방법](../../../core/clients/manage/inventory/configure-hardware-inventory.md)을 참조하세요.  

-   **MIF 파일 수집**  

     하드웨어 인벤토리가 수행되는 동안 Configuration Manager 클라이언트에서 MIF 파일을 수집할지 여부를 지정하려면 이 설정을 사용합니다.  

     MIF 파일이 하드웨어 인벤토리를 통해 수집되려면 클라이언트 컴퓨터의 올바른 위치에 있어야 합니다. 기본적으로 이 파일은 다음과 같이 배치됩니다.  

    -   IDMIF 파일은 Windows\System32\CCM\Inventory\Idmif 폴더에 있어야 합니다.  

    -   NOIDMIF 파일은 Windows\System32\CCM\Inventory\Noidmif 폴더에 있어야 합니다.  

    > [!NOTE]  
    >  이 설정은 기본 클라이언트 설정에서만 사용할 수 있습니다.

-   **최대 임의 지연**

    작업이 모든 클라이언트에서 동시에 수행되지 않도록 최대 4시간마다 하드웨어 정보가 무작위로 수집됩니다. 작업이 수행되는 기간을 제한하기 위해 최대 지연을 설정할 수 있습니다.      

##  <a name="metered-internet-connections"></a>데이터 통신 연결  
 Windows 8 클라이언트 컴퓨터에서 데이터 통신 연결을 사용할 경우 해당 컴퓨터가 Configuration Manager 사이트와 통신하는 방식을 관리할 수 있습니다. 때로 인터넷 공급자는 사용자가 요금제 인터넷 연결을 사용할 경우 보내고 받는 데이터 양을 기준으로 요금을 청구하기도 합니다.  

> [!NOTE]  
>  다음 경우에는 구성된 클라이언트 설정이 Windows 8 클라이언트 컴퓨터에 적용되지 않습니다.  
>   
> -   컴퓨터가 로밍 데이터 연결을 사용합니다. Configuration Manager 클라이언트는 데이터를 Configuration Manager 사이트에 전송해야 하는 작업을 수행하지 않습니다.  
> -   Windows 네트워크 연결 속성이 데이터 통신이 아닌 연결로 구성됩니다. Configuration Manager 클라이언트가 현재 연결이 데이터 통신 연결이 아닌 것처럼 작동하며 이에 따라 Configuration Manager 사이트에 데이터를 전송합니다.  

-   **데이터 통신 연결에서의 클라이언트 통신**  

     드롭다운 목록에서 Windows 8 클라이언트 컴퓨터에 대해 다음 중 하나를 선택합니다.  

    -   **허용**: 클라이언트 장치에서 로밍 데이터 연결을 사용하지 않는 한 모든 클라이언트 통신이 데이터 통신 연결에 대해 허용됩니다.  

    -   **제한**: 데이터 통신 연결에 대해 다음 클라이언트 통신만 허용됩니다.  

        -   클라이언트 정책 검색  

        -   사이트에 보낼 클라이언트 상태 메시지  

        -   응용 프로그램 카탈로그를 사용한 소프트웨어 설치 요청  

        -   필수 배포(설치 최종 기한에 도달하는 경우)  

        > [!IMPORTANT]  
        >  사용자가 소프트웨어 센터 또는 응용 프로그램 카탈로그에서 소프트웨어 설치를 시작하는 경우 이 작업은 요금제 인터넷 연결 설정에 관계없이 항상 허용됩니다.  

         데이터 통신 연결이 데이터 전송 제한에 도달한 경우 클라이언트는 더 이상 Configuration Manager 사이트와 통신을 시도하지 않습니다.  

    -   **차단**: Configuration Manager 클라이언트는 데이터 통신 연결을 사용할 경우 Configuration Manager 사이트와 통신을 시도하지 않습니다. 이 설정은 기본값입니다.  

##  <a name="power-management"></a>전원 관리  

-   **사용자가 전원 관리에서 장치를 제외할 수 있도록 허용**  

     소프트웨어 센터 사용자가 자신의 컴퓨터를 구성된 전원 관리 설정에서 제외할 수 있도록 허용하려면 드롭다운 목록에서 **True** 또는 **예** 를 선택합니다.  

-   **절전 모드 해제 프록시 사용**  

     유니캐스트 패킷용으로 구성할 때 사이트의 Wake On LAN 설정을 보완하려면 **예** 를 지정합니다.  

     절전 모드 해제 프록시에 대한 자세한 내용은 [System Center Configuration Manager에서 클라이언트의 절전 모드 해제 계획](../../../core/clients/deploy/plan/plan-wake-up-clients.md)을 참조하세요.  

    > [!WARNING]  
    >  프로덕션 네트워크에서 절전 모드 해제 프록시를 사용하려는 경우 먼저 절전 모드 해제 프록시의 작동 방식을 이해하고 테스트 환경에서 평가해야 합니다.  

-   **절전 모드 해제 프록시 포트 번호(UDP)**  

     Manager 컴퓨터가 절전 모드 컴퓨터에 절전 모드 해제 패킷을 전송하는 데 사용하는 포트 번호를 기본값 그대로 유지하거나 원하는 값으로 변경합니다.  

     **절전 모드 해제 프록시에 대한 Windows 방화벽 예외입니다.** 옵션을 사용하는 경우 여기서 지정한 포트 번호가 Windows 방화벽을 실행하는 클라이언트에 자동으로 구성됩니다. 클라이언트에서 다른 방화벽이 실행되는 경우 이 설정에 지정한 UDP 포트 번호를 허용하도록 수동으로 구성해야 합니다.  

-   **Wake On LAN 포트 번호(UDP)**  

     사이트 **속성**의 **포트** 탭에서 Wake On LAN(UDP) 포트 번호를 변경한 경우를 제외하고 기본값 9를 유지합니다.  

    > [!IMPORTANT]  
    >  이 번호는 사이트 **속성**에서 지정한 번호와 일치해야 합니다. 이 번호는 한곳에서 변경 시 다른 곳에서 자동으로 업데이트되지 않습니다.  

##  <a name="remote-tools"></a>원격 도구  

-   **클라이언트에서 원격 제어 사용** 및 **방화벽 예외 프로필**  

     이러한 클라이언트 설정을 받는 모든 클라이언트 컴퓨터에 대해 Configuration Manager 원격 제어를 사용할지 여부를 선택합니다. **구성**을 선택하여 원격 제어를 사용하도록 설정합니다. 필요에 따라 클라이언트 컴퓨터에 대한 원격 제어를 허용하도록 방화벽 설정을 구성합니다.  

     기본적으로 원격 제어는 사용되지 않습니다.  

    > [!IMPORTANT]  
    >  방화벽 설정이 구성되지 않으면 원격 제어가 제대로 작동하지 않을 수 있습니다.  

-   **소프트웨어 센터에서 사용자가 정책 또는 알림 설정 변경 가능**  

     사용자가 소프트웨어 센터 내에서 원격 제어 옵션을 변경할 수 있는지 여부를 선택합니다.  

-   **무인 컴퓨터의 원격 제어 허용**  

     관리자가 원격 제어를 사용하여, 로그오프되었거나 잠겨 있는 클라이언트 컴퓨터에 액세스할 수 있는지 여부를 선택합니다. 이 설정이 사용되지 않으면 로그온되어 있거나 잠겨 있지 않은 컴퓨터만 원격으로 제어됩니다.  

-   **원격 제어 권한을 묻는 메시지를 사용자에게 표시**  

     클라이언트 컴퓨터에서 원격 제어 세션을 허용하기 전에 사용자의 권한을 묻는 메시지를 표시할지 여부를 선택합니다.  

-   **로컬 관리자 그룹에 원격 제어 권한 부여**  

     원격 제어를 시작하는 서버의 로컬 관리자가 클라이언트 컴퓨터에 대한 원격 제어 세션을 설정할 수 있는지 여부를 선택합니다.  

-   **허용된 액세스 수준**  

     허용되는 원격 제어 액세스 수준을 지정합니다. 다음 중 하나를 선택할 수 있습니다.  

    -   모든 권한  

    -   보기 전용  

    -   없음  

-   **허용된 뷰어**  

     **뷰어 설정**을 선택하여 **클라이언트 설정 구성** 대화 상자를 열고 클라이언트 컴퓨터에 대한 원격 제어 세션을 설정할 수 있는 Windows 사용자의 이름을 지정합니다.  

-   **작업 표시줄에 세션 알림 아이콘 표시**  

     클라이언트 컴퓨터의 작업 표시줄에 아이콘을 표시하여 원격 제어 세션이 활성화되어 있음을 나타내려면 이 옵션을 선택합니다.  

-   **세션 연결 모음 표시**  

     클라이언트 컴퓨터에 눈에 잘 띄는 세션 연결 모음을 표시하여 원격 제어 세션이 활성화되어 있음을 나타내려면 이 옵션을 선택합니다.  

-   **클라이언트에서 소리 재생**  

     소리를 사용해서 클라이언트 컴퓨터에 원격 제어 세션이 활성화되어 있음을 나타내려면 이 옵션을 선택합니다. 세션이 연결되거나 연결 해제될 때 소리를 재생하거나 세션 중에 반복적으로 소리를 재생할 수 있습니다.  

-   **원치 않는 원격 지원 설정 관리**  

     Configuration Manager에서 원치 않는 원격 지원 세션을 관리할 수 있도록 하려면 이 옵션을 선택합니다.  

     원치 않는 원격 지원 세션은 클라이언트 컴퓨터의 사용자가 세션을 시작하도록 지원을 요청하지 않은 세션입니다.  

-   **요청된 원격 지원 설정 관리**  

     Configuration Manager에서 요청된 원격 지원 세션을 관리할 수 있도록 하려면 이 옵션을 선택합니다.  

     요청된 원격 지원 세션은 클라이언트 컴퓨터의 사용자가 관리자에게 원격 지원 요청을 보낸 세션입니다.  

-   **원격 지원의 액세스 수준**  

     Configuration Manager 콘솔에서 시작되는 원격 지원 세션에 할당할 액세스 수준을 선택합니다.  

    > [!NOTE]  
    >  클라이언트 컴퓨터의 사용자가 항상 원격 지원 세션에 대한 권한을 부여해야 합니다.  

-   **원격 데스크톱 설정 관리**  

     Configuration Manager에서 컴퓨터에 대한 원격 데스크톱 세션을 관리할 수 있도록 하려면 이 옵션을 선택합니다.  

-   **허용된 뷰어가 원격 데스크톱 연결을 사용하여 연결하도록 허용**  

     허용된 뷰어 목록에 지정된 사용자가 클라이언트 컴퓨터의 원격 데스크톱 로컬 사용자 그룹에 추가될 수 있도록 하려면 이 옵션을 선택합니다.  

-   **Windows Vista 운영 체제 이후 버전을 실행하는 컴퓨터에 네트워크 수준 인증 필요**  

     Windows Vista 이후 버전을 실행하는 클라이언트 컴퓨터에 대한 원격 데스크톱 연결을 설정할 때 네트워크 수준 인증을 사용하려면 보다 안전한 이 옵션을 선택합니다. 네트워크 수준 인증을 사용하면 사용자 인증을 완료한 후에 원격 데스크톱 연결을 설정하기 때문에 초기에 원격 컴퓨터 리소스가 더 적게 필요합니다. 이 방법은 컴퓨터를 악의적인 사용자 또는 소프트웨어로부터 보호하고 서비스 거부 공격의 위험을 줄이기 때문에 더욱 안전합니다.  

## <a name="software-deployment"></a>소프트웨어 배포  

-   **배포의 재평가 일정**  

     Configuration Manager가 모든 배포에 대한 요구 사항 규칙을 다시 평가하는 일정을 구성합니다. 기본값은 7일마다입니다.  

    > [!IMPORTANT]  
    >  이 값을 기본값보다 낮은 값으로 변경하지 않는 것이 좋습니다. 변경하면 네트워크 및 클라이언트 컴퓨터의 성능에 부정적인 영향을 미칠 수 있습니다.  

     제어판의 **Configuration Manager** **작업** 탭에서 **응용 프로그램 배포 평가 주기** 작업을 선택하여 Configuration Manager 클라이언트 컴퓨터에서 이 작업을 시작할 수도 있습니다.  

##  <a name="software-inventory"></a>소프트웨어 인벤토리  

-   **인벤토리 보고 세부 정보**  

     인벤토리 파일 정보 수준을 지정합니다. 파일에 대한 세부 정보, 파일과 연결된 제품에 대한 세부 정보 또는 파일에 대한 모든 정보를 인벤토리할 수 있습니다.  

-   **다음 파일 형식 인벤토리**  

     인벤토리할 파일 형식을 지정하려면 **유형 설정**을 선택하고 **클라이언트 설정 구성** 대화 상자에서 다음을 구성합니다.  

    > [!NOTE]  
    >  컴퓨터에 여러 사용자 지정 클라이언트 설정이 적용되는 경우, 각 설정을 통해 반환되는 인벤토리가 병합됩니다.  

    -   **새로 만들기** 아이콘을 선택하여 인벤토리에 새 파일 형식을 추가합니다. 그런 다음 **인벤토리 파일 속성** 대화 상자에서 다음 정보를 지정합니다.  

        -   **이름**: 인벤토리할 파일의 이름을 지정합니다. **\** 문자를 사용하여 모든 텍스트 문자열을 나타내고 **?** 문자를 사용하여 단일 문자를 나타낼 수 있습니다. 예를 들어 확장명 .doc을 갖는 모든 파일을 인벤토리하려는 경우 파일 이름을 **\*.doc**로 지정합니다.  

        -   **위치**: **설정**을 선택하여 **경로 속성** 대화 상자를 엽니다. 모든 클라이언트 하드 디스크에서 지정된 파일을 검색하거나, 지정된 경로(예: **C:\Folder**) 또는 지정된 변수(예: *%windir%*)를 검색하도록 소프트웨어 인벤토리를 구성할 수 있습니다. 지정된 경로 아래의 모든 하위 폴더를 검색할 수도 있습니다.  

        -   **암호화 및 압축된 파일 제외**: 이 옵션을 선택하면 압축되거나 암호화된 모든 파일이 인벤토리되지 않습니다.  

        -   **Windows 폴더의 파일 제외**: 이 옵션을 선택하면 Windows 폴더와 그 하위 폴더에 있는 모든 파일이 인벤토리되지 않습니다.  

    -   **확인**을 선택하여 **인벤토리 파일 속성** 대화 상자를 닫습니다.  

    -   인벤토리할 모든 파일을 추가한 후에 **확인**을 선택하여 **클라이언트 설정 구성** 대화 상자를 닫습니다.  

-   **파일 수집**  

     클라이언트 컴퓨터에서 파일을 수집하려면 **파일 설정**을 선택하고 다음을 구성합니다.  

    > [!NOTE]  
    >  컴퓨터에 여러 사용자 지정 클라이언트 설정이 적용되는 경우, 각 설정을 통해 반환되는 인벤토리가 병합됩니다.  

    -   **클라이언트 설정 구성** 대화 상자에서 **새로 만들기** 아이콘을 선택하여 수집할 파일을 추가합니다.  

    -   **수집된 파일 속성** 대화 상자에서 다음 정보를 지정합니다.  

        -   **이름**: 수집할 파일의 이름을 지정합니다. **\** 문자를 사용하여 모든 텍스트 문자열을 나타내고 **?** 문자를 사용하여 단일 문자를 나타낼 수 있습니다.  

        -   **위치**: **설정**을 선택하여 **경로 속성** 대화 상자를 엽니다. 모든 클라이언트 하드 디스크에서 수집할 파일을 검색하거나, 지정된 경로(예: **C:\Folder**) 또는 지정된 변수(예: *%windir%*)를 검색하도록 소프트웨어 인벤토리를 구성할 수 있습니다. 지정된 경로 아래의 모든 하위 폴더를 검색할 수도 있습니다.  

        -   **암호화 및 압축된 파일 제외**: 이 옵션을 선택하면 압축되거나 암호화된 모든 파일이 수집되지 않습니다.  

        -   **총 파일 크기(KB)가 다음을 초과하면 파일 컬렉션 중지**: 이를 초과하면 **이름** 아래 지정된 파일이 더 이상 수집되지 않는 파일 크기(KB)를 지정합니다.  

          > [!NOTE]  
          >  사이트 서버에서는 가장 최근에 변경된 버전의 수집된 파일 5개를 수집하여 *&lt;Configuration Manager 설치 디렉터리\>*\Inboxes\Sinv.box\Filecol 디렉터리에 저장합니다. 마지막 소프트웨어 인벤토리가 수집된 이후로 파일이 변경되지 않은 경우 파일이 다시 수집되지 않습니다.  
          >   
          >  소프트웨어 인벤토리는 20MB보다 큰 파일을 수집하지 않습니다.  
          >   
          >  **클라이언트 설정 구성** 대화 상자의 **모든 수집된 파일의 최대 크기(KB)** 값에는 수집된 모든 파일의 최대 크기가 표시됩니다. 이 크기에 도달하면 파일 수집이 중지됩니다. 이미 수집된 모든 파일은 유지되고 사이트 서버에 전송됩니다.  

          > [!IMPORTANT]
          >  다수의 큰 파일을 수집하도록 소프트웨어 인벤토리를 구성할 경우 네트워크와 사이트 서버의 성능에 부정적인 영향을 미칠 수 있습니다.  

        수집된 파일을 확인하는 방법에 대한 자세한 내용은 [System Center Configuration Manager에서 소프트웨어 인벤토리를 보기 위해 리소스 탐색기를 사용하는 방법](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)을 참조하세요.  

    -   **확인**을 선택하여 **수집된 파일 속성** 대화 상자를 닫습니다.  

    -   수집할 모든 파일을 추가한 후에 **확인**을 선택하여 **클라이언트 설정 구성** 대화 상자를 닫습니다.  

-   **이름 설정**  

     소프트웨어 인벤토리 동안 제조업체 이름과 제품 이름이 사이트의 클라이언트에 설치된 파일에 있는 헤더 정보에서 검색됩니다. 이러한 이름은 파일 헤더 정보에서 표준화되지 않은 경우가 많으므로 리소스 탐색기에서 소프트웨어 인벤토리 정보를 보거나 쿼리를 실행하는 경우 동일한 제조업체나 제품 이름이 여러 버전으로 나타날 수도 있습니다. 이러한 표시 이름을 표준화하려면 **이름 설정**을 선택한 후 **클라이언트 설정 구성** 대화 상자에서 다음을 구성합니다.  

    -   **이름 형식**: 소프트웨어 인벤토리는 제조업체 및 제품 둘 다에 대한 정보를 수집합니다. 드롭다운 목록에서 **제조업체** 또는 **제품**의 표시 이름을 구성할지 여부를 선택합니다.  

    -   **표시 이름**: **인벤토리 이름** 목록에 있는 이름 대신 사용할 표시 이름을 지정합니다. **새로 만들기** 아이콘을 선택하여 새 표시 이름을 지정할 수 있습니다.  

    -   **인벤토리 이름**: **새로 만들기** 아이콘을 선택하여 새 인벤토리 이름을 추가합니다. 소프트웨어 인벤토리에서 이 이름은 **표시 이름** 목록에서 선택한 이름으로 바뀝니다. 바꿀 여러 이름을 추가할 수 있습니다.  

##  <a name="software-updates"></a>소프트웨어 업데이트  

-   **클라이언트에서 소프트웨어 업데이트 사용**  

     이 설정을 사용하여 Configuration Manager 클라이언트에서 소프트웨어 업데이트를 사용하도록 설정할 수 있습니다. 이 설정을 사용하지 않으면 Configuration Manager가 클라이언트에서 기존 배포 정책을 제거합니다. 이 설정을 다시 사용하도록 설정하는 경우 클라이언트는 현재 배포 정책을 다운로드합니다.  

    > [!IMPORTANT]  
    >  이 설정을 사용하지 않는 경우 소프트웨어 업데이트에 대한 장치 설정을 사용하는 NAP 및 호환성 설정 정책이 더 이상 작동하지 않게 됩니다.  

-   **소프트웨어 업데이트 검사 일정**  

     이 설정을 사용하여 클라이언트에서 소프트웨어 업데이트 호환성 평가 검사를 시작하는 빈도를 지정할 수 있습니다. 호환성 평가 검사는 클라이언트의 소프트웨어 업데이트에 대한 상태(예: 필수 또는 설치됨)를 확인합니다. 준수 평가에 대한 자세한 내용은 [소프트웨어 업데이트 준수 평가](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance)를 참조하세요.  

     기본적으로, 단순 일정이 사용되고 호환성 검사가 7일마다 시작됩니다. 사용자 지정 일정을 만들도록 선택하여 정확한 시작 날짜와 시간을 지정할 수 있으며, UTC를 사용할지, 아니면 현지 시간을 사용할지를 선택하고, 특정 요일로 되풀이 간격을 구성할 수 있습니다.  

    > [!NOTE]  
    >  1일 미만의 간격을 지정할 경우 Configuration Manager에서 자동으로 기본값을 1일로 설정합니다.  

    > [!WARNING]  
    >  클라이언트 컴퓨터의 실제 시작 시간은 시작 시간에 임의 시간(최대 2시간)을 더한 값이 됩니다. 이를 통해 클라이언트 컴퓨터가 활성 소프트웨어 업데이트 지점 서버에서 동시에 검사를 시작하고 WSUS(Windows Server Update Services)에 연결하지 않도록 방지됩니다.  

-   **배포 재평가 일정**  

     이 설정을 사용하여 소프트웨어 업데이트 클라이언트 에이전트에서 Configuration Manager 클라이언트 컴퓨터의 소프트웨어 업데이트의 설치 상태를 재평가하는 빈도를 구성할 수 있습니다. 이전에 설치된 소프트웨어 업데이트를 클라이언트 컴퓨터에서 찾을 수 없는 경우 해당 소프트웨어 업데이트가 계속 필요하면 다시 설치됩니다.

     배포 재평가 일정은 사용자가 소프트웨어 업데이트를 제거할 수 있는 권한이 있는지 여부 등 소프트웨어 업데이트 호환성에 대한 회사 정책을 기반으로 조정해야 합니다. 각 배포 재평가 주기에 따라 일부 네트워크 및 클라이언트 CPU 작업이 활성화됩니다. 기본적으로, 단순 일정이 사용되고 배포 재평가 검사가 7일마다 시작됩니다.  

    > [!NOTE]  
    >  1일 미만의 간격을 지정할 경우 Configuration Manager에서 자동으로 기본값을 1일로 설정합니다.  

-   **소프트웨어 업데이트 배포의 최종 기한에 도달한 경우 지정한 기간 내에 기한이 있는 다른 모든 소프트웨어 업데이트 배포도 설치합니다.**  

     이 설정을 사용하여 지정한 기간 내에 최종 기한이 도래하는 필수 배포 내의 모든 소프트웨어 업데이트를 설치할 수 있습니다. 필수 소프트웨어 업데이트 배포의 최종 기한에 도달하는 경우 배포 내의 소프트웨어 업데이트에 대한 설치가 클라이언트에서 시작됩니다. 또한 이 설정을 사용하여 지정한 기간 내에 구성된 최종 기한이 있는 다른 필수 배포에 정의된 소프트웨어 업데이트 설치를 시작할지 여부를 결정할 수 있습니다.  

     이 설정을 사용하여 필수 소프트웨어 업데이트의 소프트웨어 업데이트 설치를 가속화하고, 잠재적으로 보안을 강화하며, 잠재적으로 알림 표시를 줄이고, 클라이언트 컴퓨터에서 잠재적으로 시스템 다시 설정을 줄일 수 있습니다. 기본적으로 이 설정은 사용되지 않습니다.  

-   **보류된 모든 배포도 설치할 기간(최종 기한이 해당 기간 내에 포함되는 경우)**  

     이 설정을 사용하여 이전 설정의 기간을 지정할 수 있습니다. 1~23시간 및 1~365일의 값을 입력할 수 있습니다. 기본적으로, 이 설정은 7일로 구성됩니다.  

-   **클라이언트에서 빠른 설치 파일의 설치 사용**

-   **Express 설치 파일 콘텐츠를 다운로드하는 데 사용할 포트**

-   **Office 365 클라이언트 에이전트 관리 사용** 이 설정을 사용하여 Office 365 클라이언트 에이전트의 관리를 사용하도록 설정합니다. 값을 **예**로 설정하면 Office 365 설치 설정을 구성하고, Office CDN(콘텐츠 배달 네트워크)에서 파일을 다운로드하고, Configuration Manager의 응용 프로그램으로 파일을 배포할 수 있습니다.

##  <a name="user-and-device-affinity"></a>사용자 및 장치 선호도  

-   **사용자 장치 선호도 사용량 임계값(분)**  

     Configuration Manager에서 사용자 장치 선호도 매핑을 만들기 전에 시간(분)을 지정합니다.  

-   **사용자 장치 선호도 사용량 임계값(일)**  

     지정한 기간(일)이 초과되면 사용량 기반 선호도 임계값이 측정됩니다.  

    > [!NOTE]  
    >  예를 들어 **사용자 장치 선호도 사용량 임계값(분)**이 **60**분으로 지정되고 **사용자 장치 선호도 사용량 임계값(일)**이 **5**일로 지정된 경우 사용자가 사용자 장치 선호도를 자동으로 만들려면 5일이라는 기간에 걸쳐 60분 동안 장치를 사용해야 합니다.  

-   **사용량 데이터에서 사용자 장치 선호도 자동 구성**  

     수집된 사용 정보를 기준으로 하여 Configuration Manager에서 사용자 장치 선호도를 자동으로 만들 수 있도록 설정하려면 **True** 또는 **예**를 선택합니다.  

##  <a name="mobile-devices"></a>모바일 장치  

-   **모바일 장치 등록 프로필**  

     이 설정을 구성할 수 있으려면 먼저 모바일 장치 사용자 설정인 **사용자가 모바일 장치 및 Mac 컴퓨터를 등록할 수 있도록 허용** 을 **True**로 설정해야 합니다. 그런 다음 **프로필 설정**을 선택하고 등록 프로세스 동안 사용할 인증서 템플릿 관련 정보가 포함된 등록 프로필을 지정하고, 등록 지점과 등록 프록시 지점을 포함하는 사이트를 지정하고, 등록 이후 장치를 관리할 사이트를 지정할 수 있습니다.  

    > [!IMPORTANT]  
    >  이 옵션을 구성하기 전에 모바일 장치 등록에 사용할 인증서 템플릿을 구성해야 합니다.  

##  <a name="enrollment"></a>등록  

-   **모바일 장치 등록 프로필**  

     이 설정을 구성할 수 있으려면 먼저 등록 사용자 설정인 **사용자가 모바일 장치 및 Mac 컴퓨터를 등록할 수 있도록 허용** 을 **예**로 설정해야 합니다. 그런 다음 **프로필 설정**을 선택하고 등록 프로세스 동안 사용할 인증서 템플릿 관련 정보가 포함된 등록 프로필을 지정하고, 등록 지점과 등록 프록시 지점을 포함하는 사이트를 지정하고, 등록 이후 장치를 관리할 사이트를 지정할 수 있습니다.  

    > [!IMPORTANT]  
    >  이 옵션을 구성하기 전에 모바일 장치 등록 또는 Mac 클라이언트 인증서 등록에 사용할 인증서 템플릿을 구성해야 합니다.  

## <a name="user-and-device-affinity"></a>사용자 및 장치 선호도  

-   **사용자가 기본 장치를 정의할 수 있도록 허용**  

     응용 프로그램 카탈로그의 **내 장치** 탭에서 사용자 자신의 기본 장치를 식별할 수 있도록 허용할지 여부를 지정합니다.  
