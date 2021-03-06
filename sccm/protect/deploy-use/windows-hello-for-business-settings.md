---
title: "비즈니스용 Windows Hello 설정 | Microsoft 문서"
description: "System Center Configuration Manager와 비즈니스용 Windows Hello를 통합하는 방법을 알아봅니다."
ms.custom: na
ms.date: 08/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 696edcf33936c705984d1168b2f15dd862d90d0e
ms.sourcegitcommit: 4ec2fccb2d471ba9a91fe73df01b7e96efc62594
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager의 비즈니스용 Windows Hello 설정

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager를 통해 Windows 10 장치의 대체 로그인 방법인 비즈니스용 Windows Hello(이전의 Microsoft Passport for Windows)와 통합할 수 있습니다. 비즈니스용 Windows Hello는 Active Directory 또는 Azure Active Directory 계정을 사용하여 암호, 스마트 카드 또는 가상 스마트 카드를 대체합니다.  

비즈니스용 Windows Hello를 통해 암호 대신 **사용자 제스처** 를 사용하여 로그인할 수 있습니다. 사용자 제스처는 단순 PIN, 생체 인식 인증 또는 외부 장치(예: 지문 판독기)일 수 있습니다.

[비즈니스용 Windows Hello에 대해 자세히 알아보기](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager는 다음 두 가지 방법으로 비즈니스용 Windows Hello와 통합됩니다.  

-   Configuration Manager를 사용하여 사용자가 로그인하는 데 사용할 수 있는 제스처와 사용할 수 없는 제스처를 제어할 수 있습니다.  

-   비즈니스용 Windows Hello KSP(키 저장소 공급자)에 인증 인증서를 저장할 수 있습니다. 자세한 내용은 [인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.  

- Configuration Manager 클라이언트를 실행하는 도메인에 가입된 Windows 10 장치에 비즈니스용 Windows Hello 정책을 배포할 수 있습니다. 이 구성은 아래 [도메인에 가입된 Windows 10 장치에서 비즈니스용 Windows Hello 구성](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)에서 설명합니다. Microsoft Intune(하이브리드)에서 Configuration Manager를 사용하는 경우 Windows 10 및 Windows 10 모바일 장치에서 이러한 설정을 구성할 수 있습니다. 자세한 내용은 [비즈니스용 Windows Hello 설정(하이브리드) 구성](../../mdm/deploy-use/windows-hello-for-business-settings.md)을 참조하세요.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>도메인에 가입된 Windows 10 장치에서 비즈니스용 Windows Hello 구성
비즈니스용 Windows Hello 프로필을 만들고 배포하여 도메인에 조인된 Windows 10 장치에서 비즈니스용 Windows Hello 설정을 제어할 수 있습니다. 이것이 권장 방법입니다.


인증서 기반 인증을 사용하는 경우 [인증서 프로필 구성](#configure-a-certificate-profile)에 설명된 대로 인증서 프로필도 배포해야 합니다. 키 기반 인증을 사용하는 경우 인증서 프로필을 배포할 필요가 없습니다.

## <a name="configure-a-windows-hello-for-business-profile"></a>비즈니스용 Windows Hello 프로필 구성  

Configuration Manager 콘솔의 **회사 리소스 액세스** 아래에서 **비즈니스용 Windows Hello 프로필**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택하여 프로필 마법사를 시작합니다. 마법사에서 요청된 설정을 제공하고 마지막 페이지에서 설정을 검토 및 확인한 다음 **닫기**를 클릭합니다. 설정이 표시되는 방식의 예는 다음과 같습니다.  

![비즈니스용 Windows Hello 설정](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configuration Manager에서 비즈니스용 Windows Hello 등록 인증서를 등록하도록 인증서 프로필 구성  
 비즈니스용 Windows Hello 인증서 기반 로그인을 사용하려면 다음을 구성합니다.  

-   Configuration Manager 인증서 프로필.  

-   인증서 프로필에서 스마트 카드 로그온 EKU를 사용하는 템플릿을 선택합니다.  

-   인증서를 비즈니스용 Windows Hello 키 컨테이너에 저장하려고 하고 인증서 프로필에 **스마트 카드 로그온** EKU를 사용하는 경우 인증서가 제대로 유효성이 검사되었는지 확인하려면 키 등록에 대해 다음 사용 권한을 구성해야 합니다.
먼저 **키 관리** 그룹을 만들고 모든 Configuration Manager 관리 지점 컴퓨터를 멤버로 이 그룹에 추가해야 합니다.

일부 구성에서는 사용 권한을 구성할 필요가 없거나 추가 구성이 필요할 수 있습니다. 자세한 도움말은 다음 표를 참조하세요.

|||||
|-|-|-|-|
|Windows 클라이언트 버전|Configuration Manager 1602 또는 1606|Configuration Manager 1610|Configuration Manager 1702 이상|
|Windows 10 1주년 업데이트|핫픽스가 필요하지 않음<br><br>사용 권한이 필요하지 않음<br><br>Windows 스키마 업데이트가 필요하지 않음|핫픽스가 필요하지 않음<br><br>사용 권한이 필요하지 않음<br><br>Windows 스키마 업데이트가 필요하지 않음|필요한 작업은 없습니다.|
|Windows 10 크리에이터 업데이트 이상|지원되지 않음|[이 핫픽스](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) 설치<br><br>사용 권한 구성<br><br>Active Directory에 Windows Server 2016 스키마 적용|사용 권한 구성<br><br>Active Directory에 Windows Server 2016 스키마 적용|

## <a name="to-configure-permissions"></a>사용 권한을 구성하려면

1.  도메인 관리자 또는 이와 동등한 자격 증명을 사용하여 도메인 컨트롤러 또는 관리 워크스테이션에 로그인합니다.
2.  **Active Directory 사용자 및 컴퓨터**를 엽니다.
3.  탐색 창에서 도메인 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.
4.  *<domain name>* **속성** 대화 상자의 **보안** 탭에서 **고급**을 클릭합니다. **보안** 탭이 표시되지 않으면 **Active Directory 사용자 및 컴퓨터**의 **보기** 메뉴에서 **고급 기능**을 켭니다.
5.  **추가**를 클릭합니다.
6.  *<domain name>* **권한 항목** 대화 상자에서 **보안 주체 선택**을 클릭합니다.
7.  **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 **선택할 개체 이름 입력** 텍스트 상자에 **키 관리**를 입력합니다.  **확인**을 클릭합니다.
8.  **적용 대상** 목록에서 **하위 사용자 개체**를 선택합니다.
9.  페이지 아래쪽으로 스크롤하고 **모두 지우기**를 클릭합니다.
10. **속성** 섹션에서 **msDS-KeyCredentialLink 읽기**를 선택합니다.
11. **확인**을 세 번 클릭하여 작업을 완료합니다.


## <a name="next-steps"></a>다음 단계

자세한 내용은 [인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.  




