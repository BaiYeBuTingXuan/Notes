# Agenda
- Primitives and Transformations
- Geometric Image Formation
- Photometric Image Formation
- Image Sensing Pipeline

# Primitives and Transformations
## 2D points
- 2D Point in inhomogeneous coordinates as:
  
$$ x = (x,y)^T \in \mathbb{R}^2 $$

- Or in homogeneous coordinates as:

$$ \tilde{x} = (\tilde{x},\tilde{y}, \tilde{\omega})^T \in \mathbb{P}^2 $$

where $\mathbb{P}^2 = \mathbb{R}^3 \ {(0,0,0)}$ is called __projective space__
    - __Homogenenous vectors that differ only by scale are considered equivalent__ while define an equivalence class
    - Homogenenous vectors are defined only up to scale

- An inhomogeneous vector x --> a homogenenous vector $\tilde(x)$
    - Define __Augemanted Vector__:
      
$$ \overline{x} = (x,y,1)^T $$

- Convert

$$ \overline{x} = \frac{1}{\tilde{\omega}}\tilde{x} $$

- When $\tilde{\omega} = 0$ this point is called __ideal point or point at infinity__

![2Dpoints](pic\2Dpoints.png "2Dpoints") 

## 2D lines
- $\{\overline{x} | \tilde{l}^T\overline{x} = 0\}$ for $\tilde{l} = (a,b,c)$
- $\tilde{l}_{\infty} = (0,0,1)^T$


## Cross Product
$$
a \times b = [a]_{\times} b = 
 \begin{bmatrix}
   0 & -a_3 & a_2 \\
   a_3 & 0 & -a_1 \\
   -a_2 & a_1 & 0
  \end{bmatrix} b
= \begin{bmatrix}
   a_2b_3-a_3b_2 \\
   a_3b_1-a_1b_3 \\
   a_1b_2-a_2b_1
  \end{bmatrix}
$$

## 2D line arithmetic
- Intersection of two lines:
$$\tilde{x} = \tilde{l}_1 \times \tilde{l}_2$$
- Joining of two points:
$$\tilde{l} = \tilde{x}_1 \times \tilde{x}_2$$

## 2D Conics
- $\{\overline{x} | \overline{x}^T Q \overline{x} = 0\}$

![2DConics](pic\2DConics.png "2DConics") 

## 3D Points Planes Lines
- Points
  
$$ x = (x,y,z)^T \in \mathbb{R}^3 $$

$$ \tilde{x} = (\tilde{x},\tilde{y}, \tilde{z}, \tilde{\omega})^T \in \mathbb{P}^3 $$

$$ \overline{x} = \frac{1}{\tilde{\omega}}\tilde{x}$$

- Planes
$\{\overline{x} | \tilde{m}^T\overline{x} = 0\}$ for $\tilde{m} = (a,b,c)$

$$\tilde{m}_{\infty} = (0,0,0,1)^T$$

- Lines
  
$$\{x | x = (1-\lambda) p +  \lambda q,  \lambda\in \mathbb{R}\}$$

- Quadrics
  
$$\{\overline{x} | \overline{x}^T Q \overline{x} = 0\}$$
![Quadrics](pic\3DQuadrics.png "Quadrics") 

## Transformation
![transformation](pic\transformation.png "transformation") 

- Transition(2DoF)
  
$$x' = x + t \Leftrightarrow \overline{x}' 
= \begin{bmatrix}
   I & t \\
   0 & 1
  \end{bmatrix}
  \overline{x}'
  $$

- Euclidean(2D Translation + 2D Rotation, 3DoF)
  
$$x' = Rx + t \Leftrightarrow \overline{x}' 
= \begin{bmatrix}
   R & t \\
   0 & 1
  \end{bmatrix}
  \overline{x}'
  $$
  
  where $R \in SO(2)$
  - Euclidean transformations preserve __Euclidean Distance__

- Similatrity(2D Translation + 2D Scaled Rotation, 4DoF)
  
$$x' = sRx + t \Leftrightarrow \overline{x}' 
= \begin{bmatrix}
   sR & t \\
   0 & 1
  \end{bmatrix}
  \overline{x}'
  $$
  
  where $R \in SO(2)$
    - Similatrity transformations preserve __Angles__

- Affine(2D Linear Transformation, 6DoF)
  
$$x' = Ax + t \Leftrightarrow \overline{x}' 
= \begin{bmatrix}
   A & t \\
   0 & 1
  \end{bmatrix}
  \overline{x}'
  $$
  
  where A is an arbitrary  $2\times 2$ matrix
    - Affine Transformation preserve __Parallel__ Lines

- Perspective(Homography, 8DoF)
  
$$\tilde{x}' = \tilde{H}\tilde{x}$$

  where $\tilde{H}$ is an arbitrary homogeneous $3\times 3$ matrix
    - Perspective Transformation only preserve __Straight__ lines

## 2D Transformations on Co-Vectors
Considering:

$$\tilde{x}' = \tilde{H}\tilde{x}$$

to keep the transformated 2D line equation:

$$\tilde{l}'^T\tilde{x}' = \tilde{l}'^T\tilde{H}\tilde{x} = (\tilde{H}^T\tilde{l}')^T\tilde{x}  = \tilde{l}^T\tilde{x}$$

there are:

$$\tilde{l}' = \tilde{H}^{-T}\tilde{l}$$

Thus, the action of a projective transformation an a co-vector can be represented by the __transposed inverse__ of the matrix

![group](pic\transformationgroup.png "group") 

## Homography Estimation
![estimation1](pic\estimation1.png "estimation1") 
![estimation2](pic\estimation2.png "estimation2") 
