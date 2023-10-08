---
title: "Pytorch實作系列 — DQN"
description: "Deep Q Learning 是由Mnih et al.(2014)提出，可以說是第一個將增強學習與深度學習結合的經典範例。"
date: 2020-12-07T13:47:35.464Z
image: "concept.webp"
author: "Mike Bai"
tags:
    - reinforcement learning
categories:
    - deep-learning
    - pytorch
published: true
---

## 簡介

Deep Q Learning 是由Mnih et al.(2014)在 *Playing Atari with Deep Reinforcement Learning* 提出，可以說是第一個將增強學習與深度學習結合的經典範例。

## 環境

CartPole-v0，向左或向右使木桿不傾倒的遊戲。

## 網路

設計概念是經由卷積的滑窗特性達到序列建模的性質，同時藉由遮掩未來訊息達到因果(causal)性質，也就是未來不影響現在。

![網路](concept.webp)

## 損失函數

採用Smooth L1 loss。

## 訓練

概念上先更新策略網路，以策略網路計算回憶的Q，目標網路計算value，隔一陣子更新目標網路。

## 評估

訓練不是很穩定，有時最久可維持90次計數，有時又只能30次或10次。

## 代碼連結

* [github repo](https://github.com/gitE0Z9/classical-network-series)

## 參考

* [tutorial](https://pytorch.org/tutorials/intermediate/reinforcement_q_learning.html)

* [paper](https://arxiv.org/abs/1312.5602)
