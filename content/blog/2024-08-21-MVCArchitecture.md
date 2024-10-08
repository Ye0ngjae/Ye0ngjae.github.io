---
title: "[Architecture] MVC Architecture"
dateString: August 2024
draft: false
tags:
  [
    "Architecture",
    "MVC Architecture",
    "Model-View-Controller",
    "Design Pattern"
  ]
weight: 30
date: 2024-08-21
categories: ["Architecture", "Software Architecture", "Design Pattern"]
# cover:
    # image: ""
---
# MVC 아키텍처
---
![MVC Architecture](/img/MVC-Architecture/MVC-Architecture.jpg)
MVC (Model-View-Controller)는 사용자 인터페이스를 개발할 때 자주 사용되는 디자인 패턴으로, 애플리케이션을 세 가지 상호 연결된 컴포넌트로 나눈다.

## 모델 (Model)

모델 컴포넌트는 사용자가 작업하는 모든 데이터 관련 로직에 해당한다. 이는 뷰와 컨트롤러 컴포넌트 간에 전송되는 데이터나 기타 비즈니스 로직 관련 데이터를 나타낼 수 있다.

예시: 고객 객체는 데이터베이스에서 고객 정보를 검색하고, 이를 조작하여 다시 데이터베이스에 업데이트하거나 데이터를 렌더링하는 데 사용한다.

## 뷰 (View)

뷰 컴포넌트는 애플리케이션의 모든 UI 로직에 사용된다. 이는 모델에 포함된 데이터의 시각화를 나타낸다.

예시: 고객 뷰는 최종 사용자가 상호작용하는 텍스트 상자, 드롭다운 등 모든 UI 구성 요소를 포함한다.

## 컨트롤러 (Controller)

컨트롤러 컴포넌트는 모델과 뷰 컴포넌트 사이의 인터페이스 역할을 하여 모든 비즈니스 로직과 들어오는 요청을 처리하고, 모델 컴포넌트를 사용하여 데이터를 조작하며, 뷰와 상호작용하여 최종 출력을 렌더링한다.

예시: 고객 컨트롤러는 고객 뷰의 입력을 처리하고, 고객 모델을 사용하여 데이터베이스를 업데이트한다.

## MVC 아키텍처의 장점

- 관심사의 분리: 애플리케이션은 정보의 내부 표현을 사용자에게 제시하고 받아들이는 방식과 분리된 세 가지 상호 연결된 컴포넌트로 나뉜다.
- 병렬 개발 용이: 여러 개발자가 모델, 뷰, 컨트롤러에서 동시에 작업할 수 있다.
- 유지 관리 용이: 관심사의 분리로 인해 관리와 유지보수가 더 쉽다.
- 확장성: 비즈니스 요구가 증가함에 따라 서비스의 확장이 용이하다.