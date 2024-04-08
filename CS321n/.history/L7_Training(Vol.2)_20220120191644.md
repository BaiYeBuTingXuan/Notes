#  Trainning 
Volume 2

## Outline

1. Fancier optimization
2. Regularization
3. Transfer Learning

## Fancier Optimization
### SGD Problem
$$x_{t+1} = x_t - \alpha \nabla f(x_t)$$
```python
while True:
    dx = Grad(x)
    x -= learning_rate * dx 
```
   1. Trap into a local minima or saddle point
   2. Loss comes from random mini-batch that noise.
### Improve:SGD+Momentum
$$v_{t+1} = \rho v_t +\alpha \nabla f(x_t)$$$$x_{t+1} = x_t - \alpha v_{t+1}$$where $\rho$ is a hyperparameter,nearly 0.99.
```python
vx = 0
while True:
    dx = Grad(x)
    vx = rho*vx + dx
    x -= learning_rate * vx 
```
x change with vx,which means the average of the Gradient.

### Nesterov Momentum
$$v_{t+1} = \rho v_t +\alpha \nabla f(x_t+ \rho v_t)$$ $$x_{t+1} = x_t - \alpha v_{t+1}$$
```python
vx = 0
while True:
    vx = rho*vx + Grad(x+rho*vx)
    x -= learning_rate * vx 
```

### AdaGrad
```python
grad_squared = 0
while True:
    dx = Grad(x)
    grad_squared += dx*dx
    x -= learning_rate * dx / (np.sqrt(grad_squard)+1e-7)
```
- Enlarge the direction with low gradients while divide the pace on the high-gradient-path with a large number to slow it down.
- With time going,the pace go shorter.
- Easy to be trapped in local mimima.

### RMSProp
RMSProp is a improved AdaGrad.
```python
grad_squared = 0
while True:
    dx = Grad(x)
    grad_squared = decay_rate * grad_squared + (1-decay_rate) * dx *dx
    x -= learning_rate * dx / (np.sqrt(grad_squard)+1e-7)
```
where the decay_rate is a hyperparameter near 0.9

- The pace is always slowing down.

### Mixture：Adam
#### Adam（almost）
```python
first_moment = 0
second_moment = 0
while True:
    dx = Grad(x)
    first_moment = beta1 * first_moment + (1 - beta1)*dx # like momentum
    second_moment = beta2 * second_moment + (1 - beta1)* dx *dx #like RMSProp
    x -= learning_rate * first_moment / (np.sqrt(second_moment) + 1e-7) 
```
where beta1 and beta2 is hyperparameters close to 1.

Problem： the first step will be very wide.
  
#### Adam(complete)
Using Unbia Estimates！
```python
first_moment = 0
second_moment = 0
while t in range(num_iterations):
    dx = Grad(x)
    first_moment = beta1 * first_moment + (1 - beta1)*dx # like momentum
    second_moment = beta2 * second_moment + (1 - beta1)* dx *dx #like RMSProp

    #unbias estimates
    first_unbias = first_moment / (1 - beta1**t)
    second_unbias = second_moment / (1 - beta1**t)

    x -= learning_rate * first_unbias / (np.sqrt(second_unbias) + 1e-7) 
```
where beta1 and beta2 is hyperparameters close to 1.

Bias correction for the fact that first and second moment estimates start at zero.

## Learning Rate
- Learning rate is considered to be the most important hyperparameter , for it is sentive and exists in all the algorithms.
- At start, we should find a well-performed learning rate.
![avatar](./L7_Pic1.png)
- Common method:Find a well-performed rate without decay,see what happens,than add decay factors.

### Decay learning rate
- Step decay
  e.g. decay by half every few epoches.
  $$\alpha = \beta^{[\frac{t}{T}]} \alpha_0 $$
- Exponetial decay
    $$\alpha = \alpha_0 e^{-kt}$$
- 1/t decay
  $$\alpha = \alpha_0 / (1 + kt)$$

## High-Order Optimization
With the example of Second-Order.
1. Use gradient and Hessian to form quadratic approximation.
2. Step to the minima of the approximation. 