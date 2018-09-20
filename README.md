# Keras Multi-Head

[![Travis](https://travis-ci.org/CyberZHG/keras-multi-head.svg)](https://travis-ci.org/CyberZHG/keras-multi-head)
[![Coverage](https://coveralls.io/repos/github/CyberZHG/keras-multi-head/badge.svg?branch=master)](https://coveralls.io/github/CyberZHG/keras-multi-head)
[![PyPI](https://img.shields.io/pypi/pyversions/keras-multi-head.svg)](https://pypi.org/project/keras-multi-head/)

A wrapper layer for stacking layers horizontally.

![](https://user-images.githubusercontent.com/853842/45797517-867b8580-bcd8-11e8-9ec6-39d6508cf438.png)

## Install

```bash
pip install keras-multi-head
```

## Usage

### Duplicate Layers

The layer will be duplicated if only a single layer is provided. The `layer_num` argument controls how many layers will be duplicated eventually.

```python
import keras
from keras_multi_head import MultiHead


model = keras.models.Sequential()
model.add(keras.layers.Embedding(input_dim=100, output_dim=20, name='Embedding'))
model.add(MultiHead(keras.layers.LSTM(units=32), layer_num=5, name='Multi-LSTMs'))
model.add(keras.layers.Flatten(name='Flatten'))
model.add(keras.layers.Dense(units=4, activation='softmax', name='Dense'))
model.build()
model.summary()
```

### Use Multiple-Layers

The first argument could also be a list of layers with different configurations, however, they must have the same output shapes.

```python
import keras
from keras_multi_head import MultiHead


model = keras.models.Sequential()
model.add(keras.layers.Embedding(input_dim=100, output_dim=20, name='Embedding'))
model.add(MultiHead([
    keras.layers.Conv1D(filters=32, kernel_size=3, padding='same'),
    keras.layers.Conv1D(filters=32, kernel_size=5, padding='same'),
    keras.layers.Conv1D(filters=32, kernel_size=7, padding='same'),
], name='Multi-CNNs'))
model.build()
model.summary()
```
