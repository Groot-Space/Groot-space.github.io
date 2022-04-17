---
title: "Microsoft 365 Defender"
excerpt: "Microsoft 365 Defender의 개요에 대해 다룹니다."
categories:
    - Microsoft
    - Security
    - Azure
tags:
    - 보안
    - 솔루션
toc: true
toc_sticky: true
use_math: true
---
## Microsoft 365 Defender

### 용어 설명

* XDR

  X는 무엇이든을 의미하는 변수. DR은 Detection and Response의 약자이며, XDR솔루션은 **탐지 및 대응 플랫폼** 으로서 엔드포인트 센서, 네트워크 센서이기도 하고, 클라우드 센서에서 적절한 데이터를 검색할 수 있으며, 이러한 모든 데이터의 분석을 중앙에서 관리.

### Microsoft 365 Defender 아키텍처

Microsoft 365 Defender는 다음 그림과 같은 아키텍처로 되어있습니다.

![image1](\assets\images\azure\Microsoft 365 Defender\2.jpg)

### Microsoft 365 Defender 구성 요소

* 여러 도메인의 전반에 걸친 XDR을 제공합니다. XDR이라 하면, 인시던트 대기열, 자동화된 대응, 자가 치유, 위협 헌팅 및 위협 분석이 포함됩니다.
* 전자메일 및 링크를 통한 악의적인 위협으로부터의 보호
* 손상된 계정 보호
  * Microsoft Defender for Identity는 ADFS(Activate Directory Federated Services)및 온프레미스 ADDS(Active Directory Domain Services)를 실행하는 서버의 신호를 수집합니다. Microsoft Defender for Identity는 이러한 신호를 이용하여 손상된 계정을 해코러부터 보호합니다.
* 조직에서 사용하는 디바이스의 신호를 수집하고 디바이스를 보호합니다.
* Azure AD ID 보호는 수많은 시도의 로그인에서 얻은 위험 데이터를 사용하여 사용자가 로그인을 하는 환경에서 위험을 평가합니다.

### Microsoft 365 Defender 포털

| 기능                              | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| Microsoft 365 규정 준수 센터      | M365 서비스에서 규정 준수 요구 사항을 관리합니다.            |
| Azure Activate Directory          | 조직의 ID를 관리합니다.                                      |
| Azure AD ID 보호                  | 조직의 ID에 영향을 주는 잠재적인 취약성을 검색합니다.        |
| Azure Information Protection      | 조직의 메일과 문서를 자동으로 분류 및 보호하도록 합니다.     |
| 클라우드용 Microsoft Defender     | 데이터 센터를 보호하고 클라우드와 온프레미스에서 Azure 및 Azure 이외 워크로드에 대한 지능형 위협 방지를 제공합니다. |
| Microsoft Defender for Cloud Apps | 정교한 분석을 통해 클라우드 앱을 파악하여 사이버 위협을 식별하고 방지합니다. |

### 인시던트 관리

 인시던트는 네트워크에서 악의적인 이벤트나 활동이 확인될 때 생성되는 관련 경고를 기반으로 합니다.  인시던트는 네트워크에서 악의적인 이벤트나 활동이 확인될 때 생성되는 관련 경고를 기반으로 합니다. 관련 경고를 인시던트로 그룹화하면 보안 방어자가 공격을 포괄적으로 파악할 수 있습니다.예를 들어, 보안 방어자는 공격이 시작된 위치, 사용된 전술 및 공격이 네트워크까지 이동한 거리를 확인할 수 있습니다. 또한 영향을 받는 디바이스, 사용자 및 사서함 수, 영향의 심각도, 영향을 받는 엔터티에 관한 기타 세부 정보 같은 공격 범위를 확인할 수 있습니다.

### 경고 관리 및 조사

* Microsoft 365 Defender에서는 관련 경고가 집계되어 인시던트를 형성합니다. 인시던트는 항상 더 광범위한 공격 컨텍스트를 제공하지만 더 심도 있는 분석이 필요한 경우 경고를 분석하는 것이 유용할 수 있습니다.경고 큐에는 현재 경고 집합이 표시됩니다. Microsoft 365 Defender 포털의 빠른 실행 시 인시던트 및 경고 > 인시던트에서 경고 큐를 확인할 수 있습니다.

![image3](\assets\images\azure\Microsoft 365 Defender\3.jpg)

