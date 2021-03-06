---
title: "Azure 서비스 마법사 | Microsoft Docs"
description: "System Center Configuration Manager에 대한 Azure 서비스 마법사 정보"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuration Manager에서 사용하도록 Azure 서비스 구성

*적용 대상: System Center Configuration Manager(현재 분기)*

현재 분기 버전 1706부터 **Azure 서비스 마법사**를 사용해서 Configuration Manager에서 사용하도록 Azure 서비스를 구성하는 과정을 단순화할 수 있습니다.

이 마법사는 **Azure Web App**을 사용하는 일반적인 구성 환경을 통해 구독 및 구성 세부 정보를 제공하여 합니다. 이 웹앱을 사용하면 Azure에서 새 Configuration Manager 구성 요소 또는 서비스를 설정할 때마다 같은 정보를 입력하지 않아도 됩니다.

다음과 같은 Azure 서비스는 Azure 서비스 구성 마법사를 사용하여 구성됩니다.
-   **클라우드 관리**   
    [Azure AD(Azure Active Directory)를 사용하여 클라이언트가 인증 받도록 합니다](). [Azure AD 사용자 검색을 구성](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)할 수도 있습니다.
-   **OMS 커넥터**
    [OMS(Operations Manager Suite)에 연결](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)하고 컬렉션과 같은 데이터를 OMS Log Analytics와 동기화합니다.
-   **업그레이드 준비**
    [업그레이드 준비에 연결](/sccm/core/clients/manage/upgrade/upgrade-analytics)하고 클라이언트 업그레이드 호환성 데이터를 확인합니다.
-   **비즈니스용 Windows 스토어** [비즈니스용 Windows 스토어](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)에 대한 온라인 스토어에 연결하고 Configuration Manager에서 배포할 수 있는 조직을 위한 앱을 가져옵니다.

이 마법사를 사용하여 서비스를 구성할 때 몇 가지 일반적인 작업을 사용할 수 있습니다.
여기에는 다음이 포함됩니다.
-   Azure 환경 구성: 마법사의 **앱** 페이지에서 사용하는 **Azure 환경**을 선택합니다. 공용 Azure 클라우드만 지원하는지 또는 사설 클라우드도 지원할 수 있는지 확인하려면 각 서비스에 대한 콘텐츠를 참조하세요.
-   서버 앱 만들기 또는 가져오기: 마법사의 **앱** 페이지에서 Azure Web App을 **만들고** **가져올 수** 있습니다. 사용 가능한 옵션은 구성하는 서비스에 따라 달라집니다.  또한 일부 서비스에는 추가 앱이 필요할 수도 있습니다. 예를 들어 서비스에 **네이티브 클라이언트 앱**이 필요할 수도 있습니다.


Azure Web App에 대한 자세한 내용은 [Azure App Service의 인증 및 권한 부여](/azure/app-service/app-service-authentication-overview) 및 [Web Apps 개요](/azure/app-service-web/app-service-web-overview)를 참조하세요.


## <a name="webapp"></a>Configuration Manager에서 사용하기 위해 Azure Web App 만들기

Azure 서비스 웹앱은 Configuration Manager 사이트를 Azure AD에 연결하며 인프라에서 Azure 서비스를 사용하기 위한 필수 구성 요소입니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1.  Configuration Manager 콘솔의 **관리** 작업 영역에서 **Cloud Services**를 확장한 후 **Azure 서비스**를 클릭합니다.
2.  **홈** 탭의 **Azure 서비스** 그룹에서 **Azure 서비스 구성**을 클릭합니다.
3.  Azure 서비스 마법사의 **Azure 서비스** 페이지에서 **클라우드 관리**를 선택하여 클라이언트가 Azure AD를 사용하여 계층에서 인증을 받도록 합니다.
4.  마법사의 **일반** 페이지에서 Azure 서비스에 대한 이름 및 설명을 지정합니다.
5.  마법사의 **앱** 페이지에 있는 목록에서 Azure 환경을 선택하고 **찾아보기**를 클릭하여 Azure 서비스를 구성하는 데 사용할 *웹앱* 및 *네이티브 클라이언트 앱*을 선택합니다.     
    **웹앱:** 찾아보기를 선택하면 서버 앱 창이 열립니다.    
      **서버 앱** 창에서 사용할 서버 앱을 선택한 다음 **확인**을 클릭합니다. 서버 앱은 테넌트 ID, 클라이언트 ID 및 클라이언트의 비밀 키를 비롯한 Azure 계정에 대한 구성을 포함하는 Azure 웹앱입니다.
    사용 가능한 앱이 없는 경우 다음 중 하나를 사용합니다.
        - **만들기**: 새 서버 앱을 만들려면 **만들기**를 클릭합니다. 다음에는 앱의 이름, 홈페이지 URL, 앱 ID URI 및 비밀 키 유효 기간을 제공합니다. 기본적으로 비밀 키 유효 기간은 1년입니다.

         계속하려면 누군가가 Azure에 로그인하여 Azure에서 웹앱 작성을 완료해야 합니다. Azure에 로그인하는 데 사용하는 계정은 Azure 서비스 마법사를 실행하는 계정과 같을 필요가 없습니다. Azure에 로그인하면 Configuration Manager가 Azure에서 사용자를 위해 웹앱을 만듭니다(웹앱에 사용할 클라이언트 ID 및 비밀 키 포함). 나중에 Azure Portal에서 이러한 내용을 확인할 수 있습니다.

         만들기를 사용하여 웹앱을 구성하면 Configuration Manager가 Azure AD에서 웹앱을 만들 수 있습니다.
        - **가져오기**: Azure 구독에 이미 있는 웹앱을 사용하려면 **가져오기**를 클릭합니다. 앱 및 테넌트의 이름을 입력한 다음 테넌트 ID, 클라이언트 ID 및 Configuration Manager에서 사용하도록 할 Azure 웹앱의 비밀 키를 지정합니다. 정보를 확인한 후에 **확인**을 클릭하여 계속합니다.

          이 옵션을 구성하는 모든 서비스에 대해 사용할 수 있는 것은 아닙니다.

   **네이티브 클라이언트 앱:** 찾아보기를 선택하면 클라이언트 앱 창이 열립니다.  
     **클라이언트 앱** 창에서 사용할 클라이언트 앱을 선택한 다음 **확인**을 클릭합니다.

     사용 가능한 클라이언트 앱이 없는 경우 다음 중 하나를 사용합니다.
     - **만들기**: 새 클라이언트 앱을 만들려면 **만들기**를 클릭합니다. 다음으로 앱의 이름 및 회신 URL을 입력합니다.

          계속하려면 누군가가 Azure에 로그인하여 Azure에서 클라이언트 앱 작성을 완료해야 합니다. Azure에 로그인하는 데 사용하는 계정은 Azure 서비스 마법사를 실행하는 계정과 같을 필요가 없습니다. 그런 다음 Azure에 로그인하면 Configuration Manager가 Azure에서 사용자를 위해 네이티브 클라이언트 앱을 만듭니다(웹앱에 사용할 클라이언트 ID 포함). 나중에 Azure Portal에서 이러한 내용을 확인할 수 있습니다.
          만들기를 사용하여 앱을 구성하면 Configuration Manager가 Azure AD에서 네이티브 클라이언트 앱을 만들 수 있습니다.
     - **가져오기**: Azure 구독에 이미 있는 클라이언트 앱을 사용하려면 **가져오기**를 클릭합니다. 앱 및 클라이언트 ID의 이름을 입력합니다. 그런 후 **확인**을 클릭하여 계속합니다.
           이 옵션을 구성하는 모든 서비스에 대해 사용할 수 있는 것은 아닙니다.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  마법사의 **검색** 페이지에서 **Azure Active Directory 사용자 검색 사용**을 클릭하고 **설정**을 클릭합니다.
**Azure AD 사용자 검색 설정** 대화 상자에서 검색 일정을 구성합니다. 또한 Azure AD에서 새 계정 또는 변경된 계정만 확인하는 델타 검색을 사용하도록 설정할 수도 있습니다. [Azure AD 사용자 검색](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)에 대해 자세히 알아봅니다.
 
 7. 마법사를 완료합니다.

이제 Configuration Manager 사이트가 Azure AD에 연결되었습니다.

## <a name="view-the-configuration-of-an-azure-service"></a>Azure 서비스의 구성 보기
사용하도록 구성한 Azure 서비스의 속성을 볼 수 있습니다.

콘솔에서 **관리** > **개요** > **클라우드 서비스** > **Azure 서비스**로 이동합니다. 다음으로 보거나 편집하려는 서비스를 선택하고 **속성**을 클릭합니다.
