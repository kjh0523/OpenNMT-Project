# OpenNMT 기반의 한국어-영어 신경망 기계 번역 (NMT)
This repo contains the source code and other details for a neural machine translation based on attention using pytorch. This model translates Korean into English.   
이 저장소는 pytorch를 사용하는 어텐션을 기반으로 하는 신경망 기계 번역에 관한 소스코드와 다른 내용을 포함하고 있다. 이 모델은 한국어를 영어로 번역한다. 

## Capstone 프로젝트 (2020.02 ~ )
* **주간 보고서** : [여기를 클릭](https://github.com/SoYoungCho/Korean-English-NMT/wiki/Weekly-Report-%231) :)  
2020년 02월 부터 주간보고서는 여기서 찾을 있다.

---

## 성능

* **BLEU(Bilingual Evaluation Understudy) score** 

| BLEU | BLEU1 | BLEU2 | BLEU3 | BLEU4 | 
|---|:---:|:---:|:---:|:---:|
| **33.55** | 64.6 | 40.0 | 27.5 | 19.4 | 

* **번역 문장**  

#### 예제 1 
```
차를 마시러 공원에 가던 차 안에서 나는 그녀에게 차였다.
```
```
> I was dumped by her in a car on the way to the park to drink tea .  
```
#### 예제 2  
```
사과의 의미로 사과를 먹으며 사과했다.
```
```
> I apologize while eating an apple for the meaning of an apology .
```
#### 예제 3
```
내가 그린 기린 그림은 긴 기린 그림이냐, 그냥 그린 기린 그림이냐?
```
```
> Is the giraffe I drew a long giraffe picture or just a giraffe picture ?
```
---


## 데이타셋

* 전처리 
  + `Delete` the sentence with the length of 149(Korean) or more and 387(English) or more based on space.
  + `Delete` the sentence containing some special characters.
  
* 설정

| <center>Dataset</center> | <center>Sentences</center> | <center>Download</center> | 
|---|:---:|---|  
| Written + Spoken | 920,000 | - [AI-Hub](http://www.aihub.or.kr/) (한-영 말뭉치 AI 데이터)<br>- [Tatoeba](https://tatoeba.org/eng/downloads) (Korean - English)|

---

## 사용법

### 단계 1. 전처리 데이타
```
!python preprocess.py
```
The source text file(`src`) and target text file(`tgt`) are tokenized through `Mecab`+`SentencePiece`.

### Step 2. 모델 훈련
```
!python train.py
```
If you want to continue training the model, add `--train_from (model path)/model.pt` later.

### Step 3. 번역
```
!python translate.py -model data/model/model.pt -src data/src-test.txt -tgt data/tgt-test.txt -replace_unk -verbose -gpu 0
```

### Step 4. 모델 평가
```
!perl tools/multi-bleu.perl data/tgt-test.txt < data/pred.txt
```

### tep 5. 그래픽 사용자 인터페이스 실행
```
!pyhton gui.py
```
You have to change from `"data/src-test.txt"` to `"data/demo/KoreanTokenInput.txt"` of `translate_opts > --src` in `opts.py`
and `"data/pred.txt"` to `"data/demo/EnglishTokenOutput.txt"` of `translate_opts > --output`.

---

## 
https://github.com/OpenNMT/OpenNMT-py
