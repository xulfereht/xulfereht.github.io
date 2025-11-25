---
categories: essay
layout: single
tags: AI NotebookLM 인포그래픽
title: "NotebookLM 인포그래픽 기능 테스트: 현존 최고 수준의 이미지 생성"
header:
  og_image: /assets/images/og/notebooklm-infographic-test.png
  image: /assets/images/og/notebooklm-infographic-test.png
---

Gemini 2.5 Pro (일명 나노바나나 프로) 출시 이후 다양한 유스케이스가 쏟아지고 있습니다. 여러 가지 테스트를 해봤는데요, 그중에서도 많이 이야기되는 게 NotebookLM에 탑재된 슬라이드 생성과 인포그래픽 기능입니다.

특히 인포그래픽 기능은 **현존하는 최고 수준의 이미지 생성기**라는 생각이 듭니다. 다만 적절하게 잘 제어하는 게 필요합니다.

이번 글에서는 인포그래픽 생성 테스트 결과를 단계별로 보여드리겠습니다. 슬라이드 기능은 다음 글에서 다루겠습니다.

---

## 테스트 1: 정보량이 많은 상태

여러 가지 소스를 입력한 상태에서 인포그래픽을 만들면, 다양한 정보를 임의로 구겨넣어서 그럴듯해 보이는 결과물을 만들어줍니다.

![정보량이 많은 인포그래픽](/assets/images/posts/notebooklm-infographic/01-info-overload.png)

하지만 정보량이 많아지면 특히 한글에서는 여전히 뭉개짐이나 오타가 발생합니다. 그래도 표현력이 이전에 비해 확실히 좋아졌습니다.

---

## 테스트 2: 정보량 제어

정보량을 조금 줄여서 테스트해봤습니다.

![정보량 제어 인포그래픽](/assets/images/posts/notebooklm-infographic/02-info-controlled.png)

훨씬 좋아지긴 했지만 여전히 정보량은 많습니다. 합곡혈 위치 같은 걸 이전에 비해 훨씬 잘 표현하는 것도 관찰됩니다.

---

## 테스트 3: 엄격한 프롬프팅

조금 더 엄격한 프롬프팅과 정보량 통제를 적용했습니다.

![엄격한 프롬프팅 1](/assets/images/posts/notebooklm-infographic/03-strict-prompt-1.png)
![엄격한 프롬프팅 2](/assets/images/posts/notebooklm-infographic/03-strict-prompt-2.png)

이제 텍스트도 어느 정도 안정적으로 표현하는 단계에 들어옵니다.

![엄격한 프롬프팅 3](/assets/images/posts/notebooklm-infographic/03-strict-prompt-3.png)
![엄격한 프롬프팅 4](/assets/images/posts/notebooklm-infographic/03-strict-prompt-4.png)

---

## 테스트 4: 스타일 변주

동일한 내용에 대해 스타일만 다르게 적용해봤습니다. 임의로 내용을 추가하지 않도록 강제하는 것이 필요합니다.

![스타일 변주 1](/assets/images/posts/notebooklm-infographic/04-style-1.png)
![스타일 변주 2](/assets/images/posts/notebooklm-infographic/04-style-2.png)
![스타일 변주 3](/assets/images/posts/notebooklm-infographic/04-style-3.png)

![스타일 변주 4](/assets/images/posts/notebooklm-infographic/04-style-4.png)
![스타일 변주 5](/assets/images/posts/notebooklm-infographic/04-style-5.png)
![스타일 변주 6](/assets/images/posts/notebooklm-infographic/04-style-6.png)

![스타일 변주 7](/assets/images/posts/notebooklm-infographic/04-style-7.png)
![스타일 변주 8](/assets/images/posts/notebooklm-infographic/04-style-8.png)
![스타일 변주 9](/assets/images/posts/notebooklm-infographic/04-style-9.png)

동일한 내용에 대해 매우 다양한 스타일 적용이 가능하고, 마감도 매우 훌륭합니다. 적절한 수준으로 정보량을 제어하면 한글 표현력도 매우 좋아졌습니다.

---

## Gemini 직접 생성과 비교

아래는 Gemini에서 바로 생성한 결과입니다.

![Gemini 직접 생성](/assets/images/posts/notebooklm-infographic/05-gemini-direct.png)

Gemini에서 직접 생성한 것과 비교해도 NotebookLM에서 생성한 것이 마감이 더 좋습니다. Google이 NotebookLM에 힘을 많이 준 것 같습니다.

아마 ChatGPT의 지브리 효과와 비슷한 것을 NotebookLM을 통해 만들려고 한 것 같습니다.

---

## 마무리

프레젠테이션 슬라이드 생성 능력도 매우 탁월합니다. 다만 임의성을 줄이고 커스터마이징을 위해서는 일정 정도의 제어가 필요합니다.

슬라이드 기능에 대해서는 다음 글에서 다뤄보겠습니다.

감사합니다.
