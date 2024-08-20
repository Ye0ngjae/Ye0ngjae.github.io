---
title: "[Architecture] Layered & Multitier Architecture"
dateString: August 2024
draft: false
tags:
  [
    "Architecture",
    "Layered Architecture",
    "Multitier Architecture",
    "N-tier Architecture"
  ]
weight: 30
date: 2024-06-28
categories: ["Architecture", "Software Architecture", "Design Pattern"]
# cover:
    # image: ""
---
# Layered Architecture
---
소프트웨어 시스템을 여러 계층으로 나누어 구성하는 아키텍처 스타일이다. 3 계층 구조(3 Tier Architecture)가 대표적이며, 표현 계층, 애플리케이션 계층, 데이터 계층으로 나뉜다.시스템의 모듈화와 유지 보수성을 높이기 위해 사용된다. 

## 3 계층 구조의 구성 요소
- 표현 계층(Presentation Layer)
    - 사용자와 직접 상호 작용하는 계층으로, 사용자 인터페이스를 담당한다.
    - 정보를 표시하고 사용자 입력을 받아들인다.
- 애플리케이션 계층(Application Layer) /
    - 서비스의 주 로직이 구현되어 있는 계층이다.
    - 비즈니스 로직을 처리하고 요청을 조정한다.
- 데이터 계층(Data Layer)
    - 데이터베이스와 상호 작용하는 계층이다.
    - 데이터 저장, 검색, 업데이트 등의 작업을 수행한다.
  
# Multitier Architecture
Layered Architecture의 한 형태로 볼 수 있으며, **논리적 계층을 물리적 티어로 분리**하여 구현하는 아키텍처 스타일이다. 이는 시스템의 배포 유연성을 높이고, 특정 계층의 부하를 분산시킬 수 있다.

## Layer(계층)와 Tier(티어)의 차이
---
### Tier

티어는 시스템의 물리적 분리를 나타내며, 물리적으로 각각의 티어가 구분되어 있는 형태이다. 주로 서비스의 배포와 관련이 있으며, 서로 다른 물리적 장치 혹은 서버에 배포될 수 있는 시스템의 독립적인 구성을 의미한다. 

### Layer

레이어 시스템의 논리적 분리를 나타내며, 주로 소프트웨어의 구조와 관련이 있다. 레이어 같은 애플리케이션 내에서 서로 다른 책임을 가진 모듈이나 컴포넌트를 구분하는 데 사용된다.

## N-tier Architecture
---
다중 계층 아키텍처로 불리며, 둘 이상의 계층을 가지는 모든 아키텍처를 말한다. 일반적으로 3 계층 아키텍처를 사용하며, 4 계층 이상부터는 시스템의 유지 보수의 어려움, 속도 저하 등의 문제 등으로 별로 사용하지 않는다. 

## 장점
---
### Layered Architecture의 장점

- **모듈화**: 각 레이어가 독립적으로 개발되고 유지보수될 수 있다.
- **유지보수성**: 코드의 가독성과 유지보수성이 높아진다.
- **재사용성**: 특정 레이어는 다른 애플리케이션에서도 재사용될 수 있다.
- **분리된 관심사**: 각 레이어는 특정한 기능이나 책임을 가지므로, 역할이 명확하게 분리된다.

### Multitier Architecture의 장점

- **확장성**: 특정 티어에 부하가 집중될 경우 해당 티어의 서버를 추가하여 확장할 수 있다.
- **유연한 배포**: 각 티어를 독립적으로 배포하고 관리할 수 있다.
- **보안**: 각 티어 간의 통신을 제어하여 보안을 강화할 수 있다.
- **장애 격리**: 한 티어에 문제가 발생해도 다른 티어에 영향을 최소화할 수 있다.

### 레퍼런스
---
- https://www.ibm.com/kr-ko/topics/three-tier-architecture
- https://velog.io/@yyy96/Architecture
- https://xxeol.tistory.com/26