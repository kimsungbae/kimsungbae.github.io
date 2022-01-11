---
layout: default
title: Pandas
parent: Python
nav_order: 2
---

# Pandas
{: .no_toc }
 

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## DataFrame.idxmin() / DataFrame.idxmax() : 최소/최대값 인덱스 

### 메서드 설명
  - idxmin(): 최소값을 가지는 인덱스 출력
  - idxmax(): 최대값을 가지는 인덱스 출력

### 메서드 사용 방법
```
idxmin(axis=0, skipna=True)
idxmas(axis=0, skipna=Treu)

  - axix
      default         : 0
      0 or 'index'    : 열 방향으로 최소/최대값 탐색 후 행마다 출력
      1 or 'columns'  : 행 방향으로 최소/최대값 탐색 후 열마다 출력
  - skipna
      default         : True
      True            : NaN값을 제외하고 나머지 값에서 출력
      False           : NaN이 값이 있을 경우 NaN값 출력
```

### 기타
  - 최소/최대값이 중복되면 가장 앞부분에 있는 인덱스 출력
  - Numpy함수에는 argmin() / argmax() 존재

### 예시
```
>>> df = pd.DataFrame({'영어':[100, 90, 80],
···                    '수학':[95, 85, 85],
···                    '과학':[NaN, 82, 72]},
···                    index=['철수', '영수', '영희'])
```
```
>>> df
      영어  수학  과학
철수   100    95  NaN
영수    90    85   82
영희    80    85   72
```
```
>>> df.idxmin()
영어    영희
수학    영수
과학    영희
dtype:  object
```
```
>>> df.idxmax(axis=1)
철수    영어
영수    영어
영희    수학
dtype:  object
```
```
>>> df.idxmin(axis=1. skipna=False)
철수    NaN
영수    과학
영희    과학
dtype:  object
```