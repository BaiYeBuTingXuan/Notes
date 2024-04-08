# Linear Classifier

## LIST

1. Parametric Approach
2. Hyperparameters
3. Image


## Parametric Approach：

$$ Scores = Weight * input + bias $$

- For a image 32* 32 , input is a vector of 32 * 32* 3
- Scores is output vector, record the scores of each class,the max is the class it think.
- Weight is a metrix.If input_feature，output_feature = 32 * 32 * 3,10,Weight is of course a Metrix with 32 * 32 * 3 rows and 10 columns.

## Interpreting a Linear Classifier

- From a opinion, Linear Classifier divides the n-D space to some area with linear Manifold (plane\line) 
- So for some cases,Linear Classifier do with poor outcome.

# Case:Hand-Writing numbers reconization

    on a .py file