Project : Flight delay prediction
---------------------------------



>##1. 분석 계기와 목적
>- 최근 저가 항공의 잦은 지연 문제로 많은 고객의 불만이 있다는 것을 알게 되었습니다. 하지만 항공사에서는 적절한 보상이 제대로 이루어 지지 않아서 더욱 고객불만이 가중되고 있었습니다. 저는 이 문제를 날씨와 항공 지연이 관계가 있다는고 가정하고 날씨데이터와 항공데이터를 이용해 항공 지연을 예측하여 고객들에게 제공하는 방법으로 풀고자 분석프로젝트를 시작하게 되었습니다.

-----------------------------------------------------------------------------------------------

>##2. 데이터 설명
>###1) 항공데이터
>- plan : 계획 비행 시간 
- date : 비행 날짜
- predict : 예상되어지는 비행출발시간 - 비행하기 전 기장이 직접 입력한다.
- dep : 실제 출발 시간
- company : 항공사
- month : 비행 월( 날짜 대신 실제 분석에 쓰일 feature)
- day : 비행 일( 날짜 대신 실제 분석에 쓰일 feature)
- weekday : 비행 요일( 1: 일, 2:월, 3:화 ... 7: 토)
- hour : 비행이 계획된 시간( plan 대신 실제 분석에 쓰일 feature)
- the number of delay : 이전달의 지연 횟수
- status : 비행지연 여부 (0: 출발, 1:지연) - target


>###2) 날씨데이터
>- wind : 풍향(기준은 서쪽으로 중심으로부터 틀어진 각도로 측정 예 : 서쪽에서 북쪽으로 30도 틀어져 있을 경우 30이라고 측정)
- wind2: 풍속
- temp : 기온
- dist : 시정
- rain : 강수량

>데이터는 약 5만개를 사용하였으며, 김포공항에서 제주공항으로 출발하는 모든 항공기에 대한 데이터를 크롤링을 통해 모았습니다. 대부분 feature들이 대부분 categorical하기 때문에 one hot encoding을 통해서 더미변수로 만들어줍니다.

>##3. 데이터 분석 결과
> 분석 결과를 판단 할수 있는 것은 recall값으로 정했습니다. recall이란 실제값이 예측값으로 나온 비율로 실제 지연이라고 된 비행기가 알고리즘을 통해 예측한 값도 지연이란 값으로 얼마나 나왔는지를 나타내는 값입니다.

> 적용한 알고리즘은 총 4가지로 logistic regression, random forest, SVM(Support vector machine), Navie bayes(Gaussian, Multinomial)입니다. 4가지 모형을 다 적용해본 결과 가장 좋은결과는 75%로 나타났습니다. 하지만 fall-out 값이 높게 너무 높게 나타나서 모델의 개선 필요성을 느꼈습니다.

> 4가지 모델 중 random forest 와 Naive bayes가 좋은 모형으로 나타나 Ensemble의 votingclassfiter를 적용하여 두 가지 모델을 합쳐서  예측 모델을 만들었습니다.

> 그 결과, 약 80%의 지연 예측이 가능한 모델을 구현했습니다.
