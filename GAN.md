# Generative Adversarial Network  

## GAN이란?  
- Generative Adversarial Network의 약자로 Generator가 경쟁적으로 대립 (Adversarial)시켜 학습을 시키는 신경망을 말한다.  

### Generative  
- Gererator가 **그럴듯한 가짜 데이터**를 만들어내는 내는 모델.  
- '그럴듯한 가짜'라는 것은 실제 data의 분포와 비슷한 데이터를 만들어 낸다는 소리.  

### Adversarial  
- GAN이 두 개의 Model을 적대적으로 경쟁시키면 발전시킴.  

### Example   

![image](https://user-images.githubusercontent.com/32921115/104803734-88a46f00-5814-11eb-9e61-efbd1100e176.png)

- Generator : 위조지폐범, 목표는 그럴듯한 위조지폐를 만들어 Discriminator(경찰)을 속이는 것  
- Discriminator : 경찰, 목표는 진짜 지폐와 위조지폐를 구분하는 것  
- 이 둘을 계속 learning 시키면 언젠가는 진짜 지폐와 다를 것 없는 가짜 지폐를 만들어내는 Generator를 얻을 수 있음. (Adversarial Training)  

## 아키텍처  

![image](https://user-images.githubusercontent.com/32921115/104805680-39127300-5815-11eb-90b6-ddb1310943e5.png)

## Loss Function  

![image](https://user-images.githubusercontent.com/32921115/104805727-91497500-5815-11eb-947f-69a20e9f23f0.png)

### Discriminator
- 왼쪽 항 : D(x)는 실제 데이터 x를 보고 판별하는 예측 확률값. log는 0에서 1로 향할수록 값이 커지므로, **왼쪽 항은 Discriminator 입장에서는 값이 크면 좋음.**  
- 오른쪽 항 : D(G(z))는 Discriminator가 가짜 데이터를 보고 판별하는 예측 값. Discriminator는 진짜만 1, 가짜는 0으로 판별하고 싶어하므로 **0에 가까운 값을 출력해야 함.**, log(1-x) 함수는 0에서 1로 갈수록 값이 작아지므로, **오른쪽 항도 마찬가지로 값이 크면 좋음**  
- 즉, **Discriminator 입장에서 Loss Fucntion의 값이 커야 성능이 좋다고 말할 수 있음.**

### Generator  
- 오른쪽 항 : **Generator의 목표는 D(G(z))의 값이 1이 되게 만들어야 한다.** log(1-x) 함수는 0에서 1로 갈수록 값이 작아지므로, Generator 입장에서 **오른쪽 항의 값은 작아져야 한다.**  
- 즉, **Generator 입장에서 Loss Fucntion이 작은 값을 가져야 성능이 좋다고 말할 수있다.** 이는 곳 우리의 목적과 같음.  
- 맨 처음의 D(G(z))의 값은 0에 가까울 것 -> Loss가 큼.  

## Cycle GAN  

### 나오게 된 배경  
- Image-to-image traslation은 짝이 있는 Image Training Set를 이용해 Input과 Output 이미지를 매핑하는 것이 목표인 Computer Vision 분야 중 하나. But, 짝이 지어진 Training Data를 얻는 것은 쉽지 않고 만들기도 어렵다.  
- **짝 지어진 Data없이** X라는 도메인으로부터 얻은 이미지를 Target인 Y로 바꾸면 어떨까? 해서 나온 Model  

### 원리  
1. Domain X를 Domain Y로 바꿔주는 **Translator G : X->Y를 GAN**으로 구현.  
  - pair dataset이 필요없이 X를 넣었을 때, Y를 생성할 수 있음.  
  - But, X 분포와 Y 분포에 대응하는 관계가 매우 많기 때문에 x와 y가 pair인지 보장할 수 없음 (풍경사진을 넣을 때 그 사진과 관련없는 모네 그림이 나올 수 있음)  
  
2. 위의 단점을 개선시키기 위해 **Cycle Consistent**라는 개념을 이용  
  - Cycle Consistent : Domain X에서 Y로 바꿨을 때, **다시 Y에서 translate 할 때 X가 나오는** 일관성.  
  - 반대 방향으로 도메인을 바꿔주는 translator F :Y -> X를 정의  
  
3. G(x)에서 나오는 Output을 y' F(y)에서 나오는 output을 x'라 할 때, **F(y') = x, G(x') = y**를 만족하는 방향으로 learning을 한다.  

4. 점점 **G(x) = y'은 y와 F(y) = x'는 x와 근사**하게 된다.  

5. 이 과정에서 GAN 2개가 Cycle 구조로 사용되기 때문에 **CycleGAN으로 불린다.**  

### Loss  

1. Adversarial Loss  

![image](https://user-images.githubusercontent.com/32921115/104814699-bf4daa00-5853-11eb-988b-1ae48aaf709a.png)
- G : X -> Y Translator  
- Dy : Y Discriminator  
- y~P_data(y) : Y의 data 분포를 따르는 원소 y  
- 왼쪽 항 : Dy(Y)는 Y를 예측하는 discriminator로 0 ~ 1 사이의 확룰 값을 반환함. Discriminator 입장에서는 이 항의 값이 커져야 한다.  
- 오른쪽 항 : Dy(G(x))는 Y'을 예측하는 discriminator로 이 값을 줄여야 하는 것이 목표. 이 값이 작아지면 **log(1-x) 함수의 성질에 의해 오른쪽 항의 값은 커진다.** 반면 **Generator 입장**에서는 **G(x)의 값이 커져야 하므로** 오른쪽 항의 **값이 작아지는 것을 목표**로 한다.  

2. Cycle Consistency Loss  

![image](https://user-images.githubusercontent.com/32921115/104814956-fa9ca880-5854-11eb-8130-278f80b06c57.png)

- **L1 Loss**를 사용해 **F(G(x)), G(F(y))를 x,y에 가깝게** 만들어 Cycle Consistent하게 만들어준다.  

3. 최종 Loss  

![image](https://user-images.githubusercontent.com/32921115/104814980-2c157400-5855-11eb-94bf-a9e5f95e2927.png)

![image](https://user-images.githubusercontent.com/32921115/104814987-36377280-5855-11eb-83de-b97cf6fcb575.png)

- Loss를 작게하는 G, F를 찾고 반대로 Loss를 크게 하는 Dx, Dy를 찾는 적대적 learning을 하게 된다.  
