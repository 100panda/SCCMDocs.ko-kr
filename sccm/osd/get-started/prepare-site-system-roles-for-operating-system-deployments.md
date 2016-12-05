---
title: "운영 체제 배포를 위한 사이트 시스템 역할 준비 | Configuration Manager"
description: "System Center Configuration Manager에서 운영 체제를 배포하기 전에 사이트 시스템 역할을 구성합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a9e682c855d5e1fb26f772b2af5066280e01851f


---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>System Center Configuration Manager에서 운영 체제 배포를 위한 사이트 시스템 역할 준비

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager에서 운영 체제를 배포하려면 먼저 특정 구성과 고려 사항을 요구하는 다음과 같은 사이트 시스템 역할을 준비해야 합니다.

##  <a name="a-namebkmkdistributionpointsa-distribution-points"></a><a name="BKMK_DistributionPoints"></a> 배포 지점  
 배포 지점 사이트 시스템 역할에는 클라이언트가 다운로드하는 원본 파일(예: 응용 프로그램 콘텐츠, 소프트웨어 업데이트, 운영 체제 이미지 및 부팅 이미지)이 포함됩니다. 대역폭, 제한 및 예약 옵션을 사용하여 콘텐츠 배포를 제어할 수 있습니다.  

 컴퓨터에 대한 운영 체제 배포를 지원할 만큼 충분한 배포 지점이 있어야 하고, 계층 구조에서 이러한 배포 지점의 배치를 계획해야 합니다. 이 계획 정보는 [콘텐츠 및 콘텐츠 인프라 관리](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)에 대부분 나와 있습니다. 그러나 각 운영 체제 배포에 따라 배포 지점을 계획할 때 추가로 고려할 몇 가지 사항이 있습니다.  

###  <a name="a-namebkmkadditionalplanninga-additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> 배포 지점을 계획할 때 추가로 고려할 사항  
 배포 지점을 계획할 때 추가로 고려할 사항은 다음과 같습니다.  

-   **원치 않는 운영 체제 배포를 방지하는 방법**  

     Configuration Manager는 컬렉션 내의 다른 대상 컴퓨터와 사이트 서버를 구분하지 않습니다. 사이트 서버가 포함된 컬렉션에 필수 작업 순서를 배포할 경우 사이트 서버는 컬렉션에 있는 다른 컴퓨터와 동일한 방식으로 작업 순서를 실행합니다. 운영 체제 배포에서 배포를 실행하려는 클라이언트가 포함된 컬렉션을 사용하는지 확인합니다.  

     위험 수준이 높은 작업 순서 배포의 동작을 관리할 수 있습니다. 위험 수준이 높은 배포는 클라이언트에 자동으로 설치되며 원치 않는 결과가 발생할 수 있습니다. 예를 들어 용도가 필수이며 운영 체제를 배포하는 작업 순서입니다. 위험 수준이 높은 불필요한 배포가 수행될 위험을 줄이려는 경우 배포 확인 설정을 구성할 수 있습니다. 자세한 내용은 [높은 위험 수준의 배포를 관리하는 설정](../../protect/understand/settings-to-manage-high-risk-deployments.md)을 참조하세요.  

-   **단일 배포 지점에서 한 번에 운영 체제 이미지를 받을 수 있는 컴퓨터 수는 몇 대인가요?**  

     필요한 배포 지점 수를 예상하려면 배포 지점의 처리 속도와 디스크 I/O, 네트워크의 사용 가능한 대역폭 및 이미지 패키지 크기가 이러한 리소스에 미치는 영향 등을 고려합니다. 예를 들어 다른 서버 리소스 요소를 고려하지 않는 경우 100메가바이트(MB) 이더넷 네트워크에서 1시간 안에 4기가바이트(GB)의 이미지 패키지를 처리할 수 있는 최대 컴퓨터 수는 11입니다.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     지정된 시간 안에 특정 개수의 컴퓨터에 운영 체제를 배포해야 하는 경우 적절한 개수의 배포 지점에 이미지를 배포합니다.  

-   **배포 지점에 운영 체제를 배포할 수 있나요?**  

     배포 지점에 운영 체제를 배포할 수 있지만 다른 배포 지점에서 운영 체제 이미지를 받아야 합니다.  

###  <a name="a-namebkmkpxedistributionpointa-configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> PXE 요청을 수락하도록 배포 지점 구성  
 PXE 부팅 요청을 만드는 Configuration Manager 클라이언트에 운영 체제를 배포하려면 PXE 요청을 수락하도록 하나 이상의 배포 지점을 구성해야 합니다. 구성하고 나면 배포 지점에서 PXE 부팅 요청에 응답하고 수행해야 할 적절한 배포 작업을 결정합니다.

> [!IMPORTANT]  
> 모든 PXE 사용 배포 지점에  [Windows 배포 서비스](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS)를 설치해야 합니다.  

 PXE 요청을 수락할 수 있도록 기존 배포 지점을 수정하려면 다음 절차를 수행하세요. 새로운 배포 지점을 설치하는 방법에 대한 자세한 내용은 [배포 지점 설치 또는 수정](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)을 참조하세요.  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>PXE 요청을 수락하도록 기존 배포 지점을 수정하려면  

1.  Configuration Manager 콘솔에서 **관리**를 클릭하고 **개요**를 확장한 후 **배포 지점**을 클릭합니다.  

2.  구성할 배포 지점을 선택한 다음 **홈** 탭의 **속성** 그룹에서 **속성**을 클릭합니다.  

3.  배포 지점의 속성 페이지에서 **PXE** 탭을 클릭합니다. **클라이언트에 대해 PXE 지원 사용** 을 선택하여 이 배포 지점에 PXE를 사용하도록 설정합니다.  

4.  PXE를 사용한다는 것을 확정하려면 **PXE에 필요한 포트 검토** 대화 상자에서 **예** 를 클릭합니다. Configuration Manager가 Windows 방화벽에 기본 포트를 자동으로 구성합니다. 다른 방화벽을 사용하는 경우 수동으로 포트를 구성해야 합니다.  

    > [!NOTE]  
    >  WDS와 DHCP가 동일한 서버에 설치되어 있는 경우 DHCP가 동일한 포트에서 수신 대기하므로 다른 포트에서 수신 대기하도록 WDS를 구성해야 합니다. 자세한 내용은 [WDS 및 DHCP가 동일한 서버에 있을 때 고려할 사항](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP)을 참조하세요.  

5.  WDS가 들어오는 PXE 서비스 요청에 응답할 수 있도록 하려면 **들어오는 PXE 요청에 응답하도록 이 배포 지점 허용** 을 선택합니다. 이 설정을 사용하여 배포 지점에서 PXE 기능을 제거하지 않고 이 서비스를 사용하거나 사용하지 않도록 설정할 수 있습니다.  

6.  Configuration Manager에서 관리하지 않는 컴퓨터에 운영 체제를 배포하려면 **알 수 없는 컴퓨터 지원 사용**을 선택합니다.  

7.  PXE 배포에 대한 보안을 강화하려면 **컴퓨터에서 PXE를 사용할 때 암호 필요**를 선택한 다음 강력한 암호를 지정합니다.  

8.  In the **사용자 장치 선호도** 목록에서 배포 지점을 통해 사용자를 PXE 배포 대상 컴퓨터에 연결하는 방법을 선택합니다.  

    -   대상 컴퓨터에 사용자를 연결하지 않으려면 **사용자 장치 선호도 사용 안 함** 을 선택합니다.  

    -   대상 컴퓨터에 사용자를 연결하기 전에 관리자의 승인을 기다리도록 하려면 **수동 승인으로 사용자 장치 선호도 허용** 을 선택합니다.  

    -   승인을 기다리지 않고 자동으로 대상 컴퓨터에 사용자를 연결하도록 하려면 **자동 승인으로 사용자 장치 선호도 허용** 을 선택합니다.  

     자세한 내용은 [사용자를 대상 컴퓨터에 연결](../get-started/associate-users-with-a-destination-computer.md)을 참조하세요.  

9. 배포 지점에서 모든 네트워크 인터페이스 또는 특정 네트워크 인터페이스의 PXE 요청에 응답하도록 지정합니다. 배포 지점이 특정 네트워크 인터페이스에 응답하도록 선택할 경우 각 네트워크 인터페이스의 MAC 주소를 입력해야 합니다.  

10. 여러 PXE 사용 배포 지점을 사용할 때 배포 지점에서 컴퓨터 요청에 응답할 때까지의 지연 시간을 초 단위로 지정합니다.  

11. **확인** 을 클릭하여 배포 지점의 속성을 업데이트합니다.  

###  <a name="a-namebkmkramdisktftpa-customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> PXE 사용 배포 지점에서 RamDisk TFTP 블록 크기 및 창 크기 사용자 지정  
RamDisk TFTP 블록 크기를 사용자 지정할 수 있으며 Configuration Manager 버전 1606부터는 PXE를 사용하는 배포 지점에 대한 창 크기를 사용자 지정할 수 있습니다. 네트워크를 사용자 지정한 경우 블록 또는 창 크기가 너무 커서 시간 초과 오류로 인해 부팅 이미지 다운로드가 실패할 수 있습니다. RamDisk TFTP 블록 크기 및 창 크기 사용자 지정을 통해 PXE를 사용하여 특정 네트워크 요구 사항을 충족하는 경우 TFTP 트래픽을 최적화할 수 있습니다.   
환경에서 사용자 지정된 설정을 테스트하여 가장 효율적인 설정을 결정해야 합니다.  

-   **TFTP 블록 크기**: 블록 크기는 서버에서 파일을 다운로드하는 클라이언트로 전송한 데이터 패킷의 크기(RFC 2347에 설명된 대로)입니다. 블록 크기가 클수록 서버가 더 적은 수의 패킷을 전송할 수 있으므로 서버와 클라이언트 간에 더 적은 왕복 지연이 발생합니다. 그러나 큰 블록 크기는 대부분의 PXE 클라이언트 구현에서 지원하지 않는 조각화된 패킷이 됩니다.  

-   **TFTP 창 크기**: TFTP는 전송된 데이터의 각 블록에 대한 승인(ACK) 패킷을 필요로 합니다. 서버는 이전 블록에 대한 ACK 패킷을 받을 때까지 시퀀스의 다음 블록을 전송하지 않습니다. TFTP 창 작업은 창을 채우는 데 드는 데이터 블록 수를 정의할 수 있는 Windows 배포 서비스의 기능입니다. 서버는 창이 채워질 때까지 데이터 블록을 연속적으로 보내면 클라이언트에서 ACK 패킷을 보냅니다. 이 창 크기를 늘리면 클라이언트와 서버 간의 왕복 지연 횟수가 감소되고 부팅 이미지를 다운로드하는 데 필요한 전체 시간이 줄어듭니다.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>RamDisk TFTP 창 크기를 수정하려면  

-   PXE 사용 배포 지점에 대한 다음 레지스트리 키를 추가하여 RamDisk TFTP 창 크기를 사용자 지정합니다.  

     **위치**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    이름: RamDiskTFTPWindowSize  

     **형식**: REG_DWORD  

     **값**: <사용자 지정된 창 크기\>  

 기본값은 1입니다(1 데이터 블록이 창을 채움).  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>RamDisk TFTP 블록 크기를 수정하려면  

-   PXE 사용 배포 지점에 대한 다음 레지스트리 키를 추가하여 RamDisk TFTP 창 크기를 사용자 지정합니다.  

     **위치**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    이름: RamDiskTFTPBlockSize  

     **형식**: REG_DWORD  

     **값**: <사용자 지정된 블록 크기\>  

 기본값은 4096(4k)입니다.  


###  <a name="a-namebkmkdpmulticasta-configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> 멀티캐스트를 지원하도록 배포 지점 구성  
 멀티캐스트는 여러 클라이언트가 동시에 같은 운영 체제 이미지를 다운로드할 수 있는 경우 배포 지점에서 사용할 수 있는 네트워크 최적화 방법입니다. 멀티캐스트를 사용할 경우 여러 컴퓨터가 배포 지점에서 멀티캐스트되는 운영 체제 이미지를 동시에 다운로드할 수 있으며, 배포 지점은 개별 연결을 통해 데이터 복사본을 각 클라이언트에 전송하지 않습니다. 멀티캐스트를 지원하도록 하나 이상의 배포 지점을 구성해야 합니다. 자세한 내용은 [멀티캐스트를 사용하여 네트워크를 통해 Windows 배포](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)를 참조하세요.  

 운영 체제를 배포하기 전에 멀티캐스트를 지원하도록 배포 지점을 구성해야 합니다. 멀티캐스트를 지원하도록 기존 배포 지점을 수정하려면 다음 절차를 따르십시오. 새로운 배포 지점을 설치하는 방법에 대한 자세한 내용은 [배포 지점 설치 및 구성](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)을 참조하세요.

#### <a name="to-enable-multicast-for-a-distribution-point"></a>배포 지점에 멀티 캐스트를 사용하려면  

1.  Configuration Manager 콘솔에서 **관리**를 클릭합니다.  

2.  **관리** 작업 영역에서 **개요**를 확장하고 **배포 지점** 노드를 선택합니다.  

3.  운영 체제 이미지를 멀티캐스트하는 데 사용할 배포 지점을 선택합니다.  

4.  **홈** 탭의 **속성** 그룹에서 **속성**을 클릭합니다.  

5.  **멀티캐스트** 탭을 선택하고 다음 옵션을 구성합니다.  

    -   **멀티캐스트 사용**: 배포 지점에서 멀티캐스트를 지원하도록 하려면 이 옵션을 선택해야 합니다.  

    -   **멀티 캐스트 연결 계정**: 사이트 데이터베이스에 연결할 계정을 지정합니다.  

    -   **멀티캐스트 주소 설정**: 대상 컴퓨터에 데이터를 전송하기 위한 IP 주소를 지정합니다. 기본적으로 IP 주소는 멀티캐스트 주소를 배포하기 위해 사용하도록 설정된 DHCP 서버에서 얻어집니다. 네트워크 환경에 따라 239.0.0.0과 239.255.255.255 사이에서 IP 주소 범위를 지정할 수 있습니다.  

        > [!IMPORTANT]  
        >  이러한 IP 주소는 운영 체제 이미지를 요청하는 대상 컴퓨터에서 액세스할 수 있어야 합니다. 즉, 대상 컴퓨터와 사이트 서버 사이의 라우터와 방화벽에서 멀티캐스트 트래픽을 허용하도록 구성해야 합니다.  

    -   **UDP 포트 범위**: 대상 컴퓨터에 데이터를 전송하기 위한 UDP 포트 범위를 지정합니다.  

        > [!IMPORTANT]  
        >  이러한 포트는 운영 체제 이미지를 요청하는 대상 컴퓨터에서 액세스할 수 있어야 합니다. 즉, 대상 컴퓨터와 사이트 서버 사이의 라우터와 방화벽에서 멀티캐스트 트래픽을 허용하도록 구성해야 합니다.  

    -   **예약된 멀티캐스트 사용**: 대상 컴퓨터에 운영 체제 배포를 시작하기 시작할 시기를 Configuration Manager에서 제어하는 방식을 지정합니다. **예약된 멀티캐스트 사용**을 클릭하고 다음 옵션을 선택합니다.  

         **세션 시작 지연 시간** 상자에 Configuration Manager가 첫 번째 배포 요청에 응답하기 전까지 기다리는 시간(분)을 지정합니다.  

         **최소 세션 크기** 상자에 몇 개의 요청을 받은 후 Configuration Manager에서 운영 체제 배포를 시작할지를 지정합니다.  

    -   **전송 속도**: 대상 컴퓨터에 데이터를 다운로드하기 위한 전송 속도를 선택합니다.  

    -   **최대 클라이언트**: 이 배포 지점에서 운영 체제를 다운로드할 수 있는 대상 컴퓨터의 최대 수를 지정합니다.  

6.  **확인**을 클릭합니다.  

##  <a name="a-namebkmkstatemigrationpointsa-state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> 상태 마이그레이션 지점  
 상태 마이그레이션 지점에서는 한 컴퓨터에서 캡처된 후 다른 컴퓨터에서 복원된 사용자 상태 데이터를 저장합니다. 그러나 대상 컴퓨터에서 운영 체제를 새로 고치는 배포와 같이 동일한 컴퓨터에서 운영 체제 배포에 대한 사용자 설정을 캡처하는 경우에는 하드 링크를 사용하여 동일한 컴퓨터에 데이터를 저장할지 여부를 선택하거나 상태 마이그레이션 지점을 사용할 수 있습니다. 일부 컴퓨터 배포에 대해 상태 저장소를 만들 경우 Configuration Manager에서 이 상태 저장소와 대상 컴퓨터 간에 자동으로 연결을 만듭니다. 상태 마이그레이션 지점을 계획할 경우 다음 요소를 고려하세요.  

### <a name="user-state-size"></a>사용자 상태 크기  
 사용자 상태의 크기는 상태 마이그레이션 지점의 디스크 저장소와 마이그레이션 중 네트워크 성능에 직접적인 영향을 미칩니다. 사용자 상태의 크기와 마이그레이션할 컴퓨터의 수를 적절히 고려해야 합니다. 또한 컴퓨터에서 어떤 설정을 마이그레이션할지 고려해야 합니다. 예를 들어 **내 문서** 가 이미 서버에 백업되어 있는 경우 이미지 배포의 일부로 마이그레이션할 필요가 없을 것입니다. 불필요한 마이그레이션을 생략하면 사용자 상태의 전체 크기를 줄이고 네트워크 성능과 상태 마이그레이션 지점의 디스크 저장소에 미칠 수 있는 영향을 최소화할 수 있습니다.  

### <a name="user-state-migration-tool"></a>사용자 상태 마이그레이션 도구  
 운영 체제를 배포하는 동안 사용자 상태를 캡처 및 복원하려면 USMT(사용자 상태 마이그레이션 도구) 원본 파일을 가리키는 USMT 패키지를 사용해야 합니다. Configuration Manager는 Configuration Manager 콘솔의 **소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**에서 이 패키지를 자동으로 만듭니다. Configuration Manager에서는 USMT 10.0을 사용합니다. 이는 Windows ADK(Windows Assessment and Deployment Kit)를 통해 배포되며 한 운영 체제에서 사용자 상태를 캡처한 다음 다른 운영 체제로 복원하는 데 사용할 수 있습니다.  

 USMT 10.0에 대한 여러 마이그레이션 시나리오 설명을 보려면 [일반 마이그레이션 시나리오](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)를 참조하세요.  

### <a name="retention-policy"></a>보존 정책  
 상태 마이그레이션 지점을 구성할 때 여기에 저장되는 사용자 상태 데이터의 보존 기간을 지정할 수 있습니다. 상태 마이그레이션 지점에 데이터를 보존하는 기간은 다음 두 가지 고려 사항에 따라 달라집니다.  

-   저장된 데이터가 디스크 저장소에 미치는 영향  

-   데이터를 다시 마이그레이션할 경우에 대비해 일정 기간 데이터를 보존해야 하는 잠재적 요구 사항  

 상태 마이그레이션은 데이터 캡처 및 데이터 복원이라는 두 단계로 진행됩니다. 데이터를 캡처하면 사용자 상태 데이터가 수집되어 상태 마이그레이션 지점에 저장됩니다. 데이터를 복원하면 사용자 상태 데이터가 상태 마이그레이션 지점에서 검색되어 대상 컴퓨터에 기록된 다음 **상태 저장소 해제** 작업 순서 단계에서 저장된 데이터를 해제합니다. 데이터가 해제되면 보존 타이머가 시작됩니다. 마이그레이션된 데이터를 즉시 삭제하는 옵션을 선택하면 사용자 상태 데이터는 해제되는 즉시 삭제됩니다. 데이터를 일정 기간 동안 보존하는 옵션을 선택하면 상태 데이터는 해제되고 나서 해당 기간이 경과할 때 삭제됩니다. 보존 기간을 길게 설정할수록 더 많은 디스크 공간이 필요해집니다.  

### <a name="select-drive-to-store-user-state-migration-data"></a>사용자 상태 마이그레이션 데이터를 저장할 드라이브 선택  
 상태 마이그레이션 지점을 구성할 때 서버에서 사용자 상태 마이그레이션 데이터를 저장할 드라이브를 지정해야 합니다. 이 경우 고정 드라이브 목록에서 드라이브를 선택해야 합니다. 그러나 이러한 드라이브 중 일부는 CD 드라이브나 비네트워크 공유 드라이브와 같이 쓰기 불가능한 드라이브일 수도 있습니다. 또한 일부 드라이브 문자는 컴퓨터의 어떤 드라이브에도 매핑되지 않을 수 있습니다. 상태 마이그레이션 지점을 구성할 경우 쓰기 가능한 공유 드라이브를 지정해야 합니다.  

### <a name="configure-a-state-migration-point"></a>상태 마이그레이션 지점 구성  
 다음 방법을 사용하여 사용자 상태 데이터를 저장하도록 상태 마이그레이션 지점을 구성할 수 있습니다.  

-   **사이트 시스템 서버 만들기 마법사** 를 사용하여 상태 마이그레이션 지점을 위한 새 사이트 시스템 서버를 만듭니다.  

-   **사이트 시스템 역할 추가 마법사** 를 사용하여 기존 서버에 상태 마이그레이션 지점을 추가합니다.  

 이러한 마법사를 사용하는 경우 상태 마이그레이션 지점에 대한 다음 정보를 제공해야 합니다.  

-   사용자 상태 데이터를 저장하는 폴더  

-   상태 마이그레이션 지점에 데이터를 저장할 수 있는 최대 클라이언트 수  

-   상태 마이그레이션 지점이 사용자 상태 데이터를 저장하는 데 사용할 수 있는 최소 공간  

-   역할에 대한 삭제 정책. 사용자 상태 데이터가 컴퓨터에서 복원되고 나서 즉시 또는 특정 일수 후에 데이터를 삭제하도록 지정할 수 있습니다.  

-   상태 마이그레이션 지점이 사용자 상태 데이터를 복원하는 요청에만 응답하도록 할지 여부. 이 옵션을 사용하면 상태 마이그레이션 지점을 사용하여 사용자 상태 데이터를 저장할 수 없습니다.  

 사이트 시스템 역할을 설치하는 단계는 [사이트 시스템 역할 추가](../../core/servers/deploy/configure/add-site-system-roles.md)를 참조하세요.  



<!--HONumber=Nov16_HO1-->

