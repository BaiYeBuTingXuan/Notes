# Projection
## Orthographic Projection
$$P:(x_c,y_c,z_c)^T --> (x_s,y_s)^T$$
$$x_c = x_s \quad y_c = y_s$$
$$
P = 
 \begin{bmatrix}
   1 & 0 & 0 \\
   0 & 1 & 0
  \end{bmatrix} 
$$
or
$$
P = 
 \begin{bmatrix}
   1 & 0 & 0 & 0 \\
   0 & 1 & 0 & 0 \\
   0 & 0 & 0 & 1
  \end{bmatrix} 
$$

### scaled orthography
$$
P = 
 \begin{bmatrix}
   s & 0 & 0 \\
   0 & s & 0
  \end{bmatrix} 
$$
or
$$
P = 
 \begin{bmatrix}
   s & 0 & 0 & 0 \\
   0 & s & 0 & 0 \\
   0 & 0 & 0 & 1
  \end{bmatrix} 
$$

## Perspective Projection
$$P:(x_c,y_c,z_c)^T --> (x_s,y_s)^T$$
![perspectiveprojection](pic\perspectiveprojection.png "perspectiveprojection") 
Similarity relationship:
$$
\frac{x_s}{f} = \frac{x_c}{z_c}
$$
y-coordinate behaves similarily:
$$(x_s,y_s)^T = (fx_c/z_c,fy_c/z_c)^T$$
$$
\tilde{x}_s = 
 \begin{bmatrix}
   f & 0 & 0 & 0 \\
   0 & f & 0 & 0 \\
   0 & 0 & 1 & 0
  \end{bmatrix} 
\overline{x}_c
$$

### Principal Point offset
- To ensure positive pixel coordinate
$$
\frac{x_s}{f} = \frac{x_c}{z_c}
$$
y-coordinate behaves similarily:
$$(x_s,y_s)^T = (f_x x_c/z_c+sf_y y_c/z_c + c_x,f_y y_c/z_c+c_y)^T
$$
### K: Calibration Matrix
$$
\tilde{x}_s = [K,0] \overline{x}_c
$$
$$
K = 
 \begin{bmatrix}
   f_x & s & c_x & \\
   0 & f_y & c_y & \\
   0 & 0 & 1 &
  \end{bmatrix} 
$$
- $s$: due to the sensor not mounted perpendicular to the optical axis
- In practice, $f_x=f_y$ and $s = 0$

### Chaining Transformations
- c:camera coordinate
- w:world coordinate

$$
\tilde{x}_s = [K,0] \overline{x}_c = [K,0]
\begin{bmatrix}
   R & t \\
   0 & 1
  \end{bmatrix} 
\overline{x}_w=
K[R,t]\overline{x}_w
$$
Here we note:
$$P = K[R,t]$$
that is $3\times 4$ projection matrix from world to image

### Full Rank Represantation
$$ \tilde{x}_s = [K,0] \overline{x}_c = \begin{bmatrix}
   K & 0 \\
   0 & 1
\end{bmatrix}
\begin{bmatrix}
   R & t \\
   0 & 1
  \end{bmatrix} 
\overline{x}_w
$$
where $\tilde{x}_s$ is a 4D vector
Normalize $\tilde{x}_s$:
$\overline{x}_s = \tilde{x}_s/z_s = (x_s/z_s,y_s/z_s,1,1/z_s)^T $

## Lens Distortion
- Both __radical and tangential__ distortion
- Image can be undistorted
- Second-order Approximation of Distortion
  - $r^2 = x^2+y^2$
  - __Radical__
  $$d_r = (1+\kappa_1 r^2+\kappa_2 r^4)$$
  - __Tangential__
  $$d_t = 
  \begin{bmatrix}
   2 \kappa_3 xy + \kappa_4 (r^2+2x^2)\\
   2 \kappa_4 xy + \kappa_3 (r^2+2y^2)
  \end{bmatrix} 
  $$
  - Total
  $$x' = d_r x + d_t $$
![LensDistortioin](pic\LensDistortioin.png "LensDistortioin") 
