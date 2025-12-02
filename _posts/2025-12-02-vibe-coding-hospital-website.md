---
categories: essay
layout: single
tags: vibe-coding AI automation hospital website claude antigravity
title: "바이브코딩으로 하는 병원 홈페이지 구축기"
---

## 들어가며: 블로그에서 웹사이트로

올 초에 의료광고법 시행령 해석의 변화로 블로그 심의 이슈가 한창 시끄러울 때, 독립형 블로그를 직접 설치해본 적이 있습니다.

웹사이트 형태로 블로그를 운영하면 사전심의 대상이 아니다 보니 표현에 있어서 자유가 있다는 지인 원장님의 의견을 듣고 실험적으로 작업을 했었는데요. 외부 웹사이트는 네이버 노출 면에서 단점이 있다 보니, 들이는 품에 비해서 가성비가 안 나오는 작업이기도 했습니다.

---

## 6개월 후, 트래픽이 생기기 시작하다

그럼에도 의미가 있다고 느꼈던 일이 있습니다.

이 블로그 사이트에 꾸준히 포스팅을 했었거든요. 직접 포스팅을 한 건 아니고, 네이버 블로그에 포스팅을 하면 그걸 자동으로 인식해서 데일리로 포스팅을 가져가서 등록되게 작업을 해뒀었습니다. API 기반으로 바로 포스팅을 할 수 있는 장점이 있었거든요.

그래서 그냥 한참을 잊고 지내다가 오랜만에 들어가보니, 뭔가 유입이 생기기 시작하더라는 거죠.

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/02-traffic-stats.jpg)
*8월경 확인한 트래픽 - 6개월 정도 컨텐츠가 쌓이니 네이버에서도 컨텐츠 서플라이어로서 인정을 해주는 느낌*

아직 의미 있는 정도 수준의 트래픽은 아니지만, 지속적인 컨텐츠 유입이 되면 웹사이트도 "어라 괜찮겠는데?" 하는 생각이 들었던 시점이었습니다.

---

## 클로드 코드와의 만남: 바이브코딩의 시작

그러던 찰나에 올 하반기 들어 클로드 코드를 조금 더 깊게 사용해 보면서, **개발자나 디자이너 없이도 웬만한 서비스는 만들어 볼 수 있겠다**는 생각을 하게 됐습니다.

불과 올 초만 해도 블로그형 웹사이트 하나 구축하는 것도 낑낑거렸었는데 말이죠...

구글에서 최근에 나온 **Antigravity**를 활용해서 작업을 진행했습니다.

---

## 기획 방향: 정적 페이지를 넘어서

전형적인 형태의 병원·한의원 웹사이트의 효용은 이제는 많이 떨어지는 것 같습니다.

대개 한의원 웹사이트들은 단순한 정적 페이지(static pages)들로 만들어질 뿐이고, 대부분의 경우 네이버 플레이스가 최종 엔드포인트로 기능하는 경우가 많아서 웹사이트로 들어오는 트래픽은 별로 없다 보니 "굳이 있어야 하나" 하는 생각을 저도 했었습니다.

그래서 한의원 웹사이트를 만든다면:

1. **단순 정적 페이지 구성을 벗어나**
2. **여러 가지 퍼널을 고려한 라이트하고 얇은 앱** (동적으로 기능하는) 형태
3. **LLM과의 상호작용을 고려한 형태**

이런 방향이어야 하지 않을까 생각하고 있습니다.

---

## 구현 결과물

### 메인 페이지

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/03-main-page.jpg)
*메인 페이지 - 아임웹, 식스샵 등의 웹빌더와 달리 완전히 커스텀한 구성이 가능*

기존에는 아임웹, 식스샵 등의 웹빌더에 타입폼, 채널톡 같은 서비스를 얼기설기 엮어서 고객 퍼널별로 자동화를 나름대로 했었는데요. 기존의 서비스들이 한의원에서 사용할 때 좀 만족스럽지 못했던 부분들도 있고 하다 보니, 평소 생각했던 워크플로를 녹여서 "이런 게 있으면 좋겠다" 하는 기능들을 좀 넣어보고 있습니다.

---

### 마케팅 퍼널용 자가진단 앱

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/04-self-diagnosis.jpg)
*마케팅 퍼널용 자가진단 앱 - 관리자 모드에서 라이브러리로 추가/수정 관리 가능*

마케팅과 연계되어 자연스러운 타겟 문의 전환 방식으로 활용하는 전략입니다.

---

### 클리닉별 미니진단

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/05-mini-diagnosis.jpg)
*"나와 관련된 증상을 여기서 진료를 하는구나" 느낄 수 있게 하는 섹션*

---

### 상세 페이지

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/06-detail-page-1.jpg)
*상세 페이지 예시 1*

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/07-detail-page-2.jpg)
*상세 페이지 예시 2 - 후기 등은 회원가입 후 조회하도록 하는 기능 구현*

---

## 관리자 기능: 고객 관리까지

### 관리자 대시보드

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/08-admin-dashboard.jpg)
*관리자 모드 - 웹사이트 관리뿐 아니라 고객관리 기능을 포함*

---

### 환자 여정 팔로업

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/09-patient-journey.jpg)
*비급여 환자를 중심으로 환자 여정을 팔로업할 수 있습니다*

---

### 결제·배송 관리

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/10-payment-shipping-1.jpg)

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/11-payment-shipping-2.jpg)

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/12-payment-shipping-3.jpg)
*결제와 연동해서 배송 수량을 관리하고, 배송예정일 및 해피콜을 대시보드에서 바로 확인*

---

### 프로그램 관리

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/13-program-management.jpg)
*원내에서 운영 중인 프로그램을 관리하는 페이지 - 고객이 보는 홈페이지 구성과 연동*

---

### 웹 빌더 방식 편집

![Vibe Coding Hospital](/assets/images/vibe-coding-hospital/14-web-builder.jpg)
*웹 빌더 방식으로 각 페이지 세부 사항을 섹션별로 수정 가능*

---

## 앞으로의 확장 가능성

그 외에도 다양한 기능들을 이것저것 만들어보고 있습니다:

- **문자나 카톡 연동** 같은 부분까지 해결되면 좋을 것 같고
- **내부 직원용 메신저**를 붙인다든지 하는 것들도 가능할 것 같습니다

---

## 마치며

아무튼 이런 걸 제가 만들 수 있을 거라고는 생각을 안 했던 것 같은데, AI로 인해 여러 가지 도메인에 대한 장벽이 낮아지고 있다는 생각이 듭니다.

**뭐 생각만 하면 뚝딱 만들어주는 세상이 되어가고 있네요.**