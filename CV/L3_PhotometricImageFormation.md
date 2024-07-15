# Photometric Image Formation
- We now discuss how an image is formed in terms of pixel intensities and colors

## Rendering Equation
- $v$ : direction of view
- $n$ : normal
- $\Omega$ : a unit hemisphere at normal n
- $p$ : the position
- $\lambda$ : wavelength
- $BRDF(p,r,v,\lambda)$ : The __Bidirectional Reflectance Distribution Function__

$$L_{out}(p,v,\lambda) = L_{emit}(p,v,\lambda) + \int_{\Omega} BRDF(p,r,v,\lambda)L_{in}(p,v,\lambda)(n^T r)dr$$

### Diffuse and Specular Reflection
- Typical BRDFs have componets of diffuse and specular items
- The diffuse component  scatters uniformly in all directions
- The specular component depends on the outgoing light direction

## Thin Lens Model
$$\frac{1}{z_s} + \frac{1}{z_c} = \frac{1}{f}$$
If index of refraction is n, from Snell's law:
$$f = \frac{R}{2(n-1)}$$

Axis-parallel rays pass the focal point, rays via center keep direction

If the image plane is out of focus, a 3D point project to a __circle of confusion c__

__f-number__ N:
$$N = \frac{f}{d}$$

Decreasing the aperture diameter increase the DoF(Depth of Field)

## Chromatic Aberration
- The __index of refraction__ for glass varies slight as a function of wavelength
- Chromatic --> blur, color shift

## Vignetting(晕影)
- Vignetting is the tendency for the brightness to fall off towards the image edge
- Composition of 2 effects: natural and mechanical vignetting
- Vignetting can be undone

# Image Sensing Pipeline
- Physical Light Transport
- Photon Measurement
- Image Signal Processing (ISP)

## Sensor
- CCD
- CMOS

## Color
- Bayer Grid
![ColorArray](pic\ColorArray.png "ColorArray") 