---
title: "System Center Configuration Manager 개인정보취급방침 – Configuration Manager Cmdlet 라이브러리"
description: "Microsoft에서 System Center Configuration Manager Cmdlet 라이브러리와 관련된 데이터를 수집하고 사용하는 방법을 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 개인정보취급방침 – Configuration Manager Cmdlet 라이브러리

*적용 대상: System Center Configuration Manager(현재 분기)*

이 개인 정보 취급 방침에서는 System Center Configuration Manager Cmdlet 라이브러리에 대한 기능을 다룹니다.  

## <a name="usage-data"></a>사용 현황 데이터  
 **이 기능의 용도:**   
System Center Configuration Manager Cmdlet 라이브러리를 사용하면 Windows PowerShell cmdlet 및 스크립트를 사용하여 Configuration Manager 계층 구조를 관리할 수 있습니다. Cmdlet 라이브러리는 경향과 사용 패턴을 식별하기 위해 라이브러리에 포함된 cmdlet의 사용 방법에 대한 정보를 수집합니다.  또한 Cmdlet 라이브러리는 cmdlet을 사용하는 동안 발생하는 오류의 유형과 개수를 수집합니다.  

 **정보 수집, 처리 또는 전송:**   
수집되는 사용 현황 데이터에는 cmdlet의 시작, 중지 및 종료, 사용되지 않는 cmdlet의 실행 및 cmdlet과 관련된 SMS 공급자 작업에 대한 활동 메트릭이 포함됩니다. 이 정보는 개인적으로 식별할 수 없습니다.  수집되는 오류 정보에는 cmdlet에서 반환하는 오류와 예외 오류에 대한 오류 세부 정보가 포함됩니다. 일부 오류 세부 정보 보고서에는 컴퓨터에 연결된 장치에 대한 일련 번호와 같은 개별 식별자가 의도하지 않게 포함될 수도 있습니다. Cmdlet 라이브러리는 오류 보고서에 포함된 정보를 필터링하고 익명으로 처리하여 개인 식별자를 제거한 후에 Microsoft에 전송합니다.  

 **정보의 사용:**   
이 정보는 Microsoft에서 제공하는 제품과 서비스의 품질, 보안 및 무결성을 향상하기 위해 사용됩니다.  

 **선택/제어:**   
이 사용 현황 데이터 기능은 기본적으로 사용하도록 설정됩니다. System Center Configuration Manager Cmdlet 라이브러리에는 이 기능을 제어하기 위한 두 개의 레지스트리 키가 포함되어 있습니다.  

 완전히 옵트아웃하려면 이 두 개의 레지스트리 키 값을 설정해야 합니다. ETW(Windows용 이벤트 추적) 공급자 각각에 대해 하나씩입니다.  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0(드라이브 공급자에 대한 사용 현황 데이터 옵트아웃)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0(cmdlet에 대한 사용 현황 데이터 옵트아웃)  

 사용 현황 데이터 설정에 대한 변경은 변경이 수행된 컴퓨터에서만 할 수 있습니다.  

 사용 현황 데이터(컬렉션)를 구성하는 방법에 대한 자세한 내용은 [System Center Configuration Manager Cmdlet 라이브러리 설명서](https://technet.microsoft.com/en-us/library/dn958404.aspx)를 참조하세요.  

## <a name="update-check"></a>업데이트 확인  
 **이 기능의 용도:**   
System Center Configuration Manager Cmdlet 라이브러리는 매일 라이브러리 업데이트를 자동으로 확인하고 사용자에게 업데이트된 라이브러리를 다운로드하도록 알립니다.  

 **정보 수집, 처리 또는 전송:**   
Cmdlet 라이브러리 업데이트 확인을 수행하면 버전 확인을 위해 Microsoft 다운로드 센터에서 작은 텍스트 파일을 다운로드합니다.   이 파일은 로컬에 저장되지 않습니다.  Cmdlet 라이브러리는 자동으로 소프트웨어를 업그레이드하지 않습니다.  

 **정보의 사용:**   
이 정보는 Microsoft에서 제공하는 제품과 서비스의 품질, 보안 및 무결성을 향상하기 위해 사용됩니다.  

 **선택/제어:**   
업데이트 확인은 기본적으로 사용하도록 설정됩니다.  System Center Configuration Manager Cmdlet 라이브러리에는 업데이트 알림 기능을 제어하기 위해 이러한 cmdlet이 포함되어 있습니다.  

-   `Get-CMCmdletUpdateCheck` 은(는) 업데이트 기능 구성을 가져오고, 사용자 정책이 시스템 정책에 의해 재정의되는지 표시합니다.  

-   `Send-CMCmdletUpdateCheck` 을(를) 사용하면 예약되지 않은 업데이트 확인을 수행할 수 있습니다. 예약되지 않은 확인에서는 정책 설정이 고려되지 않습니다.  

-   `Set-CMCmdletUpdateCheck` 은(는) 사용자별 또는 시스템별로 업데이트 확인 설정을 구성합니다. 시스템 설정을 구성하려면 관리자 권한으로 실행해야 합니다.  

 업데이트 확인 구성에 대한 자세한 내용은 [System Center Configuration Manager Cmdlet 라이브러리 설명서](https://technet.microsoft.com/en-us/library/dn958404.aspx)에서 확인할 수 있습니다.  



<!--HONumber=Nov16_HO1-->

