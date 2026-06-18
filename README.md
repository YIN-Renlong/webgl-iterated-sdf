# WebGL Iterated SDF Morphing

A high-performance, cinematic demoscene visualization of iterated spatial deformations built with WebGL, GLSL, and Three.js.

## 🌟 Live Demo
https://yin-renlong.github.io/webgl-iterated-sdf

## 🧮 The Mathematics
At first glance, the deformation function appears deceptively simple. However, the immense visual complexity arises from **recursive function composition**, **vector swizzling**, and **implicit surface evaluation**.

**1. The Base Shape**
The foundation is a standard unit sphere, defined as an implicit surface where the magnitude of vector `p` equals 1:
`||p|| = 1`

**2. The Deformation Operator**
The space is warped using a non-linear operator:
`f(p) = p + 0.5 * sin(π * p.yzx)`
*Note the vector swizzle (`yzx`). This cross-couples the dimensions so that the displacement on the X-axis is driven by the Y-coordinate, creating a twisting, topological vortex rather than a uniform bulge.*

**3. Recursive Iteration**
The states shown in the UI are iterations of this operator fed into itself:

- State 0: `||p|| = 1`
- State 1: `||f(p)|| = 1`
- State 2: `||f(f(p))|| = 1`
- State 4: `||f(f(f(f(p))))|| = 1`

**4. Continuous Interpolation**
To achieve the fluid morphing animation, the shader continuously interpolates between discrete iterated states. Given a transition float `t` from 0.0 to 4.0, where `i = floor(t)` and `a = fract(t)`, the surface is evaluated as:
`|| mix( f^i(p), f^(i+1)(p), a ) || = 1`

## 🚀 Technical Highlights
- **Analytic Plane Intersection:** The infinite mirror floor is calculated analytically via ray-plane intersection rather than stepped, saving massive GPU overhead.
- **Dynamic Safety Factors:** As the mathematical space folds more aggressively at higher iterations, the raymarcher dynamically shrinks its step-size to prevent rendering artifacts (overshooting the distance field).
- **Bounding Volume Optimization:** Fast empty-space skipping using an unscaled bounding sphere.
- **Topological Texturing:** The spherical grid is projected through the morphed coordinate `q`, allowing the grid lines to stretch, twist, and fold *with* the mathematics.
- **Cinematic Rendering:** Features Fresnel rim lighting, fake ambient occlusion, physical reflections, filmic tonemapping, and vignette post-processing.

## 🛠️ Usage
No build step is required. The entire engine is contained within a single file.
Simply open `index.html` in any modern web browser.

## 📚 Credits
- Architecture and Raymarching concepts inspired by demoscene techniques pioneered by Inigo Quilez.
- Camera and boilerplate handled via [Three.js](https://threejs.org/).
EOF
