# 📚 강의 개요
## 목표

- Word2Vec의 나머지 개념 정리

- 단어 의미를 더 잘 포착할 수 있는 방법 탐색

- 단어 임베딩 평가 방법

- 단어 다의성과 Word Sense

- 분류(classification)와 신경망 도입

# 🧠 Word2Vec 복습 및 확장
## 기본 아이디어
~~~
- 단어 벡터는 초기에는 랜덤

- 중심 단어(c)로 주변 단어(o)를 예측하며 벡터 업데이트

- 문제점: Softmax의 분모 계산이 너무 비쌈
→ 해결: Negative Sampling

- 진짜 단어쌍과 가짜 단어쌍을 구분하는 이진 분류 문제로 전환

- 자주 등장하는 단어는 덜 뽑히도록 확률 조정 P(w)∝U(w)^3/4

~~~
# 📊 단어 임베딩 직접 카운팅은 어떤가?
## Co-occurrence Matrix

- 윈도우 기반 동시 등장 행렬을 만들고 단어 벡터로 사용

- 고차원이고 희소하지만 의미 정보는 있음

## 차원 축소 방법

- SVD (Singular Value Decomposition)로 dense vector 추출

- 여러 스케일링 트릭 (log, 빈도 상한선, 불용어 제거 등)을 적용하면 성능 향상

## GloVe

- 단어 간 공기 확률의 비율을 벡터 차이로 표현

- Word2Vec과 달리 글로벌 정보 사용

- 빠르게 학습 가능하고 대규모 코퍼스에 적합

# 🔍 단어 벡터 평가
## 내재적 평가 (Intrinsic)
~~~
유사도/유추 과제:

예: king - man + woman ≈ queen

cosine similarity, WordSim353 등

GloVe가 Word2Vec보다 전반적으로 좋은 성능
~~~
## 외재적 평가 (Extrinsic)
~~~
실제 NLP 태스크에서의 성능 측정

예: Named Entity Recognition (NER), 문장 분류 등
~~~
# 🔁 Word Sense (다의어 문제)
- 대부분 단어는 다의어

- Word2Vec 같은 단일 벡터로는 모든 의미를 담기 어려움

- 해결책:
~~~
1. 다중 프로토타입 방식

각 단어의 문맥을 클러스터링해 여러 벡터로 표현 (Huang et al.)

2. 선형 중첩 이론 (Arora et al.)

하나의 단어 벡터는 여러 의미 벡터의 가중합으로 표현 가능

희소 부호화 기반으로 의미를 분리할 수 있음
~~~
# 🧠 신경망 분류기 소개
## NER 과제 예시

- 문장에서 인물, 장소, 날짜 등의 엔터티를 식별

- 예: “Paris Hilton lives in Palo Alto.” → PER, PER, LOC

## 단순 분류기

- 중심 단어 주변 단어 벡터를 concatenate → 로지스틱 회귀로 분류

- 또는 Softmax 분류기 사용

## 신경망 분류기

- 임베딩 벡터를 학습하면서 W (가중치)도 함께 학습

- 여러 층을 쌓아 비선형 함수 근사 가능

## 손실 함수

- Cross-Entropy Loss 사용 (PyTorch에서 기본)

# 🧮 신경망 구조
~~~
입력 벡터 → 여러 뉴런(logistic unit) 통과 → 히든 레이어 → 출력 레이어

비선형 활성화 함수 (sigmoid, ReLU 등) 사용으로 복잡한 함수 근사 가능

여러 층 쌓으면 복잡한 구조도 학습 가능
~~~
# 📝 핵심 요약
- Word2Vec은 확률적 예측으로 단어 간 유사도 학습

- Negative Sampling으로 학습 속도 개선

- Co-occurrence 기반 모델(GloVe)도 강력한 대안

- 단어 의미는 다의어 문제를 해결해야 더 잘 표현됨

- 신경망은 단순 분류기보다 더 유연하고 강력한 모델 구성 가능
