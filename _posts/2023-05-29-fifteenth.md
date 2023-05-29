---
title: 2023 [Easy Study Project X 이지스퍼블리싱] BDA 학회 딥러닝 스터디 3주차 7. 콘벌루션 신경망 모델 (Convolution Neural Network Model)
tags: [2023, BDA, CNN]
author: Jins
---

# Summary
한 달 동안 "Do it! 딥러닝 교과서"를 가지고 BDA 내부 스터디를 진행하며, 이번주는 6,7단원을 공부했다. 
<img width="412" alt="스크린샷 2023-05-29 오전 8 56 40" src="https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/7f925ac8-8fcd-43c1-80f9-bbd5475564a9">

포스팅할 내용은 7단원으로, 순서는 다음과 같다. 

    7.1 ReNet-5
    7.2 AlexNet
    7.3 ZFNet
    7.4 VGGNet
    7.5 GoogLeNet
    7.6 ResNet
    7.7 콘볼루션 신경망 비교
    7.8 다양한 모델의 등장

<br/>

# **Content**

<br/>

## **연도별 모델 순서**
    - 1998 : LeNet-5
------`ILSVRC대회 시행`----- 

=> 1000개 클래스에 대한 이미지 분류 및 객체 인식 목적

    - 2012 : AlexNet
    - 2013 : ZFNet
    - 2014 : GoogLeNet, VGGNet
    - 2015 : ResNet

<br/>

## 1998 : **LeNet-5**
- 의의 : 최초의 콘볼루션 신경망
- 목적 : 필기체 우편번호 인식
- 구조 : 7계층 (Conv 계층 - Pooling 계층 - Conv 계층 - Pooling 계층 - Fully Connected 계층 - Fully Connected 계층 - Fully Connected 계층)
    - Conv 계층 & Pooling 계층 : 신체 신경망의 시각영역
    - Fully Connected 계층 : 신체 신경망의 연관영역
- 전체 파라미터 수 : 60K

![32×32×1 1](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/23be5465-8c63-49c0-bf95-721d82140fb8)

<br/>

## 2012 : **AlexNet**
- 의의 : 2개의 GPU에서 실행되는 **병렬처리** 구조
    - 병렬처리 구조 : Conv 필터를 두 그룹으로 나눈 뒤 그룹별로 처리 => 중간 계층에서 정보 교환 => 한쪽 그룹으로 최종 결과 합침
- 구조 : 8계층 (Conv 계층 - Conv 계층 - Conv 계층 - Conv 계층 - Conv 계층 - Fully Connected 계층 - Fully Connected 계층 - Fully Connected 계층)
    - 첫번째 Conv 계층 : Convolution - MaxPooling - Normalization(LRN)
        - LRN (= 지역응답정규화)
            - 사용 이유 : ReLU의 출력 무한히 커지므로
            - 의미 : 픽셀별로 이웃 채널의 픽셀 이용
    - 마지막 Conv 계층 : Convolution - MaxPooling
    - 모든 Conv 계층에는 MaxPooling 포함
- 전체 파라미터 수 : 62,378,344
---
문제 : FC층으로 인해 과도한 수의 파라미터 발생 => 이후 출력 계층을 제외한 신경망으로 개선
![32×32×1 2](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/013d42f1-9247-41a0-a0b0-7f22399d77ae)

<br/>

## 2013 : **ZFNet**
- 의의 : AlexNet의 문제점을 **모델 시각화 방식**으로 분석 & 개선
- 구조 : AlexNet과 동일
    - 모델 시각화 결과 **첫번재 계층이 잘 학습되지 않음** => 첫번째 Conv 계층의 Conv 필터 크기와 스트라이트를 조정함 **(11 * 11 * 4 => 7 * 7 * 2)**=> AlexNet의 죽은 특징과 특징 속의 잡음을 개선하여 선명하게 특징이 포착되도록 개선됨
    - 3,4,5번째 Conv계층의 필터 개수 조정 **(384,384,256 => 512, 1024, 412)**
    - AlexNet에서 Convolution 필터를 두 그룹으로 나눈 것을 여기서는 하나로 합침.
- 전체 파라미터 수 : 62,378,344
![32×32×1 3](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/d2fc8d2d-3b81-4858-bdf9-dfdbe507a8cb)
<br/>

## 2014 : **VGGNet**
- 의의 : 3*3의 Conv 필터 사용 , 매우 단순한 구조
- 목적 : 파라미터의 수를 줄이고, 신경망을 깊게 쌓자!
![32×32×1 4](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/9872fb6a-1e7e-4eea-a128-b86f1885cc1b)
- 구조 
    - 11계층
    - 13계층
    - **16계층** => **VGG16** 
        - Conv 계층 (2회) - Conv계층 (2회) - Conv계층 (3회) - Conv 계층 (3회) - Conv 계층 (3회) - FC층 (3회)
        - 중간 중간에 MaxPooling/2 적용
    - 19계층
- 전체 파라미터 수 : 138MB

<br/>

## 2014 : **GoogLeNet**
- 의의 : 네트워크 속 네트워크 구조
- 구조 : 22계층
- 전체 파라미터 수 : 5M

<br/>

## 2015 : **ResNet**
- 의의 : 네트워크 속 네트워크 구조
- 구조 
    - 18계층
    - 34계층
    - 50계층
    - 101계층
    - 152계층
- 전체 파라미터 수 : 5M
![32×32×1 5](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/3decd472-91d3-49e2-ad4c-ad59c8bacd2a)

<br/>

## **콘볼루션 신경망 비교**

- 모델 정확도와 파라미터 수 비교
![32×32×1 6](https://github.com/whatareyoudoingz/whatareyoudoingz.github.io/assets/108795647/0527b817-2e80-427d-a14d-1287ef660b0c)

## **다양한 모델의 등장**
- 와이드 레즈넷, 레즈넥스트, 깊이가 확률적으로 변하는 신경망, 프랙탈넷, 댄스넷, 나스넷, 인셉션v4, 인셉션-레즈넷v1

---
<br/>

# **회고**

    전공자로써 전공 수업들을 통해서 배운 것은 많지만 완전히 흡수하지 못한 것들이 많다고 느꼈는데, 공부하면서 전공 시간에 배운 내용들이 생각나고, 이 책의 내용을 이해하는 데 많은 도움이 되는 것을 통해 자신감이 생겼고, 깊게 배우지 못한 내용들을 배우고 배웠던 내용들도 다시 보강함으로써 자신감이 생겼다. 
    
    그리고 책에 대한 부분을 말하자면, 책의 내용이 시간의 순서대로 신경망들을 나열되어 있어 좋았고, 각 신경망 설명을 자세히, 하나의 용어도 세심히 적혀있어 내용을 이해하는데 큰 도움이 되었다.

    마지막으로, 공부하면서 알지 못했던 신경망들이 많아 앞으로 스터디가 끝나더라도 하나씩 공부하여 응용해봐야겠다. 요즘 스터디, 프로젝트를 하면서 부족함이 많음을 느낀다.. 갈 길이 멀다... 화이팅!!