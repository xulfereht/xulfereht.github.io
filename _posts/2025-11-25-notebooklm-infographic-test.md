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

![](https://t1.daumcdn.net/cafeattach/fjM0/ebfb5297f37440d61bee11b6008d09cd7a69b030)

하지만 정보량이 많아지면 특히 한글에서는 여전히 뭉개짐이나 오타가 발생합니다. 그래도 표현력이 이전에 비해 확실히 좋아졌습니다.

---

## 테스트 2: 정보량 제어

정보량을 조금 줄여서 테스트해봤습니다.

![](https://t1.daumcdn.net/cafeattach/fjM0/1715455f1a00480be2c15c3c4fd03b0043b989bf)

훨씬 좋아지긴 했지만 여전히 정보량은 많습니다. 합곡혈 위치 같은 걸 이전에 비해 훨씬 잘 표현하는 것도 관찰됩니다.

---

## 테스트 3: 엄격한 프롬프팅

조금 더 엄격한 프롬프팅과 정보량 통제를 적용했습니다.

![](https://t1.daumcdn.net/cafeattach/fjM0/99d93b0332132a3ad2f09eafde39142e64155545)
![](https://t1.daumcdn.net/cafeattach/fjM0/78b42ca6f8ff9724b99e2954fc93fb0193033a75)

이제 텍스트도 어느 정도 안정적으로 표현하는 단계에 들어옵니다.

![](https://t1.daumcdn.net/cafeattach/fjM0/ebd030c1f3eedfd3050e33c407d0bac06c160b8c)
![](https://t1.daumcdn.net/cafeattach/fjM0/7fe2bc8e903cfa112e556fa5134491f2d5387303)

---

## 테스트 4: 스타일 변주

동일한 내용에 대해 스타일만 다르게 적용해봤습니다. 임의로 내용을 추가하지 않도록 강제하는 것이 필요합니다.

![](https://t1.daumcdn.net/cafeattach/fjM0/e33175a893d5a0c2bac304209bbe3c7007164fd8)
![](https://t1.daumcdn.net/cafeattach/fjM0/102808e7333d43b0a7d1cfe7333fa369dfe0788c)
![](https://t1.daumcdn.net/cafeattach/fjM0/3b5772bac5fdd0487be3494bf0e6bc2d186a5c3e)

![](https://t1.daumcdn.net/cafeattach/fjM0/bbfa719ca0eedf84852cf2783fd1693697488aa0)
![](https://t1.daumcdn.net/cafeattach/fjM0/b394da22725d9a0dfda92290fb27d31be3c9b7bb)
![](https://t1.daumcdn.net/cafeattach/fjM0/1caf0fea22f7dfbc5c9da17df652e6bd8c468880)

![](https://t1.daumcdn.net/cafeattach/fjM0/8f71dbbc3e526a0f051667ccf92e6b01854074ea)
![](https://t1.daumcdn.net/cafeattach/fjM0/72bd152685e8e8ad30e466e16b0e2ce78c21239d)
![](https://t1.daumcdn.net/cafeattach/fjM0/0d3acc98a79a42acb462f3af202a07a989dc2055)

동일한 내용에 대해 매우 다양한 스타일 적용이 가능하고, 마감도 매우 훌륭합니다. 적절한 수준으로 정보량을 제어하면 한글 표현력도 매우 좋아졌습니다.

---

## Gemini 직접 생성과 비교

아래는 Gemini에서 바로 생성한 결과입니다.

![](https://t1.daumcdn.net/cafeattach/fjM0/03c23311723938732a17b5da55375e5d4077a99e)

Gemini에서 직접 생성한 것과 비교해도 NotebookLM에서 생성한 것이 마감이 더 좋습니다. Google이 NotebookLM에 힘을 많이 준 것 같습니다.

아마 ChatGPT의 지브리 효과와 비슷한 것을 NotebookLM을 통해 만들려고 한 것 같습니다.

---

## 마무리

프레젠테이션 슬라이드 생성 능력도 매우 탁월합니다. 다만 임의성을 줄이고 커스터마이징을 위해서는 일정 정도의 제어가 필요합니다.

슬라이드 기능에 대해서는 다음 글에서 다뤄보겠습니다.

감사합니다.
