# Structure From Motion

## Agenda
- Preliminaries
- Two-frame Structure-from-motion
- Factorition
- Bundle Adjustment

## Preliminaries

### Camera Calibration
- __Camera Calibration__ is the process of finding the __intrinsic/extrinsic parameters__
- Steps:
    - __Known__ calibration target is captured in __different poses__;
    - features on the target are detected;
    - camera __intrinsics and extrinsics__ are __jointly optimized__.
        - Closed-form solution
        - Non-linear optimization

### Feature Detection and Description

#### Point feature:local,salient regions
- usage
    -  describe and match images
    - basis of spare 3D reconstruction method
- invarient to perspective effects and illumination
- similar vector independent of pose or viewpoint
- SIFT : Scale Invariant Feature Transform

## Two-frame Structure-from-Motion

### Epipolar Geometry
![Epipolar](pic\Epipolar.png "Epipolar") 
- 3D point x is projected to pixel $\overline{x}_1$ in image 1 and pixel $\overline{x}_2$ in image 2.
- The 3D point x and the two camera centers span the __epipolar plane__
- __Epipolar line__: Intersection of image 1 or 2 and the __Epipolar Plane__
- __Base line__ connected the focuses of image 1 and image 2
- __Epipoles__: Intersection of image 1 oi 2 and the baseline
- Let __R__ and __t__ denote the relative pose between 2 camera

For a 3D point x, there are:
- Coordinates in Camera 1 $x_1$ , in Camera 2 $x_2$
$$x_2 = Rx_1+t$$
- $x_1$, $\tilde{x}_1$ is on the same line:
$$x_1 \propto  \tilde{x}_1$$
$$x_2 \propto  \tilde{x}_2$$
- So that(s is a scaled parameter)：
$$\tilde{x}_2 \propto x_2 = Rx_1+t \propto R\tilde{x}_1+st $$
- To eliminate $s$, appliy $t \times$ both side:
 $$t \times \tilde{x}_2 \propto  t \times R\tilde{x}_1 $$
- To obtain a equation, apply $\tilde{x}_2 \cdot$ both side:
 $$ 0 =\tilde{x}_2 \cdot( t \times R\tilde{x}_1) $$
- Let __Epipolar matrix__ $E = t \times R$:
 $$ \tilde{x}_2^T  E\tilde{x}_1 =0$$
- hence, a point in image 1 $\tilde{x}_1$ is correspond to a Epipolar line in image 2
$$ \tilde{l}_2 = E\tilde{x}_1$$
$$ \tilde{x}_2^T \tilde{l}_2 = 0$$
- Notably, there stands a point called __epipolar point__ $e_2$ on every epipolar line derived from point in image 1 that:
$$ \tilde{e}_2^T \tilde{l}_2 = 0$$
- Or we could say $\tilde{e}_2^T$ is __left null-space__ of $E$. Further, $\tilde{e}_1$ is __right null-space__ of $E$
- Find $E$: __Normalized 8-point Algorithm__:
    - Find corresponding pairs of 8
    - Using Equation  $\tilde{x}_2^T  E\tilde{x}_1 =0$ and $det(E)=0$

- From known $E$ with obtain $t$ as $E$'s left eigenvector with eigenvalue of 0 (In practice, choose the smallest eigenvalue):
$$\hat{t}_T E = \hat{t}^T (t \times R) = 0$$
- and we could get $R$

Usually, we dont know $\tilde{x}$ but know $\overline{x}$ that can be read directly from pixels because $K$ that $\overline{x} = K \tilde{x}$ is unknown, hence we use __fundamental matrix__ $F$:
 $$ \tilde{x}_2^T  E\tilde{x}_1 = \overline{x}_2^T  F\overline{x}_1 = 0$$
 where $$F = K_2^{-1}EK_1^{-1}$$

### Triangulation
2 picture, Camera Intrinsics and the Extrinsics -- > 3D points cloud
#### Direct Linear Transformation
- Let:
$$\tilde{x}_i^s = \tilde{P}_i\tilde{x}_w$$
$$\tilde{x}_i^s \times \tilde{P}_i\tilde{x}_w$$
Using $\tilde{p}^T_{ik}$ to denote the k'th row of the ith camera's projection matrix $\tilde{P}_i$, we obtain:
$$
A_i
\tilde{x}_w
=
\begin{bmatrix}
   x_i^s\tilde{p}^T_{i3}-\tilde{p}^T_{i1} \\
   y_j^s\tilde{p}^T_{i3}-\tilde{p}^T_{i2}
\end{bmatrix}
\tilde{x}_w = 0
$$
where $$\tilde{x}_i^s=(x_i^s,y_i^s,w_i^s)^T$$
- If there are N(more than 2) observations of a point, we obtain:
$$A\tilde{x}_w=0$$
that is the __right singluar vector problem(DLT)__ or __least squares problem__ in practice.

#### Reprojection Error Minimization
- Clearly there are a mapping from $x_w$ to $x_s$:
$$x_s = f(x_w)$$
- The gold standard is to minimize the reprojection error using:
$$\overline{x}_w^* = arg \ min \Sigma_i ||f(\overline{x}_w)-\overline{x}_i^o||^2_2$$

## Factorization