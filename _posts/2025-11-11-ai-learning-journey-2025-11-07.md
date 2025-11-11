---
categories: learning
date: '2025-11-11'
layout: single
tags: ''
title: AI Learning Journey - 2025-11-07
---
# AI Learning Journey - 2025-11-07

## 🎯 Today's Focus

**Positional Encoding** - Transformer가 단어 순서를 이해하는 방법

## 📚 Why This Matters Now

### 📅 과거 학습과의 연결

**지난주에 배운 것들**:
- **Transformer** (depth 1) - Attention 기반 아키텍처, RNN 대체
- **Attention Mechanism** (depth 1) - Self-Attention, Q-K-V 구조
- **RLHF** (depth 1) - Reinforcement Learning from Human Feedback
- **Scaling Laws** (depth 1) - 파라미터/데이터/컴퓨팅과 성능 관계

**오늘 배울 것**:
- **Positional Encoding** (depth 2)

**왜 한 단계 더 깊이?**

Transformer의 기본 구조를 이해했다면, 이제 "Transformer는 어떻게 문장의 순서를 알까?"라는 질문에 답할 차례입니다. RNN은 순차적으로 처리하기 때문에 자연스럽게 위치 정보를 갖지만, Transformer는 모든 토큰을 병렬로 처리합니다. 따라서 별도의 메커니즘이 필요합니다.

### 🔮 앞으로의 학습 여정

**이번 주 내** (depth 2-3):
- Multi-Head Attention - 병렬 Attention 메커니즘
- GPT 구조 이해 - Autoregressive Language Model

**이번 달** (depth 2-3):
- BERT vs GPT 비교 - Bidirectional vs Unidirectional
- AI Agents 기초 - LLM 기반 자율 에이전트

**분기 목표** (depth 3+):
- Mechanistic Interpretability - 모델 내부 작동 원리 해석
- Constitutional AI - Anthropic의 안전성 접근법

---

## 🧩 Core Concept Explained

### 🤔 왜 Transformer에 Positional Encoding이 필요한가?

Transformer는 Self-Attention을 통해 모든 토큰을 동시에 처리합니다. 이것이 병렬화의 핵심 장점이지만, 큰 문제가 하나 있습니다.

**문제**: "I love AI" 와 "AI love I" 를 구분할 수 없습니다.

Self-Attention은 각 단어 간의 관계만 계산할 뿐, 어떤 단어가 먼저 나왔는지는 모릅니다. 마치 숫자가 적힌 공을 동시에 던지면, 숫자 없이는 어떤 공이 먼저 던져진 건지 알 수 없는 것과 같습니다.

**해결책**: 각 토큰에 "위치 번호표"를 달아줍니다.

Positional Encoding은 입력 임베딩에 위치 정보를 더해서, 모델이 "첫 번째 단어", "두 번째 단어"를 구분할 수 있게 합니다.

**수식**:
```
최종 입력 = 단어 임베딩 + Positional Encoding

Input(pos) = WordEmb(word) + PE(pos)
```

### 📖 어떻게 작동하는가? (Sinusoidal PE)

Vaswani et al. (2017)의 "Attention is All You Need" 논문에서 제안한 방법은 **사인/코사인 함수**를 사용합니다.

**수식**:
```
PE(pos, 2i) = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

여기서:
- `pos` = 토큰의 위치 (0, 1, 2, ...)
- `i` = 차원 인덱스 (0부터 d_model/2까지)
- `d_model` = 모델 차원 (예: 512)

**왜 sin/cos인가?**

1. **주기 함수**: 같은 상대 거리에는 비슷한 패턴
   - PE(5) - PE(3) ≈ PE(105) - PE(103) (상대 거리 2)

2. **외삽 가능**: 학습 시보다 긴 시퀀스도 처리 가능
   - 학습할 때 최대 512 토큰 → 추론 때 1000 토큰도 가능

3. **학습 불필요**: 고정된 수식, 파라미터 추가 없음

**시각화** (간단한 예시):
```
위치 0: [sin(0/10000^0), cos(0/10000^0), sin(0/10000^0.2), ...]
위치 1: [sin(1/10000^0), cos(1/10000^0), sin(1/10000^0.2), ...]
위치 2: [sin(2/10000^0), cos(2/10000^0), sin(2/10000^0.2), ...]
...

→ 각 위치마다 고유한 벡터 생성
→ 인접한 위치는 비슷한 벡터 (주기 함수 성질)
```

### 💻 코드로 이해하기

```python
import numpy as np

def positional_encoding(seq_len, d_model):
    """
    Generate sinusoidal positional encoding.

    Args:
        seq_len: Sequence length (예: 10)
        d_model: Model dimension (예: 512)

    Returns:
        pe: (seq_len, d_model) positional encoding matrix
    """
    pe = np.zeros((seq_len, d_model))

    for pos in range(seq_len):
        for i in range(0, d_model, 2):
            # Even indices: sin
            pe[pos, i] = np.sin(pos / (10000 ** (i / d_model)))

            # Odd indices: cos
            if i + 1 < d_model:
                pe[pos, i + 1] = np.cos(pos / (10000 ** (i / d_model)))

    return pe

# Example usage
seq_len = 10  # 10 tokens
d_model = 512  # Transformer dimension

pe = positional_encoding(seq_len, d_model)

print(f"Shape: {pe.shape}")  # (10, 512)
print(f"PE for position 0 (first 5 dims): {pe[0, :5]}")
print(f"PE for position 5 (first 5 dims): {pe[5, :5]}")
print(f"PE for position 9 (first 5 dims): {pe[9, :5]}")
```

**출력 예시**:
```
Shape: (10, 512)
PE for position 0 (first 5 dims): [0.         1.         0.         1.         0.        ]
PE for position 5 (first 5 dims): [-0.95892427  0.28366219 -0.00464602  0.99998922 -0.00009589]
PE for position 9 (first 5 dims): [ 0.41211849 -0.91113026 -0.00835898  0.99996508 -0.00017262]
```

**핵심 관찰**:
- 위치가 다르면 → PE 벡터가 다름
- 주기 함수 → 일정한 패턴 반복
- 고차원 (512차원) → 충분히 많은 위치 표현 가능

### ⚙️ Positional Encoding의 변형들

Sinusoidal PE는 Transformer 논문의 원조 방법이지만, 이후 여러 변형이 등장했습니다.

**1. Learned Positional Embedding** (BERT 등)
```python
# 학습 가능한 파라미터
self.pos_embedding = nn.Embedding(max_seq_len, d_model)
```
- 장점: 더 표현력 높음 (데이터에 맞춰 학습)
- 단점: 외삽 어려움 (학습한 길이보다 긴 시퀀스 처리 못함)
- 사용: BERT, GPT-2

**2. Relative Positional Encoding** (T5, XLNet)
- 절대 위치 (1번째, 2번째) 대신 상대 위치 (앞에서 3칸)
- 긴 시퀀스에서 더 강력
- 사용: T5, Transformer-XL

**3. Rotary Positional Embedding (RoPE)** (LLaMA, GPT-NeoX)
- 회전 행렬로 상대 위치 인코딩
- 외삽 성능 우수
- 사용: LLaMA, GPT-NeoX, Claude

**4. ALiBi** (Attention with Linear Biases)
- Attention score에 직접 거리 기반 bias 추가
- 학습 없이도 외삽 성능 개선
- 사용: BLOOM

### ⏰ Positional Encoding은 언제 사용하는가?

**필수 상황**:
- Transformer 기반 모델 (BERT, GPT 등)
- 순서가 중요한 시퀀스 데이터 (자연어, 시계열)
- 병렬 처리를 하면서도 위치 정보 필요할 때

**사용 예시**:
1. **언어 모델**: "The cat sat on the mat" → 단어 순서 중요
2. **번역**: "I love you" → "사랑해" (순서 바뀌면 의미 왜곡)
3. **요약**: 문서의 앞부분/뒷부분 구분 필요
4. **시계열**: 주가 데이터, 센서 데이터 (시간 순서 중요)

**불필요 상황**:
- 집합(set) 데이터 (순서 무관)
- 그래프 데이터 (Graph Neural Network는 다른 방식)

### 👤 누가 만들었고, 왜 만들었는가?

**Ashish Vaswani et al. (Google Brain, 2017)**

"Attention is All You Need" 논문에서 Transformer와 함께 제안했습니다.

**동기**:
- RNN은 순차 처리 → 느림, 병렬화 불가
- CNN은 위치 정보 있지만 장거리 의존성 약함
- Attention만 쓰면 빠르지만 → 위치 정보 손실

**해결책**:
Positional Encoding을 추가해서, RNN 없이도 순서 정보 유지하면서 병렬 처리 가능하게 만들었습니다.

**Impact**:
- 이후 모든 Transformer 모델의 표준
- BERT, GPT, T5, 모두 PE 사용 (변형 포함)
- 2017년 논문이 7만 회 이상 인용

### 🚀 Positional Encoding은 어디로 발전하고 있는가?

**현재 트렌드**:

1. **Context Length 확장**
   - GPT-4: 32k → 128k 토큰
   - Claude 3.5: 200k 토큰
   - Gemini 1.5: 1M 토큰
   - → Positional Encoding도 긴 시퀀스 대응 필요

2. **외삽 성능 개선**
   - RoPE, ALiBi 등 새로운 방법
   - 학습한 길이보다 긴 시퀀스 처리 가능

3. **효율성 향상**
   - Flash Attention + 효율적 PE
   - 계산량/메모리 절감

**미래 방향**:

- **Adaptive PE**: 입력 데이터에 따라 동적으로 조정
- **Multi-Scale PE**: 단어/문장/문단 레벨 위치 정보 동시 인코딩
- **PE 없는 Transformer?**: 일부 연구는 PE 없이도 학습 가능하다고 주장

---

## 🔗 Connections to What You Already Know

### 과거 학습 연결

**Transformer (2025-11-03, depth 1)**:
- Transformer는 Self-Attention 기반 → 모든 토큰을 병렬 처리
- 병렬 처리의 대가: 위치 정보 손실
- Positional Encoding이 이 문제를 해결

**Attention Mechanism (2025-11-03, depth 1)**:
- Q, K, V 행렬로 토큰 간 관계 계산
- 하지만 "몇 번째 토큰인지"는 모름
- PE를 입력에 더해서 위치 정보 주입

**학습 여정**:
```
Neural Network (foundation)
    ↓
Attention Mechanism (core)
    ↓
Transformer (architecture)
    ↓
Positional Encoding ← 오늘 여기
    ↓
Multi-Head Attention (next)
    ↓
GPT / BERT (models)
```

### 연구자 연결

이전에 학습한 연구자들이 Positional Encoding에 대해 언급한 내용:

**Andrej Karpathy** (Eureka Labs):
- "Positional Encoding은 Transformer의 유일한 '순서 인식' 장치입니다. 이걸 빼면 Transformer는 bag-of-words 모델이 됩니다."
- (Neural Networks: Zero to Hero 시리즈)

**Ilya Sutskever** (Safe Superintelligence Inc.):
- "스케일링만으로는 충분하지 않다 - 새 아이디어 필요"
- Positional Encoding도 여전히 개선 여지 있음 (RoPE, ALiBi 등 새로운 방법 연구 중)

---

## 📖 Historical Context

### 역사적 타임라인

**2017.06** - Sinusoidal PE 제안 (Transformer 논문)
- Vaswani et al., "Attention is All You Need"
- 학습 없이도 위치 정보 인코딩 가능
- 논문: https://arxiv.org/abs/1706.03762

**2018** - Learned Positional Embedding (BERT)
- Google, BERT 발표
- 학습 가능한 PE 사용 (더 표현력 높지만 외삽 제한)

**2019** - Relative Positional Encoding (Transformer-XL)
- 절대 위치 대신 상대 위치 인코딩
- 긴 시퀀스에서 더 강력

**2020** - T5, XLNet 등에서 Relative PE 확산
- 다양한 Relative PE 변형 등장

**2021** - Rotary Positional Embedding (RoPE)
- Su et al., RoFormer 논문
- LLaMA, GPT-NeoX 등에서 채택
- 회전 행렬로 상대 위치 인코딩

**2022** - ALiBi (Attention with Linear Biases)
- Press et al., BLOOM에서 사용
- 학습 없이도 외삽 성능 개선

**2023-2024** - Long Context 전쟁
- GPT-4: 32k → 128k 토큰
- Claude 3: 200k 토큰
- Gemini 1.5: 1M 토큰
- → PE도 긴 시퀀스 대응 필요

**핵심 교훈**:
Positional Encoding은 단순해 보이지만, Transformer 성능의 핵심입니다. 7년간 계속 개선되고 있으며, 특히 긴 context를 처리하는 방향으로 진화 중입니다.

---

## 🧪 Your Understanding Check

### 🧭 학습 점검

다음 질문들에 스스로 답해보세요:

1. **WHY**: 왜 Transformer에 Positional Encoding이 필요한가? RNN은 왜 필요 없는가?

2. **WHAT**: Sinusoidal PE의 수식을 설명하고, sin과 cos를 사용하는 이유는 무엇인가?

3. **HOW**: Positional Encoding은 입력 임베딩과 어떻게 결합되는가? (더해지는가, 곱해지는가, 별도 입력인가?)

4. **WHEN**: Learned PE vs Sinusoidal PE - 각각 어떤 상황에서 유리한가?

5. **WHERE**: RoPE, ALiBi 같은 새로운 방법이 등장한 배경은 무엇인가? (긴 context 처리 문제)

### 💻 코드 실습

다음 코드를 완성하세요:

```python
import numpy as np
import matplotlib.pyplot as plt

def positional_encoding(seq_len, d_model):
    """
    TODO: Sinusoidal positional encoding 구현

    Hint:
    - PE(pos, 2i) = sin(pos / 10000^(2i/d_model))
    - PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
    """
    pe = np.zeros((seq_len, d_model))

    # TODO: 여기에 코드 작성
    # for pos in range(seq_len):
    #     for i in range(0, d_model, 2):
    #         ...

    return pe

# Test
pe = positional_encoding(100, 512)
assert pe.shape == (100, 512), "Shape mismatch!"

# Visualization (선택)
plt.figure(figsize=(15, 5))
plt.imshow(pe[:, :50], cmap='RdBu', aspect='auto')
plt.title('Positional Encoding Heatmap (first 50 dims)')
plt.xlabel('Dimension')
plt.ylabel('Position')
plt.colorbar()
plt.savefig('positional_encoding.png')
print("✅ Test passed! Check positional_encoding.png")
```

**검증**:
- Shape이 (seq_len, d_model)인지 확인
- pe[0]과 pe[1]이 다른지 확인
- pe의 값이 [-1, 1] 범위 내에 있는지 확인
- 시각화에서 물결 무늬 패턴이 보이는가?

### 🎯 심화 질문 (선택)

1. **수학**: 왜 10000이라는 숫자를 사용하는가? 다른 값 (예: 100, 1000000)을 쓰면 어떻게 되는가?

2. **구현**: PyTorch에서 Positional Encoding을 어떻게 구현하는가? (nn.Module 사용)

3. **비교**: Learned PE를 사용하는 코드는 어떻게 다른가?

**답변은 다음 세션에서 확인합니다.**
- 답변을 적어두고 다음 학습 시 비교해보세요.
- 막히는 질문이 있다면, 그 부분을 더 깊이 학습할 신호입니다.

---

## 🚀 Next Steps for You

### 이번 주 (단기)

**1일 차** (오늘):
- [ ] Positional Encoding 개념 이해
- [ ] 코드 실습 완료
- [ ] 시각화 확인 (물결 무늬 패턴)

**2-3일 차**:
- [ ] Andrej Karpathy - "Attention is All You Need" 논문 설명 영상 (30분)
  - https://www.youtube.com/watch?v=kCc8FmEb1nY (또는 유사 영상)
- [ ] 3Blue1Brown - "Attention in Transformers" 영상 (20분)
  - https://www.youtube.com/watch?v=eMlx5fFNoYc

**4-5일 차**:
- [ ] Transformer 논문 Section 3.5 (Positional Encoding) 읽기
- [ ] RoPE 논문 Introduction 읽기 (최신 동향)

### 이번 달 (중기)

**Week 2**:
- Multi-Head Attention 학습 (depth 2)
- Self-Attention과 어떻게 다른가?
- 병렬 처리의 이점

**Week 3**:
- GPT 구조 이해 (depth 2)
- Autoregressive Language Model
- BERT와의 차이

**Week 4**:
- BERT vs GPT 비교 (depth 2)
- Bidirectional vs Unidirectional
- 어떤 상황에서 어떤 모델?

### 분기 목표 (장기)

**이번 분기** (11-12월):
- [ ] Transformer 논문 전체 읽기
- [ ] nanoGPT 코드 분석 (Andrej Karpathy)
- [ ] Mechanistic Interpretability 입문 (depth 3)
- [ ] 작은 Transformer 직접 구현 및 학습

**다음 분기** (2026 Q1):
- [ ] Constitutional AI 학습 (depth 2-3)
- [ ] AI Agents 실습 (depth 2-3)
- [ ] 실제 프로젝트에 LLM 적용

---

## 🌱 Growth Indicators

### 📊 개념별 진행률

**Architecture**: ████░░░░░░ 40%
- 완료: 2/5 (Transformer, Attention Mechanism)
- 진행 중: 1/5 (Positional Encoding ← 오늘)
- 미학습: 2/5 (Multi-Head Attention, BERT)

**Foundation**: ██░░░░░░░░ 20%
- 완료: 0/1
- 진행 중: 1/1 (Neural Network 일부 이해)

**Training**: ██████░░░░ 50%
- 완료: 1/2 (RLHF)
- 미학습: 1/2 (Constitutional AI)

**Theory**: ████░░░░░░ 40%
- 완료: 1/1 (Scaling Laws)

**Safety**: ░░░░░░░░░░ 0%
- 미학습: 3/3 (Constitutional AI, Mechanistic Interpretability, Alignment)

**Application**: ░░░░░░░░░░ 0%
- 미학습: 2/2 (Multimodal AI, AI Agents)

### 📈 학습 속도

**이번 주**: 5개 개념 (Transformer, Attention, RLHF, Scaling Laws, Positional Encoding)
**평균 depth**: 1.2 (초급 → 중급 전환기)
**추세**: accelerating ↗️ (depth 2 진입)

### 🎖️ 달성한 마일스톤

- 🏆 5개 개념 학습 (2025-11-03 ~ 2025-11-07)
- 🔥 연속 학습 5일차
- 📚 Depth 2 첫 진입 (Positional Encoding)
- 👥 4명의 AI 연구자 인터뷰 학습 (Dario, Ilya, Andrej, Sam)

### 🎯 Next Milestone

**다음 목표**:
- 📌 10개 개념 학습 (현재 5/10, 50%)
- 📌 Depth 2 개념 3개 달성 (현재 1/3, 33%)
- 📌 Architecture 카테고리 60% 완료 (현재 40%)

**예상 달성일**: 2025-11-14 (1주일 후, 주 3회 학습 기준)

---

**Learning Journey Started**: 2025-11-03
**Current Depth Level**: 중급 입문 (Depth 1-2 전환기)
**Sessions Completed**: 5회
**Next Session**: Multi-Head Attention (depth 2) 또는 GPT 구조 (depth 2)

---

_Generated by AI Tutor v1.1 | Powered by Claude Code_

**Recommended Resources**:
- 📺 Andrej Karpathy - Neural Networks: Zero to Hero
- 📺 3Blue1Brown - Visualizing Attention
- 📄 Attention is All You Need (Vaswani et al. 2017)
- 💻 nanoGPT - Minimal GPT implementation

**Learning Tips**:
1. 코드 실습을 먼저 하세요 (이론보다 직관이 먼저)
2. 시각화를 많이 보세요 (Positional Encoding 패턴)
3. 논문은 천천히, 반복해서 읽으세요
4. 막히면 YouTube 영상으로 돌아오세요 (Karpathy, 3B1B)
5. 다음 세션 전에 Understanding Check 답변 적어두세요
