---
layout: post
title: Test markdown
subtitle: RNN MODEL
categories: markdown_test
tags: [test]
---

# Practical Exercise with MNIST Example


```python
import torch
import torch.nn
```


```python
import sys
import numpy as np
import matplotlib.pyplot as plt

from mnist_classification.data_loader import load_mnist

from mnist_classification.models.fc_model import FullyConnectedClassifier
from mnist_classification.models.cnn_model import ConvolutionalClassifier
from mnist_classification.models.rnn_model import SequenceClassifier
```


```python
model_fn = "./model.pth"
```


```python
device = torch.device('cuda') if torch.cuda.is_available() else torch.device('cpu')
```


```python
def load(fn, device):
    d = torch.load(fn, map_location=device)
    
    return d['config'], d['model']
```


```python
def plot(x, y_hat):
    for i in range(x.size(0)):
        img = (np.array(x[i].detach().cpu(), dtype='float')).reshape(28,28)

        plt.imshow(img, cmap='gray')
        plt.show()
        print("Predict:", float(torch.argmax(y_hat[i], dim=-1)))
```


```python
def test(model, x, y, to_be_shown=True):
    model.eval()
    
    with torch.no_grad():
        y_hat = model(x)

        correct_cnt = (y.squeeze() == torch.argmax(y_hat, dim=-1)).sum()
        total_cnt = float(x.size(0))
        
        accuracy = correct_cnt / total_cnt
        print("Accuracy: %.4f" % accuracy)
        
        if to_be_shown:
            plot(x, y_hat)
```


```python
from train import get_model

train_config, state_dict = load(model_fn, device)

model = get_model(train_config).to(device)
model.load_state_dict(state_dict)

print(model)
```

    SequenceClassifier(
      (rnn): LSTM(28, 64, num_layers=4, batch_first=True, dropout=0.2, bidirectional=True)
      (layers): Sequential(
        (0): ReLU()
        (1): BatchNorm1d(128, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)
        (2): Linear(in_features=128, out_features=28, bias=True)
        (3): Softmax(dim=-1)
      )
    )
    


```python
# Load MNIST test set.
x, y = load_mnist(is_train=False,
                  flatten=True if train_config.model == 'fc' else False)

x, y = x.to(device), y.to(device)

test(model, x[:20], y[:20], to_be_shown=True)
```

    Accuracy: 1.0000
    


    
![svg](output_9_1.svg)
    


    Predict: 7.0
    


    
![svg](output_9_3.svg)
    


    Predict: 2.0
    


    
![svg](output_9_5.svg)
    


    Predict: 1.0
    


    
![svg](output_9_7.svg)
    


    Predict: 0.0
    


    
![svg](output_9_9.svg)
    


    Predict: 4.0
    


    
![svg](output_9_11.svg)
    


    Predict: 1.0
    


    
![svg](output_9_13.svg)
    


    Predict: 4.0
    


    
![svg](output_9_15.svg)
    


    Predict: 9.0
    


    
![svg](output_9_17.svg)
    


    Predict: 5.0
    


    
![svg](output_9_19.svg)
    


    Predict: 9.0
    


    
![svg](output_9_21.svg)
    


    Predict: 0.0
    


    
![svg](output_9_23.svg)
    


    Predict: 6.0
    


    
![svg](output_9_25.svg)
    


    Predict: 9.0
    


    
![svg](output_9_27.svg)
    


    Predict: 0.0
    


    
![svg](output_9_29.svg)
    


    Predict: 1.0
    


    
![svg](output_9_31.svg)
    


    Predict: 5.0
    


    
![svg](output_9_33.svg)
    


    Predict: 9.0
    


    
![svg](output_9_35.svg)
    


    Predict: 7.0
    


    
![svg](output_9_37.svg)
    


    Predict: 3.0
    


    
![svg](output_9_39.svg)
    


    Predict: 4.0
    


```python

```
