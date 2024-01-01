---
title: "矩陣分解"
description: "記錄幾種常用的矩陣分解方法"
date: 2023-12-27T19:00:00.000Z
image: "matrix.png"
author: "Mike Bai"
tags:
    - math
    - linear algebra
categories:
    - math
published: true
---

## 方法

### 上下三角分解(LU decomposition)

$A = LU$

$A$是方陣，$L$是下三角矩陣，$U$是上三角矩陣。

- *Cholesky decomposition*: 若$A$是正定矩陣或Hermitian，則 $A=LL^{\dagger}$，此關係是唯一且一定存在

- *Partial pivoting*: $PA=LU$，$P$是permutation矩陣

- *LDU decomposition*: $D$是對角矩陣，$L$跟$U$是unitriangular矩陣(對角是1)

### QR分解(QR decomposition)

$A = QR$

$Q$是正交矩陣，$R$是上三角矩陣

### 正交分解(orthogonal decomposition)

$A = UTV^*$

$U$跟$V^*$是unitary矩陣，$T$是三角矩陣

### 極分解(Polar decomposition)

$A = UP$

$detA = detUdetP = e^{i\theta}r$

$U$是unitary矩陣，$P$是半正定Hermitian矩陣

=> $U$是正交矩陣，$P$是半正定對稱矩陣

### Schur分解(Schur decomposition)

$A = USU-1$

$A$是方陣，$U$是unitary矩陣，$S$是上三角矩陣

### 本徵分解(eigen decomposition) / 譜分解(spectral decomposition)

$A = U{\Lambda}U^{-1}$

${\Lambda}$是本徵值的對角矩陣，$U$是本徵向量組成的矩陣

可從關係式$AU = U{\Lambda}$推導而來，是$Ax = {\lambda}x$的矩陣版本

### 奇異值分解(sigular value decomposition, SVD)

$A = U{\Sigma}V^*$

$U$跟$V$是unitary矩陣，${\Sigma}$是對角矩陣，具備low-rank性質

SVD的特性之一是可以用更少rank的表達呈現原有資訊，被使用在IMDB推薦比賽中獲勝而獲得更多名聲，過去也被使用在線性迴歸、降低維度（資訊壓縮或多變數分析）及語意分析

## 應用面

矩陣分解多半應用在解決線性系統的數學問題上，用來簡化複雜計算

### 推薦系統

*協同過濾中的奇異值分解(SVD)*： 奇異值分解藉由分解用戶-內容交互矩陣，有助於識別對用戶偏好有貢獻的潛在因素(latent factor)，從而實現個性化推薦。

$I = U{\Sigma}C$

$I$是交互矩陣，也就是使用者與內容互動的量化結果。

$U$是用戶的潛在因素矩陣，用一個向量表達用戶。

${\Sigma}$是潛在因素矩陣，介接用戶$U$跟$C$。

$C$是內容的潛在因素矩陣，用一個向量表達內容。

### 機器人學

*QR分解在機器人運動學中的應用*： QR分解在解決機器人逆運動學問題中被廣泛應用。通過分解變換矩陣，QR分解簡化了關節角度的計算，從而實現機器人的高效運動。

機器人學上會需要計算Euler angle的旋轉矩陣，推導從初始狀態移動到最後狀態的情況。可以參考線性啟示錄的[Givens旋轉](https://ccjou.wordpress.com/2010/02/18/givens-%E6%97%8B%E8%BD%89%E6%96%BC-qr-%E5%88%86%E8%A7%A3%E7%9A%84%E6%87%89%E7%94%A8/)。

### 統計迴歸

*LU分解在線性迴歸中的應用*： LU分解被用於解決線性迴歸問題，提供了解決線性方程組的數值方法。這種分解方法增強了迴歸計算的穩定性和效率。

統計迴歸的矩陣運算，需要以下權重${\beta}={(X^{\prime}X)}^{-1}X^{\prime}Y$，而此共變異矩陣的反矩陣計算量較高，不穩定性也高。因此若可用LU分解共變異矩陣的話，$X^{\prime}X=LU$，前者是一個實正定對稱矩陣，所以可以用Cholesky分解進一步簡化。

### 數學分析

*本徵分解在動態系統中的應用*： 本徵分解應用於數學分析，特別是理解線性動態系統的行為。它允許將系統動態表示為本徵值和本徵向量，有助於穩定性分析。

在求解動態系統的微分方程時，本徵分解可取出對應的本徵值和本徵向量，本徵值可用來表達系統的穩定程度，而本徵向量表達穩定狀態。

$A^t = U{\Lambda^t}U^{-1}$

上式反映出當系統狀態是本徵向量時，$A$的效果可用本徵值表達，即便$A$持續作用$t$遍，因此若本徵值的大小也反映了系統演化的程度。

### 圖神經網路

*圖神經網路中的譜圖理論*： 在圖神經網路（GNN）中，利用矩陣的本徵分解和譜性質來分析圖結構。譜圖理論根植於本徵分解，有助於理解神經網絡應用中的圖連通性和性質。

利用本徵分解的特性，可以重構出一組線性獨立的新基底，且本徵值反映了基底間的重要性。譜圖理論從拉普拉斯量矩陣推導，利用本徵值反映出圖的連通結構數。

