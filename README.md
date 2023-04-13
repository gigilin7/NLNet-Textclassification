# NLNet-Textclassification

* Model: xlnet-base-cased
* Dataset: IMDB ( 電影評論，label 0 為 Negative，label 1 為 Positive )

| Name         | Model Class   | Training Method  |
|-------|-------|-------|
| XLNET-Textclassification-IMDB | xlnet-base-cased | XLNetForSequenceClassification |

## Different from BERT
We need to add special tokens ("[SEP]" and "[CLS]") at the beginning and end of each sentence for XLNet to work properly. 

For BERT, the special token pattern looks like this:

    [CLS] + Sentence_A + [SEP] + Sentence_B + [SEP]

Whereas with XLNet the token pattern looks like this:

    Sentence_A + <sep> + Sentence_B + <sep> + <cls>
    
For single sentence inputs here, we just need to add [SEP] and [CLS] to the end:

    Sentence + <sep> + <cls>

## Examples
```
sentence: "god is great, the movie's not." 
```
**BERT:**

* 將文本中的單詞劃分為基本單元

  `"god", "is", "great", ",", "the", "movie", "'", "s", "not", "."`

* 在單詞前添加一個特殊字符"##"

  `"go", "##d", "is", "great", ",", "the", "mov", "##ie", "'", "s", "not", "."`

**XLNet:**

* 將文本中的單詞劃分為基本單元

  `"god", "is", "great", ",", "the", "movie", "'", "s", "not", "."`

* 將每個單詞轉化為由多個子詞组成的序列

  `"▁god", "▁is", "▁great", ",", "▁the", "▁movie", "'", "s", "▁not", "."`
  
  
## input_mask VS. attention_mask
+ input_mask
  + 0 : real tokens 
  + 1 : padding tokens
+ attention_mask
  + 1 : real tokens 
  + 0 : padding tokens
+ Can only uses one of input_mask and attention_mask
 
 
## Score
+ classification_report(y_pred,y_true)用於顯示主要分類指標的文本報告
  + y_pred : 預測結果
  + y_true : 真實結果
 
![image](https://user-images.githubusercontent.com/43805264/231718595-aa4a6429-e006-45f6-a528-ed8c255e2c7c.png)

  
  
