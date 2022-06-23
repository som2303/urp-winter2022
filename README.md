# 2022 동계우수학부생
## 연구 주제 및 설명
 
이 연구는 질병을 진단하는 모델을 구현하는 연구로 사람의 생명과 관련이 있는 분야이기 때문에 오류를 줄이고 정확도를 높이는 것이 중요하다. 최종적으로 실제 의료 산업에서 안전성 있는 수준까지 폐렴을 진단할 수 있게 하는 것이 목표이다.

본 연구에서는 data augmentation기법과 bagging을 사용하여 정확도가 높은 모델을 만들고자 한다. 이를 통한 결과는 VGGnet, Resnet 등의 결과와 성능을 비교를 할 예정이다. 이때 모델의 평가 지표로 accuracy, precision, recall, f1-score을 사용할 계획이다. 또한 의료 분야에서 실제 질병에 대해 양성인 사람들이 양성이라고 진단되는 것이 중요하다. 그래서 이에 대한 지표인 sensitivity를 통해 모델의 성능을 평가할 예정이다.
## 데이터 설명
 본 연구에서는 캐글(Kaggle)에서 제공하는 [흉부 X-ray이미지](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia)를 활용하여 폐렴을 진단할 수 있는 모델을 구축하고자 한다.
## Method – Train / Test
* Vggnet

Vggnet은 기존의 CNN깊이를 16 – 19 layers까지 깊이를 늘린 모델이다. 7x7, 11x11 Convolution filter를 사용했던 CNN모델과 달리 3x3 Convolution filter만 사용하여 깊이를 늘릴 수 있었고, 여러번의 활성화 함수 (ReLu)를 지나가면서 비선형성이 증가하여 이미지를 더 잘 분류할 수 있게되었다. 깊이를 늘렸음에도 불구하고 파라미터 수가 기존의 CNN보다 늘어나지 않았고, CNN 모델 역사에 있어서 중요한 의의를 갖는 모델이 되었다. 

* Resnet

Resnet은 기존의 CNN에 새로운 개념인 잔차(Residual)이라는 개념이 적용되었다. Residual은 결과의 오류를 의미하고 Resnet은 이전 layer의 결과를 다시 입력 데이터로 이용한 모델이다. H(x) = F(x) + x 인 residual function을 사용하여 입력 layer를 다시 이용하여 더 쉬운 최적화와 깊은 네트워크에서의 정확도 향상이 가능해졌다. 결과적으로 Resnet은 Vggnet의 8배인 152 layer를 자랑한다. 

* data augmentation 기법

매개변수를 제대로 훈련하기 위해서는 충분한 학습 데이터가 필요하다. 그렇지 않으면 모델의 성능을 저해하는 과적합(overfitting) 문제가 발생하기 쉽다. 이러한 문제를 줄이기 위한 기법 중 하나가 data augmentation이다. data augmentation은 기존의 훈련데이터에 인위적인 변화(flipping, cropping 등)을 가하여 충분한 양의 새로운 훈련 데이터를 확보하는 기법을 말한다. 이를 통해 현실에서도 존재할만한 데이터를 생성함으로써 더 일반화된 모델을 얻을 수 있다.

* bagging

bagging은 데이터를 동일한 크기의 여러 개의 표본으로 복원 임의 추출하고(bootstrap) 각각의 표본 자료들을 모델링한 후 그 결과를 집계(aggregating)하여 최종 결과를 구하는 방법이다. bagging은 예측 모형의 변동성이 큰 경우 예측 모형의 변동성을 감소 시켜준다.

## Result
* resnet / vggnet 성능 결과  

| | Accuarcy | precision | recall | f1-score |
---|---|---|---|---|
ResNet | 84% | 0.87 | 0.79 | 0.81 |
VggNet | 83% | 0.85 | 0.75 | 0.78 |


* resnet을 augmentation을 진행하고 bagging한 결과 

다른 모델에 비해 resnet이 성능이 높아 resnet에 추가적으로 augmentation과 bagging을 진행하였다.

| | 결과 |
---|---|
Accuarcy | 92% |
precision | 0.935 |
recall | 0.91 |
f1-score | 0.915 |
