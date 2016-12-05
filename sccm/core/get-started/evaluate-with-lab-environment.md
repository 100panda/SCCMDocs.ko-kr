---
title: "고유한 랩 환경을 구축하여 System Center Configuration Manager 평가"
description: "조직에서 사용할 System Center Configuration Manager를 평가하는 랩 환경을 만듭니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 363e6a929b72e027d5fff7584905fb552dc695b0


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>고유한 랩 환경을 구축하여 System Center Configuration Manager 평가

*적용 대상: System Center Configuration Manager(현재 분기)*

조직에서 사용할 System Center Configuration Manager를 평가하는 랩 환경을 만드는 방법에 알아봅니다.  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>고유한 랩 환경을 구축하여 System Center Configuration Manager 평가  
 System Center Configuration Manager는 사용자, 장치 및 소프트웨어를 관리하는 복잡하고 강력한 도구입니다. 개념적 이해를 바탕으로 실무 연습을 진행할 수 있도록 전체 배포 전에 System Center Configuration Manager에 대한 철저한 평가를 완료하는 것이 좋습니다.  

 이 가이드는 주로 기업 환경에서 Configuration Manager의 사용을 평가하는 관리자를 위해 작성되었습니다.  

-   PC, 서버 및 모바일 장치를 완전하게 관리하기 위한 솔루션을 원하는 관리자  

-   클라우드 기반 장치 관리의 유연성과 더불어 온-프레미스 장치 관리를 위한 보안이 요구되는 높은 수준의 보안 분야에서 일하는 관리자  

-   온-프레미스 서버 아키텍처의 수직 확장을 관리하려는 관리자  

### <a name="what-this-lab-does"></a>이 랩에서 수행하는 작업  
 이 환경을 만드는 기본 목표는 Configuration Manager로 작업을 시작하고 수행을 통해 Configuration Manager에 대한 이해를 향상시키기 위한 일반 지식을 제공하는 것입니다. 이 작업은 다음 두 서버를 사용하여 현재 버전의 긴급 Configuration Manager 어셈블리를 통해 수행됩니다.  

-   Active Directory, 도메인 컨트롤러 및 DNS 서버를 호스트하는 서버  

-   두 번째 호스팅 Configuration Manager 및 모든 관련된 SQL Server 구성 요소  

-   클라이언트 컴퓨터는 Hyper-V 내에서 설치됩니다. 랩 자체를 단일 서버의 완전 가상화 시스템으로 실행할 수도 있습니다.  

### <a name="what-this-lab-does-not-do"></a>이 랩에서 수행하지 않는 작업  
 이 랩에서 모든 Configuration Manager 시나리오를 설명하지는 않으며 활성 환경으로 즉시 마이그레이션할 수 있도록 설계되지도 않았습니다.  

 이 랩을 구축하면 작업할 수 있는 기능 환경이 구현되게 됩니다. 그러나 이 환경은 시스템 성능, 하드 디스크 공간 관리, SQL Server 저장소 등에 맞게 최적화되지는 않습니다.  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> 랩 시작 전에 읽어보면 좋은 자료  
 [System Center Configuration Manager에 대한 설명서](http://docs.microsoft.com/sccm/)에는 사용 가능한 풍부한 콘텐츠가 있습니다. 이 라이브러리에는 랩에서 작업하는 모든 관리자가 이러한 연습을 시작하기 전에 읽어보면 좋은 항목들이 포함되어 있어서 선택할 수 있습니다.  

-   [System Center Configuration Manager 소개](../../core/understand/introduction.md)에서 Configuration Manager 콘솔, 최종 사용자 포털 및 예제 시나리오에 대한 핵심 개념을 알아봅니다.  

-   [System Center Configuration Manager의 기능 및 특성](../../core/plan-design/changes/features-and-capabilities.md)에서 Configuration Manager의 기본 관리 기능에 대해 알아봅니다.  

-   [System Center Configuration Manager의 기본 사항](../../core/understand/fundamentals.md)으로 풍부한 지식을 얻습니다.  

-   [System Center Configuration Manager의 역할 기반 관리 기본 사항](../../core/understand/fundamentals-of-role-based-administration.md)에서 보안 역할의 중요성을 알아봅니다.  

-   이러한 [콘텐츠 관리 관련 개념](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts)을 이해하면 콘텐츠 관리와 관련된 특정 개념을 제공할 수 있습니다.  

-   [클라이언트가 System Center Configuration Manager에 대한 사이트 리소스 및 서비스를 찾는 방법 이해](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)를 통해 배포 전체에서 매일 진행하는 작업을 성공적으로 지원할 수 있습니다.  



<!--HONumber=Nov16_HO1-->

