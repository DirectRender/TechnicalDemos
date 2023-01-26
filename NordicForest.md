# Nordic Forest ``Technical Demo``
## Download: https://renderu.itch.io/nordic-forest
![ScreenshotOne](https://user-images.githubusercontent.com/54723076/214756604-83baa711-414c-46c7-bf2f-8775a6fd9d89.png)

````
- Assets used: https://www.unrealengine.com/marketplace/en-US/product/nordic-conifer-biome
````
````
- Uses RendererSystem (My own settings handler to optimize easy and fast for projects. It's not public yet*)
- RendererSystem is still in preview, not close to done and is not doing much in this project, but it will get better with time.
- RendererSystem is fully made in C++ for performance and because Blueprint (BP) does not offer everything. It will have Blueprint (BP) support.
````

## Technical details
```
- Uses Nanite to handle about ~100 million triangles. The bigger version level of "Nordic Forest" uses about 5 billion triangles and is running the same performance. 
- Uses Lumen for Global Illumination and Reflections.
- Uses Ray Traced Shadows instead of Shadow Mapping/Virtual Shadow Mapping (SM/VSM).
- Uses Contact Shadows for smaller foliage/meshes such as grass, leafs and swamps.
- Uses Temporal Super Resolution (TSR) for Anti-Aliasing.
- Has an average of ~2 million tris being drawned, there for it's not optimized good enough. (The bigger version level has around ~500 thousand tris)
- Nanite calculates 5-10 thousand instances/meshes, depending on where the camera/player is.
- Alot of Ray Tracing is used, so Draw calls is exactly optimized enough to keep up with the GPU. (We do not support bottleneck)
- Reflections does not use High Quality Translucency Reflections (Look in the water, picture above*) since that costs way too much in this scene.
- It does use Virtual Textures since we are using up to 8192x8192 (8k) textures, but most textures are 4096x4096 (4k).
- It doesn't use RVT (Runtime Virtual Textures), but it is planned for the future in other technical demos.

- Currently only works on Windows for 10 and 11.
- It uses DX12 (DirectX 12) with both Shader 5 & 6. <- This might cause crashes or even visible bugs on AMD GPU's.
- I strongly recommend an RTX 2000 / RX 6000 series or higher GPU for atleast 30 frames per second (33ms). My 3070 Ti can handle about 60 frames per second (16ms).
````

## How Ray Tracing works in this scene
```
Every shadow in this scene uses Ray Tracing, there for it's also a high computational cost. However, if Shadow Maps were utilized instead, an additional 100ms of GPU processing time would be gained (depending on cascades and distance). Currently, the GPU is operating at a rate of 12-18ms on a 3070 Ti.

Ray tracing only culls objects that are in-front and behind the camera/player, utilizing a 15000-unit (150 meter) distance and a 5-degree angle.

Things such as grass, moss and tiny rocks does not dynamic shadows at all, since we want the best performance with little to no impact on quality.
So for grass, moss and tiny rocks we only use contact shadows instead of anything dynamic.
```
An example of RTCS: https://images.nvidia.com/geforce-com/international/comparisons/control/control-ray-traced-contact-shadows-interactive-comparison-001-on-vs-off.html

#
```This is the whole scene, it does not look like you thought.```
![ScreenshotTwo](https://user-images.githubusercontent.com/54723076/214756654-3586291c-2d96-4ecb-aaf0-f590c5252691.png)
#
```This is the whole scene but in Nanite Triangles viewmode, calculating over 100 million triangles (No LODs or cull distance at all)```
![ScreenshotTwoTriangles](https://user-images.githubusercontent.com/54723076/214756662-bbb120e6-9c69-495c-8a5a-6d98315ac011.png)
#
```One of the mesh without Nanite```
![TreeWithoutNanite](https://user-images.githubusercontent.com/54723076/214756685-5ba27a29-fb2e-4806-9c98-066b04ef8205.png)
#
```One of the mesh WITH Nanite. Take a note that the bigger scene has over 5 billion triangles and this tree has around 6000 triangles without visible quality changes in that scene. The bigger scene is not dual for production/tech since it only offers limited stuff, there for I only released the small one I made in one hour. Everything is mostly procedural since I'm not a level designer nor do I like it.```
![TreeWithNanite](https://user-images.githubusercontent.com/54723076/214756689-15ec9d1b-b90f-40e3-81ae-09abd9fedefa.png)

