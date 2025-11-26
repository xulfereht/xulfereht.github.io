---
categories: essay
layout: single
tags: AI NotebookLM 슬라이드 MARP Gemini 프레젠테이션
title: "NotebookLM 슬라이드 기능 테스트: MARP + 나노바나나 프로 워크플로우"
header:
  og_image: /assets/images/og/notebooklm-slide-test-marp-workflow.png
  image: /assets/images/og/notebooklm-slide-test-marp-workflow.png
---

지난 글에 이어서 나노바나나 프로에 대한 테스트입니다.

잘 알려져있다시피, 이번에 notebookLM에 새로 들어간 슬라이드 기능은 매우 강력한데요.

소스 자료를 넣고 알아서 ppt를 넣어달라고 하면 아무튼 잘 만들어줍니다.

이 과정에서 전체 맥락을 잘 파악해서 부족한 부분이 있다면 웹을 통해 보강을 해서 추가를 해주기도 합니다.

해서 기본적으로 어쨋든 마감도가 높은 형태의 작업을 해주긴 합니다.

헌데, 자율적으로 작동을 하다보니 임의성이 높고 딱 내가 원하는 내용만 담되 시각적 보강을 하는 정도의 용도로 제어하려면 조금 더 고민이 필요합니다.

---

## MARP: 마크다운 기반 슬라이드 생성

일단 MARP 라는 게 있는데요.

마크다운 파일로 작성을 하면 그걸 ppt 슬라이드 형태로 렌더링 해주는 방식입니다.

![MARP 에디터 화면](/assets/images/posts/notebooklm-slide-test/01-marp-editor.png)

좌측 처럼 마크다운 형태의 문서를 우측에 슬라이드 처럼 보여주는 거죠.

이 방식을 활용하면 텍스트를 슬라이드로 만드는게 아주 쉬워지는데요.

내가 가진 자료들을 바탕으로 LLM에게 marp 스타일의 md 파일을 작성하게 하면 매우 빠고 간편하게 발표 자료 초안을 마련할 수 있습니다.

마크타운은 기본적으로 텍스트 파일이므로, 수작업 수정도 매우 용이하고 LLM에게 특정 내용의 수정 첨삭도 빠르게 진행할 수 있습니다.

그런 작업은 LLM이 아주아주 잘하는 작업이니까요. 내 자료와 맥락을 주고 그라운딩을 시켜서 새로운 포맷으로 전환하는 일입니다.

MARP에도 기본적으로 CSS 같은 방식으로 꾸미는 것이 가능하긴 하지만 아무래도 제한적이죠.

---

## MARP 기본 슬라이드 초안

![MARP 기본 슬라이드 1](/assets/images/posts/notebooklm-slide-test/02-marp-basic-1.png)
![MARP 기본 슬라이드 2](/assets/images/posts/notebooklm-slide-test/02-marp-basic-2.png)

이런 식이 기본적인 md to marp 방식의 초안입니다.

---

## 구글 슬라이드 나노바나나 프로

구글 슬라이드에서는 이런 슬라이드를 꾸며주는 기능이 있고 최근에 나노바나나 프로로 업데이트 되었습니다.

[https://docs.google.com/presentation](https://docs.google.com/presentation)

내용은 그대로 둔 상태에서 적절하게 꾸며주는 형태로 작업을 하게 되는데 꽤 괜찮게 꾸며줍니다.

구글 슬라이드에서 작업의 단점은 슬라이드 전체에 대한 적용이 안되서 슬라이드 한장씩 적용해야 하다는 점입니다.

---

## Gemini 웹 UI 캔버스

비슷한 방식은 제미나에 웹UI에서 marp 스타일로 작성된 md를 캔버스에 올려서 슬라이드로 그려달라고 하는 것인데요.

![Gemini 캔버스 슬라이드 1](/assets/images/posts/notebooklm-slide-test/03-gemini-canvas-1.png)

![Gemini 캔버스 슬라이드 2](/assets/images/posts/notebooklm-slide-test/03-gemini-canvas-2.png)
![Gemini 캔버스 슬라이드 3](/assets/images/posts/notebooklm-slide-test/03-gemini-canvas-3.png)

컬러나 전반적인 스타일을 내용과 잘 부합되게 잘 만들어줍니다.

---

## NotebookLM: 제어 없이 생성할 때

notebookLM에서 강한 프롬프트로 제어를 하지 않으면 MARP 형태로 만든 슬라이드를 그대로 출력해주지는 못합니다.

![NotebookLM 제어 없는 슬라이드 1](/assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-1.png)
![NotebookLM 제어 없는 슬라이드 2](/assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-2.png)

내용이 나쁘지는 않은데, 원래 만들어둔 MARP 파일의 내용을 그대로 따르지 않습니다.

내용을 축약하거나 첨삭 추가하는 등 임의성이 높아지는 구조입니다.

그렇게 되면 추가적인 수정 작업을 거쳐야 하는데, 아직까지는 그게 쉽지 않은 상황입니다.

그래서 내용적으로는 내가 원하는 형태를 그대로 유지하되 꾸밈 요소에만 변화를 줄 수 있도록 강한 제어를 하는 과정이 필요합니다.

---

## NotebookLM: 강한 제어 후

![NotebookLM 제어된 슬라이드 1](/assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-1.png)
![NotebookLM 제어된 슬라이드 2](/assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-2.png)

내용은 잘 유지하면서 제미나이에서 만들었던 슬라이드에 비해서는 훨씬 이미지의 완성도가 높아진 것을 볼 수 있습니다.

이제 내용적으로 잘 제어할 수 있다는 것까지 확인 했으니 다음으로 넘어갑니다.

---

## 스타일 베리에이션 테스트

기본적으로 해줘 하는 방식으로 슬라이드를 만들다보니, 이미 쏟아지는 샘플 사례들에서 스타일이 비슷비슷해서 벌써 피로를 느낀 다는 분들도 있습니다.

스타일을 다양하게 만드는 방법도 한번 테스트해봅니다.

아래는 동일한 내용에 대한 스타일 베리에이션 테스트입니다.

![스타일 변주 1](/assets/images/posts/notebooklm-slide-test/06-style-var-1.png)
![스타일 변주 2](/assets/images/posts/notebooklm-slide-test/06-style-var-2.png)

![스타일 변주 3](/assets/images/posts/notebooklm-slide-test/06-style-var-3.png)
![스타일 변주 4](/assets/images/posts/notebooklm-slide-test/06-style-var-4.png)

![스타일 변주 5](/assets/images/posts/notebooklm-slide-test/06-style-var-5.png)
![스타일 변주 6](/assets/images/posts/notebooklm-slide-test/06-style-var-6.png)

![스타일 변주 7](/assets/images/posts/notebooklm-slide-test/06-style-var-7.png)
![스타일 변주 8](/assets/images/posts/notebooklm-slide-test/06-style-var-8.png)

![스타일 변주 9](/assets/images/posts/notebooklm-slide-test/06-style-var-9.png)
![스타일 변주 10](/assets/images/posts/notebooklm-slide-test/06-style-var-10.png)

텍스트 내용은 슬라이드별로 유지된 채로 스타일만 잘 변화하고 있는 걸 확인할 수 있었습니다.

---

## 마무리

스타일 베리에이션까지 적용할 수 있다면 내용적 커스터마이징은 md - marp 를 통해 제어하고 스타일은 각자의 취향에 맞게 활용하면 현재 notebookLM에서 발생하는 임의성을 제어하면서 완성도 높은 발표 자료를 만들 수 있을 것입니다.

감사합니다.
