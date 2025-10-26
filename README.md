# MNIST Classification : Model development using advanced CNN's
Achieve 99.4 % accuracy using less than 8000 parameters. Results should be eveident in last 3 epochs. Use 3 iteration to arrive at final mode.
## Overall Target
* Accuracy: 99.4% (consistently in last few epochs)
* Epochs: 15
* Parameters < 8000
* Result Summary
| Model | Train accuracy | Test accuracy | No. of parameters | Epochs | Target met |
|-------|-----------|----------|------------|---------|------------|
| Model 1 | 98.8 | 98.8 | 7998 | 15 | NA |
| Model 2 | 97.9 | 98.9 | 7936 | 15 | NA |
| Model 3 | 98.8 | 99.4 | 5178 | 15 | Yes |

## Model 1 : Baseline
## Target :
* Base model trained with upto 8k parameters.
* Data loading & imports from MNIST
* Basic pipeline using convolution , batch normalization & relu
* Using 1 * 1 on last layer.

## Results
* Final Train accuracy: 98.8
* Final Test accuracy: 98.8
* Total parameters: 7998

## Analysis
**Architecture decisions:**
* started with CNN : 10 -> 8 -> 10
* Using max pooling after 3 layers of convolution
* Using Adam optimizer with learning rate 1e-4

**Training observation:**
* Achieved 98.8 accuracy in 15 iterations
* Batch normalization & relu after each convolution helped in training stability.

### File link
[mnist_session6_iteration1.py](./mnist_session6_iteration1.py)

## Model 2 : Add new features to improve accuracy
## Target :
* Base model trained with less than 8k parameters.
* Implement Regularization techniques
* Use dropout  to prevent overfitting
* Use average pooling to decrease no. of parameters

## Results
* Final Train accuracy: 97.9
* Final Test accuracy: 98.9
* Total parameters: 7936

## Analysis
**Architecture decisions:**
* Dropout added after each layer of convolution
* Average pooling introduced
* Channel progression changed as follows : 20 -> 10 -> 20 -> 12 -> 10
* Introduced SGD with learning rate of 0.01 & momentum of 0.1

**Training observation:**
* Achieved 98.9 accuracy in 15 iterations
* Test accuracy achieved 98.9 till last epoch.

File link
[mnist_session6_iteration2.py](./mnist_session6_iteration2.py)

## Model 3 : Final training
## Target :
* Achieve 99.4 % accuracy in last three iterations
* Max pooling introduced twice for better feature extraction
* Image augmentation introduced
* Adaptive average pooling added 

## Results
* Final Train accuracy: 98.8
* Final Test accuracy: 99.4
* Total parameters: 5178

## Analysis
**Architecture decisions:**
* 6→12→12→10 progression
* MaxPool locations for maximum feature retention
* OnecycleLR for optimal covergence.

**Target Achievement:**

* 99.4% Accuracy: Advanced techniques should push beyond 99% barrier
* <8000 Parameters: Architecture carefully designed to meet constraint
* ≤15 Epochs: OneCycleLR + augmentation should enable fast convergence
* Consistency: Batch norm + proper regularization for stable final epochs

### File link
[mnist_session6_iteration3.py](./mnist_session6_iteration3.py)


# LOGS

## Model 1
```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 10, 26, 26]             100
              ReLU-2           [-1, 10, 26, 26]               0
       BatchNorm2d-3           [-1, 10, 26, 26]              20
            Conv2d-4            [-1, 8, 24, 24]             728
              ReLU-5            [-1, 8, 24, 24]               0
       BatchNorm2d-6            [-1, 8, 24, 24]              16
            Conv2d-7           [-1, 10, 22, 22]             730
              ReLU-8           [-1, 10, 22, 22]               0
       BatchNorm2d-9           [-1, 10, 22, 22]              20
        MaxPool2d-10           [-1, 10, 11, 11]               0
          Dropout-11           [-1, 10, 11, 11]               0
           Conv2d-12              [-1, 8, 9, 9]             728
             ReLU-13              [-1, 8, 9, 9]               0
      BatchNorm2d-14              [-1, 8, 9, 9]              16
           Conv2d-15             [-1, 10, 7, 7]             730
           Conv2d-16             [-1, 10, 1, 1]           4,910
================================================================
Total params: 7,998
Trainable params: 7,998
Non-trainable params: 0
----------------------------------------------------------------
```
```
Epoch: 1/15..  Time: 42.99s.. Training Loss: 0.366..  Training Accu: 0.892..  Val Loss: 0.111..  Val Accu: 0.968
Epoch: 2/15..  Time: 37.06s.. Training Loss: 0.113..  Training Accu: 0.967..  Val Loss: 0.075..  Val Accu: 0.977
Epoch: 3/15..  Time: 38.15s.. Training Loss: 0.085..  Training Accu: 0.975..  Val Loss: 0.054..  Val Accu: 0.982
Epoch: 4/15..  Time: 37.38s.. Training Loss: 0.072..  Training Accu: 0.978..  Val Loss: 0.050..  Val Accu: 0.983
Epoch: 5/15..  Time: 37.42s.. Training Loss: 0.065..  Training Accu: 0.981..  Val Loss: 0.044..  Val Accu: 0.985
Epoch: 6/15..  Time: 37.52s.. Training Loss: 0.058..  Training Accu: 0.982..  Val Loss: 0.048..  Val Accu: 0.983
Validation loss has not improved since: 0.044.. Count:  1
Epoch: 7/15..  Time: 37.92s.. Training Loss: 0.055..  Training Accu: 0.983..  Val Loss: 0.041..  Val Accu: 0.986
Epoch: 8/15..  Time: 38.01s.. Training Loss: 0.052..  Training Accu: 0.984..  Val Loss: 0.038..  Val Accu: 0.987
Epoch: 9/15..  Time: 37.73s.. Training Loss: 0.049..  Training Accu: 0.985..  Val Loss: 0.037..  Val Accu: 0.988
Epoch: 10/15..  Time: 37.86s.. Training Loss: 0.048..  Training Accu: 0.985..  Val Loss: 0.038..  Val Accu: 0.988
Validation loss has not improved since: 0.037.. Count:  1
Epoch: 11/15..  Time: 38.49s.. Training Loss: 0.045..  Training Accu: 0.986..  Val Loss: 0.035..  Val Accu: 0.989
Epoch: 12/15..  Time: 37.78s.. Training Loss: 0.043..  Training Accu: 0.987..  Val Loss: 0.034..  Val Accu: 0.989
Epoch: 13/15..  Time: 37.85s.. Training Loss: 0.041..  Training Accu: 0.987..  Val Loss: 0.034..  Val Accu: 0.987
Validation loss has not improved since: 0.034.. Count:  1
Epoch: 14/15..  Time: 38.05s.. Training Loss: 0.040..  Training Accu: 0.987..  Val Loss: 0.033..  Val Accu: 0.989
Epoch: 15/15..  Time: 37.66s.. Training Loss: 0.039..  Training Accu: 0.988..  Val Loss: 0.032..  Val Accu: 0.988
```
## Model 2
```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 20, 26, 26]             200
              ReLU-2           [-1, 20, 26, 26]               0
       BatchNorm2d-3           [-1, 20, 26, 26]              40
           Dropout-4           [-1, 20, 26, 26]               0
            Conv2d-5           [-1, 10, 24, 24]           1,810
              ReLU-6           [-1, 10, 24, 24]               0
       BatchNorm2d-7           [-1, 10, 24, 24]              20
           Dropout-8           [-1, 10, 24, 24]               0
            Conv2d-9           [-1, 20, 22, 22]           1,820
             ReLU-10           [-1, 20, 22, 22]               0
      BatchNorm2d-11           [-1, 20, 22, 22]              40
        MaxPool2d-12           [-1, 20, 11, 11]               0
           Conv2d-13             [-1, 10, 9, 9]           1,810
             ReLU-14             [-1, 10, 9, 9]               0
      BatchNorm2d-15             [-1, 10, 9, 9]              20
          Dropout-16             [-1, 10, 9, 9]               0
           Conv2d-17             [-1, 10, 7, 7]             910
             ReLU-18             [-1, 10, 7, 7]               0
      BatchNorm2d-19             [-1, 10, 7, 7]              20
          Dropout-20             [-1, 10, 7, 7]               0
           Conv2d-21             [-1, 12, 7, 7]           1,092
             ReLU-22             [-1, 12, 7, 7]               0
      BatchNorm2d-23             [-1, 12, 7, 7]              24
          Dropout-24             [-1, 12, 7, 7]               0
        AvgPool2d-25             [-1, 12, 1, 1]               0
           Conv2d-26             [-1, 10, 1, 1]             130
================================================================
Total params: 7,936
Trainable params: 7,936
Non-trainable params: 0
----------------------------------------------------------------
```
```
Epoch: 1/15..  Time: 42.21s.. Training Loss: 1.253..  Training Accu: 0.712..  Val Loss: 0.492..  Val Accu: 0.932
Epoch: 2/15..  Time: 42.39s.. Training Loss: 0.420..  Training Accu: 0.923..  Val Loss: 0.167..  Val Accu: 0.968
Epoch: 3/15..  Time: 42.37s.. Training Loss: 0.223..  Training Accu: 0.950..  Val Loss: 0.092..  Val Accu: 0.977
Epoch: 4/15..  Time: 41.22s.. Training Loss: 0.164..  Training Accu: 0.958..  Val Loss: 0.066..  Val Accu: 0.982
Epoch: 5/15..  Time: 41.15s.. Training Loss: 0.135..  Training Accu: 0.965..  Val Loss: 0.057..  Val Accu: 0.983
Epoch: 6/15..  Time: 41.92s.. Training Loss: 0.116..  Training Accu: 0.968..  Val Loss: 0.050..  Val Accu: 0.985
Epoch: 7/15..  Time: 40.89s.. Training Loss: 0.107..  Training Accu: 0.969..  Val Loss: 0.053..  Val Accu: 0.984
Validation loss has not improved since: 0.050.. Count:  1
Epoch: 8/15..  Time: 40.91s.. Training Loss: 0.099..  Training Accu: 0.972..  Val Loss: 0.046..  Val Accu: 0.986
Epoch: 9/15..  Time: 41.98s.. Training Loss: 0.092..  Training Accu: 0.973..  Val Loss: 0.043..  Val Accu: 0.987
Epoch: 10/15..  Time: 40.61s.. Training Loss: 0.087..  Training Accu: 0.975..  Val Loss: 0.046..  Val Accu: 0.986
Validation loss has not improved since: 0.043.. Count:  1
Epoch: 11/15..  Time: 40.79s.. Training Loss: 0.083..  Training Accu: 0.975..  Val Loss: 0.040..  Val Accu: 0.988
Epoch: 12/15..  Time: 41.85s.. Training Loss: 0.081..  Training Accu: 0.976..  Val Loss: 0.035..  Val Accu: 0.989
Epoch: 13/15..  Time: 41.00s.. Training Loss: 0.075..  Training Accu: 0.978..  Val Loss: 0.035..  Val Accu: 0.989
Validation loss has not improved since: 0.035.. Count:  1
Epoch: 14/15..  Time: 41.42s.. Training Loss: 0.071..  Training Accu: 0.979..  Val Loss: 0.035..  Val Accu: 0.989
Epoch: 15/15..  Time: 41.34s.. Training Loss: 0.070..  Training Accu: 0.979..  Val Loss: 0.034..  Val Accu: 0.989
```
## Model 3
```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 6, 26, 26]              54
              ReLU-2            [-1, 6, 26, 26]               0
       BatchNorm2d-3            [-1, 6, 26, 26]              12
            Conv2d-4           [-1, 12, 24, 24]             648
              ReLU-5           [-1, 12, 24, 24]               0
       BatchNorm2d-6           [-1, 12, 24, 24]              24
         MaxPool2d-7           [-1, 12, 12, 12]               0
            Conv2d-8           [-1, 12, 10, 10]           1,296
              ReLU-9           [-1, 12, 10, 10]               0
      BatchNorm2d-10           [-1, 12, 10, 10]              24
           Conv2d-11             [-1, 12, 8, 8]           1,296
             ReLU-12             [-1, 12, 8, 8]               0
      BatchNorm2d-13             [-1, 12, 8, 8]              24
        MaxPool2d-14             [-1, 12, 4, 4]               0
           Conv2d-15             [-1, 12, 2, 2]           1,296
             ReLU-16             [-1, 12, 2, 2]               0
      BatchNorm2d-17             [-1, 12, 2, 2]              24
           Conv2d-18             [-1, 10, 1, 1]             480
AdaptiveAvgPool2d-19             [-1, 10, 1, 1]               0
================================================================
Total params: 5,178
Trainable params: 5,178
Non-trainable params: 0
----------------------------------------------------------------
```
```
Epoch: 1/15..  Time: 57.07s.. Training Loss: 0.242..  Training Accu: 0.923..  Val Loss: 0.105..  Val Accu: 0.967
Epoch: 2/15..  Time: 56.86s.. Training Loss: 0.119..  Training Accu: 0.964..  Val Loss: 0.124..  Val Accu: 0.955
Validation loss has not improved since: 0.105.. Count:  1
Epoch: 3/15..  Time: 55.97s.. Training Loss: 0.108..  Training Accu: 0.967..  Val Loss: 0.060..  Val Accu: 0.981
Epoch: 4/15..  Time: 55.16s.. Training Loss: 0.092..  Training Accu: 0.972..  Val Loss: 0.081..  Val Accu: 0.974
Validation loss has not improved since: 0.060.. Count:  1
Epoch: 5/15..  Time: 55.92s.. Training Loss: 0.083..  Training Accu: 0.975..  Val Loss: 0.048..  Val Accu: 0.984
Epoch: 6/15..  Time: 56.36s.. Training Loss: 0.073..  Training Accu: 0.977..  Val Loss: 0.032..  Val Accu: 0.991
Epoch: 7/15..  Time: 56.07s.. Training Loss: 0.062..  Training Accu: 0.981..  Val Loss: 0.033..  Val Accu: 0.990
Validation loss has not improved since: 0.032.. Count:  1
Epoch: 8/15..  Time: 59.39s.. Training Loss: 0.059..  Training Accu: 0.982..  Val Loss: 0.029..  Val Accu: 0.990
Epoch: 9/15..  Time: 57.27s.. Training Loss: 0.055..  Training Accu: 0.983..  Val Loss: 0.030..  Val Accu: 0.990
Validation loss has not improved since: 0.029.. Count:  1
Epoch: 10/15..  Time: 58.46s.. Training Loss: 0.048..  Training Accu: 0.985..  Val Loss: 0.022..  Val Accu: 0.993
Epoch: 11/15..  Time: 58.85s.. Training Loss: 0.044..  Training Accu: 0.986..  Val Loss: 0.021..  Val Accu: 0.994
Epoch: 12/15..  Time: 60.56s.. Training Loss: 0.043..  Training Accu: 0.987..  Val Loss: 0.020..  Val Accu: 0.993
Epoch: 13/15..  Time: 58.34s.. Training Loss: 0.041..  Training Accu: 0.987..  Val Loss: 0.019..  Val Accu: 0.994
Epoch: 14/15..  Time: 59.82s.. Training Loss: 0.040..  Training Accu: 0.988..  Val Loss: 0.019..  Val Accu: 0.994
Validation loss has not improved since: 0.019.. Count:  1
Epoch: 15/15..  Time: 58.90s.. Training Loss: 0.040..  Training Accu: 0.988..  Val Loss: 0.019..  Val Accu: 0.994

```


