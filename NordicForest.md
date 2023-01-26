# Nordic Forest ``Technical Demo``
## Download: https://renderu.itch.io/nordic-forest
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
- Has an average of ~3 million tris being drawned (Not optimized good enough, the bigger version level has around ~500 thousand tris)
- Nanite calculates 5-10 thousand instances/meshes (Depending on where the camera/player is).
- Alot of Ray Tracing is used, so Draw calls is exactly optimized enough to keep up with the GPU. (We do not support bottleneck)
- Reflections does not use High Quality Translucency Reflections (Look in the water, picture below*) since that costs way too much in this scene.
- It does use Virtual Textures since we are using up to 8192x8192 (8k) textures, but most textures are 4096x4096 (4k).
- It doesn't use RVT (Runtime Virtual Textures), but it is planned for the future in other technical demos.

- Currently only works on Windows for 10 and 11.
- It uses DX12 (DirectX 12) with both Shader 5 & 6. <- This might cause crashes or even visible bugs on AMD GPU's.
- I strongly recommend an RTX 2000 / RX 6000 series or higher GPU for atleast 30 frames per second (33ms). My 3070 Ti can handle about 60 frames per second (16ms).
````
