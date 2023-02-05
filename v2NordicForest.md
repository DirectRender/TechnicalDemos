# Nordic Forest ``Technical Demo`` with the power of RendererSystem
## Download: https://drive.google.com/file/d/1vH_k0Vpylg7DBEK4WkNFb20YU4cDEmwN/edit (I can't upload it to itch, since it's over the 1GB limit)
![image](https://user-images.githubusercontent.com/54723076/216806145-eebddadb-637c-4055-849c-0b0c4b79c7d6.png)


````
- Assets used: https://www.unrealengine.com/marketplace/en-US/product/nordic-conifer-biome
````
````
- Uses RendererSystem (My own settings handler to optimize easy and fast for projects. It's not public yet*)
- RendererSystem is still in preview, and this project is heavily used by it to get the best performance and quality.
- RendererSystem is fully made in C++ for performance and because Blueprint (BP) does not offer everything. It will have Blueprint (BP) support.
````

## Controls
```
F1 - Set Anti-Aliasing to TSR, this option may not be suitable for lower-end GPUs.
F2 - Set Anti-Aliasing to TAA, best option for performance.
F5 - Set shadow cascades to 4 (4x can be heavy, since this is the highest shadow detail the engine can go)
F6 - Set shadow cascades to 3 (3x is the default, still expensive but best option for visual quality & performance)
F7 - Set shadow cascades to 2 (2x is the poorest option you get, best option for performance)
```

## Technical details
```
- In total this scene has around 2 billion triangles, everything besides the trees have culling on.
- Uses Lumen for Global Illumination.
- Uses Screen Space (SSR) for Reflections.
- Uses Shadow Mapping with cascades between 2-4 (3 is default).
- Uses Contact Shadows for smaller foliage/meshes such as grass, leafs and swamps.
- Uses Temporal Super Resolution (TSR) and Temporal Anti Aliasing (TAA) for Anti-Aliasing.
- Has an average of ~3 million tris being drawned every frame.
- It does use Virtual Textures since we are using up to 8192x8192 (8k) textures, but most textures are 4096x4096 (4k).
- It doesn't use RVT (Runtime Virtual Textures), but it is planned for the future in other technical demos.

- Currently only works on Windows for 10 and 11.
- It uses DX11 (DirectX 11) with Shader Model 5. <- This should fix crashes for AMD GPU's since version 1 of the Nordic Forest had problems with this using DX12 with SM5 & SM6.
- I strongly recommend an RTX 1060 / RX 5000 series or higher GPU for atleast 60 frames per second (16.6ms). My 3070 Ti can handle about 150 frames per second (7ms).
- I recommend atleast 4GB RAM and as much VRAM as you can share.
````

## Why and how?
```
- We use Screen Space Reflections (SSR) instead of Lumen Reflections because Lumen Reflections relies on Ray Tracing. However, not a single mesh support Ray Tracing due to the high number of draw calls involved.
- Lumen rays only travel a distance of 50 meters. Beyond that, Screen Space Global Illumination takes over. However, this transition may not be easily noticeable.
- Shadows only exists up to 200m. Beyond that, Distance Field Shadows takes over.
- Distance Field Shadows have a limited range of 512 meters, which is 1/4th of the map size. Although Distance Field Shadows provide low-detailed shadows compared to Cascaded Shadow Maps, they have the advantage of being highly efficient, only taking 0.2 milliseconds on the GPU. In comparison, Cascaded Shadow Maps consume 1-2 milliseconds (depending on the number of cascades used and where you are in the scene).
- The map also uses Ultra Dynamic Sky (UDS), which is a fantastic tool with impressive performance! https://www.unrealengine.com/marketplace/en-US/product/ultra-dynamic-sky
```

#
```This is the whole scene from a higher z-point of view```
![image](https://user-images.githubusercontent.com/54723076/216807182-2aa95830-abfe-421f-946b-4a4244069b2a.png)
#
