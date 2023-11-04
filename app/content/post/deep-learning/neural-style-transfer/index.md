---
title: "Pytorch 實作系列 — Neural style transfer"
description: "圖像風格遷移由Gatys et al.(2016)提出，是最早使圖片能變換成另一張圖片風格的深度學習技術之一。"
date: 2020-12-10T14:02:33.883Z
image: "output.png"
author: "Mike Bai"
tags:
    - computer vision
    - computer art
categories:
    - deep-learning
    - pytorch
published: true
---

## 簡介

Neural style transfer 由 Gatyss et al. (2016)在論文 *A Neural Algorithm of Artistic Style* 提出，是最早使圖片能變換成另一張圖片風格的深度學習技術之一。

## 網路

![network](network.webp)

## 損失函數

採用 MSE loss 做內容損失和風格損失。每次迭代更新內容圖片，使得輸出圖片可以更接近風格圖片。

## 訓練

採用LBFGS最佳化，以第四層卷積特徵圖計算輸入圖片與內容圖片的內容損失，取前五層卷積特徵圖計算輸入圖片與風格圖片的風格損失，風格損失經Gram矩陣處理後比較。

## 評估

![左邊是101，右邊是梵谷的星空](compare.png)

![合成圖，高解析度有助表現](output.png)

## 筆記

Gram矩陣可以視為顏色的變異數矩陣，有利於學習風格圖片與內容圖片間的顏色變化。

風格遷移的損失函數是以內容圖片的重建損失為目標，並以風格圖片的損失做規範，這也體現在內容圖片只取一層並且比較整張圖的數值，確保輸入的圖片可以保持內容圖片的特質，而風格圖片則用Gram矩陣表示，並取多層訓練，將不同層次的風格特質加入到生成的圖片上。

使用的卷積特徵是前五層，沒有使用更深的網路，可能是基於淺層的卷積過濾器可取得低階的語意特徵(線條、紋理)，在深層的網路取得的是抽象語意特徵。雖然取的層跟論文不同，但結果不差。

## 代碼連結

* [github repo](https://github.com/gitE0Z9/classical-network-series)

## 參考

* [original github repo](https://pytorch.org/tutorials/advanced/neural_style_tutorial.html)

* [paper](https://arxiv.org/abs/1508.06576)