---
title: "Configuration Manager를 지원하는 하이브리드 MDM의 새로운 기능 | Microsoft 문서"
description: "Configuration Manager를 포함하는 하이브리드 배포에 사용할 수 있는 새 모바일 장치 관리 기능에 대해 알아봅니다."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: "40"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 93609815ab4d93eddb99b8461dda9f4b4bf8058e
ms.sourcegitcommit: 9a6f8e028fb5eb2e752da70f42a5b548339bd8f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2017
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 및 Microsoft Intune을 지원하는 하이브리드 모바일 장치 관리의 새로운 기능

*적용 대상: System Center Configuration Manager(현재 분기)*

이 문서에서는 System Center Configuration Manager 및 Intune을 포함하는 하이브리드 배포에 사용할 수 있는 새 MDM(모바일 장치 관리) 기능에 대한 세부 정보를 제공합니다.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager 버전과 호환성  

 이 문서의 각 섹션에서는 세 가지 범주로 하이브리드 기능이 나열되어 있습니다. 각 범주의 기능과 다양한 Configuration Manager 버전 간의 호환성을 확인하려면 다음 지침을 따르세요.  

|기능 범주|설명|
|-|-|
|**Microsoft Intune의 새로운 기능** | 일반적으로 이 범주 아래에 나열된 모든 기능은 Intune 서비스만 필요하고 Configuration Manager의 추가 기능이 필요하지 않으므로 System Center 2012 R2 Configuration Manager 릴리스를 비롯한 모든 Configuration Manager 릴리스에서 사용할 수 있어야 합니다.|
|**Configuration Manager Technical Preview의 새로운 기능**| 이 범주 아래에 나열된 모든 기능은 지정된 Technical Preview 릴리스에서만 사용할 수 있습니다. 이러한 기능을 시험해보려면 기능 설명에 지정된 기술 미리 보기 버전을 설치해야 합니다. 자세한 내용은 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)를 참조하세요.|
|**Configuration Manager(현재 분기)의 새로운 기능**| 이 범주 아래에 나열된 모든 기능은 지정된 버전의 Configuration Manager(현재 분기)(예: 버전 1511 또는 1602)에서만 사용할 수 있습니다. 하이브리드 배포에 이전 버전의 Configuration Manager를 사용하는 경우 기능 설명에 지정된 Configuration Manager(현재 분기) 버전으로 업그레이드해야 합니다. 자세한 내용은 [System Center Configuration Manager 업그레이드](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)를 참조하세요.|

## <a name="july-2017"></a>2017년 7월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **Android 및 Windows Phone에 대한 지원 알림 종료**

    Android 및 Windows Phone 버전에 대한 지원 종료 새 알림이 추가되었습니다. 자세한 내용은 [알림](#notices)을 참조하세요.



### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능

이전에 Configuration Manager Technical Preview 릴리스에서 사용할 수 있었던 다음 기능을 이제 Intune과 Configuration Manager(현재 분기) 버전 1706을 포함하는 하이브리드 배포에서 사용할 수 있습니다.

- [Entrust 인증 기관에 대한 Entrust 지원](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [새 모바일 응용 프로그램 관리 정책 설정](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Android for Work 공유 구성에 대한 업데이트](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [새 장치 준수 정책 규칙](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Configuration Manager 클라이언트에서 관리되지 않는 Windows 10 장치에 대한 새 구성 설정](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [macOS VPN 프로필에 대한 Cisco(IPsec) 지원](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Android 및 iOS 등록 제한](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>2017년 6월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **MDM 기관 변경**

  Configuration Manager 버전 1610 및 Microsoft Intune 버전 1705부터, Microsoft 지원에 문의하지 않고 기존의 관리 장치를 등록 취소했다가 다시 등록하지 않고도, MDM 기관을 변경할 수 있습니다. 자세한 내용은 [MDM 기관 변경]( /sccm/mdm/deploy-use/change-mdm-authority)을 참조하세요.

- **관리되는 브라우저 및 앱 프록시 통합**

  Intune Managed Browser는 이제 Azure AD 응용 프로그램 프록시 서비스와 통합되어 사용자가 원격으로 작업하는 동안에도 내부 웹 사이트에 액세스할 수 있도록 할 수 있습니다. 브라우저의 사용자는 평소와 같이 사이트 URL를 입력하고 관리되는 브라우저는 응용 프로그램 프록시 웹 게이트웨이를 통해 요청을 라우팅합니다. 자세한 내용은 [관리되는 브라우저 정책을 사용하여 인터넷 액세스 관리](/intune/app-configuration-managed-browser)를 참조하세요.

- **Android용 회사 포털 앱에서 앱 보호 정책에 대해 새로운 최종 사용자 환경 제공**

  고객의 의견에 따라, **회사 콘텐츠 액세스** 단추를 표시하도록 Android용 회사 포털 앱을 수정하고 있습니다. 이러한 작업은 최종 사용자가 Intune 모바일 응용 프로그램 관리의 기능인 앱 보호 정책을 지원하는 앱에만 액세스하면 될 경우 불필요하게 등록 프로세스를 거치지 않도록 하기 위한 것입니다. [앱 UI의 새로운 기능](/intune/whats-new-app-ui) 페이지에서 이러한 변경 내용을 확인할 수 있습니다.

- **회사 포털을 쉽게 제거하기 위한 새 메뉴 작업**

  사용자의 의견에 따라 Android용 회사 포털 앱에는 장치에서 회사 포털 제거를 시작하기 위한 새 메뉴 작업이 추가되었습니다. 이 작업은 사용자가 장치에서 앱을 제거할 수 있도록 Intune 관리에서 장치를 제거합니다. 이러한 변경 내용은 [앱 UI의 새로운 기능](/intune/whats-new-app-ui) 페이지 및 [Android 최종 사용자 설명서](/intune-user-help/unenroll-your-device-from-intune-android)에서 확인할 수 있습니다.

- **Windows 10 크리에이터스 업데이트와의 앱 동기화 개선**

  이제 Windows 10용 회사 포털 앱에서는 Windows 10 크리에이터스 업데이트(버전 1703)와의 장치에 대한 앱 설치 요청 동기화가 자동으로 시작됩니다. 따라서 “동기화 보류 중” 상태일 때 앱 설치가 중단되는 문제가 줄어듭니다. 사용자는 앱 내에서 수동으로 동기화를 시작할 수도 있습니다. [앱 UI의 새로운 기능](/intune/whats-new-app-ui) 페이지에서 이러한 변경 내용을 확인할 수 있습니다.

- **Windows 10 회사 포털에 대한 새로운 단계별 환경**

  Windows 10용 회사 포털 앱에 식별되거나 등록되지 않은 장치에 대한 단계별 Intune 연습 환경이 포함됩니다. 이 새로운 환경은 Azure Active Directory에 등록(조건부 액세스 기능에 필요)하고 MDM 등록(장치 관리 기능에 필요)을 진행하는 과정을 안내하는 단계별 지침을 제공합니다. 이 단계별 안내 환경은 회사 포털 홈페이지에서 액세스할 수 있습니다. 사용자는 이러한 등록을 완료하지 않아도 앱을 계속 사용할 수 있지만 제한된 기능만 사용할 수 있습니다.

  이 업데이트는 Windows 10 1주년 업데이트(빌드 1607) 이상을 실행하는 장치에서만 볼 수 있습니다. [앱 UI의 새로운 기능](/intune/whats-new-app-ui) 페이지에서 이러한 변경 내용을 확인할 수 있습니다.

- **iOS용 회사 포털 앱의 앱 타일 기능 개선**

  회사 포털에 대해 설정한 브랜딩 색에 맞게 홈페이지의 앱 타일 디자인이 업데이트되었습니다. 자세한 내용은 [앱 UI의 새로운 기능](/intune/whats-new-app-ui)을 참조하세요.

- **iOS용 회사 포털 앱에서 계정 선택 기능 사용 가능**

  iOS 장치 사용자는 회사 또는 학교 계정을 사용하여 다른 Microsoft 앱에 로그인한 상태에서 회사 포털에 로그인할 때 새 계정 선택 기능을 사용할 수 있습니다. 자세한 내용은 [앱 UI의 새로운 기능](/intune/whats-new-app-ui)을 참조하세요.

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706의 새로운 기능

- **새 모바일 응용 프로그램 관리 정책 설정**    

  이제 다음 MAM(모바일 응용 프로그램 관리) 정책 설정을 사용할 수 있습니다.

  - **화면 캡처 차단(Android 장치만 해당):** 이 앱을 사용할 때 장치의 화면 캡처 기능을 차단하도록 지정합니다.
  - **연락처 동기화 사용 안 함:** 앱에서 장치의 네이티브 연락처 앱에 데이터를 저장하는 것을 방지합니다.
  - **인쇄 사용 안 함:** 앱에서 회사 또는 학교 데이터를 인쇄하는 것을 방지합니다.

  새로운 앱 보호 정책 설정을 사용하려면 [Configuration Manager에서 앱 보호 정책을 사용하여 앱 보호](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)를 참조하세요.

- **새 Windows 구성 항목 설정**  <!-- 1354715 -->    

  새 Windows 구성 항목은 암호, 장치, 저장소 및 Microsoft Edge 설정 범주에 사용할 수 있습니다. 자세한 내용은 [새 Windows 구성 항목 설정](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)을 참조하세요.

- **새 장치 준수 정책 규칙**    

  이전에는 Intune 독립 실행형에서만 사용할 수 있었던 준수 정책에 대해 새 옵션을 구성할 수 있습니다. 자세한 내용은 [향상된 장치 준수 정책](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)을 참조하세요.

- **Android 및 iOS 등록 제한** <!-- 1290826 -->      

  관리자는 이제 사용자가 하이브리드 환경에서 개인 Android 또는 iOS 장치를 등록할 수 었도록 지정할 수 있습니다. 이렇게 하면 등록된 장치를 미리 선언된 회사 소유 장치 또는 장치 등록 프로그램에 등록된 iOS 장치로만 제한할 수 있습니다. 자세한 내용은 [Android 및 iOS 등록 제한](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)을 참조하세요.

- **Entrust 인증 기관에 대한 지원** <!-- 1350740 -->     

  Configuration Manager는 이제 Entrust 인증 기관을 지원합니다. 따라서 Microsoft Intune에 등록된 장치에 PFX 인증서를 전달할 수 있습니다.    

  Configuration Manager에서 인증서 등록 지점 역할을 추가할 때 Entrust를 인증 기관으로 구성할 수 있습니다. PFX 인증서를 발급하는 새 인증서 프로필을 추가할 때는 Microsoft 또는 Entrust 인증 기관을 선택할 수 있습니다.

  **알려진 문제**: 1706 Technical Preview에서는 PFX 인증서가 Microsoft 인증 기관에 대해 발급되지 않습니다. 이러한 문제는 가져온 PFX 인증서 또는 SCEP 프로필에는 영향을 주지 않습니다.

- **macOS VPN 프로필에 대한 Cisco(IPSec) 지원**  <!-- 1321367 -->    

  연결 유형으로 Cisco(IPsec)를 사용하여 macOS VPN 프로필을 만들 수 있습니다. 자세한 내용은 [VPN 프로필 만들기](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)를 참조하세요.


## <a name="april-2017"></a>2017년 4월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **Managed Browser에 사용 가능한 MyApps**

  이제 Managed Browser에서 Microsoft MyApps의 지원이 향상되었습니다. 관리를 목표로 하지 않는 Managed Browser 사용자가 MyApps 서비스로 직접 연결되므로, 여기에서 관리 프로비저닝된 SaaS 앱에 액세스할 수 있습니다. Intune 관리를 목표로 하는 사용자는 기본 제공되는 Managed Browser 책갈피에서 MyApps에 계속 액세스할 수 있습니다.

- **Managed Browser 및 회사 포털의 새 아이콘**

  Managed Browser는 앱의 Android 및 iOS 버전 모두에서 업데이트된 아이콘을 받습니다. Enterprise Mobility + Security(EM+S)의 다른 앱과 더욱 일관되도록 새 아이콘에는 업데이트된 Intune 배지가 포함됩니다. [Intune 앱 UI 페이지](/intune/whats-new/whats-new-in-intune-app-ui.md)에서 Managed Browser의 새 아이콘을 볼 수 있습니다.

  회사 포털에서는 EM + S에 있는 다른 앱과의 일관성을 향상시키기 위해 Android, iOS 및 Windows 버전의 앱에 대한 업데이트된 아이콘도 받습니다. 이러한 아이콘은 4월부터 5월 말까지 점진적으로 전체 플랫폼에 릴리스됩니다.

- **Android 회사 포털의 로그인 진행률 표시기**

  Android 회사 포털 앱 업데이트에서는 사용자가 앱을 시작하거나 다시 시작할 때 로그인 진행률 표시기를 보여 줍니다. 사용자가 앱에 액세스하도록 허용하기 전에 표시기가 “연결 중...”, “로그인 중...”, “보안 요구 사항 확인 중...”과 같이 새로운 상태로 진행됩니다. [Intune 앱 UI의 새로운 기능 페이지](/intune/whats-new/whats-new-in-intune-app-ui.md)에서 Android용 회사 포털 앱의 새 화면이 표시됩니다.

- **앱이 SharePoint Online에 액세스하지 못하게 차단**

  이제 앱 보호 정책이 적용되지 않은 앱이 [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online)에 액세스하지 못하게 차단하는 앱 기반 조건부 액세스 정책을 만들 수 있습니다. 앱 기반 조건부 액세스 시나리오에서 Azure 포털을 사용하여 SharePoint Online에 액세스하게 할 앱을 지정할 수 있습니다.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704의 새로운 기능

- **앱 구성 정책을 사용하여 Android 앱 구성**

  System Center Configuration Manager(Configuration Manager)에서 앱 구성 정책을 사용하여 사용자가 Android for Work 장치에서 앱을 실행할 때 미리 구성된 설정을 배포할 수 있습니다. Android 앱 구성 정책은 Android for Work를 실행 중인 장치에서만 사용 가능하며 Play for Work 스토어의 승인된 앱에 적용됩니다. 이 기능을 사용해 보는 방법에 대한 자세한 내용은 [앱 구성 정책을 사용하여 Android 앱 구성](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)을 참조하세요.

## <a name="march-2017"></a>2017년 3월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **Android용 회사 포털 앱의 새 사용자 환경**

  Android용 회사 포털 앱의 사용자 인터페이스의 모양과 느낌이 더욱 세련되어집니다. 중요한 업데이트는 다음과 같습니다.

  - 색: 회사 포털 탭 헤더의 색을 IT에서 정의하는 브랜딩에서 지정합니다.
  - 앱: **앱** 탭에서 **추천 앱** 및 **모든 앱** 단추가 업데이트되었습니다.
  - 검색: **앱** 탭에서 **검색** 단추는 부동 작업 단추입니다.
  - 앱 탐색: **모든 앱** 뷰는 쉽게 탐색할 수 있도록 **추천**, **전체** 및 **범주** 탭으로 구분된 뷰를 표시합니다.
  - 지원: **내 장치** 및 **IT 담당자** 탭이 가독성을 높이기 위해 업데이트되었습니다.

  이러한 변경 사항에 자세한 내용은 [Intune 최종 사용자 앱 UI 업데이트](/intune/whats-new/whats-new-in-intune-app-ui)를 참조하세요.

- **Windows 10 회사 포털용 서명 스크립트**

  Windows 10 회사 포털 앱을 다운로드하고 사이드로드해야 하는 경우 이제 스크립트를 사용하여 조직의 앱 서명 프로세스를 간소화할 수 있습니다.  스크립트와 스크립트 사용 지침을 다운로드하려면 TechNet 갤러리의 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)(Windows 10 회사 포털용 Microsoft Intune 서명 스크립트)을 참조하세요. 이 알림에 대한 자세한 내용은 Intune 지원 팀 블로그의 [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)(Windows 10 회사 포털 앱 업데이트)을 참조하세요.

- **중국에 있는 Android 사용자에 대한 지원 향상**

  중국에는 Google Play 스토어가 없으므로 Android 장치 사용자는 중국 마켓플레이스에서 앱을 다운로드해야 합니다. 회사 포털에서는 중국의 Android 사용자가 로컬 앱 스토어에서 회사 포털 및 Outlook 앱을 다운로드하도록 리디렉션하여 이 워크플로 지원합니다. 따라서 모바일 장치 관리 및 모바일 응용 프로그램 관리 모두에서 조건부 액세스 정책을 사용하도록 설정하는 경우 사용자 환경이 개선됩니다. 다음과 같은 중국 앱 스토어에서 Android용 회사 포털 및 Outlook 앱을 사용할 수 있습니다.

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **회사 포털 앱을 최신 상태로 유지**

  2016년 12월에 사용자가 iOS, Android, Windows 8.1 이상 또는 Windows Phone 8.1 이상 장치를 등록할 때 사용자 그룹에 대해 MFA(다단계 인증)를 적용할 수 있도록 하는 업데이트가 출시되었습니다. 회사 포털 앱의 특정 기준 버전(Android: v5.0.3419.0 이상 및 iOS: v2.1.17 이상)이 없으면 이 기능이 작동되지 않습니다.

  Intune의 관리 기능을 지속적으로 개선되고 있으며 여러 개선 사항이 지원되는 모든 플랫폼의 회사 포털 앱에 대한 업데이트로 제공됩니다. 따라서 장치에서 Intune의 개선 사항을 활용하고 사용자 환경을 최적화하려면 최신 버전의 회사 포털 앱을 설치하는 것이 좋습니다.

  >[!Tip]
  > 사용자에게 해당 앱 스토어에서 앱을 자동으로 업데이트하도록 장치를 설정하게 하세요. Android 회사 포털 앱은 네트워크 공유에서 사용할 수 있게 한 경우 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=49140)에서 최신 버전을 다운로드할 수 있습니다.

- **iOS 및 Android에서 MAM에 Microsoft Teams를 사용할 수 있음**

  이제 Intune MAM(모바일 응용 프로그램 관리) 기능에 iOS 및 Android용 Microsoft Teams 앱을 사용할 수 있으므로 팀이 여러 장치에서 자유롭게 작업할 수 있도록 하고 언제 어디에서나 대화 및 회사 데이터를 보호할 수 있습니다. 자세한 내용은 Enterprise Mobility + Security 블로그에서 [Microsoft Teams announcement](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)(Microsoft Teams 알림)를 참조하세요.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703의 새로운 기능

- **Apple Volume Purchase Program 시나리오에 대한 추가 지원**

   Technical Preview 1703부터 이제 다음과 같은 VPP(Volume Purchase Program) 시나리오가 지원됩니다.

   - 장치 라이선스 - 장치 라이선스를 지원하고 장치 컬렉션에 배포되는 앱은 이제 장치당 라이선스가 하나만 있으면 됩니다.  이전에는 장치의 각 사용자에 대해 라이선스를 사용해야 했습니다. 자세한 내용은 [장치 컬렉션에 대량 구매한 iOS 앱 배포](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)를 참조하세요.
   - 두 토큰이 모두 VPP 앱 관리에 사용되는 단일 하이브리드 테넌트에 여러 VPP 토큰을 사용합니다.
   - 비즈니스 토큰과 교육 토큰을 구분하는 기능으로 VPP 교육 토큰을 사용합니다.

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능

이전에 Configuration Manager Technical Preview 릴리스에서 사용할 수 있었던 다음 기능을 이제 Intune과 Configuration Manager(현재 분기) 버전 1702를 포함하는 하이브리드 배포에서 사용할 수 있습니다.

- [Android for Work 지원](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [비규격 앱 준수 설정](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 인증서 만들기 및 배포와 S/MIME 지원](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android 및 iOS 버전은 하이브리드 MDM 만들기 마법사에서 대상 지정이 가능하지 않음](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Configuration Manager(현재 분기)의 버전 1702에는 다음과 같은 추가 하이브리드 기능도 포함되어 있습니다.

- **Apple VPP(Volume Purchase Program)에 대한 향상된 지원**

  - 이제 사용이 허가된 앱을 사용자 및 장치에 배포할 수 있습니다. 장치 라이선스를 지원하는 앱 기능에 따라 앱 배포 시 다음과 같이 적절한 라이선스가 청구됩니다.

    | Configuration Manager 버전 | 앱이 장치 라이선싱을 지원하나요? | 배포 컬렉션 유형 | 청구된 라이선스 |
    |-|-|-|-|
    |1702 이전|예|사용자|사용자 라이선스|
    |1702 이전|아니요|사용자|사용자 라이선스|
    |1702 이전|예|장치|사용자 라이선스|
    |1702 이전|아니요|장치|사용자 라이선스|
    |1702 이상|예|사용자|사용자 라이선스|
    |1702 이상|아니요|사용자|사용자 라이선스|
    |1702 이상|예|장치|장치 라이선스|
    |1702 이상|아니요|장치|사용자 라이선스|

  - 이제 교육용 iOS Volume Purchase Program에서 구매한 앱을 배포하고 추적할 수도 있습니다.

  - 이제 여러 Apple Volume Purchase Program 토큰을 Configuration Manager와 연결할 수 있습니다.

  대량 구매한 iOS 앱에 대한 자세한 내용은 [대량 구매한 iOS 앱 관리](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)를 참조하세요.

- **비즈니스용 Windows 스토어의 기간 업무 앱 지원**

  이제 비즈니스용 Windows 스토어에서 사용자 지정 기간 업무 앱을 동기화할 수 있습니다.

- **새로운 Mobile Threat Defense 모니터링 도구**

    이제 Mobile Threat Defense 서비스 공급자를 통해 준수 상태를 모니터링하는 새로운 방법을 사용할 수 있습니다.

    자세한 내용은 [Mobile Threat Defense 준수를 모니터링하는 방법](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)을 참조하세요.

## <a name="february-2017"></a>2017년 2월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **회사 포털 웹 사이트 현대화**

  회사 포털 웹 사이트는 관리되는 장치가 없는 사용자를 대상으로 하는 앱을 지원합니다. 이 웹 사이트는 새로운 고대비 색 구성표, 동적 그림, 기술 지원팀 연락처 세부 정보 및 기존 관리되는 장치에 대한 정보를 포함하는 “햄버거 메뉴”를 사용하여 다른 Microsoft 제품 및 서비스에 맞춥니다. 방문 페이지는 추천 및 최근에 업데이트된 앱에 대한 슬라이드를 포함하여 사용자가 사용할 수 있는 앱을 강조하도록 재조정됩니다. [UI 업데이트](/intune/whats-new/whats-new-in-intune-app-ui) 페이지에서 사용 가능한 이전 및 이후 이미지를 찾을 수 있습니다.

- **Windows 장치의 새 MDM 서버 주소**

  Windows 및 Windows Phone 장치 등록을 위한 MDM 서버 주소가 manage.microsoft.com에서 enrollment.manage.microsoft.com으로 변경되었습니다. 사용자에게 Windows 또는 Windows Phone 장치를 등록하는 동안 MDM 서버 주소를 입력하라는 메시지가 표시되면 enrollment.manage.microsoft.com을 사용하라고 알리세요. 이 업데이트에는 또한 EnterpriseEnrollment.contoso.com을 manage.microsoft.com으로 리디렉션하는 DNS의 CNAME이 필요하며, 이 manage.microsoft.com은 EnterpriseEnrollment.contoso.com을 EnterpriseEnrollment-s.manage.microsoft.com으로 리디렉션하는 DNS의 CNAME으로 대체됩니다. 이 변경에 대한 자세한 내용은 http://aka.ms/intuneenrollsvrchange를 방문하세요.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702의 새로운 기능

- **Android for Work 지원**

  이제 Configuration Manager Technical Preview 1702를 사용하여 하이브리드 MDM 환경에서 Android for Work를 통해 Android 장치를 관리할 수 있습니다. 이제 지원되는 Android 장치를 Android for Work 장치로 등록할 수 있으며, Play for Work에서 승인된 앱을 배포할 수 있는 장치에 작업 프로필이 생성됩니다. 이러한 장치에 대한 구성 항목, 준수 정책 및 리소스 액세스 프로필을 구성하고 배포할 수도 있습니다. 자세한 내용은 [Android for Work 지원](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support)을 참조하세요.

- **비규격 앱 준수 설정**

  이제 준수 정책에서 Android 및 iOS 앱에 대한 비규격 앱 규칙을 만들 수 있습니다. 장치에 지정한 응용 프로그램이 설치되어 있으면 “비규격”으로 표시되며, 적용된 조건부 액세스 정책에 따라 회사 리소스에 액세스할 수 없게 됩니다. 자세한 내용은 [조건부 액세스 장치 준수 정책 개선](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)을 참조하세요.

- **PFX 인증서 만들기 및 배포와 S/MIME 지원**

  이제 하이브리드 환경에서 PFX 인증서를 만들고 사용자에게 배포할 수 있습니다. 그러면 사용자가 등록한 장치에서 이 인증서를 S/MIME 메일 암호화 및 암호 해독에 사용할 수 있습니다. 자세한 내용은 [S MIME을 지원하는 PFX 인증서 만들기](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support)를 참조하세요.

- **추가 iOS 구성 설정에 대한 지원**
   
    이제 구성 항목의 일부로 구성할 수 있는 42개의 추가 iOS 설정이 있습니다. 감독된 iOS 장치에 대해 대부분의 설정(전체 중 35개)이 추가되었습니다. 자세한 내용은 [iOS 장치에 대한 새 준수 설정](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices)을 참조하세요.

## <a name="january-2017"></a>2017년 1월

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능

- **Android 7.1.1 지원**

  이제 Intune에서 Android 7.1.1을 완벽하게 지원하고 관리합니다.

- **iOS 장치가 비활성 상태이거나 관리 콘솔이 장치와 통신할 수 없는 문제 해결**

  사용자 장치와 Intune의 연결이 끊어진 경우 회사 리소스에 다시 액세스할 수 있도록 지원할 새로운 문제 해결 단계를 제공할 수 있습니다. [장치가 비활성 상태이거나 관리 콘솔이 장치와 통신할 수 없음](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)을 참조하세요.

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701의 새로운 기능

- **Android 및 iOS 버전은 하이브리드 MDM 만들기 마법사에서 대상 지정이 가능하지 않음**

  하이브리드 MDM(모바일 장치 관리)에 대한 Technical Preview 1701부터 Intune 관리 장치에 대한 새 정책 및 프로필을 만들 때 특정 버전의 Android 및 iOS를 대상으로 지정할 필요가 없습니다. 이러한 변경으로 인해 하이브리드 배포에서 새 Configuration Manager 릴리스나 확장 없이 새 Android 및 iOS 버전을 더 빠르게 지원할 수 있습니다. 자세한 내용은 [Android 및 iOS 버전은 만들기 마법사에서 대상 지정이 가능하지 않음](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)을 참조하세요.


## <a name="notices"></a>알림

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>플랫폼 지원 알림: Windows Phone 8.1 기본 지원은 2017년 7월 11일에 종료됩니다.
<!-- 1327781 -->
*2017년 7월 11일*

Windows Phone 8.1 플랫폼 기본 지원이 종료되어 갑니다. Windows 8.1 PC 지원은 영향을 받지 않습니다.

하이브리드 MDM에 등록된 장치를 포함하여 Intune 서비스가 관리하는 Windows Phone 8.1 장치에는 즉각적인 영향이 없습니다. 등록된 장치는 계속 작동하며 모든 정책, 구성 및 앱은 예상대로 계속 작동합니다. Intune 서비스 내의 Windows Phone 8.1 플랫폼과 Windows Phone 8.1 회사 포털 앱을 대상으로 하는 향상된 기능은 없습니다.

가능하면 빨리 적합한 Windows Phone 8.1 장치를 Windows 10 Mobile로 업그레이드하는 것이 좋습니다.  

### <a name="end-of-support-for-android-43-and-lower"></a>Android 4.3 이하에 대한 지원 종료
<!---1171127--->
*2017년 7월 6일*

Android용 회사 포털 앱과 관리되는 앱이 회사 리소스에 액세스하려면 Android 4.4 이상이 필요합니다. 10월이 시작되기 전에 업데이트되지 않은 장치는 더 이상 회사 포털 또는 이러한 앱에 액세스할 수 없습니다. 12월까지 등록된 모든 장치는 12월에 강제 사용 중지되며, 따라서 회사 리소스에 액세스할 수 없게 됩니다. MDM 없이 앱 보호 정책을 사용 중인 경우 앱이 업데이트를 받지 못하며 해당 환경 품질이 시간이 흐름에 따라 저하됩니다.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 및 System Center 2012 R2 Configuration Manager(RTM): 하이브리드 모바일 장치 관리에 대한 지원이 2017년 4월 10일에 종료됩니다.
*2017년 1월 11일*

System Center 2012 Configuration Manager SP1 및 System Center 2012 R2 Configuration Manager RTM에 대한 지원이 2016년 7월 12일에 종료됩니다. 그 이후 Microsoft Intune 서비스에 연결하는 이러한 릴리스의 하이브리드 MDM에 대한 지원이 2017년 4월 10일에 종료됩니다. 이 날짜 이후에는 이러한 릴리스에서 하이브리드 MDM의 작동이 중지됩니다. Intune 커넥터가 더 이상 Intune 서비스에 연결되지 않으므로 관리되는 장치는 기본적으로 관리되지 않습니다. 업그레이드가 발생할 때까지 Configuration Manager 데이터(예: 정책 및 응용 프로그램)가 Intune으로 이동하지 않으며 관리되는 장치 데이터가 Configuration Manager로 이동하지 않습니다.

Configuration Manager 2012 SP1 또는 R2 RTM과 함께 하이브리드 배포를 실행하는 경우 2017년 4월 10일 이전에 Configuration Manager(현재 분기)로 업그레이드하거나 Configuration Manager 2012의 지원되는 최신 서비스 팩(R2 SP1 또는 SP2)으로 업그레이드하여 서비스 중단을 방지하는 것이 좋습니다.

추가 리소스:
-   [System Center Configuration Manager(현재 분기)로 업그레이드](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [System Center 2012 R2 Configuration Manager SP1로의 업그레이드 계획](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [System Center 2012 Configuration Manager SP2로의 업그레이드 계획](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 회사 포털 업로드가 사용되지 않음
*2016년 10월 25일*

Windows 8, Windows Phone 8 및 Windows RT에 대한 Intune 지원이 중단되고 Windows Phone 8 회사 포털에 대한 지원이 9월에 종료되므로 서명된 회사 포털 앱을 업로드하는 기능이 Configuration Manager 콘솔에서 제거되었습니다.  이미 등록된 Windows 8, Windows Phone 8 및 Windows RT 장치는 계속 지원되지만 이러한 플랫폼에 추가 장치를 등록할 수 없습니다.


### <a name="see-also"></a>참고 항목

- [과거 하이브리드 MDM 기능](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager의 새로운 MDM 기능](https://technet.microsoft.com/library/mt445560.aspx)
