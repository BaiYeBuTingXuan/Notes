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
- Learning rate is considered to be the most important hyperparameter , for it is sentive and exists in almost all the algorithms.
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

### Strict Seconde-Order
1. Use gradient and Hessian to form quadratic approximation.
2. Step to the minima of the approximation.

Second order Taulor Expansion:
$$J(\theta) \approx J(\theta_0) + (\theta-\theta_0)^T \nabla_{\theta}J(\theta_0)+\frac{1}{2}(\theta-\theta_0)^TH(\theta-\theta_0)$$ 

Solving the Critical Point（驻点）,we obtain the Newton parameter update:
$$\theta^* = \theta_0 - H^{-1}\nabla_{\theta}J(\theta_0)$$

COOL:there is not Learning Rate!!!
But in pratice,you nead learning rate,for the estimation not fitting perfectly.
Bad news:Hessian Matrix is N * N where N is Hundreds of Millions,that cost expensively.

### Quasi-Newton Method（BGFS）
Instead of inverting the Hessian(O(n^3)),approximate inverse Hessian with rank 1 updates over time(O(n^2))

### L-BGFS(limit-memory BGFS)
- Usually work very well in full batch,deterministic mode i.e. if you have a single,deterministic f(x) then L-BGFS will probably work nicely.
- Does not transfer very well to mini-batch setting.Gives bad result.Adapting L-BGFS to large-scale,stochastic setting is an active area of research.

## Embadded Model
- Train several model in some time
- Get results of all of them,then the average of that is the final resualts.

## Regularization
 $$Full\_Loss = \Sigma Loss_{i}+ \lambda R(Weight)$$
 Common use:
      - L2 regularization : $R(W) = \Sigma_i \Sigma_j W^{2}_{i,j}$
        ''Average the Weight!''
      - L1 regularization : $R(W) = \Sigma_i \Sigma_j |W_{i,j}|$ 
        "More zeros in Weight!"
      - Elastic net(L1+L2) : $R(W) = \Sigma_i \Sigma_j \beta|W_i,j|+W^{2}_{i,j}$ 
      - Max Norm Regularization
        ''Average each column,not each item''
      - Dropout 

### Dropout
In each forward pass,randomly set some of the neurons to zero.Probability of dropping is a hyperparameter,that 0.5 is common.

```python
p = 0.5
def train_step(x):
""" X contains the data """

#forward pass for example 3-layer neural network
H1 = np.maximun(0,np.dot(W1,X)+b1) #ReLU
U1 = np.random.rand(*H1.shape) < p #drop mask
H1 *= U1 # drop!

""" * : 序列解包 """

H2 = np.maximun(0,np.dot(W2,H1)+b2)
U2 = np.random.rand(*H2.shape) < p #drop mask
H2 *= U2 #drop!

out = np.dot(W3,H2) + b3

# backward pass:computing gradients...
# perform parameter update...
```

#### Q：Why Dropout Effects？
Ans：
  1. Forces the network to have a redundant represantation;Prevent co-adaptation of features(Prevent overfitting somehow).
  2. Dropout seems training a large ensemble of models that share parameters--Each binary mask is a model!

#### Testing
Problem:Dropout make the output random!
$$output = f_W(input,dropout\_mask)$$

- Average out
    $$ output = E_{dropout\_mask}[f_W(input,dropout\_mask)] 
    $$$$=\int p(dropout\_mask)f_W(input,dropout\_mask)d(dropout\_mask) $$
But the intergral is hard to deal with,so that we want to approximate the intergral.

One easy is to multiply by dropout probability at test time.

```python
def predict(x):
    #ensemble forward pass ...
    H1 = np.maximun(0,np.dot(W1,X)+b1) * p
    H2 = np.maximun(0,np.dot(W2,H1)+b2) * p
    out = np.dot(W3,H2)+b3
```

More common,we use the 'inverted dropout',that divides 'p' at trainning rather than wasting testing time.

### Data Augmentation(数据增强)
Idea:change the input data randomly and slightly,like random crops(裁剪) and scales
