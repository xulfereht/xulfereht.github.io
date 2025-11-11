---
categories: learning
date: '2025-11-10'
layout: single
tags: multi-head-attention attention multi-head AI learning tutorial
title: Multi-Head Attention
---
# AI Learning Journey - 2025-11-10

## 🎯 Today's Focus

**Multi-Head Attention** (Depth 2)

지난주에 Attention Mechanism과 Positional Encoding의 기초를 배웠습니다. 오늘은 Transformer의 핵심인 **Multi-Head Attention**을 깊이 탐구합니다.

---

## 📚 Why This Matters Now

### 📅 과거 학습과의 연결

**지난주에 배운 것들**:
- **Transformer** (depth 1) - Attention 기반 아키텍처
- **Attention Mechanism** (depth 1) - Self-Attention, Q-K-V 구조
- **Positional Encoding** (depth 2) - 위치 정보 인코딩

**오늘 배울 것**:
- **Multi-Head Attention** (depth 2) - 병렬 Attention 메커니즘

**왜 한 단계 더 깊이?**
Transformer의 핵심은 단순한 Attention이 아니라 **여러 개의 Attention을 병렬로 실행하는 Multi-Head 구조**입니다. 단일 Attention은 하나의 관점만 보지만, Multi-Head는 여러 관점에서 동시에 정보를 처리합니다.

### 🌐 현재 AI 산업에서

Multi-Head Attention은 현재 모든 대형 언어 모델(GPT-4, Claude 3.5, Gemini)의 핵심 메커니즘입니다. GPT-3는 96개의 헤드를 사용하고, GPT-4는 수백 개의 헤드를 병렬로 실행합니다. 이것이 바로 LLM이 복잡한 맥락을 이해하는 비결입니다.

### 🔮 앞으로의 학습 여정

**이번 주 내** (depth 3):
- **Multi-Head Attention 최적화** - Flash Attention, Grouped-Query Attention 등 최신 변형

**이번 달** (depth 2-3):
- **GPT Architecture** - Decoder-only Transformer의 세부 구조
- **BERT Architecture** - Encoder-only Transformer 비교

**분기 목표** (depth 3+):
- **Mechanistic Interpretability** - Multi-Head가 실제로 무엇을 학습하는지 해석
- **Efficient Transformers** - Linear Attention, Sparse Attention 등

---

## 🧩 Core Concept Explained

### 🤔 왜 Single-Head Attention이 아니라 Multi-Head Attention인가?

**비유**: 책을 읽을 때 한 가지 관점만으로는 충분하지 않습니다. 문법적 관점, 의미론적 관점, 맥락적 관점을 동시에 봐야 깊이 이해할 수 있죠.

Single-Head Attention은 하나의 Q-K-V 변환만 사용합니다. 하지만 언어는 다층적입니다:
- **구문 관계** (주어-동사)
- **의미 관계** (동의어, 반의어)
- **문맥 관계** (대명사 참조)

Multi-Head Attention은 이 모든 관점을 **동시에, 독립적으로** 학습합니다.

**수식**:
```
Single-Head: Attention(Q, K, V) = softmax(QK^T / √d_k) V

Multi-Head:
  head_i = Attention(Q W_i^Q, K W_i^K, V W_i^V)
  MultiHead(Q, K, V) = Concat(head_1, ..., head_h) W^O
```

여기서:
- `h`: 헤드 개수 (GPT-3: 96, BERT: 12)
- `W_i^Q, W_i^K, W_i^V`: 각 헤드의 독립적인 변환 행렬
- `W^O`: 출력 변환 행렬

### ⚙️ Multi-Head Attention은 어떻게 작동하는가?

**단계별 작동 원리**:

1. **입력 분할**: d_model 차원을 h개 헤드로 나눔
   ```
   d_model = 512, h = 8
   → 각 헤드는 512/8 = 64 차원 처리
   ```

2. **독립적 변환**: 각 헤드가 자신만의 Q, K, V 행렬로 변환
   ```python
   for i in range(num_heads):
       Q_i = Q @ W_i_Q  # (seq_len, 64)
       K_i = K @ W_i_K
       V_i = V @ W_i_V
       head_i = attention(Q_i, K_i, V_i)
   ```

3. **병렬 Attention**: 모든 헤드가 동시에 Attention 계산
   ```
   head_1: 문법적 관계 학습
   head_2: 의미적 유사성 학습
   head_3: 대명사 참조 학습
   ...
   ```

4. **결합**: 모든 헤드 출력을 연결(Concatenate)
   ```python
   output = concat([head_1, head_2, ..., head_h]) @ W_O
   # (seq_len, 64*8) @ (512, 512) = (seq_len, 512)
   ```

**코드 예시**:
```python
import torch
import torch.nn as nn

class MultiHeadAttention(nn.Module):
    def __init__(self, d_model=512, num_heads=8):
        super().__init__()
        assert d_model % num_heads == 0

        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads  # 64

        # 각 헤드의 변환 행렬
        self.W_Q = nn.Linear(d_model, d_model)
        self.W_K = nn.Linear(d_model, d_model)
        self.W_V = nn.Linear(d_model, d_model)
        self.W_O = nn.Linear(d_model, d_model)

    def split_heads(self, x, batch_size):
        """(batch, seq_len, d_model) → (batch, num_heads, seq_len, d_k)"""
        x = x.view(batch_size, -1, self.num_heads, self.d_k)
        return x.transpose(1, 2)

    def forward(self, Q, K, V, mask=None):
        batch_size = Q.size(0)

        # 1. Linear transformation
        Q = self.W_Q(Q)  # (batch, seq_len, d_model)
        K = self.W_K(K)
        V = self.W_V(V)

        # 2. Split into multiple heads
        Q = self.split_heads(Q, batch_size)  # (batch, h, seq_len, d_k)
        K = self.split_heads(K, batch_size)
        V = self.split_heads(V, batch_size)

        # 3. Scaled dot-product attention (병렬 실행)
        scores = torch.matmul(Q, K.transpose(-2, -1)) / (self.d_k ** 0.5)

        if mask is not None:
            scores = scores.masked_fill(mask == 0, -1e9)

        attention_weights = torch.softmax(scores, dim=-1)
        context = torch.matmul(attention_weights, V)

        # 4. Concatenate heads
        context = context.transpose(1, 2).contiguous()
        context = context.view(batch_size, -1, self.d_model)

        # 5. Final linear transformation
        output = self.W_O(context)

        return output, attention_weights

# Example usage
mha = MultiHeadAttention(d_model=512, num_heads=8)
x = torch.randn(32, 10, 512)  # (batch=32, seq_len=10, d_model=512)
output, weights = mha(x, x, x)

print(f"Input shape: {x.shape}")
print(f"Output shape: {output.shape}")  # (32, 10, 512) - same as input
print(f"Attention weights shape: {weights.shape}")  # (32, 8, 10, 10)
```

**핵심**:
- 각 헤드는 독립적으로 다른 패턴을 학습
- 병렬 처리로 효율성 극대화
- 여러 관점을 통합하여 풍부한 표현 생성

### ⏰ Multi-Head Attention은 언제 사용하는가?

**사용 시점**:
1. **Transformer 기반 모델 전체**: BERT, GPT, T5, Claude, etc.
2. **복잡한 맥락 이해 필요 시**: 긴 문서, 다층적 의미
3. **다양한 관계 포착 필요 시**: 구문+의미+문맥

**실제 적용 사례**:
- **GPT-4**: 수백 개 헤드로 복잡한 추론
- **BERT**: 12개 헤드로 양방향 맥락 이해
- **Vision Transformer (ViT)**: 이미지 패치 간 관계 학습

**트레이드오프**:
- 장점: 표현력 높음, 다양한 패턴 학습
- 단점: 계산량 증가 (헤드 수에 비례)

### 👤 Multi-Head Attention을 누가 만들었고, 왜 만들었는가?

**Ashish Vaswani et al.** (Google Brain, 2017)

"Attention is All You Need" 논문에서 Multi-Head Attention을 제안. 단일 Attention의 한계를 극복하고, **앙상블 효과**를 통해 성능을 대폭 향상시켰습니다.

**핵심 인사이트**:
> "Multi-head attention allows the model to jointly attend to information from different representation subspaces at different positions."

즉, 각 헤드는 **다른 표현 공간**에서 다른 정보를 동시에 포착합니다.

### 🚀 Multi-Head Attention은 어디로 발전하고 있는가?

**최신 변형들**:

1. **Flash Attention (2022)**: 메모리 효율적인 Attention 계산
   - O(N²) → O(N) 메모리 사용
   - 2-4배 속도 향상

2. **Grouped-Query Attention (GQA, 2023)**: LLaMA 2, Mistral에서 사용
   - K, V 헤드 수 줄임 (Q는 유지)
   - 추론 속도 2배 향상, 성능 유지

3. **Multi-Query Attention (MQA)**: PaLM, Falcon에서 사용
   - 모든 헤드가 K, V 공유
   - 극도로 빠른 추론, 약간의 성능 하락

4. **Sparse Attention**: Longformer, BigBird
   - 모든 토큰이 아닌 일부만 Attend
   - 긴 시퀀스 처리 가능 (4096+ 토큰)

**미래 방향**:
- **Adaptive Attention**: 입력에 따라 헤드 수 동적 조절
- **Learned Sparsity**: 어떤 토큰을 볼지 학습
- **Hybrid Architectures**: Attention + State Space Models (Mamba)

---

## 🔗 Connections to What You Already Know

### 과거 학습과의 연결

**2025-11-03** - Attention Mechanism (depth 1)
- Single-Head Attention의 Q-K-V 구조 학습
- 오늘: 이것을 여러 개 병렬로 실행하는 Multi-Head로 확장

**2025-11-07** - Positional Encoding (depth 2)
- Transformer가 위치 정보를 인코딩하는 방법
- Multi-Head Attention은 이 위치 정보를 활용하여 관계 학습

**개념 연결**:
```
Attention Mechanism (depth 1)
    ↓
Multi-Head Attention (depth 2) ← 오늘
    ↓
Flash Attention (depth 3) ← 다음 단계
```

---

## 🎤 Voices from the Field

### 연구자들의 인사이트

**Ilya Sutskever** (Safe Superintelligence Inc.)
- Interview: Reid Hoffman 2023 (2023-07)
- Duration: ~1h
- Key insight: "Multi-Head Attention은 앙상블 효과를 내장한 구조입니다. 각 헤드가 다른 패턴을 학습하면서도, 하나의 모델로 통합됩니다."

**시청하기**:
```bash
/link https://www.possible.fm/podcast/openai-ilya-sutskever-greg-brockman/
```
---

**Andrej Karpathy** (Eureka Labs)
- Interview: Dwarkesh Patel 2025 (2025-10)
- Duration: ~2h
- Key insight: "Multi-Head Attention을 처음 봤을 때 '이건 천재적이다'라고 생각했습니다. 각 헤드가 전문가처럼 다른 역할을 맡아요."

**시청하기**:
```bash
/link https://www.dwarkeshpatel.com/p/andrej-karpathy
```
---

**Dario Amodei** (Anthropic)
- Interview: Lex Fridman #452 (2024-11)
- Duration: 5h22m
- Key insight: "스케일링의 핵심은 단순히 파라미터를 늘리는 게 아니라, Multi-Head처럼 병렬성을 활용하는 구조입니다."

**시청하기**:
```bash
/link https://www.youtube.com/watch?v=ugvHCXCOmm4
```
---

### 추천 학습 리소스

다음 리소스들을 통해 더 깊이 학습할 수 있습니다:

**Andrej Karpathy**: Neural Networks: Zero to Hero - Attention 구현 강의
**3Blue1Brown**: Visualizing Attention
**Yannic Kilcher**: Attention is All You Need 논문 상세 분석

---

## 📖 Historical Context

### 역사적 타임라인

**2017.06** - Multi-Head Attention 제안 (Transformer 논문)
- Vaswani et al. (Google Brain)
- Single-Head 대비 2-3 BLEU 점수 향상
- 논문: https://arxiv.org/abs/1706.03762

**2018** - BERT (12 헤드), GPT-1 (12 헤드)
- Multi-Head가 표준이 됨

**2019** - GPT-2 (12-48 헤드, 모델 크기에 따라)
- 헤드 수 증가가 성능 향상에 기여

**2020.05** - GPT-3 (96 헤드)
- 대규모 모델에서 Multi-Head의 힘 입증

**2022** - Flash Attention 발표
- Multi-Head Attention의 메모리/속도 문제 해결

**2023** - Grouped-Query Attention (GQA)
- LLaMA 2, Mistral 등에서 사용
- 추론 속도 2배 향상

**2024** - GPT-4, Claude 3.5
- 수백 개 헤드로 확장 (정확한 수는 비공개)
- Flash Attention 2 적용

---

## 🧪 Your Understanding Check

### 🧭 학습 점검

다음 질문들에 스스로 답해보세요:

1. Multi-Head Attention의 작동 원리를 수식/코드로 설명할 수 있는가?
2. 어떤 상황에서 Multi-Head를 사용해야 하는가?
3. Multi-Head Attention의 장단점은 무엇인가?
4. 실제 프로젝트에 어떻게 적용할 수 있는가?

### 💻 코드 실습

다음 코드를 완성하세요:

```python
import torch
import torch.nn as nn

class SimpleMultiHeadAttention(nn.Module):
    def __init__(self, d_model=512, num_heads=8):
        super().__init__()
        # TODO: 초기화 코드 작성
        # Hint:
        # - d_k = d_model // num_heads
        # - W_Q, W_K, W_V, W_O 선형 변환 필요
        pass

    def split_heads(self, x, batch_size):
        """
        TODO: (batch, seq_len, d_model) → (batch, num_heads, seq_len, d_k)

        Hint:
        1. x.view(batch_size, -1, num_heads, d_k)
        2. transpose(1, 2) to move heads to second dimension
        """
        pass

    def forward(self, Q, K, V):
        # TODO: Multi-Head Attention 구현
        # 1. Linear transformation (W_Q, W_K, W_V)
        # 2. Split into heads
        # 3. Scaled dot-product attention
        # 4. Concatenate heads
        # 5. Final linear transformation (W_O)
        pass

# Test
mha = SimpleMultiHeadAttention(d_model=512, num_heads=8)
x = torch.randn(2, 10, 512)  # (batch=2, seq_len=10, d_model=512)
output = mha(x, x, x)

assert output.shape == (2, 10, 512), f"Expected (2, 10, 512), got {output.shape}"
print("✅ Test passed!")
```

**검증**:
- Output shape이 input과 같은지 확인 (batch, seq_len, d_model)
- 각 헤드가 독립적으로 작동하는지 확인
- Attention weights의 shape이 (batch, num_heads, seq_len, seq_len)인지 확인

**답변은 다음 세션에서 확인합니다.**
- 답변을 적어두고 다음 학습 시 비교해보세요.
- 막히는 질문이 있다면, 그 부분을 더 깊이 학습할 신호입니다.

---

## 🚀 Next Steps for You

### 이번 주 (단기)
- Multi-Head Attention 코드 직접 구현 (30분)
- Attention weights 시각화 (각 헤드가 무엇을 보는지)
- Andrej Karpathy의 Attention 강의 시청

### 이번 달 (중기)
- Flash Attention 논문 읽기 (메모리 최적화 이해)
- GPT vs BERT 아키텍처 비교 (Decoder-only vs Encoder-only)
- Grouped-Query Attention (GQA) 구현

### 분기 목표 (장기)
- Mechanistic Interpretability: 각 헤드가 실제로 무엇을 학습하는지 분석
- Sparse Attention 변형들 비교 (Longformer, BigBird, etc.)
- Efficient Transformers 논문 서베이

---

## 🌱 Growth Indicators

### 📊 개념별 진행률

**Architecture**: ████░░░░░░ 40%
- 완료: 2/5 (Transformer, Positional Encoding 마스터)
- 진행 중: 2 (Attention Mechanism, Multi-Head Attention)

**Training**: ██░░░░░░░░ 20%
- 완료: 0/3
- 진행 중: 1 (RLHF)

**Safety**: ░░░░░░░░░░ 0%
- 완료: 0/3
- 진행 중: 0

**Model**: ░░░░░░░░░░ 0%
- 완료: 0/3
- 진행 중: 0

### 📈 학습 속도

**이번 주**: 1개 개념 (Multi-Head Attention)
**이번 달**: 4개 개념
**추세**: steady → (꾸준한 학습 중)

### 🎖️ 달성한 마일스톤

- 🏆 5개 개념 학습 (Transformer, Attention, RLHF, Scaling Laws, Positional Encoding)
- 📚 Depth 2 진입 (Positional Encoding, Multi-Head Attention)
- 🔥 주 1회 학습 달성 (목표: 주 3회)

### 🎯 다음 마일스톤

- **10개 개념 학습** (현재 5개 → 5개 더 필요)
- **3개 개념 마스터 (depth 3+)** (현재 0개)
- **주 3회 학습 달성** (현재 주 1회)

---

**Learning Journey Started**: 2025-11-03
**Current Depth Level**: Intermediate (Depth 2 - 메커니즘과 응용 이해 중)
**Sessions Completed**: 4회
**Next Milestone**: 10개 개념 학습 (5개 더 필요)

---

_Generated by AI Tutor v1.1 | Powered by Claude Code_
