---
title: "인터넷 기반 클라이언트 관리 | Microsoft 문서"
description: "System Center Configuration Manager에서 인터넷 기반 클라이언트 관리 계획을 만듭니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 82867e77840e14e9b8170801ea3c4a9f399c9890


---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 인터넷 기반 클라이언트 관리 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 클라이언트가 회사 네트워크에 연결되어 있지 않지만 표준 인터넷 연결이 있는 경우 인터넷 기반 클라이언트 관리(IBCM이라고도 함)를 통해 해당 클라이언트를 관리할 수 있습니다. 이러한 방식에는 가상 사설망(VPN)을 실행할 필요가 없고 소프트웨어 업데이트를 적시에 배포할 수 있는 데서 발생하는 비용 절감을 포함해 여러 이점이 있습니다.  

 공용 네트워크에서 클라이언트 컴퓨터를 관리할 경우 높은 수준의 보안이 요구되므로 인터넷 기반 클라이언트 관리를 사용하려면 클라이언트 및 클라이언트가 연결하는 사이트 시스템 서버에서 PKI 인증서를 사용해야 합니다. 이렇게 하면 연결은 독립 기관에 의해 인증되고 이 사이트 시스템에 전송되거나 이 사이트 시스템에서 전송되는 데이터는 SSL(Secure Sockets Layer)로 암호화됩니다.  

 다음 섹션에서는 인터넷 기반 클라이언트 관리를 계획하는 방법에 대해 설명합니다.  

##  <a name="a-namebkmkibcmfeaturesnotsupporteda-features-that-are-not-supported-on-the-internet"></a><a name="BKMK_IBCM_FeaturesNotSupported"></a> 인터넷에서 지원하지 않는 기능  
 모든 클라이언트 관리 기능이 인터넷에 적합한 것은 아니므로 클라이언트가 인터넷에서 관리될 때 일부 기능은 지원되지 않습니다. 인터넷 관리에 대해 지원되지 않는 기능은 일반적으로 Active Directory Domain Services에 의존하거나 네트워크 검색 및 Wake-On-LAN(WOL)과 같은 공용 네트워크에 적합하지 않습니다.  

 다음 기능은 클라이언트가 인터넷에서 관리될 때 지원되지 않습니다.  

-   클라이언트 강제 및 소프트웨어 업데이트 기반 클라이언트 배포와 같은 인터넷을 통한 클라이언트 배포. 대신 수동 클라이언트 설치를 사용합니다.  

-   자동 사이트 할당  

-   Wake-On-LAN  

-   운영 체제 배포. 그러나 운영 체제를 배포하지 않는 작업 순서(예: 클라이언트에서 스크립트 및 유지 관리 작업을 실행하는 작업 순서)는 배포할 수 있습니다.  

-   원격 제어  

-   인터넷 기반 관리 지점에서 Windows 인증(Kerberos 또는 NTLM)을 사용하여 Active Directory Domain Services의 사용자를 인증할 수 없는 경우의 사용자에 대한 소프트웨어 배포. 이 기능은 인터넷 기반 관리 지점에서 사용자 계정이 상주하는 포리스트를 트러스트할 때 지원됩니다.  

 또한 인터넷 기반 클라이언트 관리는 로밍을 지원하지 않습니다. 로밍을 사용하면 클라이언트는 항상 가장 가까운 배포 지점을 검색하여 콘텐츠를 다운로드할 수 있습니다. 인터넷에서 관리되는 클라이언트는 해당 사이트 시스템이 인터넷 FQDN을 사용하도록 구성되고 사이트 시스템 역할이 인터넷의 클라이언트 연결을 허용할 경우 할당된 사이트의 사이트 시스템과 통신합니다. 클라이언트는 대역폭 또는 실제 위치에 관계없이 인터넷 기반 사이트 시스템 중 하나를 임의로 선택합니다.  

 인터넷의 연결을 허용하도록 구성된 소프트웨어 업데이트 지점이 있는 경우 인터넷상의 Configuration Manager 인터넷 기반 클라이언트는 항상 이 소프트웨어 업데이트 지점을 검색하여 필요한 소프트웨어 업데이트를 확인합니다. 그러나 이러한 클라이언트가 인터넷에 있는 경우 인터넷 기반 배포 지점이 아닌 Microsoft Update에서 먼저 소프트웨어 업데이트 다운로드를 시도합니다. Microsoft Update에서 다운로드하지 못하는 경우에만 인터넷 기반 배포 지점에서 필요한 소프트웨어 업데이트를 다운로드합니다. 인터넷 기반 클라이언트 관리를 위해 구성되지 않은 클라이언트는 Microsoft 업데이트에서 소프트웨어 업데이트 다운로드를 시도하지 않으며 항상 Configuration Manager 배포 지점을 사용합니다.  

##  <a name="a-namebkmkplanforinternetsitesystemsa-considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a><a name="BKMK_PlanforInternetSiteSystems"></a> 인터넷 또는 신뢰할 수 없는 포리스트에서의 클라이언트 통신에 대한 고려 사항  
 기본 사이트에 설치된 다음 사이트 시스템 역할은 인터넷 또는 신뢰할 수 없는 포리스트와 같은 신뢰할 수 없는 위치에 있는 클라이언트에서의 연결을 지원합니다(보조 사이트는 신뢰할 수 없는 위치에서의 클라이언트 연결을 지원하지 않음).  

-   응용 프로그램 카탈로그 웹 사이트 지점  

-   Configuration Manager 정책 모듈  

-   배포 지점(HTTPS는 클라우드 기반 배포 지점에 필요)  

-   등록 프록시 지점  

-   대체 상태 지점  

-   관리 지점  

-   소프트웨어 업데이트 지점  

 **인터넷 연결 사이트 시스템 정보:**   
클라이언트 포리스트와 사이트 시스템 서버 포리스트 간의 신뢰 관계에 대한 요구 사항이 없는 경우에도 인터넷 연결 사이트 시스템을 포함하는 포리스트가 사용자 계정을 포함하는 포리스트를 신뢰할 수 있다면 이 구성은 **클라이언트 정책** 클라이언트 설정 **인터넷 클라이언트의 사용자 정책 요청 사용**을 사용하는 경우 인터넷상의 장치에 대해 사용자 기반 정책을 지원합니다.  

 예를 들어 다음 구성은 인터넷 기반 클라이언트 관리에서 인터넷의 장치에 대해 사용자 정책을 지원하는 경우를 보여 줍니다.  

-   인터넷 기반 관리 지점은 읽기 전용 도메인 컨트롤러가 사용자 인증을 위해 상주하는 경계 네트워크에 있으며 중간 방화벽은 Active Directory 패킷을 허용합니다.  

-   사용자 계정은 포리스트 A(인트라넷)에 있고 인터넷 기반 관리 지점은 포리스트 B(경계 네트워크)에 있습니다. 포리스트 B는 포리스트 A를 트러스트하고 중간 방화벽은 인증 패킷을 허용합니다.  

-   사용자 계정 및 인터넷 기반 관리 지점은 포리스트 A(인트라넷)에 있습니다. 관리 지점은 웹 프록시 서버(예: Forefront Threat Management Gateway)를 통해 인터넷에 게시됩니다.  

> [!NOTE]  
>  Kerberos 인증이 실패하면 자동으로 NTLM 인증이 시도됩니다.  

 이전 예제에서 볼 수 있듯이 인터넷 기반 사이트 시스템은 ISA Server 및 Forefront Threat Management Gateway와 같은 웹 프록시 서버를 통해 인터넷에 게시될 때 인트라넷에 배치할 수 있습니다. 이러한 사이트 시스템은 인터넷의 클라이언트 연결에 대해서만 구성하거나 인터넷 및 인트라넷의 클라이언트 연결 모두에 대해 구성할 수 있습니다. 웹 프록시 서버를 사용할 경우 해당 웹 프록시 서버에서 보안 수준이 더 높은 SSL(Secure Sockets Layer) 또는 SSL 터널링에 대한 SSL 브리징을 구성할 수 있습니다.  

-   **SSL에 대한 SSL 브리징:**   
    인터넷 기반 클라이언트 관리에 대해 프록시 웹 서버를 사용할 경우 권장되는 구성은 SSL에 대한 SSL 브리징입니다. 이 구성에서는 인증과 함께 SSL 종료를 사용합니다. 클라이언트 컴퓨터는 컴퓨터 인증으로 인증되어야 하며 모바일 장치 기존 클라이언트는 사용자 인증으로 인증됩니다. Configuration Manager에서 등록된 모바일 장치는 SSL 브리징을 지원하지 않습니다.  

     프록시 웹 서버에서 SSL 종료의 이점은 인터넷의 패킷은 내부 네트워크에 전달되기 전에 검사를 받아야 한다는 것입니다. 프록시 웹 서버는 클라이언트에서의 연결을 인증하고 종료한 다음 인터넷 기반 사이트 시스템에 대한 새로운 인증 연결을 개시합니다. Configuration Manager 클라이언트에서 프록시 웹 서버를 사용하면 클라이언트 ID(클라이언트 GUID)는 패킷 페이로드에 안전하게 보관되므로 관리 지점은 프록시 웹 서버를 클라이언트로 간주하지 않습니다. Configuration Manager에서 HTTP에서 HTTPS로 또는 HTTPS에서 HTTP로의 브리징은 지원되지 않습니다.  

-   **터널링:**:   
    프록시 웹 서버가 SSL 브리징에 대한 요구 사항을 지원할 수 없는 경우 또는 Configuration Manager에서 등록된 모바일 장치에 대해 인터넷 지원을 구성하려는 경우를 위해 SSL 터널링도 지원됩니다. 이는 보안 수준이 더 낮은 옵션입니다. 인터넷의 SSL 패킷이 SSL 종료 없이 사이트 시스템으로 전달되기 때문이며, 이 경우 악성 콘텐츠는 검사되지 않습니다. SSL 터널링을 사용할 경우 프록시 웹 서버에 대한 인증서 요구 사항은 없습니다.  

##  <a name="a-namebkmkplanforinternetclientsa-planning-for-internet-based-clients"></a><a name="BKMK_PlanforInternetClients"></a> 인터넷 기반 클라이언트 계획  
 인터넷을 통해 관리할 클라이언트 컴퓨터를 인트라넷 및 인터넷상에서 관리 가능하도록 구성할지 또는 인터넷 전용 클라이언트 관리가 사용되도록 구성할지 지정해야 합니다. 클라이언트 컴퓨터를 설치하는 동안만 클라이언트 관리 옵션을 구성할 수 있습니다. 나중에 구성을 변경하려면 클라이언트를 다시 설치해야 합니다.  

> [!NOTE]  
>  인터넷 지원 관리 포털을 구성한 경우 다음에 사용 가능한 관리 지점 목록을 새로 고치면 관리 지점에 연결된 클라이언트에서 인터넷을 사용할 수 있게 됩니다.  

> [!TIP]  
>  인터넷 전용 클라이언트 관리의 구성은 인터넷으로 제한할 필요는 없으며 인트라넷에서도 사용할 수 있습니다.  

 인터넷 전용 클라이언트 관리를 사용하도록 구성된 클라이언트는 인터넷의 클라이언트 연결을 사용하도록 구성된 사이트 시스템과만 통신합니다. 이러한 구성은 원격 위치의 POS(Point of Sale) 컴퓨터와 같이 회사 인트라넷에 연결하지 않는 컴퓨터에 적합합니다. 또한 방화벽 및 제한된 보안 정책을 지원하는 경우처럼 클라이언트 통신을 HTTPS만으로 제한하려 할 때, 경계 네트워크에 인터넷 기반 사이트 시스템을 설치하고 이러한 서버를 Configuration Manager 클라이언트를 사용하여 관리하려 할 때 적합할 수 있습니다.  

 인터넷에서 작업 그룹 클라이언트를 관리하려면 클라이언트를 인터넷 전용으로 설치해야 합니다.  

> [!NOTE]  
>  모바일 장치 클라이언트는 인터넷 기반 관리 지점을 사용하도록 구성될 때 자동으로 인터넷 전용으로 구성됩니다.  

 다른 클라이언트 컴퓨터는 인터넷 및 인트라넷 클라이언트 관리를 사용하도록 구성될 수 있습니다. 이러한 컴퓨터는 네트워크의 변경 사항이 검색되면 인터넷 기반 클라이언트 관리 및 인트라넷 클라이언트 관리 사이에서 자동으로 전환합니다. 이 클라이언트는 인트라넷에서 클라이언트 연결에 대해 구성된 관리 지점을 검색하고 이 관리 지점에 연결할 수 있는 경우 전체 Configuration Manager 관리 기능이 있는 인트라넷 클라이언트로서 관리됩니다. 또는 인트라넷에서 클라이언트 연결에 대해 구성된 관리 지점을 검색하지 못하거나 이 관리 지점에 연결할 수 없는 경우 이 클라이언트는 인터넷 기반 관리 지점에 연결을 시도하고 이 연결이 성공하면 할당된 사이트의 인터넷 기반 사이트 시스템에 의해 관리됩니다.  

 인터넷 기반 클라이언트 관리 및 인트라넷 클라이언트 관리 간 자동 전환의 이점은 클라이언트 컴퓨터가 인트라넷에 연결할 때마다 모든 Configuration Manager 기능을 자동으로 사용할 수 있고 인터넷상에 있을 때 필수 관리 기능이 계속적으로 관리된다는 것입니다. 또한 인터넷에서 시작한 다운로드는 인트라넷에서 끊김 없이 다시 시작할 수 있으며 그 반대의 경우도 마찬가지입니다.  

##  <a name="a-namebkmkprerequisitsforinternetclientmgmta-prerequisites-for-internet-based-client-management"></a><a name="BKMK_PrerequisitsForInternetClientMgmt"></a> 인터넷 기반 클라이언트 관리에 대한 필수 조건  
 Configuration Manager의 인터넷 기반 클라이언트 관리에는 다음과 같은 외부 종속성이 있습니다.  

-   인터넷에서 관리될 클라이언트에는 인터넷 연결이 있어야 합니다.  

     Configuration Manager에서는 기존 ISP(인터넷 서비스 공급자) 인터넷 연결을 사용하며 이는 영구적 연결이거나 임시 연결일 수 있습니다. 클라이언트 모바일 장치에는 직접 인터넷 연결이 있어야 하지만 클라이언트 컴퓨터에는 직접 인터넷 연결 또는 프록시 웹 서버를 통한 연결 중 하나가 있으면 됩니다.  

-   인터넷 기반 클라이언트 관리를 지원하는 사이트 시스템은 인터넷 연결을 갖추어야 하고 Active Directory 도메인 안에 있어야 합니다.  

     인터넷 기반 사이트 시스템은 사이트 서버의 Active Directory 포리스트와 트러스트 관계를 가질 필요가 없습니다. 그러나 인터넷 기반 관리 지점에서 Windows 인증을 사용하여 사용자를 인증할 수 있으면 사용자 정책이 지원됩니다. Windows 인증이 실패하면 컴퓨터 정책만 지원됩니다.  

    > [!NOTE]  
    >  사용자 정책을 지원하려면 다음 두 개의 **클라이언트 정책** 클라이언트 설정을 **True** 로 설정해야 합니다.  
    >   
    >  -   **클라이언트에서 사용자 정책 폴링 사용**  
    > -   **인터넷 클라이언트의 사용자 정책 요청 사용**  

     인터넷 기반 응용 프로그램 카탈로그 웹 사이트 지점도 사용자 컴퓨터가 인터넷에 있을 때 해당 사용자를 인증하기 위해 Windows 인증을 필요로 합니다. 이 요구 사항은 사용자 정책과 독립적입니다.  

-   클라이언트에서 요구하고 인터넷 및 인터넷 기반 사이트 시스템 서버에서 관리되는 인증서를 배포 및 관리할 수 있는 지원 PKI(공개 키 인프라)가 있어야 합니다.  

     PKI 인증서에 대한 자세한 내용은 [System Center Configuration Manager를 위한 PKI 인증서 요구 사항](/sccm/core/plan-design/network/pki-certificate-requirements)을 참조하세요.  

-   인터넷 기반 클라이언트 관리를 지원하는 사이트 시스템의 인터넷 FQDN(정규화된 도메인 이름)은 공용 DNS 서버에 호스트 항목으로 등록되어야 합니다.  

-   중간 방화벽 또는 프록시 서버에서 인터넷 기반 사이트 시스템과 연결된 클라이언트 통신을 허용해야 합니다.  

     클라이언트 통신 요구 사항:  

    -   HTTP 1.1 지원  

    -   multipart MIME 첨부 파일의 HTTP 콘텐츠 형식(multipart/mixed 및 application/octet-stream) 허용  

    -   인터넷 기반 관리 지점에 대해 다음 동사 허용:  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   인터넷 기반 배포 지점에 대해 다음 동사 허용:  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   인터넷 기반 대체 상태 지점에 대해 다음 동사 허용:  

        -   POST  

    -   인터넷 기반 응용 프로그램 카탈로그 웹 사이트 지점에 대해 다음 동사 허용:  

        -   POST  

        -   GET  

    -   인터넷 기반 관리 지점에 대해 다음 HTTP 헤더 허용:  

        -   Range:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   인터넷 기반 배포 지점에 대해 다음 HTTP 헤더 허용:  

        -   Range:  

     이 요구 사항을 지원하기 위한 구성 정보를 보려면 해당 방화벽 또는 프록시 서버 설명서를 참조하세요.  

     인터넷의 클라이언트 연결에 대해 소프트웨어 업데이트 지점을 사용할 경우 이와 비슷한 통신 요구 사항을 보려면 WSUS(Windows Server Update Services)용 설명서를 참조하세요. 예를 들어 Windows Server 2003의 WSUS는 보안 설정에 대한 배포 부록인 [부록 D: 보안 설정](http://go.microsoft.com/fwlink/p/?LinkId=143368)을 참조하세요.



<!--HONumber=Dec16_HO3-->

