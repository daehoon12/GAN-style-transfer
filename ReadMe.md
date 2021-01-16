# GAN Style Transfer


# Team Name : GAN때문이야

## Member
|소속|이름  | 비고|
|--|--|--|
|컴퓨터 과학과|정창현|팀장|
|컴퓨터 과학과|임상균|
|컴퓨터 과학과|홍우기|
|휴먼지능정보학과|추희승|
|컴퓨터 과학과|강대훈|
|컴퓨터 과학과|안지민|모델 설계|

# 프로젝트 요약
Cycle GAN을 이용하여 paired data가 없이도 학습이 가능하도록 하였다.  

Cycle GAN 의 Generator에는 U-Net, Discriminator 에는 fully connected layer을 적용하였고, 미국의 tv 애니메이션인 The simpsons의 스타일을 Learning하여 input 영상을 simpson 풍의 영상으로 변환하여 출력해줍니다.  


## 프로젝트 계획 및 일정

|날짜|내용| 수행 여부|
|--|--|--|
|9/10|GAN, 머신러닝에 대한 공부| |
|9/17|[GAN 논문](http://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf) 리뷰 및 질의응답| |
|9/24|모델 구상 및 설계| |
|10/01|모델 구상 및 설계| |
|10/08|모델 학습 및 하이퍼 파라미터 조정| |
|10/29|모델 학습 및 하이퍼 파라미터 조정| |
|11/05|모델 학습 및 하이퍼 파라미터 조정| |
|11/12|GAN variation 적용 & 웹 서버 구축| |
|11/19|GAN variation 적용 & 웹 서버 구축| |
|11/26|문서작업| |
|12/03|프로젝트 마무리| |

* 프로젝트 일정은 조정될 수 있습니다.

## 모델
[/model](./model)

## 절차  
1) 영상을 Input으로 넣어 Frame 별로 나눈다.  
2) Frame 별로 나눈 도메인들을 Cycle GAN에 넣는다.  
3) 애니메이션 화풍으로 변환된 도메인들을 다시 동영상으로 변환 시킨다.  

## 프로젝트 결과
> original

![original](./images/original.gif)


> converted

![converted](./images/converted.gif)


---
# 참고자료

- [Generative Adversarial Nets](https://proceedings.neurips.cc/paper/2014/hash/5ca3e9b122f61f8f06494c97b1afccf3-Abstract.html)
-[Unpaired Image-To-Image Translation Using Cycle-Consistent Adversarial Networks](https://openaccess.thecvf.com/content_iccv_2017/html/Zhu_Unpaired_Image-To-Image_Translation_ICCV_2017_paper.html)
- [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://link.springer.com/chapter/10.1007/978-3-319-24574-4_28)
- [Deep Residual Learning for Image Recognition](https://openaccess.thecvf.com/content_cvpr_2016/html/He_Deep_Residual_Learning_CVPR_2016_paper.html)
- [Cycle GAN Github](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix)
- [Simpsons Homepage](https://www.fox.com/the-simpsons/)



