---
title: "소프트웨어 업데이트 지점 설치 및 구성 | Microsoft 문서"
description: "소프트웨어 업데이트 준수 평가를 수행하고 클라이언트에 소프트웨어 업데이트를 배포하려면 중앙 관리 사이트에 기본 사이트에 대한 소프트웨어 업데이트 지점이 있어야 합니다."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/30/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 7d369384d133c90a15e01df50ac53992d61f3873
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-configure-a-software-update-point"></a>소프트웨어 업데이트 지점 설치 및 구성  

*적용 대상: System Center Configuration Manager(현재 분기)*


> [!IMPORTANT]  
>  소프트웨어 업데이트 지점 사이트 시스템 역할을 설치하기 전에 서버가 필수 종속성을 충족하는지 확인하고 사이트의 소프트웨어 업데이트 지점 인프라를 결정해야 합니다. 소프트웨어 업데이트를 계획하고 소프트웨어 업데이트 지점 인프라를 결정하는 방법에 대한 자세한 내용은 [소프트웨어 업데이트 계획](../plan-design/plan-for-software-updates.md)을 참조하세요.  

 소프트웨어 업데이트 호환성 평가를 사용하도록 설정하고 클라이언트에 소프트웨어 업데이트를 배포하려면 중앙 관리 사이트 및 기본 사이트에 소프트웨어 업데이트 지점이 필요합니다. 보조 사이트에서는 소프트웨어 업데이트 지점이 선택 사항입니다. WSUS가 설치된 서버에서 소프트웨어 업데이트 지점 사이트 시스템 역할을 만들어야 합니다. 소프트웨어 업데이트 지점은 WSUS 서비스와 상호 작용하여 소프트웨어 업데이트 설정을 구성하고 소프트웨어 업데이트 메타데이터의 동기화를 요청합니다. Configuration Manager 계층 구조가 있으면 중앙 관리 사이트, 자식 기본 사이트, 보조 사이트(필요한 경우) 순으로 소프트웨어 업데이트 지점을 설치하고 구성합니다. 중앙 관리 사이트가 아니라 독립 실행형 기본 사이트가 있으면 먼저 기본 사이트에 소프트웨어 업데이트 지점을 설치하고 구성한 후, 필요하면 그 다음에 보조 사이트에도 설치하고 구성합니다. 일부 설정은 최상위 사이트에서 소프트웨어 업데이트 지점을 구성할 때만 사용할 수 있습니다. 소프트웨어 업데이트 지점을 설치한 위치에 따라 고려해야 할 옵션이 다릅니다.  

> [!IMPORTANT]  
>  사이트에 소프트웨어 업데이트 지점을 두 개 이상 설치할 수 있습니다. 설치하는 첫 번째 소프트웨어 업데이트 지점은 동기화 원본으로 구성되어 Microsoft Update나 업스트림 동기화 원본에서 업데이트를 동기화합니다. 사이트의 다른 소프트웨어 업데이트 지점은 첫 번째 소프트웨어 업데이트 지점의 복제본으로 구성됩니다. 따라서 첫 번째 소프트웨어 업데이트 지점을 설치하고 구성한 후 일부 설정은 사용할 수 없습니다.  

> [!IMPORTANT]  
>  독립 실행형 WSUS 서버로 구성 및 사용되었거나 소프트웨어 업데이트 지점을 사용하여 WSUS 클라이언트를 직접 관리하는 서버에 소프트웨어 업데이트 지점 사이트 시스템 역할을 설치하는 것은 지원되지 않습니다. 기존 WSUS 서버는 활성 소프트웨어 업데이트 지점에 대한 업스트림 동기화 원본으로서만 지원됩니다. [업스트림 데이터 원본 위치에서 동기화](#BKMK_wsussync)을 참조하세요.

 기존 사이트 시스템 서버에 소프트웨어 업데이트 지점 사이트 시스템 역할을 추가하거나 새로 만들 수 있습니다. 사이트 시스템 역할을 기존 사이트 서버에 추가하는지 아니면 새 사이트 서버에 추가하는지에 따라 **사이트 시스템 서버 만들기 마법사** 또는 **사이트 시스템 역할 추가 마법사** 의 **시스템 역할 선택** 페이지에서 **소프트웨어 업데이트 지점**을 선택한 다음 마법사에서 소프트웨어 업데이트 지점 설정을 구성합니다. 설정은 사용하는 Configuration Manager 버전에 따라 다릅니다. 사이트 시스템 역할을 설치하는 방법에 대한 자세한 내용은 [사이트 시스템 역할 설치](../../core/servers/deploy/configure/install-site-system-roles.md)를 참조하세요.  

 사이트의 소프트웨어 업데이트 지점 설정에 대한 정보는 다음 섹션을 참조하세요.  

## <a name="proxy-server-settings"></a>프록시 서버 설정  
 사용 중인 Configuration Manager 버전에 따라 **사이트 시스템 서버 만들기 마법사** 또는 **사이트 시스템 역할 추가 마법사**의 각기 다른 페이지에서 프록시 서버 설정을 구성할 수 있습니다.  

-   프록시 서버를 구성한 다음 소프트웨어 업데이트에 프록시 서버를 사용할 시간을 지정해야 합니다. 다음 설정을 구성합니다.  

    -   마법사의 **프록시** 페이지에서 또는 사이트 시스템 속성의 **프록시** 탭에서 프록시 서버 설정을 구성합니다. 프록시 서버 설정은 사이트 시스템별로 다릅니다. 즉, 모든 사이트 시스템 역할은 사용자가 지정하는 프록시 서버 설정을 사용합니다.  

    -   Configuration Manager에서 소프트웨어 업데이트를 동기화할 때와 자동 배포 규칙을 사용하여 콘텐츠를 다운로드할 때 프록시 서버를 사용할지 여부를 구성합니다. 마법사의 **프록시 및 계정 설정** 페이지에서 또는 소프트웨어 업데이트 지점 속성의 **프록시 및 계정 설정** 탭에서 소프트웨어 업데이트 지점 프록시 서버 설정을 구성합니다.  

        > [!NOTE]  
        >  **자동 배포 규칙을 사용하여 콘텐츠 다운로드 시 프록시 서버 사용** 설정을 사용할 수 있지만 보조 사이트의 소프트웨어 업데이트 지점에는 이 설정이 사용되지 않습니다. 중앙 관리 사이트 및 기본 사이트의 소프트웨어 업데이트 지점만 Microsoft Update 페이지에서 콘텐츠를 다운로드합니다.  

> [!IMPORTANT]  
>  자동 배포 규칙을 실행하면 기본적으로 자동 배포 규칙을 만든 서버의 **로컬 시스템** 계정을 사용하여 인터넷에 연결하고 소프트웨어 업데이트를 다운로드합니다. 이 계정에 인터넷 액세스 계정이 없으면 소프트웨어 업데이트를 다운로드하지 못하고 ruleengine.log에 다음 항목이 로깅됩니다. **인터넷에서 업데이트를 다운로드하지 못했습니다. 오류 = 12007**. 로컬 시스템 계정이 인터넷에 액세스할 수 없으면 프록시 서버에 연결할 자격 증명을 구성합니다.  


## <a name="wsus-settings"></a>WSUS 설정  
 사용 중인 Configuration Manager 버전에 따라 **사이트 시스템 서버 만들기 마법사** 또는 **사이트 시스템 역할 추가 마법사**의 각기 다른 페이지에서 WSUS 설정을 구성해야 하며, 경우에 따라서는 소프트웨어 업데이트 지점의 속성(또는 소프트웨어 업데이트 지점 구성 요소 속성)에서만 이 설정을 구성해야 합니다. WSUS 설정을 구성하려면 다음 섹션의 정보를 참조하세요.  

### <a name="BKMK_wsusport"></a>WSUS 포트 설정  
 마법사의 소프트웨어 업데이트 지점 페이지에서 또는 소프트웨어 업데이트 지점의 속성에서 WSUS 포트 설정을 구성해야 합니다. WSUS에 사용되는 포트 설정을 확인하려면 다음 절차를 따르세요.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>IIS에서 사용되는 포트 설정을 확인하려면  

 1.  WSUS 서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  

 2.  **웹 사이트**를 확장하고 WSUS 서버의 웹 사이트를 마우스 오른쪽 단추로 클릭한 후 **바인딩 편집**을 클릭합니다. 사이트 바인딩 대화 상자에서 HTTP 및 HTTPS 포트 값이 **포트** 열에 표시됩니다.


### <a name="configure-ssl-communications-to-wsus"></a>WSUS에 대한 SSL 통신 구성  
 마법사의 **일반** 페이지에서 또는 소프트웨어 업데이트 지점 속성의 **일반** 탭에서 SSL 통신을 구성할 수 있습니다.  

 SSL을 사용하는 방법에 대한 자세한 내용은 [SSL을 사용하도록 WSUS를 구성할지 여부 결정](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL)을 참조하세요.  

### <a name="wsus-server-connection-account"></a>WSUS 서버 연결 계정  
 소프트웨어 업데이트 지점에서 실행하는 WSUS에 연결할 때 사이트 서버에서 사용할 계정을 구성할 수 있습니다. 이 계정을 구성하지 않으면 Configuration Manager에서 사이트 서버가 WSUS에 연결할 때 사용하는 컴퓨터 계정을 사용합니다. 마법사의 **프록시 및 계정 설정** 페이지에서 또는 소프트웨어 업데이트 지점 속성의 **프록시 및 계정 설정** 탭에서 WSUS 서버 연결 계정을 구성할 수 있습니다.  사용하는 Configuration Manager 버전에 따라 마법사의 각기 다른 위치에서 계정을 구성할 수 있습니다.  

 Configuration Manager 계정에 대한 자세한 내용은 [System Center Configuration Manager에서 사용된 계정](../../core/plan-design/hierarchy/accounts.md)을 참조하세요.  

## <a name="synchronization-source"></a>동기화 원본  
 마법사의 **동기화 원본** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **동기화 설정** 탭에서 소프트웨어 업데이트 동기화에 대한 업스트림 동기화 원본을 구성할 수 있습니다. 동기화 원본에 대한 옵션은 사이트에 따라 달라집니다.  

 사이트에 소프트웨어 업데이트 지점을 구성할 때 사용할 수 있는 옵션을 보려면 다음 표를 참조하세요.  

|사이트|사용 가능한 동기화 원본 옵션|  
|----------|----------------------------------------------|  
|-   중앙 관리 사이트<br />-   독립 실행형 기본 사이트|-   Microsoft Update 웹 사이트에서 동기화<br />-   업스트림 데이터 원본 위치에서 동기화<br />-   Microsoft Update 또는 업스트림 데이터 원본에서 동기화 안 함|  
|-   사이트의 추가 소프트웨어 업데이트 지점<br />-   자식 기본 사이트<br />-   보조 사이트|-   업스트림 데이터 원본 위치에서 동기화|  

 다음 목록에는 동기화 원본으로 사용할 수 있는 각 옵션에 대한 추가 정보가 나열되어 있습니다.  

-   **Microsoft 업데이트에서 동기화**: Microsoft 업데이트에서 소프트웨어 업데이트 메타데이터를 동기화하려면 이 설정을 사용합니다. 중앙 관리 사이트에서는 인터넷 액세스가 가능해야 하며 그렇지 않으면 동기화가 실패합니다. 이 설정은 소프트웨어 업데이트 지점을 최상위 사이트에 구성하는 경우에만 사용할 수 있습니다.  

    > [!NOTE]  
    >  소프트웨어 업데이트 지점과 인터넷 간에 방화벽이 있는 경우 WSUS 웹 사이트에 사용되는 HTTP 및 HTTPS 포트를 허용하도록 이 방화벽을 구성해야 할 수 있습니다. 또한 방화벽에서 제한된 도메인에 대한 액세스를 제한하도록 선택할 수 있습니다. 소프트웨어 업데이트를 지원하는 방화벽을 계획하는 방법에 대한 자세한 내용은 [방화벽 구성](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)을 참조하세요.  

-   **<a name="BKMK_wsussync"></a>S업스트림 데이터 원본 위치에서 동기화**: 업스트림 동기화 원본에서 소프트웨어 업데이트 메타데이터를 동기화하려면 이 설정을 사용합니다. 자식 기본 사이트 및 보조 사이트는 이 설정에 부모 사이트 URL을 사용하도록 자동으로 구성됩니다. 기존 WSUS 서버에서 소프트웨어 업데이트를 동기화할 수 있는 옵션이 제공됩니다. 이 경우 https://WSUSServer:8531 과 같이 URL을 지정하면 되며 여기서 8531은 WSUS 서버에 연결하는 데 사용되는 포트입니다.  

-   **Microsoft 업데이트 또는 업스트림 데이터 원본에서 동기화 안 함**: 최상위 사이트에서 소프트웨어 업데이트 지점의 인터넷 연결이 끊어졌을 때 소프트웨어 업데이트를 수동으로 동기화하려면 이 설정을 사용합니다. 자세한 내용은 [연결이 끊긴 소프트웨어 업데이트 지점에서 소프트웨어 업데이트 동기화](synchronize-software-updates-disconnected.md)를 참조하세요.  

> [!NOTE]  
>  소프트웨어 업데이트 지점과 인터넷 간에 방화벽이 있는 경우 WSUS 웹 사이트에 사용되는 HTTP 및 HTTPS 포트를 허용하도록 이 방화벽을 구성해야 할 수 있습니다. 또한 방화벽에서 제한된 도메인에 대한 액세스를 제한하도록 선택할 수 있습니다. 소프트웨어 업데이트를 지원하는 방화벽을 계획하는 방법에 대한 자세한 내용은 [방화벽 구성](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)을 참조하세요.  

 마법사의 **동기화 원본** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **동기화 설정** 탭에서 WSUS 보고 이벤트를 만들지 여부를 구성할 수도 있습니다. Configuration Manager에서는 이러한 이벤트를 사용하지 않으므로 일반적으로는 기본 설정인 **WSUS 보고 이벤트 생성 안 함**을 선택합니다.  

## <a name="synchronization-schedule"></a>동기화 일정  
 동기화 일정은 마법사의 **동기화 일정** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성에서 구성합니다. 이 설정은 최상위 사이트의 소프트웨어 업데이트 지점에만 구성됩니다.  

 일정을 사용하도록 설정하면 되풀이되는 단순 또는 사용자 지정 동기화 일정을 구성할 수 있습니다. 단순 일정을 구성할 경우 시작 시간은 일정을 만들 때 Configuration Manager 콘솔을 실행하는 컴퓨터의 현지 시간을 기준으로 합니다. 사용자 지정 일정에 대한 시작 시간은 Configuration Manager 콘솔을 실행하는 컴퓨터의 현지 시간을 기준으로 구성합니다.  

> [!TIP]  
>  사용자 환경에 적합한 시간 프레임을 사용하여 소프트웨어 업데이트 동기화의 실행을 예약합니다. 일반적으로 매월 두 번째 화요일의 Microsoft 정규 보안 업데이트 릴리스 직후에 소프트웨어 업데이트 동기화 일정이 실행되도록 설정하는 방법이 있으며 이를 보통 화요일 패치라고 합니다. 또 다른 일반적인 방법으로는 소프트웨어 업데이트를 사용하여 Endpoint Protection 정의 및 엔진 업데이트를 제공하는 경우 소프트웨어 업데이트 동기화 일정을 매일 실행하도록 설정하는 방법이 있습니다.  

> [!NOTE]  
>  소프트웨어 업데이트 동기화 일정을 사용하도록 설정하지 않는 경우 소프트웨어 라이브러리 작업 영역의 **모든 소프트웨어 업데이트** 또는 **소프트웨어 업데이트 그룹** 노드에서 수동으로 소프트웨어 업데이트를 동기화할 수 있습니다. 자세한 내용은 [소프트웨어 업데이트 동기화](synchronize-software-updates.md)를 참조하세요.  

## <a name="supersedence-rules"></a>교체 규칙  
 교체 설정은 마법사의 **교체 규칙** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **교체 규칙** 탭에서 구성합니다. 교체 규칙은 최상위 사이트에서만 구성할 수 있습니다.  

 이 페이지에서, 교체된 소프트웨어 업데이트의 즉시 만료를 지정할 수 있습니다. 이렇게 하면 교체된 소프트웨어 업데이트가 새 배포에 포함되지 않으며 교체된 소프트웨어 업데이트에 하나 이상의 만료된 소프트웨어 업데이트가 포함되어 있음을 나타내도록 기존 배포에 플래그를 설정할 수 있습니다. 또는 교체된 소프트웨어 업데이트가 만료되기 전까지의 기간을 지정할 수 있습니다. 이 기간 동안에는 해당 업데이트를 계속 배포할 수 있습니다. 자세한 내용은 [교체 규칙](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)을 참조하세요.  

> [!NOTE]  
>  마법사의 **대체 규칙** 페이지는 사이트의 첫 번째 소프트웨어 업데이트 지점을 구성할 때만 사용할 수 있습니다. 이 페이지는 추가 소프트웨어 업데이트 지점을 설치할 때는 표시되지 않습니다.  

## <a name="classifications"></a>분류  
 분류 설정은 마법사의 **분류** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **분류** 탭에서 구성합니다. 소프트웨어 업데이트 분류에 대한 자세한 내용은 [업데이트 분류](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications)를 참조하세요.  

> [!NOTE]  
>  마법사의 **분류** 페이지는 사이트의 첫 번째 소프트웨어 업데이트 지점을 구성할 때만 사용할 수 있습니다. 이 페이지는 추가 소프트웨어 업데이트 지점을 설치할 때는 표시되지 않습니다.  

> [!TIP]  
>  최상위 사이트에 처음 소프트웨어 업데이트 지점을 설치할 때 모든 소프트웨어 업데이트 분류를 지우십시오. 초기 소프트웨어 업데이트 동기화가 완료된 후 업데이트 목록에서 분류를 구성한 다음 동기화를 다시 시작합니다. 이 설정은 최상위 사이트의 소프트웨어 업데이트 지점에만 구성됩니다.  

## <a name="products"></a>제품  
 제품 설정은 마법사의 **제품** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **제품** 탭에서 구성합니다.  

> [!NOTE]  
>  마법사의 **제품** 페이지는 사이트의 첫 번째 소프트웨어 업데이트 지점을 구성할 때만 사용할 수 있습니다. 이 페이지는 추가 소프트웨어 업데이트 지점을 설치할 때는 표시되지 않습니다.  

> [!TIP]  
>  최상위 사이트에 처음 소프트웨어 업데이트 지점을 설치할 때 모든 제품을 지우십시오. 초기 소프트웨어 업데이트 동기화가 완료된 후 업데이트 목록에서 제품을 구성한 다음 동기화를 다시 시작합니다. 이 설정은 최상위 사이트의 소프트웨어 업데이트 지점에만 구성됩니다.  

## <a name="languages"></a>언어  
 언어 설정은 마법사의 **언어** 페이지 또는 소프트웨어 업데이트 지점 구성 요소 속성의 **언어** 탭에서 구성합니다. 소프트웨어 업데이트 파일 및 요약 정보를 동기화하려는 언어를 지정하세요. **소프트웨어 업데이트 파일** 설정은 Configuration Manager 계층 구조의 각 소프트웨어 업데이트 지점에서 구성됩니다. **요약 정보** 설정은 최상위 소프트웨어 업데이트 지점에서만 구성됩니다. 자세한 내용은 [언어](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages)를 참조하세요.  

> [!NOTE]  
>  마법사의 **언어** 페이지는 중앙 관리 사이트에 소프트웨어 업데이트 지점을 설치할 때만 사용할 수 있습니다. 자식 사이트의 소프트웨어 업데이트 파일 언어는 소프트웨어 업데이트 지점 구성 요소 속성의 **언어** 탭에서 구성할 수 있습니다.  

## <a name="next-steps"></a>다음 단계
Configuration Manager 계층 구조의 최상위 사이트부터 시작하여 소프트웨어 업데이트 지점을 설치했습니다. 하위 사이트에 소프트웨어 업데이트 지점을 설치하려면 이 항목의 절차를 반복합니다.

소프트웨어 업데이트 지점을 설치했으면 [소프트웨어 업데이트 동기화](synchronize-software-updates.md)로 이동합니다.
