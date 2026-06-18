# WebGL Iterated SDF Morphing

A high-performance, cinematic demoscene visualization of iterated spatial deformations built with WebGL, GLSL, and Three.js.

## 🌟 Live Demo
*(After you push to GitHub, enable GitHub Pages and put your link here: `https://yourusername.github.io/webgl-iterated-sdf`)*

## 🧮 The Mathematics
This project visualizes the recursive application of a spatial deformation function using Signed Distance Fields (SDFs) and Raymarching. 

The core deformation function is:
`f(p) = p + 0.5 * sin(π * p.yzx)`

The shader calculates the 3D space for the unit sphere `||p|| = 1`, and interpolates through 4 iterations of the function up to `||f(f(f(f(p))))|| = 1`.

## 🚀 Technical Highlights
- **Analytic Plane Intersection:** The infinite mirror floor is calculated analytically rather than stepped, saving massive GPU overhead.
- **Dynamic Safety Factors:** As the mathematical space folds more aggressively at higher iterations, the raymarcher dynamically shrinks its step-size to prevent rendering artifacts (black holes).
- **Bounding Volume Optimization:** Fast empty-space skipping using an unscaled bounding sphere.
- **Topological Texturing:** The black grid is mapped to the morphed coordinate `q`, allowing the grid lines to stretch and fold *with* the mathematics.
- **Frame-Rate Independent Easing:** JavaScript UI and camera interpolations use delta-time to ensure identical animation speeds across 60hz and 144hz monitors.
- **Cinematic Rendering:** Features Fresnel rim lighting, fake ambient occlusion, physical reflections, filmic tonemapping, and vignette post-processing.

## 🛠️ Usage
No build step is required. The entire engine is contained within a single file.
Simply open `index.html` in any modern web browser.

## 📚 Credits
- Architecture inspired by demoscene techniques pioneered by Inigo Quilez.
- Camera and boilerplate handled via [Three.js](https://threejs.org/).
