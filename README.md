# BERT를 이용한 단어간 유사도 확인

## W2V vs. BERT
||W2V|BERT|
|--|--|--|
|Context|independent|dependent|
|input level|word|sentence|
|OOV|처리를 할 수 없음|subword를 이용해서 처리 가능|

> https://medium.com/swlh/differences-between-word2vec-and-bert-c08a3326b5d1


## 한국어 BERT 모델
한국어 BERT 모델의 종류
> https://littlefoxdiary.tistory.com/81


`LMKor` 모델을 사용 
> https://github.com/kiyoungkim1/LMkor

Data
  - 국내 주요 커머스 리뷰 1억개 + 블로그 형 웹사이트 2000만개 (75GB)
  - 모두의 말뭉치 (18GB)
  - 위키피디아와 나무위키 (6GB)

이전에 사용하던 wiki 데이터와 커머스 리뷰(상품)에 대한 정보가 존재 

## 유사도 구현
> ref : https://towardsdatascience.com/bert-for-measuring-text-similarity-eec91c6bf9e1

LMKor 모델을 이용해서 유사도를 계산 하는 함수 구현 
> https://github.com/sigongjoa/emotion_thearpy/blob/main/bert_sim.ipynb

## BERT input check
BERT는 wordpeice tokenizer를 사용하는데 이는 자주 나오지 않는 단어의 경우에 쪼개버리는 상황이 발생 
>tokenizer 확인 코드 : https://github.com/sigongjoa/BERT_simi/blob/main/bert_intput_test.ipynb

> tokenizer 결과 : https://github.com/sigongjoa/BERT_simi/blob/main/bert_tokenized_excel.csv

## hand_craft vs. crawling
hand_craft와 인터넷에서 긁어온 데이터를 유사도 추정 후 비교

* crawling
![](https://i.imgur.com/WQ5oFGx.png)
* hand_craft
![](https://i.imgur.com/NzFV1Mx.png)


> crawling : https://github.com/sigongjoa/BERT_simi/blob/main/bert_sim_scawed_sent.ipynb

> hand craft : https://github.com/sigongjoa/BERT_simi/blob/main/bert_sim_keyword.ipynb


## 예상되는 최대 차원
* 수치화가 제대로 되었는지에 대한 비교값이 없음  
* 아래 Table을 이용해서 수치화가 제대로 되었는지 확인  

|행동| 예상되는 최대 차원 |
|---:|---:|
| 명상 | 에너지 |
| 산책 | ? |
| 등산 | ? |
| 샤워 | 정화 |
| 수영 | 에너지 |
| 자전거 타기 | 에너지, 회복 |
| 요가 | 에너지 |
| 스트레칭 | 에너지, 회복 |
| 여행 | ?? |

# Test
1. 현재 유사도 방식이 적절한가?
└ latent factor를 mean_pooling을 적용함 -> max_pooling 혹은 pooling 없이 factor만 해서 유사도 계산
2. 현재 모델이 적절한가?
└ 다른 한국어 BERT 모델에서 확인 
