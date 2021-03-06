---
title: "하드웨어 인벤토리 확장 | Microsoft 문서"
description: "System Center Configuration Manager에서 하드웨어 인벤토리를 확장하는 방법에 대해 알아봅니다."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: "10"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 3e5517e1710d0d12e51fba58efda5dc5edd08544
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 하드웨어 인벤토리를 확장하는 방법

*적용 대상: System Center Configuration Manager(현재 분기)*

하드웨어 인벤토리가 WMI(Windows Management Instrumentation)를 사용하여 Windows PC에서 정보를 읽습니다. WMI는 WBEM(Web-Based Enterprise Management)을 Microsoft에서 구현한 것으로, 엔터프라이즈에서 관리 정보에 액세스하기 위한 산업 표준입니다. 이전 버전의 Configuration Manager에서는 사이트 서버에서 sms_def.mof 파일을 수정하여 하드웨어 인벤토리를 확장할 수 있습니다. 이 파일에서 읽을 수 있는 WMI 클래스의 목록이 포함 하드웨어 인벤토리 합니다. 이 파일을 편집한 경우 기존 클래스를 사용하거나 사용하지 않도록 설정할 수 있으며 새 클래스를 인벤토리에 만들 수도 있습니다.  

Configuration.mof 파일은 클라이언트의 하드웨어 인벤토리에서 인벤토리에 포함할 데이터 클래스를 정의하는 데 사용되며 Configuration Manager 2012에서 변경되지 않았습니다. 클라이언트 시스템에 있는 기존 또는 사용자 지정 WMI 리포지토리 데이터 클래스나 레지스트리 키를 인벤토리에 포함하기 위해 데이터 클래스를 만들 수 있습니다.  

 또한 Configuration.mof 파일을 정의 하 고 하드웨어 인벤토리 중 장치 정보에 액세스 하는 WMI 공급자를 등록 합니다. 공급자를 등록 하는 중 사용할 공급자의 형식 및 공급자가 지 원하는 클래스를 정의 합니다.  

 Configuration Manager 클라이언트가 정책을 요청할 때(예: 해당 표준 클라이언트 정책 폴링 간격 중) Configuration.mof가 정책 본문에 연결됩니다. 그런 다음이 파일 다운로드 하 고 클라이언트에 의해 컴파일되며 됩니다. 추가, 수정 또는 Configuration.mof 파일에서 데이터 클래스를 삭제 하는 경우 클라이언트에 재고와 관련 된 데이터 클래스에 대 한 이러한 변경 내용을 자동으로 컴파일합니다. Configuration Manager 클라이언트에서 새 데이터 클래스 또는 수정된 데이터 클래스를 인벤토리에 포함하기 위해 필요한 추가 작업은 없습니다. 이 파일은 기본 사이트 서버의 **<CM 설치 위치\>\Inboxes\clifiles.src\hinv\\**에 있습니다.  

 Configuration Manager에서는 Configuration Manager 2007에서와 같이 더 이상 sms_def.mof 파일을 편집하지 않습니다. 대신 WMI 클래스를 사용하거나 사용하지 않도록 설정하고 클라이언트 설정을 사용하여 하드웨어 인벤토리로 수집할 새 클래스를 추가할 수 있습니다. Configuration Manager는 하드웨어 인벤토리를 확장하도록 다음 방법을 제공합니다.  

> [!NOTE]  
>  사용자 지정 인벤토리 클래스를 추가하기 위해 Configuration.mof 파일을 수동으로 변경한 경우 1602 버전으로 업데이트할 때 이러한 변경 내용을 덮어씁니다. 업데이트한 후 사용자 지정 클래스를 계속 사용하려면 1602로 업데이트한 후 Configuration.mof 파일의 "Added extensions" 섹션에 이러한 클래스를 추가해야 합니다.  
> 그러나 이 섹션 위의 어떤 항목도 수정해서는 안 됩니다. 이러한 섹션은 Configuration Manager에서 수정하도록 예약되었기 때문입니다. 사용자 지정 Configuration.mof의 백업은 다음 위치에 있습니다.  
> **<CM 설치 디렉터리\>\data\hinvarchive\\**  

|메서드|추가 정보|  
|------------|----------------------|  
|사용 하도록 설정 하거나 기존 인벤토리 클래스를 사용 하지 않도록 설정|기본 인벤토리 클래스를 사용 또는 사용하지 않도록 설정하거나, 지정된 클라이언트 컬렉션에서 다른 하드웨어 인벤토리 클래스를 수집할 수 있는 사용자 지정 클라이언트 설정을 만듭니다. 이 항목의 [기존 인벤토리 클래스를 사용하거나 사용하지 않도록 설정하려면](#BKMK_Enable) 절차를 참조하세요.|  
|새 인벤토리 클래스를 추가 합니다.|WMI 네임스페이스의 다른 장치에서 새 인벤토리 클래스를 추가합니다. 이 항목의 [새 인벤토리 클래스를 추가하려면](#BKMK_Add) 절차를 참조하세요.|  
|가져오기 및 내보내기 하드웨어 인벤토리 클래스|Configuration Manager 콘솔에서 인벤토리 클래스가 포함된 MOF(Managed Object Format) 파일을 가져오고 내보냅니다. 이 항목의 [하드웨어 인벤토리 클래스를 가져오려면](#BKMK_Import) 및 [하드웨어 인벤토리 클래스를 내보내려면](#BKMK_Export) 절차를 참조하세요.|  
|NOIDMIF 파일 만들기|NOIDMIF 파일을 사용하여 Configuration Manager에서 인벤토리에 포함할 수 없는 클라이언트 장치에 대한 정보를 수집합니다. 예를들어, 다음 레이블을 장치에만 존재 하는 장치 자산 번호 정보를 수집 하는 것이 좋습니다. NOIDMIF 인벤토리 클라이언트 장치에서 수집 된 자동으로 연결 됩니다. 이 항목의 [NOIDMIF 파일을 만들려면](#BKMK_NOIDMIF)을 참조하세요.|  
|IDMIF 파일 만들기|IDMIF 파일을 사용하여 조직에서 Configuration Manager 클라이언트와 연결되지 않은 프로젝터, 복사기, 네트워크 프린터 등의 자산에 대한 정보를 수집합니다. 이 항목의 [IDMIF 파일을 만들려면](#BKMK_IDMIF)을 참조하세요.|  

## <a name="procedures-to-extend-hardware-inventory"></a>하드웨어 인벤토리를 확장하는 절차  
이러한 절차를 통해 하드웨어 인벤토리에 대 한 기본 클라이언트 설정을 구성할 수 있으며 계층의 모든 클라이언트에 적용. 이러한 설정이 일부 클라이언트에만 적용되도록 하려면 사용자 지정 클라이언트 장치 설정을 만들어서 특정 클라이언트의 컬렉션에 할당합니다. [System Center Configuration Manager에서 클라이언트 설정을 구성하는 방법](../../../../core/clients/deploy/configure-client-settings.md)을 참조하세요.  

###  <a name="BKMK_Enable"></a> 기존 인벤토리 클래스를 사용하거나 사용하지 않도록 설정하려면  

1.  Configuration Manager 콘솔에서 **관리** > **클라이언트 설정** > **기본 클라이언트 설정**을 선택합니다.  

4.  **홈** 탭의 **속성** 그룹에서 **속성**을 선택합니다.  

5.  **기본 클라이언트 설정** 대화 상자에서 **하드웨어 인벤토리**를 선택합니다.  

6.  에 **장치 설정을** 목록에서 클릭 **클래스 설정**.  

7.  에 **하드웨어 인벤토리 클래스** 대화 상자를 선택 하거나 클래스 및 하드웨어 인벤토리를 통해 수집 되려면 클래스 속성의 선택을 취소 합니다. 선택 하거나 해당 클래스 내에서 개별 속성을 선택 취소 하는 클래스를 확장할 수 있습니다. 사용 하 여는 **인벤토리 클래스에 대 한 검색** 개별 클래스에 대 한 검색에 필드를 추가 합니다.  

    > [!IMPORTANT]  
    >  새 클래스를 Configuration Manager 하드웨어 인벤토리에 추가하는 경우 수집하여 사이트 서버에 보낼 인벤토리 파일 크기가 늘어납니다. 이는 네트워크 및 Configuration Manager 사이트의 성능에 부정적인 영향을 미칠 수 있습니다. 수집 하려는 인벤토리 클래스를 사용 하도록 설정 합니다.  


###  <a name="BKMK_Add"></a> 새 인벤토리 클래스를 추가하려면  

만 하 고 기본 클라이언트 설정을 수정 하 여 계층의 최상위 수준 서버에서 인벤토리 클래스를 추가할 수 있습니다. 사용자 지정 장치 설정을 만들 때에이 옵션을 사용할 수 없습니다.

1.  Configuration Manager 콘솔에서 **관리** > **클라이언트 설정** > **기본 클라이언트 설정**을 선택합니다.  

4.  **홈** 탭의 **속성** 그룹에서 **속성**을 선택합니다.  

5.  **기본 클라이언트 설정** 대화 상자에서 **하드웨어 인벤토리**를 선택합니다.  

6.  **장치 설정** 목록에서 **클래스 설정**을 선택합니다.  

7.  **하드웨어 인벤토리 클래스** 대화 상자에서 **추가**를 선택합니다.  

8.  에 **하드웨어 인벤토리 클래스 추가** 대화 상자를 클릭 하 여 **Connect**.  

9. 에 **Windows Management Instrumentation (WMI)에 연결** 대화 상자를 WMI 클래스와 클래스를 검색 하기 위한 사용 하 여 WMI 네임 스페이스를 검색 합니다 컴퓨터의 이름을 지정 합니다. 클릭으로 지정한 WMI 네임 스페이스 아래의 모든 클래스를 검색 하려는 경우 **재귀**. 로컬 컴퓨터에 연결 하는 컴퓨터가 없는 경우 원격 컴퓨터에서 WMI에 액세스할 수 있는 권한이 있는 계정에 대 한 로그인 자격 증명을 제공 합니다.  

10. **연결**을 선택합니다.  

11. **하드웨어 인벤토리 클래스 추가** 대화 상자의 **인벤토리 클래스** 목록에서 Configuration Manager 하드웨어 인벤토리에 추가할 WMI 클래스를 선택합니다.  

12. 선택한 WMI 클래스에 대한 정보를 편집하려면 **편집**을 선택하고 **클래스 한정자** 대화 상자에서 다음 정보를 제공합니다.  

    -   **표시 이름** – 리소스 탐색기에 표시됩니다.  

    -   **속성** – WMI 클래스의 각 속성이 표시될 단위를 지정합니다.  

     또한 클래스의 각 인스턴스를 고유 하 게 식별 하는데 도움이 되는 키 속성으로 속성을 지정할 수 있습니다. 키가 정의 되어있지는 클래스에 대 한 클래스의 여러 인스턴스는 클라이언트에서 보고 하는 경우 발견 된 최신 인스턴스만 데이터베이스에 저장 됩니다.  

     속성 구성을 완료했으면 **확인**을 클릭하여 **클래스 한정자** 대화 상자와 다른 열린 대화 상자를 닫습니다. 


###  <a name="BKMK_Import"></a> 하드웨어 인벤토리 클래스를 가져오려면  

기본 클라이언트 설정을 수정 하는 경우에 인벤토리 클래스를 가져올 수 있습니다. 스키마 변경에서 기존 클래스의 속성을 변경 하는 등을 포함 하지 않는 정보를 가져오는 사용자 지정 클라이언트 설정을 사용할 수 있습니다 **True** 를 **False**.  

1.  Configuration Manager 콘솔에서 **관리** >  **클라이언트 설정** > **기본 클라이언트 설정**을 선택합니다.  

4.  **홈** 탭의 **속성** 그룹에서 **속성**을 선택합니다.  

5.  **기본 클라이언트 설정** 대화 상자에서 **하드웨어 인벤토리**를 선택합니다.  

6.  **장치 설정** 목록에서 **클래스 설정**을 선택합니다.  

7.  **하드웨어 인벤토리 클래스** 대화 상자에서 **가져오기**를 선택합니다.  

8.  **가져오기** 대화 상자에서 가져올 MOF(Managed Object Format) 파일을 선택한 다음 **확인**을 선택합니다. 가져올 항목을 검토한 다음 **가져오기**를 클릭합니다.  

###  <a name="BKMK_Export"></a> 하드웨어 인벤토리 클래스를 내보내면  

1.  Configuration Manager 콘솔에서 **관리** > **클라이언트 설정** > **기본 클라이언트 설정**을 선택합니다.  

4.  **홈** 탭의 **속성** 그룹에서 **속성**을 선택합니다.  

5.  **기본 클라이언트 설정** 대화 상자에서 **하드웨어 인벤토리**를 선택합니다.  

6.  **장치 설정** 목록에서 **클래스 설정**을 선택합니다.  

7.  **하드웨어 인벤토리 클래스** 대화 상자에서 **내보내기**를 선택합니다.  

    > [!NOTE]  
    >  클래스를 내보낼 때 현재 선택 된 모든 클래스를 내보냅니다.  

8.  **내보내기** 대화 상자에서 클래스를 내보낼 MOF(Managed Object Format) 파일을 지정한 다음 **저장**을 선택합니다.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>MIF(관리 정보 형식) 파일을 사용하여 하드웨어 인벤토리를 확장하는 방법  
 MIF(관리 정보 형식) 파일을 사용하여 Configuration Manager에 의해 클라이언트에서 수집된 하드웨어 인벤토리 정보를 확장합니다. 하드웨어 인벤토리 중 MIF 파일에 저장 된 정보는 클라이언트 인벤토리 보고서에 추가 되 고, 기본 클라이언트 인벤토리 데이터를 사용 하는 동일한 방식으로 데이터를 사용할 수 있는 사이트 데이터베이스에 저장 합니다. MIF 파일 NOIDMIF와 IDMIF의 두가지 유형이 있습니다.

> [!IMPORTANT]  
>  MIF 파일의 정보를 Configuration Manager 데이터베이스에 추가하려면 이러한 파일에 대한 클래스 정보를 만들거나 가져와야 합니다. 자세한 내용은 이 항목의 [새 인벤토리 클래스를 추가하려면](#BKMK_Add) 및 [하드웨어 인벤토리 클래스를 가져오려면](#BKMK_Import) 섹션을 참조하세요.  

###  <a name="BKMK_NOIDMIF"></a> NOIDMIF 파일을 만들려면  
 NOIDMIF 파일은 일반적으로 Configuration Manager에서 수집할 수 없는 클라이언트 하드웨어 인벤토리에 정보를 추가하는 데 사용할 수 있으며 특정 클라이언트 장치와 연결됩니다. 예를 들어 많은 회사가 조직의 자산 번호를 사용하여 각 컴퓨터에 레이블을 지정한 다음 수동으로 카탈로그화합니다. NOIDMIF 파일을 만들면 이 정보를 Configuration Manager 데이터베이스에 추가하고 쿼리 및 보고를 위해 사용할 수 있습니다. NOIDMIF 파일 만들기에 대한 자세한 내용은 Configuration Manager SDK 설명서를 참조하세요.  

> [!IMPORTANT]  
>  NOIDMIF 파일을 만들 때 ANSI 인코딩 형식으로 저장해야 합니다. UTF-8 인코딩 형식으로 저장된 NOIDMIF 파일은 Configuration Manager에서 읽을 수 없습니다.  

 NOIDMIF 파일을 만든 후 각 클라이언트의 *%Windir%***\CCM\Inventory\Noidmifs** 폴더에 이 파일을 저장합니다. Configuration Manager에서 다음에 예약된 하드웨어 인벤토리 주기 동안 이 폴더의 NODMIF 파일에서 정보를 수집합니다.  

###  <a name="BKMK_IDMIF"></a> IDMIF 파일을 만들려면  
 IDMIF 파일은 특정 클라이언트 장치와 연결되지 않고 일반적으로 Configuration Manager에서 인벤토리에 포함할 수 없는 자산에 대한 정보를 Configuration Manager 데이터베이스에 추가하는 데 사용할 수 있습니다. 예를 들어 IDMIFS를 사용하여 프로젝터, DVD 플레이어, 복사기 또는 Configuration Manager 클라이언트가 없는 다른 장비에 대한 정보를 수집할 수 있습니다. IDMIF 파일 만들기에 대한 내용은 Configuration Manager SDK 설명서를 참조하세요.  

 IDMIF 파일을 만든 후 클라이언트 컴퓨터의 *%Windir%***\CCM\Inventory\Idmifs** 폴더에 이 파일을 저장합니다. Configuration Manager에서 다음에 예약된 하드웨어 인벤토리 주기 중 이 파일에서 정보를 수집합니다. 추가 하거나 가져와 하 여 파일에 포함 된 정보에 대 한 새 클래스를 선언 해야 합니다.  

> [!NOTE]
> MIF 파일은 데이터를 대량으로 포함할 수 있으므로 이 데이터를 수집하면 사이트의 성능에 부정적인 영향을 줄 수 있습니다. 필요한 경우에만 MIF 컬렉션을 사용하도록 설정하고 하드웨어 인벤토리 설정에서 **최대 사용자 지정 MIF 파일 크기(KB)** 옵션을 구성합니다. 자세한 내용은 [System Center Configuration Manager의 하드웨어 인벤토리 소개](introduction-to-hardware-inventory.md)를 참조하세요.
