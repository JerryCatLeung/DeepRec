![](https://s1.ax1x.com/2017/09/24/QzeaQ.png) 

# **Table Contents**
- **What is DeepRec** 
- **How to Use**
- **Benchmark Results**
- **References**

## **What is DeepRec**

Deeprec is a portable, flexible and comprehensive library including a variety of state-of-the-art deep learning based recommendation models. It aims to solve the item ranking task. Deeprec implements both feature based methods and raw-signal based methods. In feature based methods, deep learning models are applied to the extracted feature files with the specified format. In raw-signal based methods, deep learning models are directly applied to raw singal such as text, images and graph. Current supported models are listed in the following, more methods will be expected in the near future. 

### **supported model**

model | type | 
----|------| 
lr | feature-based | 
fm | feature-based |   
dnn | feature-based |  
ipnn | feature-based |  
opnn | feature-based |  
deepWide | feature-based | 
deepFM | feature-based | 
deep&cross | feature-based |
din | feature-based |
cccfnet | feature-based |
dkn | text_feature-based |
exDeepFM | feature-based |
ripple | knowledge-graph-based |
mkr | knowledge-graph-based-cf |

## **How to Use**

### **Requirement**
- tensorflow(>=1.4.0)
- linux
- sklearn,yaml,numpy 

in order to use the tool, firstly,prepare your data, we support data format include libffm format, cccfnet format, din format. each model corresponds to the data format is as follows

model | data format | configuration example
----|------|------| 
lr | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/lr.yaml | 
fm | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/fm.yaml |   
dnn | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/dnn.yaml |  
ipnn | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/ipnn.yaml |  
opnn | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/opnn.yaml |  
deepWide | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/deepWide.yaml | 
deepFM | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/deepFM.yaml | 
deep&cross | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/deep&cross.yaml | 
exDeepFM | [libffm](https://github.com/guestwalk/libffm) | DeepRec/example/exDeepFM.yaml|
din | [din](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FDIN%20Format)| DeepRec/example/din.yaml | 
cccfnet | [cccfnet](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FCCCFNet%20Format)| DeepRec/example/cccfnet_classfy.yaml, cccfnet_regress.yaml| 
dkn | [dkn](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FDKN%20Format) | DeepRec/example/dkn.yaml |
ripple | [ripple](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FRippleNetwork%20Format) | DeepRec/example/ripple.yaml |
mkr | [mkr](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FMKR%20Format) | DeepRec/example/mkr.yaml |

secondly, you just need to download code and edit the configuration file.
for example:
```
git clone git@bitbucket.org:lujaindong/deeprec.git
cd deeprec/
cd config/
```
then you edit **network.yaml** based on your demand,do not modify the name of the configuration file.
finally
```
python mainArg.py [Dirname] train/infer 
``` 

### **parameter configuration**
model| configuration example |
----|------| 
dkn | [dkn configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FDKN%20Configuration) |
cccfnet | [cccfnet configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FCCCFNet%20Configuration) | 
din | [din configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FDIN%20Configuration) |
dnn-based model |[dnn-based model configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FDNN%252Dbased%20model%20Configuration) | 
ripple | [ripple configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FRippleNetwork%20Configuration) |
mkr | [mkr configuration](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FMKR%20Configuration) |

### **parameter description**
parameter description is [here](https://deeprec.visualstudio.com/deeprec/_wiki/wikis/deeprec.wiki?wikiVersion=GBwikiMaster&pagePath=%2FDeepRec%2FParameter%20Description) 
 
## **Benchmark Results**
**Note**：because our tool is for the mulit-hot data type, that is more common. sparse matrix is ​​used to store data. building a network requires a lot of sparse operations. our tools are currently only for academic experiments, if the number of samples is larger than 1000w, and feature num is larger than 100w, our tool performance may be relatively low.
we are trying to improve efficiency 
### **benchmark-1**
we sample 300w from criteo dataset([dataset](https://www.kaggle.com/c/criteo-display-ad-challenge)), dealing with long tail features and continuous features. the dataset has 26w features and 300w samples.we split the dataset randomly into three parts: 80% is for training, 10% is for validating, 10% is for testing.


model | auc | logloss | train time per epoch/s|
----|------|------|------| 
lr | 0.7779 | 0.4692 | 20.4| 
fm | 0.7895 | 0.4591 | 90.8 |   
dnn | 0.7939 | 0.4552 | 425.1 |  
ipnn | 0.7947 | 0.4546 | 413.3 |  
opnn | 0.7957 | 0.4539 | 417.6 |  
deepWide | 0.7936 | 0.4557 | 412.4 | 
deepFM | 0.7944 | 0.4549 | 680.8 | 

### **benchmark-2**
we conduct experiment on Company* dataset.the dataset has 20w samples and 19w features. 

model | auc | logloss | train time per epoch/s|
----|------|------|------| 
lr | 0.6555 | 0.3914 | 21.9| 
fm | 0.6873 | 0.39 | 58.4 |   
dnn | 0.7315 | 0.3711 | 201.7 |  
ipnn | 0.7297 | 0.3712 | 199.3 |  
opnn | 0.7332 | 0.3698 | 197.3 |  
deepWide | 0.7346 | 0.3721 | 202.1 | 
deepFM | 0.7324 | 0.3759 | 233.6 | 
din | 0.7401 | 0.3763 | 331.4 | 

## References
- [xDeepFM: Combining Explicit and Implicit Feature Interactions for Recommender Systems](https://arxiv.org/abs/1803.05170)
- [DKN: Deep Knowledge-Aware Network for News Recommendation](https://arxiv.org/pdf/1801.08284v1.pdf)
- [A Factorization-Machine based Neural Network for CTR Prediction](https://arxiv.org/abs/1703.04247)
- [Deep Learning over Multi-field Categorical Data: A Case Study on User Response Prediction](https://arxiv.org/abs/1601.02376)
- [Product-based Neural Networks for User Response Prediction](https://arxiv.org/abs/1611.00144)
- [Wide & Deep Learning for Recommender Systems](https://arxiv.org/abs/1606.07792)
- [A Content-Boosted Collaborative Filtering Neural Network for Cross Domain Recommender Systems](http://dl.acm.org/citation.cfm?id=3054207)
- [product-nets](https://github.com/Atomu2014/product-nets)
- [RippleNetwork: Propagating User Preferences on the Knowledge Graph for RecommenderSystems](https://arxiv.org/pdf/1803.03467.pdf)