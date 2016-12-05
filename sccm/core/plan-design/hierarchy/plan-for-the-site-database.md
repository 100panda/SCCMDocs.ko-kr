---
title: "사이트 데이터베이스 계획 | System Center Configuration Manager"
description: "System Center Configuration Manager 계층 구조를 계획할 때 사이트 데이터베이스 및 사이트 데이터베이스 서버 역할을 고려하세요."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 40ebfaa9b82a65a6265f0c031dbbd0bcdb85da6e


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>System Center Configuration Manager용 사이트 데이터베이스에 대한 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

사이트 데이터베이스 서버는 Configuration Manager 사이트에 대한 정보를 저장하는 지원되는 Microsoft SQL Server 버전이 실행되는 컴퓨터입니다. Configuration Manager 계층 구조의 각 사이트에는 사이트 데이터베이스를 포함해 사이트 데이터베이스 서버 역할이 할당된 서버가 있습니다.  

-   중앙 관리 사이트 및 기본 사이트의 경우 사이트 서버에 SQL Server를 설치하거나 사이트 서버가 아닌 컴퓨터에 SQL Server를 설치할 수 있습니다.  

-   보조 사이트에서는 전체 SQL Server를 설치하는 대신 SQL Server Express를 사용할 수 있지만 데이터베이스 서버를 보조 사이트 서버에서 실행해야 합니다.  

원격 데이터베이스 서버 컴퓨터를 사용하는 경우 중간 네트워크 연결을 고가용성 및 고대역폭으로 구성해야 합니다. 이는 사이트 서버 및 일부 사이트 시스템 역할은 사이트 데이터베이스를 호스팅하는 SQL Server와 안정적으로 통신해야 하기 때문입니다.  


**원격 데이터베이스 서버 위치를 선택할 경우 다음 사항을 고려하세요.**  

-   데이터베이스 서버와의 통신에 필요한 대역폭 양은 다양한 사이트 및 클라이언트 구성의 조합에 따라 달라지므로 필요한 실제 대역폭은 적절히 예측할 수 없습니다.  

-   SMS 공급자를 실행하고 사이트 데이터베이스에 연결하는 각 컴퓨터로 인해 네트워크 대역폭 요구 사항이 증가됩니다.  

-   SQL Server를 실행하는 컴퓨터는 SMS 공급자를 실행하는 모든 컴퓨터 및 사이트 서버와 양방향 트러스트 관계가 있는 도메인에 배치해야 합니다.  

-   사이트 데이터베이스가 사이트 서버와 함께 배치된 경우 사이트 데이터베이스 서버에 대해 클러스터된 SQL Server를 사용할 수 없습니다.  


일반적으로 사이트 시스템 서버는 단일 Configuration Manager 사이트의 사이트 시스템 역할만 지원하지만 SQL Server를 실행하는 클러스터되거나 클러스터되지 않은 서버에서 SQL Server의 다른 인스턴스를 사용하면 다른 Configuration Manager 사이트의 데이터베이스를 호스트할 수 있습니다. 다른 사이트의 데이터베이스를 지원하려면 SQL Server의 각 인스턴스가 통신에 고유한 포트를 사용하도록 구성해야 합니다.  


**사이트 데이터베이스를 호스트하는 데 다음 SQL Server 구성을 사용할 수 있습니다.**  

-   SQL Server의 기본 인스턴스  

-   SQL Server를 실행하는 단일 컴퓨터의 명명된 인스턴스  

-   SQL Server의 클러스터된 인스턴스의 명명된 인스턴스  

-   SQL Server AlwaysOn 가용성 그룹(1602 버전 이상)


**사이트 데이터베이스에 대한 필수 조건:**  

-   사이트 데이터베이스를 호스트하려면 SQL Server는 [System Center Configuration Manager에 대한 SQL Server 버전 지원](../../../core/plan-design/configs/support-for-sql-server-versions.md)에 자세히 설명되어 있는 요구 사항을 충족해야 합니다.  



<!--HONumber=Nov16_HO1-->

