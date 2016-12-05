---
title: "작업을 자동화하는 작업 순서 관리 | Configuration Manager"
description: "System Center Configuration Manager 환경에서 작업 순서 만들기 편집, 배포, 가져오기 및 내보내기를 통해 작업 순서를 관리할 수 있습니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 04e4e8193d427289a3b84a14efe18511bf5c9731


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 작업을 자동화하는 작업 순서 관리

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 환경에서 작업 순서를 사용하여 단계를 자동화할 수 있습니다. 이러한 단계는 대상 컴퓨터에 운영 체제 이미지를 배포하고, 운영 체제 설치 파일 집합에서 운영 체제 이미지를 만들고 캡처하며, 사용자 상태 정보를 캡처하고 복원할 수 있습니다. 작업 순서는 Configuration Manager 콘솔의 **소프트웨어 라이브러리** > **운영 체제** > **작업 순서**에 있습니다. **작업 순서** 노드는 사용자가 만든 하위 폴더를 포함하여 Configuration Manager 계층 구조 전체에 복제됩니다. 계획 정보는 [작업 자동화에 대한 계획 고려 사항](../plan-design/planning-considerations-for-automating-tasks.md)을 참조하세요.  

 작업 순서를 관리하려면 다음 섹션을 참조하세요.

##  <a name="a-namebkmkcreatetasksequencea-create-task-sequences"></a><a name="BKMK_CreateTaskSequence"></a> 작업 순서 만들기  
 작업 순서 만들기 마법사를 사용하여 작업 순서를 만듭니다. 이 마법사는 다음 유형의 작업 순서를 만들 수 있습니다.  

|작업 순서 유형|추가 정보|  
|------------------------|----------------------|  
|[운영 체제를 설치하는 작업 순서](create-a-task-sequence-to-install-an-operating-system.md)|이 작업 순서 유형은 사용자 데이터를 마이그레이션하고, 소프트웨어 업데이트를 포함하고, 응용 프로그램을 설치하는 옵션 뿐만 아니라 운영 체제를 설치하는 단계를 만듭니다.|  
|[운영 체제를 업그레이드하는 작업 순서](create-a-task-sequence-to-upgrade-an-operating-system.md)|이 작업 순서 유형은 소프트웨어 업데이트를 포함하고, 응용 프로그램을 설치하는 옵션 뿐만 아니라 운영 체제를 업그레이드하는 단계를 만듭니다.|  
|[운영 체제를 캡처하는 작업 순서](create-a-task-sequence-to-capture-an-operating-system.md)|이 작업 순서 유형은 참조 컴퓨터에서 운영 체제를 빌드하고 캡처하는 단계를 만듭니다. 이미지를 캡처하기 전에 참조 컴퓨터에서 소프트웨어 업데이트를 포함하고 응용 프로그램을 설치할 수 있습니다.|  
|[사용자 상태를 캡처 및 복원하는 작업 순서](create-a-task-sequence-to-capture-and-restore-user-state.md)|이 작업 순서는 사용자 상태 데이터를 캡처 및 복원하기 위해 기존 작업 순서에 추가할 단계를 제공합니다.|  
|[가상 하드 디스크를 관리하는 작업 순서](use-a-task-sequence-to-manage-virtual-hard-disks.md)|이 작업 순서 유형에는 Configuration Manager 콘솔에서 System Center VMM(Virtual Machine Manager)에 게시할 수 있는 운영 체제 및 응용 프로그램을 설치하기 위해 포함되는 VHD 생성 단계가 포함됩니다.|  
|[사용자 지정 작업 순서](create-a-custom-task-sequence.md)|이 작업 순서 유형은 작업 순서에 단계를 추가하지 않습니다. 작업 순서를 만든 후에 작업 순서를 편집하고 작업 순서에 단계를 추가해야 합니다.|  

##  <a name="a-namebkmkmodifytasksequencea-edit-a-task-sequence"></a><a name="BKMK_ModifyTaskSequence"></a> 작업 순서 편집  
 작업 순서 단계를 추가 또는 제거하거나, 작업 순서 그룹을 추가 또는 제거하거나, 단계의 순서를 변경하여 작업 순서를 수정할 수 있습니다. 기존 작업 순서를 수정하려면 다음 절차를 수행하세요.  

> [!IMPORTANT]  
>  작업 순서 만들기 마법사를 사용하여 만든 작업 순서를 편집하면 단계의 작업 또는 단계의 유형이 단계 이름이 될 수 있습니다. 예를 들어 "파티션 디스크 0"이라는 단계가 표시되는 경우, 이는 [디스크 포맷 및 파티션 만들기](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) 유형의 단계에 대한 작업입니다. 모든 작업 순서 단계는 편집기에 표시되는 단계의 이름이 아니라 단계의 유형별로 설명되어 있습니다.  

#### <a name="to-edit-a-task-sequence"></a>작업 순서를 편집하려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **작업 순서** 목록에서 편집할 작업 순서를 선택합니다.  

4.  **홈** 탭의 **작업 순서** 그룹에서 **편집**을 클릭한 후 다음 작업 중 필요한 작업을 수행합니다.  

    -   작업 순서 단계를 추가하려면 **추가**를 클릭하고 단계의 유형을 선택한 다음 추가하려는 작업 순서 단계를 클릭합니다. 예를 들어 명령줄 실행 단계를 추가하려면 **추가**를 클릭하고 **일반**을 선택한 후에 **명령줄 실행**을 클릭합니다.  

         모든 작업 순서 단계 및 해당 유형 목록은 이 절차 다음에 나오는 표를 참조하세요.  

    -   작업 순서에 그룹을 추가하려면 **추가**를 클릭하고 **새 그룹**을 클릭합니다. 그룹을 추가한 후에는 그룹에 단계를 추가할 수 있습니다.  

    -   작업 순서에서 단계 및 그룹의 순서를 변경하려면 순서를 바꿀 단계나 그룹을 선택한 다음 **위로 항목 이동** 또는 **아래로 항목 이동** 아이콘을 사용합니다. 단계나 그룹은 한 번에 하나만 이동할 수 있습니다.  

    -   단계 또는 그룹을 제거하려면 단계 또는 그룹을 선택하고 **제거**를 클릭합니다.  

5.  **확인** 을 클릭하여 변경 내용을 저장합니다.  

 사용 가능한 작업 순서 단계 목록을 보려면 [작업 순서 단계](../understand/task-sequence-steps.md)를 참조하세요.  

##  <a name="a-namebkmkdistributetsa-distribute-content-referenced-by-a-task-sequence"></a><a name="BKMK_DistributeTS"></a> 작업 순서에서 참조되는 콘텐츠 배포  
 클라이언트가 콘텐츠를 참조하는 작업 순서를 실행하기 전에 해당 콘텐츠를 배포 지점에 배포해야 합니다. 언제든지 작업 순서를 선택하고 해당 콘텐츠를 배포하여 배포를 위한 새 참조 패키지 목록을 만들 수 있습니다. 작업 순서를 업데이트된 콘텐츠로 변경한 경우 먼저 해당 콘텐츠를 클라이언트에서 사용할 수 있도록 재배포해야 합니다. 작업 순서에서 참조하는 콘텐츠를 배포하려면 다음 절차를 수행하세요.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>참조되는 콘텐츠를 배포 지점에 배포하려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **작업 순서** 목록에서 배포할 작업 순서를 선택합니다.  

4.  **홈** 탭의 **배포** 그룹에서 **콘텐츠 배포** 를 클릭하여 콘텐츠 배포 마법사를 시작합니다.  

5.  **일반** 페이지에서 올바른 작업 순서를 배포하도록 선택했는지 확인하고 **다음**을 클릭합니다.  

6.  **콘텐츠** 페이지에서 배포할 콘텐츠(예: 작업 순서에서 참조하는 부팅 이미지)를 확인하고 **다음**을 클릭합니다.  

7.  **콘텐츠 대상** 페이지에서 작업 순서 콘텐츠를 배포할 컬렉션, 배포 지점 또는 대상 지점 그룹을 지정한 후 **다음**을 클릭합니다.  

    > [!IMPORTANT]  
    >  선택한 작업 순서가 특정 배포 지점에 이미 배포된 콘텐츠를 참조하는 경우 해당 배포 지점은 마법사에 나열되지 않습니다.  

8.  마법사를 완료합니다.  

 작업 순서에서 참조되는 콘텐츠를 사전 준비할 수 있습니다. Configuration Manager에서는 선택한 콘텐츠의 파일, 관련 종속성 및 관련 메타데이터가 포함된 사전 준비된 압축 콘텐츠 파일을 만듭니다. 그런 다음 사이트 서버, 보조 사이트 또는 배포 지점에서 콘텐츠를 수동으로 가져올 수 있습니다. 콘텐츠 파일을 사전 준비하는 방법에 대한 자세한 내용은 [콘텐츠 사전 준비](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content)를 참조하세요.  

##  <a name="a-namebkmkdeploytsa-deploy-a-task-sequence"></a><a name="BKMK_DeployTS"></a> 작업 순서 배포  
 컬렉션의 컴퓨터에 작업 순서를 배포하려면 다음 절차를 수행하세요.  

> [!WARNING]  
>  위험 수준이 높은 작업 순서 배포의 동작을 관리할 수 있습니다. 위험 수준이 높은 배포는 자동으로 설치되며 원치 않는 결과가 발생할 수 있는 배포입니다. 예를 들어 용도가 **필수** 이며 운영 체제를 배포하는 작업 순서는 위험 수준이 높은 배포로 간주됩니다. 자세한 내용은 [높은 위험 수준의 배포를 관리하는 설정](../../protect/understand/settings-to-manage-high-risk-deployments.md)을 참조하세요.  

> [!NOTE]  
>  기본 사이트의 메시지 창에는 작업 순서 배포에 대한 상태 메시지가 표시되지만 중앙 관리 사이트에는 표시되지 않습니다.  

#### <a name="to-deploy-a-task-sequence"></a>작업 순서를 배포하려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **작업 순서** 목록에서 배포할 작업 순서를 선택합니다.  

4.  **홈** 탭의 **배포** 그룹에서 **배포**를 클릭합니다.  

    > [!NOTE]  
    >  **배포** 를 사용할 수 없으면 작업 순서에 잘못된 참조가 있습니다.  참조를 수정한 다음 다시 작업 순서를 배포해 보세요.  

5.  **일반** 페이지에서 다음 정보를 지정한 후에 **다음**을 클릭합니다.  

    -   **작업 순서**: 배포할 작업 순서를 지정합니다. 기본적으로 이 상자에는 사용자가 선택한 작업 순서가 표시됩니다.  

    -   **컬렉션**: 작업 순서를 실행할 컴퓨터가 포함된 컬렉션을 지정합니다.  

         **모든 시스템** 컬렉션과 같은 부적절한 컬렉션에 운영 체제를 설치하는 작업 순서는 배포하지 마세요. 선택한 컬렉션에는 작업 순서를 실행할 컴퓨터만 포함해야 합니다.  

        > [!NOTE]  
        >  운영 체제 등 위험 수준이 높은 배포를 수행할 때 **컬렉션 선택** 창에 사이트 속성에서 구성한 배포 확인 설정을 충족하는 사용자 지정 컬렉션만 표시됩니다. 위험 수준이 높은 배포는 항상 사용자 지정 컬렉션, 직접 작성하는 컬렉션 및 기본적으로 제공되는 **알 수 없는 컴퓨터** 컬렉션으로 제한됩니다. 위험 수준이 높은 배포를 만드는 경우 **모든 시스템**같은 기본 제공 컬렉션을 선택할 수 없습니다. 구성된 최대 크기보다 적은 수의 클라이언트를 포함하는 모든 사용자 지정 컬렉션을 표시하려면 **사이트의 최소 크기 구성보다 많은 멤버 수가 포함된 컬렉션 숨기기** 선택을 취소합니다. 자세한 내용은 [높은 위험 수준의 배포를 관리하는 설정](../../protect/understand/settings-to-manage-high-risk-deployments.md)을 참조하세요.  
        >   
        >  배포 확인 설정은 컬렉션의 현재 멤버 자격을 기반으로 합니다. 작업 순서를 배포한 후에는 위험 수준이 높은 배포 설정에 대해 컬렉션 멤버 자격을 다시 평가하지 않습니다.  
        >   
        >  **기본 크기**를 100으로 설정하고 **최대 크기**를 1,000으로 설정하는 경우를 예로 들어 보겠습니다. 위험 수준이 높은 배포를 만들 때 **컬렉션 선택** 창에는 클라이언트 수가 100개 미만인 컬렉션만 표시됩니다. **사이트의 최소 크기 구성보다 많은 멤버 수가 포함된 컬렉션 숨기기** 설정의 선택을 취소하면 1,000개 미만의 클라이언트가 포함된 컬렉션이 창에 표시됩니다.  
        >   
        >  사이트 역할을 포함하는 컬렉션을 선택하는 경우에는 다음 사항이 적용됩니다.  
        >   
        >  -   컬렉션에 사이트 시스템 서버가 포함되어 있는 경우 배포 확인 설정에서 사이트 시스템 서버가 포함된 컬렉션을 차단하도록 구성하면 오류가 발생하며 작업을 계속할 수 없습니다.  
        > -   컬렉션에 사이트 시스템 서버가 포함되어 있는 경우 배포 확인 설정에서 컬렉션이 사이트 시스템 서버를 포함하거나, 기본 크기 값을 초과하거나, 서버를 포함하는 경우 경고를 표시하도록 구성하면 소프트웨어 배포 마법사에 높은 위험 수준 경고가 표시됩니다. 이 경우 위험 수준이 높은 배포 만들기에 동의해야 하며, 그러면 감사 상태 메시지가 작성됩니다.  

    -   **설명(선택 사항)**: 이 작업 순서 배포를 설명하는 추가 정보를 지정합니다.  

6.  **배포 설정** 페이지에서 다음 정보를 지정한 후에 **다음**을 클릭합니다.  

    -   **목적**: 드롭다운 목록에서 다음 옵션 중 하나를 선택합니다.  

        -   **사용 가능**: 작업 순서가 사용자에게 배포되면 사용자가 응용 프로그램 카탈로그에서 게시된 작업 순서를 보고 필요 시 요청할 수 있습니다. 작업 순서가 장치에 배포되면 사용자가 소프트웨어 센터에서 작업 순서를 보고 필요 시 설치할 수 있습니다.  

        -   **필수**: 구성된 일정에 따라 자동으로 작업 순서가 배포됩니다. 그러나 작업 순서 배포 상태가 숨겨져 있지 않으면 사용자가 이 상태를 추적할 수 있으며 소프트웨어 센터를 사용하여 최종 기한 전에 작업 순서를 설치할 수 있습니다.  

    -   **사용자의 로그인 여부에 상관없이 일정에 따라 자동으로 배포**: 이 옵션은 작업 순서를 배포하는 경우에는 사용할 수 없습니다.  

    -   **절전 모드 해제 패킷 보내기**: 배포 목적이 **필수** 로 설정된 경우 이 옵션을 선택하면 설치 최종 기한 시간에 컴퓨터의 절전 모드를 해제하기 위해 배포를 설치하기 전에 컴퓨터에 절전 모드 해제 패킷이 전송됩니다. 이 옵션을 사용하려면 먼저 컴퓨터와 네트워크에 Wake-On-LAN을 구성해야 합니다.  

    -   **설치 최종 기한에 도달한 후 클라이언트에서 요금제 인터넷 연결을 사용하여 콘텐츠를 다운로드하도록 허용(추가 비용이 발생할 수 있음)**: 응용 프로그램을 설치하지만 운영 체제는 배포하지 않는 작업 순서가 있는 경우, 설치 최종 기한에 도달한 후 클라이언트에서 요금제 인터넷 연결을 사용하여 콘텐츠를 다운로드하도록 허용할지 여부를 지정할 수 있습니다. 때로 인터넷 공급자는 사용자가 요금제 인터넷 연결을 사용할 경우 보내고 받는 데이터 양을 기준으로 요금을 청구하기도 합니다.  

        > [!NOTE]  
        >  요금제 인터넷 연결이 운영 체제를 배포하지 않는 작업 순서에 대해 올바른 작동이 가능하더라도 이 연결의 사용은 지원되지 않습니다.  

    -   **사용자가 이 응용 프로그램을 요청하는 경우 관리자 승인 필요**: 이 옵션은 작업 순서를 배포하는 경우에는 사용할 수 없습니다.  

    -   **다음에 사용 가능하도록 설정**: 작업 순서를 Configuration Manager 클라이언트, 미디어 또는 PXE에 사용할 수 있는지 여부를 지정합니다.  

        > [!IMPORTANT]  
        >  자동화된 작업 순서 배포에는 **미디어 및 PXE만(숨김)** 설정을 사용합니다. 배포 시 컴퓨터가 사용자 개입 없이 자동으로 부팅되도록 허용하려면 미디어의 일부로 **운영 체제 자동 배포 허용** 을 선택하고 SMSTSPreferredAdvertID 변수를 설정합니다. 작업 순서 변수에 대한 자세한 내용은 [작업 순서 기본 제공 변수](../understand/task-sequence-built-in-variables.md)를 참조하세요.  

7.  **일정** 페이지에서 다음 정보를 지정한 후에 **다음**을 클릭합니다.  

    > [!IMPORTANT]  
    >  Windows PE 클라이언트가 PXE 또는 부팅 미디어에서 시작되는 경우 이 클라이언트는 배포 일정(시작, 만료 또는 마감 시간)을 평가하지 않습니다. 전체 Windows 운영 체제에서 시작되는 클라이언트로의 배포에서만 일정을 구성합니다. Windows PE에서 시작된 클라이언트에 배포되는 활성 작업 순서를 제어하려면 유지 관리 기간과 같은 다른 방법을 사용하는 것이 좋습니다.  

    -   **이 배포를 사용할 수 있는 시점 예약**: 작업 순서가 대상 컴퓨터에서 실행될 수 있는 날짜 및 시간을 지정합니다. **UTC** 확인란을 선택하면 작업 순서는 여러 대상 컴퓨터에서 서로 다른 시간이 아닌 동일한 시간(대상 컴퓨터의 현지 시간 기준)에 사용될 수 있도록 설정됩니다.  

         시작 시간이 필요한 시간보다 이전인 경우 클라이언트는 사용자가 지정한 시작 시간에 작업 순서를 다운로드합니다.  

    -   **이 배포의 만료 시점 예약**: 대상 컴퓨터에서 작업 순서가 만료되는 날짜와 시간을 지정합니다. **UTC** 확인란을 선택하면 작업 순서는 여러 대상 컴퓨터에서 서로 다른 시간이 아닌 동일한 시간(대상 컴퓨터의 현지 시간 기준)에 만료되도록 설정됩니다.  

    -   **할당 일정**: 필수 작업 순서가 대상 컴퓨터에서 실행되는 시점을 지정합니다. 여러 일정을 추가할 수 있습니다.  

         일정이 시작되는 날짜 및 시간을 지정하고, 작업 순서가 매주, 매월 또는 사용자 지정 간격 중 어느 간격에 따라 실행될지 지정하고, 작업 순서가 컴퓨터 로그온 또는 로그오프 등과 같은 이벤트 후에 실행될지 여부를 지정할 수 있습니다.  

        > [!NOTE]  
        >  필수 작업 순서의 시작 시간을 해당 작업 순서의 사용 가능 날짜 및 시간보다 이전으로 예약하면 Configuration Manager 클라이언트에서는 작업 순서를 그보다 더 이전에 사용할 수 있게 되더라도 예약된 시작 시간에 다운로드합니다.  

    -   **다시 실행 동작**: 작업 순서가 다시 실행될 시점을 지정합니다. 다음 옵션 중 하나를 지정할 수 있습니다.  

        -   **배포한 프로그램을 다시 실행 안 함**: 작업 순서가 이전에 클라이언트에서 실행된 경우 이 작업 순서를 해당 클라이언트에서 다시 실행하지 않습니다. 이 작업 순서는 처음 실행했을 때 실패한 경우나 작업 순서 파일이 변경된 경우에도 다시 실행되지 않습니다.  

        -   **프로그램을 항상 다시 실행**: 배포가 예약된 경우 작업 순서를 이전에 성공적으로 실행한 경우에도 항상 클라이언트에서 다시 실행합니다. 이 설정은 특히 작업 순서가 일상적으로 업데이트되는 되풀이 배포를 사용할 경우 유용합니다.  

            > [!IMPORTANT]  
            >  이 옵션은 기본값으로 설정되지만 사용자가 필수 배포를 할당할 때까지 아무런 영향을 미치지 않습니다. 사용 가능한 배포는 사용자가 언제든지 다시 실행할 수 있습니다.  

        -   **이전 시도가 실패한 경우 다시 실행**: 배포가 예약된 경우 작업 순서는 이전에 실행에 실패한 경우에만 다시 실행됩니다. 이 설정은 특히 필수 배포가 마지막으로 실행을 시도했을 때 실패한 경우 할당 일정에 따라 자동으로 다시 실행을 시도할 수 있도록 구성하는 데 유용합니다.  

        -   이전 시도가 성공한 경우 다시 실행: 작업 순서는 이전에 클라이언트에서 성공적으로 실행된 경우에만 다시 실행됩니다. 이 설정은 작업 순서가 일상적으로 업데이트되고 각 업데이트를 사용하려면 이전 업데이트가 성공적으로 설치되어야 하는 되풀이 배포를 사용할 경우 유용합니다.  

        > [!NOTE]  
        >  사용자는 사용 가능한 작업 순서 배포를 다시 실행할 수 있으므로, 사용 가능한 작업 순서를 운영 환경에 배포하려면 먼저 사용자가 해당 작업 순서를 여러 번 다시 실행할 경우 어떤 일이 발생하는지 신중하게 평가 및 테스트해야 합니다.  

8.  **사용자 환경** 페이지에서 다음과 같은 정보를 지정한 후 **다음**을 클릭합니다.  

    -   **사용자가 할당과 별개로 프로그램을 실행할 수 있도록 허용**: 사용자가 배포 할당과 별개로 필수 작업 순서를 실행할 수 있는지 여부를 지정합니다.  

    -   **작업 순서 진행률 표시**: Configuration Manager 클라이언트가 작업 순서의 진행률을 표시할지 여부를 지정합니다.  

    -   **소프트웨어 설치**: 사용자가 예약된 시간이 지난 후 구성된 유지 관리 기간을 벗어나 소프트웨어를 설치할 수 있는지 여부를 지정합니다.  

    -   **시스템 다시 시작(설치를 완료하는 데 필요한 경우)**: 사용자가 할당 시간이 지난 후 구성된 유지 관리 기간을 벗어나 소프트웨어 설치 후 컴퓨터를 다시 시작할 수 있는지 여부를 지정합니다.  

    -   **작업 순서가 인터넷을 통해 클라이언트에 대해 실행되도록 허용**: 작업 순서가 Configuration Manager에 의해 인터넷에 있는 것으로 검색된 인터넷 기반 클라이언트에서 실행될 수 있는지 여부를 지정합니다. 운영 체제와 같은 소프트웨어를 설치하는 작업은 이 설정으로 지원되지 않습니다. 이 옵션은 표준 운영 체제에서 작업을 수행하는 일반 스크립트 기반 작업 순서에만 사용할 수 있습니다.  

9. **경고** 페이지에서 이 작업 순서 배포에 사용할 경고 설정을 지정한 후 **다음**을 클릭합니다.  

10. **배포 지점** 페이지에서 다음 정보를 지정한 후에 **다음**을 클릭합니다.  

    -   **배포 옵션**: 다음 옵션 중 하나를 지정할 수 있습니다.  

        > [!NOTE]  
        >  멀티캐스트를 사용하여 운영 체제를 배포할 경우 콘텐츠는 필요할 때 또는 작업 순서 실행 전에 대상 컴퓨터에 다운로드되어야 합니다.  

        -   클라이언트가 작업 순서의 필요에 따라 배포 지점에서 대상 컴퓨터로 콘텐츠를 다운로드하도록 지정합니다.  

        -   클라이언트가 작업 순서가 실행되기 위해 배포 지점에서 대상 컴퓨터로 모든 콘텐츠를 다운로드하도록 지정합니다. 이 옵션은 작업 순서를 PXE 및 부팅 미디어 배포에 대해 사용할 수 있도록 지정한 경우 표시되지 않습니다( **배포 설정** 페이지 참조).  

        -   클라이언트가 배포 지점에서 콘텐츠를 실행하도록 지정합니다. 이 옵션은 작업 순서와 연결된 모든 패키지가 배포 지점의 패키지 공유를 사용하도록 설정된 경우에만 사용할 수 있습니다. 콘텐츠에서 패키지 공유를 사용하도록 설정하려면 각 패키지에 대한 **속성** 에서 **데이터 액세스** 탭을 사용하세요.  

    -   **사용할 수 있는 로컬 배포 지점이 없는 경우 원격 배포 지점을 사용합니다**: 작업 순서에 필요한 콘텐츠를 다운로드할 때 클라이언트가 느리고 불안정한 네트워크에 있는 배포 지점을 사용할 수 있는지 여부를 지정합니다.  

11. 마법사를 완료합니다.  

##  <a name="a-namebkmkexportimporta-export-and-import-task-sequences"></a><a name="BKMK_ExportImport"></a> 작업 순서 내보내기 및 가져오기  
 작업 순서는 운영 체제 이미지, 부팅 이미지, 클라이언트 에이전트 패키지, 드라이버 패키지 및 종속성이 있는 응용 프로그램 등과 같은 관련 개체의 포함 여부에 상관없이 내보내고 가져올 수 있습니다.  

 작업 순서를 내보내고 가져올 때 다음 사항을 고려하세요.  

-   작업 순서에 저장된 암호는 내보낼 수 없습니다. 암호가 포함된 작업 순서를 내보내고 가져올 경우 가져온 작업 순서를 편집하여 암호를 다시 지정해야 합니다. [도메인 또는 작업 그룹 가입](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [네트워크 폴더에 연결](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) 및 [명령줄 실행](../understand/task-sequence-steps.md#BKMK_RunCommandLine) 동작에 대한 암호를 지정해야 합니다.  

-   기본 사이트가 여러 개인 경우 중앙 관리 사이트의 작업 순서를 가져오는 것이 좋습니다.  

 작업 순서를 내보내고 가져오려면 다음 절차를 따르세요.  

#### <a name="to-export-task-sequences"></a>작업 순서를 내보내려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **작업 순서** 목록에서 내보내려는 작업 순서를 선택합니다. 두 개 이상의 작업 순서를 선택하면 모든 작업 순서는 하나의 내보내기 파일로 저장됩니다.  

4.  **홈** 탭의 **작업 순서** 그룹에서 **내보내기** 를 클릭하여 작업 순서 내보내기 마법사를 시작합니다.  

5.  **일반** 페이지에서 다음과 같은 설정을 지정한 후 **다음**을 클릭합니다.  

    -   **파일** 상자에서 내보내기 파일의 위치 및 이름을 지정합니다. 파일 이름을 직접 입력할 경우 파일 이름에 .zip 확장명을 포함해야 합니다. 내보내기 파일을 찾아볼 때 이 파일 이름 확장명이 자동으로 추가됩니다.  

    -   작업 순서 종속성을 내보내지 않으려면 **모든 작업 순서 종속성 내보내기** 확인란을 선택 취소하세요. 기본적으로 마법사에서는 모든 관련 개체를 검색하고 검색된 개체를 작업 순서와 함께 내보냅니다. 여기에는 응용 프로그램에 대한 모든 종속성이 포함됩니다.  

    -   콘텐츠를 패키지 원본에서 내보내기 위치로 복사하지 않으려면 **선택한 작업 순서 및 종속성의 모든 콘텐츠 내보내기** 확인란을 선택 취소하세요. 이 확인란을 선택하면 작업 순서 가져오기 마법사에서는 가져오기 경로를 새 패키지 원본 위치로 사용합니다.  

    -   **관리자 설명** 상자에 내보낼 작업 순서의 설명을 추가합니다.  

6.  마법사를 완료합니다.  

 마법사에서는 다음 출력 파일을 만듭니다.  

-   콘텐츠를 내보내지 않는 경우: .zip 파일  

-   콘텐츠를 내보내는 경우: .zip 파일 및 *export*_files 폴더. 여기서 *export* 는 내보낸 콘텐츠를 포함하는 .zip 파일의 이름입니다.  

 작업 순서를 내보낼 때 콘텐츠를 포함하는 경우 .zip 파일 및 *export*_files 폴더를 복사해야 하며 그렇지 않으면 가져오기가 실패합니다.  

#### <a name="to-import-task-sequences"></a>작업 순서를 가져오려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **작업 순서 가져오기** 를 클릭하여 작업 순서 가져오기 마법사를 시작합니다.  

4.  **일반** 페이지에서 내보낸 .zip 파일을 지정한 후 **다음**을 클릭합니다.  

5.  **파일 콘텐츠** 페이지에서 가져오는 각 개체에 필요한 작업을 선택합니다. 이 페이지는 Configuration Manager에서 가져올 모든 개체를 표시합니다.  

    -   개체를 가져온 적이 없는 경우 **새로 만들기**를 선택하세요.  

    -   이전에 개체를 가져온 적이 있는 경우 다음 작업 중 하나를 선택합니다.  

        -   **중복 무시** (기본값): 이 작업은 개체를 가져오지 않습니다. 대신 마법사에서 기존 개체를 작업 순서에 연결합니다.  

        -   **덮어쓰기**: 이 작업은 기존 개체를 가져온 개체로 덮어씁니다. 응용 프로그램의 경우 수정 버전을 추가하여 기존 응용 프로그램을 업데이트하거나 새 응용 프로그램을 만들 수 있습니다.  

6.  마법사를 완료합니다.  

 작업 순서를 가져온 후 작업 순서를 편집하여 원래 작업 순서에 있던 암호를 지정할 수 있습니다. 보안상의 이유로 암호는 내보내지지 않습니다.  

##  <a name="a-namebkmkcreatetsvariablesa-create-task-sequence-variables-for-computers-and-collections"></a><a name="BKMK_CreateTSVariables"></a> 컴퓨터 및 컬렉션에 대한 작업 순서 변수 만들기  
 컴퓨터 및 컬렉션에 대해 사용자 지정 작업 순서 변수를 정의할 수 있습니다. 컴퓨터에 정의된 변수는 컴퓨터별 작업 순서 변수라고도 하고, 컬렉션에 정의된 변수는 컬렉션별 작업 순서 변수라고도 합니다. 충돌이 발생하는 경우 컴퓨터별 변수가 컬렉션별 변수보다 우선 적용됩니다. 즉, 특정 컴퓨터에 할당된 작업 순서 변수가 자동으로 컴퓨터가 속한 컬렉션에 할당된 변수보다 높은 우선 순위를 보유합니다.  

 예를 들어 컬렉션 ABC에 할당된 변수가 있고, 컬렉션 ABC의 구성원인 컴퓨터 XYZ에 동일한 이름의 변수가 할당된 경우 컴퓨터 XYZ에 할당된 변수가 컬렉션 ABC에 할당된 변수보다 높은 우선 순위를 보유합니다.  

 컴퓨터별 변수 및 컬렉션별 변수를 숨겨 Configuration Manager 콘솔에 표시하지 않을 수 있습니다. 이러한 변수를 숨기지 않으려는 경우 이들을 삭제한 후, 숨기는 옵션을 선택하지 않은 상태로 다시 정의해야 합니다. **Configuration Manager 콘솔에 이 값 표시 안 함**옵션을 사용하면 변수 값이 표시되지 않지만 실행되는 작업 순서에서는 계속 사용할 수 있습니다.  

 기본 사이트 또는 중앙 관리 사이트에서 컴퓨터별 변수를 관리할 수 있습니다. Configuration Manager에서는 컴퓨터당 할당되는 변수를 1,000개까지만 지원합니다.  

> [!WARNING]  
>  작업 순서에 컬렉션별 변수를 사용하는 경우 다음을 고려해야 합니다.  
>   
>  -   컬렉션의 변경 내용은 항상 계층 전체에 복제되므로 컬렉션 변수의 변경 내용은 현재 사이트의 구성원뿐 아니라 계층 전체의 모든 컬렉션 구성원에 적용됩니다.  
> -   컬렉션을 삭제하는 경우 컬렉션에 구성된 작업 순서 변수도 삭제됩니다.  

 컴퓨터 또는 컬렉션에 작업 순서 변수를 만들려면 다음 절차를 따르세요.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>컴퓨터에 대한 작업 순서 변수를 만들려면  

1.  Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.  

2.  **자산 및 준수** 작업 영역에서 변수를 추가할 컴퓨터가 포함된 컬렉션을 확장합니다.  

3.  컴퓨터를 선택하고 **속성**을 클릭합니다.  

4.  **속성** 대화 상자에서 **변수** 탭을 클릭합니다.  

5.  만들려는 각 변수에 대해 **<새\> 변수** 대화 상자에서 **새로 만들기** 아이콘을 클릭하고 작업 순서 변수의 이름과 값을 지정합니다. 변수를 숨겨 Configuration Manager 콘솔에 표시하지 않으려면 **Configuration Manager 콘솔에 이 값 표시 안 함** 확인란의 선택을 취소합니다.  

6.  컴퓨터에 모든 변수를 추가한 후 **확인**을 클릭합니다.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>컬렉션에 대한 작업 순서 변수를 만들려면  

1.  Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.  

2.  **자산 및 준수** 작업 영역에서 변수를 추가할 컬렉션을 선택하고 **속성**을 클릭합니다.  

3.  **속성** 대화 상자에서 **컬렉션 변수** 탭을 클릭합니다.  

4.  만들려는 각 변수에 대해 **<새\> 변수** 대화 상자에서 **새로 만들기** 아이콘을 클릭하고 작업 순서 변수의 이름과 값을 지정합니다. 변수를 숨겨 Configuration Manager 콘솔에 표시하지 않으려면 **Configuration Manager 콘솔에 이 값 표시 안 함** 확인란의 선택을 취소합니다.  

5.  선택적으로, 작업 순서 변수가 평가되는 경우 Configuration Manager에서 사용할 우선 순위를 지정합니다.  

6.  컬렉션에 모든 변수를 추가한 후 **확인**을 클릭합니다.  

##  <a name="a-namebkmkadditionalactionstsa-additional-actions-to-manage-task-sequences"></a><a name="BKMK_AdditionalActionsTS"></a> 작업 순서를 관리하기 위한 추가 작업  
 다음 절차에 따라 작업 순서를 선택할 때 추가 작업을 사용하여 작업 순서를 관리할 수 있습니다.  

#### <a name="to-select-a-task-sequence-to-manage"></a>관리할 작업 순서를 선택하려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제** 를 확장하고 **작업 순서**를 클릭합니다.  

3.  **작업 순서** 목록에서 관리하려는 작업 순서를 선택한 후 사용할 수 있는 옵션 중 하나를 선택합니다.  

 작업 순서를 관리하는 추가 작업에 대한 자세한 내용은 다음 표를 참조하세요.  

|작업|설명|  
|------------|-----------------|  
|**복사**|선택한 작업 순서의 복사본을 만듭니다. 기존 작업 순서에 기반하여 새 작업 순서를 만들려는 경우에 이 작업이 유용합니다.<br /><br /> 폴더에서 작업 순서의 복사본을 만들면 복사본은 작업 순서 노드를 새로 고칠 때까지 해당 폴더에만 나열됩니다.  새로 고친 후 복사본이 루트 폴더에 나타납니다.|  
|**사용 안 함**|컴퓨터에서 실행하지 않을 작업 순서를 사용하지 않도록 설정합니다. 사용하지 않는 작업 순서는 컴퓨터에 배포될 수 있지만, 사용하도록 설정할 때까지 컴퓨터에서 실행되지 않습니다.|  
|**사용**|컴퓨터에서 실행할 수 있도록 작업 순서를 사용하도록 설정합니다. 사용하도록 설정된 이후 배포된 작업 순서를 다시 배포할 필요는 없습니다.|  
|**사전 준비된 콘텐츠 파일 만들기**|사전 준비된 콘텐츠 파일 만들기 마법사를 시작하여 작업 순서 콘텐츠를 사전 준비합니다. 사전 준비된 콘텐츠 파일을 만드는 방법에 대한 자세한 내용은 [콘텐츠 사전 준비](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content)를 참조하세요.|  
|**이동**|선택한 작업 순서를 다른 폴더로 이동합니다.|  
|**데이터 액세스**|선택한 작업 순서에 대한 **속성** 대화 상자를 엽니다. 이 대화 상자에서 작업 순서 개체의 동작을 변경할 수 있습니다. 하지만 이 대화 상자에서 작업 순서의 단계를 변경할 수는 없습니다.|  

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 운영 체제를 배포하는 시나리오](scenarios-to-deploy-enterprise-operating-systems.md)



<!--HONumber=Nov16_HO1-->

