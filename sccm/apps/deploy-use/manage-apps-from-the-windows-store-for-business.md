---
title: "비즈니스용 Windows 스토어에서 앱 관리 | System Center Configuration Manager"
description: "System Center Configuration Manager를 사용하여 비즈니스용 Windows 스토어에서 앱을 관리 및 배포합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>System Center Configuration Manager를 사용하여 비즈니스용 Windows 스토어에서 앱 관리

*적용 대상: System Center Configuration Manager(현재 분기)*

[비즈니스용 Windows 스토어](https://www.microsoft.com/business-store)에서 조직을 위한 Windows 앱을 찾아서 개별적으로 또는 대량으로 구매할 수 있습니다. 저장소를 Configuration Manager에 연결하면 구입한 앱 목록을 Configuration Manager와 동기화하고 Configuration Manager 콘솔에서 해당 앱을 보고 다른 앱처럼 배포할 수 있습니다.


## <a name="online-and-offline-apps"></a>온라인 및 오프라인 앱

비즈니스용 Windows 스토어에서는 다음 두 가지 유형의 앱을 지원합니다.

- **온라인** - 이 라이선스 유형에서는 사용자와 장치가 저장소에 연결하여 앱과 해당 라이선스를 가져와야 합니다. Windows 10 장치는 Azure Active Directory 도메인에 가입된 장치여야 합니다.
- **오프라인** - 조직에서 저장소에 연결하거나 인터넷에 연결하지 않고도 앱과 라이선스를 캐시하여 온-프레미스 네트워크 내에 직접 배포할 수 있습니다.

비즈니스용 Windows 스토어에 대해 [자세히 알아보세요](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager에서는 Configuration Manager 클라이언트를 실행하는 Windows 10 장치 및 Microsoft Intune에 등록된 Windows 10 장치(하이브리드 구성이라고 함) 둘 다에서 비즈니스용 Windows 스토어 앱 관리를 지원합니다. Configuration Manager는 온라인 및 오프라인 앱에 대해 다음과 같은 기능을 제공합니다.

> [!IMPORTANT]
> 이 기능을 사용하려면 Windows 10 장치에서 2015년 11월(1511) 릴리스 이상을 실행해야 합니다.

|기능|오프라인 앱|온라인 앱|
|------------|------------|------------|
|Configuration Manager에 앱 데이터 동기화<br>(24시간마다 동기화 발생)|예|예|
|스토어 앱에서 Configuration Manager 응용 프로그램 만들기|예|예|
|스토어에서 무료 앱 지원|예|예|
|스토어에서 유료 앱 지원|아니요|아니요|
|사용자 또는 장치 컬렉션에 대한 필수 배포 지원|예|예<sup>1</sup>|
|사용자 또는 장치 컬렉션에 대한 사용 가능한 배포 지원|예<sup>3</sup>|아니요<sup>2</sup>|

<sup>1</sup>Intune에서 관리하는 장치만 지원합니다. Configuration Manager 콘솔에서 온라인 응용 프로그램을 만들어 Configuration Manager 클라이언트에서 관리하는 장치에 배포하는 작업이 차단되지는 않지만 이 기능은 작동하지 않습니다. 최종 사용자는 앱 스토어의 관련 페이지로 이동되며, 여기서 수동으로 앱을 설치해야 합니다.

<sup>2</sup>온라인 앱은 Configuration Manager 클라이언트에서 관리하는 장치에 대해서만 사용자 또는 장치 컬렉션에 사용 가능한 앱으로 배포할 수 있지만 최종 사용자가 소프트웨어 센터에서 앱을 선택할 경우 비즈니스용 Windows 스토어로 이동되며, 여기서 수동으로 앱을 설치해야 합니다. Microsoft Intune에 등록된 장치에 대한 사용 가능한 배포는 지원되지 않습니다.

<sup>3</sup>Intune에서 관리하는 장치에 대해서는 지원되지 않습니다.

> [!IMPORTANT]
> 이 릴리스에서는 중앙 관리 사이트와 하나 이상의 기본 사이트를 포함하는 Configuration Manager 계층 구조가 있을 경우 Intune에서 관리하는 장치에 오프라인 비즈니스용 Windows 스토어 앱을 배포하려고 하면 실패합니다.


## <a name="activate-the-windows-store-for-business-capability"></a>비즈니스용 Windows 스토어 기능 활성화
시험판 기능이므로 Configuration Manager를 비즈니스용 Windows 스토어에 연결하려면 먼저 다음 단계를 수행해야 합니다.

**시험판 기능 사용에 동의**
1. Configuration Manager 콘솔의 **관리** 작업 영역에서 **사이트 구성** > **사이트**를 클릭합니다.
2. 계층 구조의 최상위 사이트를 선택하고 **계층 설정**을 엽니다.
3. **계층 설정 속성** 대화 상자에서 **시험판 기능 사용 동의** 확인란을 선택합니다.
4. **확인**을 클릭합니다.

**비즈니스용 Windows 스토어 기능 활성화**
1. Configuration Manager 콘솔의 **관리** 작업 영역에서 **클라우드 서비스** > **업데이트 및 서비스** > **기능**을 클릭합니다.
2. **비즈니스용 Windows 스토어 통합**을 선택한 다음 **홈** 탭의 **기능** 그룹에서 **켜기**를 클릭합니다.
3. Configuration Manager 콘솔을 닫았다가 다시 엽니다.
4. 이제 **관리** 작업 영역의 **클라우드 서비스** 아래에 **비즈니스용 Windows 스토어** 노드가 표시됩니다.

## <a name="set-up-windows-store-for-business-synchronization"></a>비즈니스용 Windows 스토어 동기화 설정

**Azure Active Directory에서 Configuration Manager를 "웹 응용 프로그램 및/또는 웹 API" 관리 도구로 등록합니다. 이렇게 하면 나중에 필요한 클라이언트 ID가 제공됩니다.**
1. [https://manage.windowsazure.com](https://manage.windowsazure.com)의 Active Directory 노드에서 Azure Active Directory를 선택한 후 **응용 프로그램** > **추가**를 클릭합니다.
2.  **조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.
3.  응용 프로그램의 이름을 입력하고, **웹 응용 프로그램** 및/또는 **웹 API**를 선택한 후 **다음** 화살표를 클릭합니다.
4.  **로그온 URL** 및 **앱 ID URI** 모두에 대해 동일한 URL을 입력합니다. URL은 어떤 문자열이든 될 수 있으며, 실제 주소로 확인할 필요는 없습니다. 예를 들어 *https://yourdomain/sccm*을 입력할 수 있습니다.
5.  마법사를 완료합니다.

**Azure Active Directory에서 등록된 관리 도구에 대한 클라이언트 키를 만듭니다.**
1.  방금 만든 응용 프로그램을 강조 표시하고 **구성**을 클릭합니다.
2.  **키** 아래의 목록에서 기간을 선택하고 **저장**을 클릭합니다. 그러면 새 클라이언트 키가 생성됩니다. 비즈니스용 Windows 스토어를 Configuration Manager에 성공적으로 등록할 때까지 이 페이지에서 이동하지 마세요.

**비즈니스용 Windows 스토어에서 Configuration Manager를 저장소 관리 도구로 구성**
1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)를 열고 메시지가 표시되면 로그인합니다.
2.  필요한 경우 사용 약관에 동의합니다.
3.  **관리 도구**에서 **관리 도구 추가**를 클릭합니다.
4.  **이름별 도구 검색**에서 이전에 AAD에서 만든 응용 프로그램의 이름을 입력한 후 **추가**를 클릭합니다.
5.  방금 가져온 응용 프로그램 옆에 있는 **활성화**를 클릭합니다.
6.  오프라인 사용이 허가된 앱을 구매할 수 있도록 허용하려면 **관리 > 계정 정보** 페이지에서 **오프라인 사용이 허가된 앱 표시**를 선택합니다.

**Configuration Manager에 스토어 계정 추가**

1. 비즈니스용 Windows 스토어에서 앱을 하나 이상 구매했는지 확인합니다. Configuration Manager 콘솔의 **관리** 작업 영역에서 **클라우드 서비스**를 확장하고 **비즈니스용 Windows 스토어**를 클릭합니다.
2.  **홈** 탭의 **비즈니스용 Windows 스토어** 그룹에서 **비즈니스용 Windows 스토어 계정 추가**를 클릭합니다.
3.  Azure Active Directory의 테넌트 ID, 클라이언트 ID 및 클라이언트 키를 추가한 후 마법사를 완료합니다.
4. 완료한 후에는 Configuration Manager 콘솔의 **비즈니스용 Windows 스토어** 목록에서 구성한 계정이 표시됩니다.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>비즈니스용 Windows 스토어 앱에서 Configuration Manager 응용 프로그램을 만들고 배포합니다.
1.  Configuration Manager 콘솔의 **소프트웨어 라이브러리** 작업 영역에서 **응용 프로그램 관리**를 확장한 다음 **스토어 앱에 대한 라이선스 정보**를 클릭합니다.
2.  배포하려는 앱을 선택한 후 **홈** 탭의 **만들기** 그룹에서 **응용 프로그램 만들기**를 클릭합니다.
비즈니스용 Windows 스토어 앱을 포함하여 Configuration Manager 응용 프로그램이 만들어집니다. 그런 다음 이 응용 프로그램을 원하는 Configuration Manager 응용 프로그램으로 배포 및 모니터링할 수 있습니다.

> [!IMPORTANT]
> Intune에 등록된 장치의 경우 원래 장치를 등록한 사용자만 배포된 앱을 사용할 수 있습니다. 다른 사용자는 앱에 액세스할 수 없습니다.

## <a name="monitor-windows-store-for-business-apps"></a>비즈니스용 Windows 스토어 앱 모니터링

**소프트웨어 라이브러리** 작업 영역에서 **응용 프로그램 관리**를 확장한 다음 **스토어 앱에 대한 라이선스 정보**를 클릭합니다.

앱 이름, 플랫폼, 소유한 앱의 라이선스 수, 사용할 수 있는 라이선스 수 등을 포함하여 관리하는 각 스토어 앱에 대한 앱 정보를 볼 수 있습니다.



<!--HONumber=Nov16_HO1-->

