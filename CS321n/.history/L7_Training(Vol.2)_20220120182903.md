#  Trainning 
Volume 2

## Outline

1. Fancier optimization
2. Regularization
3. Transfer Learning

## Fancier Optimization
### SGD Problem
$$x_{t+1} = x_t - \alpha \nabla f(x_t)$$
   1. Trap into a local minima or saddle point
   2. Loss comes from random mini-batch that noise.
### Improve:SGD+Momentum
$$v_{t+1} = \rho v_t +\alpha \nabla f(x_t)$$$$x_{t+1} = x_t - \alpha v_{t+1}$$where $\rho$ is a hyperparameter,nearly 0.99.
```python
vx = 0
while True:
    dx = Grad(x)
    vx = rho*vx + dx
    x += learning_rate * vx 
```
x change with vx,which means the average of the Gradient.
### Nesterov Momentum
$$v_{t+1} = \rho v_t +\alpha \nabla f(x_t+ \rho v_t)$$$$x_{t+1} = x_t - \alpha v_{t+1}$$
