---
categories: essay
layout: single
tags: AI NotebookLM 슬라이드 MARP Gemini 프레젠테이션
title: "NotebookLM 슬라이드 기능 테스트: MARP + 나노바나나 프로 워크플로우"
header:
  og_image: /assets/images/og/notebooklm-slide-test-marp-workflow.png
  image: /assets/images/og/notebooklm-slide-test-marp-workflow.png

marp_gallery:
  - url: /assets/images/posts/notebooklm-slide-test/02-marp-basic-1.png
    image_path: /assets/images/posts/notebooklm-slide-test/02-marp-basic-1.png
    alt: "MARP 기본 슬라이드 1"
  - url: /assets/images/posts/notebooklm-slide-test/02-marp-basic-2.png
    image_path: /assets/images/posts/notebooklm-slide-test/02-marp-basic-2.png
    alt: "MARP 기본 슬라이드 2"

gemini_gallery:
  - url: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-1.png
    image_path: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-1.png
    alt: "Gemini 캔버스 슬라이드 1"
  - url: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-2.png
    image_path: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-2.png
    alt: "Gemini 캔버스 슬라이드 2"
  - url: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-3.png
    image_path: /assets/images/posts/notebooklm-slide-test/03-gemini-canvas-3.png
    alt: "Gemini 캔버스 슬라이드 3"

uncontrolled_gallery:
  - url: /assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-1.png
    image_path: /assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-1.png
    alt: "NotebookLM 제어 없는 슬라이드 1"
  - url: /assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-2.png
    image_path: /assets/images/posts/notebooklm-slide-test/04-notebooklm-uncontrolled-2.png
    alt: "NotebookLM 제어 없는 슬라이드 2"

controlled_gallery:
  - url: /assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-1.png
    image_path: /assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-1.png
    alt: "NotebookLM 제어된 슬라이드 1"
  - url: /assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-2.png
    image_path: /assets/images/posts/notebooklm-slide-test/05-notebooklm-controlled-2.png
    alt: "NotebookLM 제어된 슬라이드 2"

style_gallery:
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-1.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-1.png
    alt: "스타일 변주 1"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-2.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-2.png
    alt: "스타일 변주 2"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-3.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-3.png
    alt: "스타일 변주 3"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-4.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-4.png
    alt: "스타일 변주 4"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-5.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-5.png
    alt: "스타일 변주 5"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-6.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-6.png
    alt: "스타일 변주 6"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-7.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-7.png
    alt: "스타일 변주 7"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-8.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-8.png
    alt: "스타일 변주 8"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-9.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-9.png
    alt: "스타일 변주 9"
  - url: /assets/images/posts/notebooklm-slide-test/06-style-var-10.png
    image_path: /assets/images/posts/notebooklm-slide-test/06-style-var-10.png
    alt: "스타일 변주 10"
---

지난 글에 이어서 나노바나나 프로에 대한 테스트입니다.

잘 알려져있다시피, 이번에 NotebookLM에 새로 들어간 슬라이드 기능은 매우 강력한데요.

소스 자료를 넣고 알아서 PPT를 만들어달라고 하면 아무튼 잘 만들어줍니다.

이 과정에서 전체 맥락을 잘 파악해서 부족한 부분이 있다면 웹을 통해 보강을 해서 추가를 해주기도 합니다.

해서 기본적으로 어쨌든 마감도가 높은 형태의 작업을 해주긴 합니다.

헌데, 자율적으로 작동을 하다보니 임의성이 높고 딱 내가 원하는 내용만 담되 시각적 보강을 하는 정도의 용도로 제어하려면 조금 더 고민이 필요합니다.

---

## MARP: 마크다운 기반 슬라이드 생성

일단 MARP라는 게 있는데요.

마크다운 파일로 작성을 하면 그걸 PPT 슬라이드 형태로 렌더링 해주는 방식입니다.

![MARP 에디터 화면](/assets/images/posts/notebooklm-slide-test/01-marp-editor.png)

좌측처럼 마크다운 형태의 문서를 우측에 슬라이드처럼 보여주는 거죠.

<div class="notice--info" markdown="1">
**💡 MARP란?**
MARP(Markdown Presentation Ecosystem)는 마크다운으로 슬라이드를 만드는 오픈소스 도구입니다. VS Code 확장 또는 CLI로 사용할 수 있으며, frontmatter에 `marp: true`만 추가하면 바로 슬라이드 모드가 활성화됩니다. PDF, PPTX, HTML 등 다양한 형식으로 내보내기가 가능합니다.
</div>

이 방식을 활용하면 텍스트를 슬라이드로 만드는 게 아주 쉬워지는데요.

내가 가진 자료들을 바탕으로 LLM에게 MARP 스타일의 md 파일을 작성하게 하면 매우 빠르고 간편하게 발표 자료 초안을 마련할 수 있습니다.

마크다운은 기본적으로 텍스트 파일이므로, 수작업 수정도 매우 용이하고 LLM에게 특정 내용의 수정 첨삭도 빠르게 진행할 수 있습니다.

그런 작업은 LLM이 아주아주 잘하는 작업이니까요. 내 자료와 맥락을 주고 그라운딩을 시켜서 새로운 포맷으로 전환하는 일입니다.

MARP에도 기본적으로 CSS 같은 방식으로 꾸미는 것이 가능하긴 하지만 아무래도 제한적이죠.

---

## MARP 기본 슬라이드 초안

{% include gallery id="marp_gallery" caption="기본적인 md to MARP 방식의 초안" %}

이런 식이 기본적인 md to MARP 방식의 초안입니다.

---

## 구글 슬라이드 나노바나나 프로

구글 슬라이드에서는 이런 슬라이드를 꾸며주는 기능이 있고 최근에 나노바나나 프로로 업데이트 되었습니다.

[https://docs.google.com/presentation](https://docs.google.com/presentation)

내용은 그대로 둔 상태에서 적절하게 꾸며주는 형태로 작업을 하게 되는데 꽤 괜찮게 꾸며줍니다.

<div class="notice--warning" markdown="1">
**⚠️ 구글 슬라이드의 한계**
구글 슬라이드에서 작업의 단점은 슬라이드 전체에 대한 일괄 적용이 안 돼서 슬라이드 한 장씩 적용해야 한다는 점입니다. 슬라이드가 많으면 반복 작업이 상당히 번거로워집니다.
</div>

---

## Gemini 웹 UI 캔버스

비슷한 방식은 Gemini 웹 UI에서 MARP 스타일로 작성된 md를 캔버스에 올려서 슬라이드로 그려달라고 하는 것인데요.

{% include gallery id="gemini_gallery" caption="Gemini 캔버스로 생성한 슬라이드" %}

컬러나 전반적인 스타일을 내용과 잘 부합되게 잘 만들어줍니다.

---

## NotebookLM: 제어 없이 생성할 때

NotebookLM에서 강한 프롬프트로 제어를 하지 않으면 MARP 형태로 만든 슬라이드를 그대로 출력해주지는 못합니다.

{% include gallery id="uncontrolled_gallery" caption="제어 없이 생성한 NotebookLM 슬라이드" %}

내용이 나쁘지는 않은데, 원래 만들어둔 MARP 파일의 내용을 그대로 따르지 않습니다.

내용을 축약하거나 첨삭 추가하는 등 임의성이 높아지는 구조입니다.

그렇게 되면 추가적인 수정 작업을 거쳐야 하는데, 아직까지는 그게 쉽지 않은 상황입니다.

그래서 내용적으로는 내가 원하는 형태를 그대로 유지하되 꾸밈 요소에만 변화를 줄 수 있도록 강한 제어를 하는 과정이 필요합니다.

---

## NotebookLM: 강한 제어 후

{% include gallery id="controlled_gallery" caption="강한 프롬프트로 제어한 NotebookLM 슬라이드" %}

내용은 잘 유지하면서 Gemini에서 만들었던 슬라이드에 비해서는 훨씬 이미지의 완성도가 높아진 것을 볼 수 있습니다.

이제 내용적으로 잘 제어할 수 있다는 것까지 확인했으니 다음으로 넘어갑니다.

<div class="notice--success" markdown="1">
**✅ 핵심 포인트**
NotebookLM의 슬라이드 생성은 마감도가 뛰어나지만, 원하는 내용을 정확히 담으려면 강한 프롬프트 제어가 필수입니다. "내용은 절대 변경하지 말고 시각적 요소만 추가해줘"와 같은 명시적인 지시가 효과적입니다.
</div>

---

## 스타일 베리에이션 테스트

기본적으로 해줘 하는 방식으로 슬라이드를 만들다보니, 이미 쏟아지는 샘플 사례들에서 스타일이 비슷비슷해서 벌써 피로를 느낀다는 분들도 있습니다.

스타일을 다양하게 만드는 방법도 한번 테스트해봅니다.

아래는 동일한 내용에 대한 스타일 베리에이션 테스트입니다.

{% include gallery id="style_gallery" caption="동일한 내용에 대한 10가지 스타일 베리에이션" %}

텍스트 내용은 슬라이드별로 유지된 채로 스타일만 잘 변화하고 있는 걸 확인할 수 있었습니다.

<div class="notice--info" markdown="1">
**💡 스타일 베리에이션 팁**
"미니멀한 스타일로", "다크 모드로", "손그림 느낌으로", "기업 프레젠테이션 스타일로" 등 구체적인 스타일 키워드를 프롬프트에 추가하면 다양한 결과물을 얻을 수 있습니다. 같은 내용이라도 청중과 상황에 맞는 스타일을 선택하는 것이 중요합니다.
</div>

---

## 마무리

스타일 베리에이션까지 적용할 수 있다면 내용적 커스터마이징은 md - MARP를 통해 제어하고 스타일은 각자의 취향에 맞게 활용하면 현재 NotebookLM에서 발생하는 임의성을 제어하면서 완성도 높은 발표 자료를 만들 수 있을 것입니다.

<div class="notice--primary" markdown="1">
**📋 추천 워크플로우 요약**
1. **내용 작성**: 마크다운(MARP 형식)으로 슬라이드 내용 작성
2. **LLM 활용**: 내용 수정/첨삭은 LLM에게 맡기기 (텍스트 기반이라 빠름)
3. **시각화**: NotebookLM에 업로드 후 "내용 유지 + 시각적 보강" 프롬프트로 생성
4. **스타일 조정**: 원하는 스타일 키워드로 베리에이션 생성
</div>

감사합니다.
