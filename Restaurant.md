# Restaurant ``Technical Demo``
## Download: https://renderu.itch.io/restaurant
![image](https://user-images.githubusercontent.com/54723076/216186252-bff738af-7cef-4907-afe9-460327373c45.png)

````
- Assets used: https://www.unrealengine.com/marketplace/en-US/product/bistro-restaurant-scene-asset-pack-realtime-archviz
````

## Technical details
```
- We do not use Nanite at all, as it requires Shader Model 6 (SM6), which would reduce our performance massively. The scene has around one million triangles in total.
- Uses Lumen for Global Illumination and Reflections.
- Uses both shadow maps and raytraced shadows. Shadow maps are used for the shadow that comes from the sun, while raytraced shadows are generated from the light source inside the resturant.
- Uses Temporal Anti-Aliasing (TAA) for Anti-Aliasing.
- Has an average of ~1 million tris being drawned.
- Reflections uses High Quality Translucency for real reflections, instead of fake reflections that doesn't make any sense.

- Currently only works on Windows 10 & 11.
- It uses DX12 (DirectX 12) with only Shader 5. Instead of using Shader Model 6 (SM6) we gain performance and AMD GPUs should not experience bugs. (Yes, this was tested on a A
- I strongly recommend an GTX 2060 / RX 5000 series or higher GPU for atleast 60 frames per second (17ms).
- An NVIDIA 3070 Ti can handle about 200 (5ms) frames per second at high settings. (You can see more details below)
- An AMD 5600 XT can handle about 120 (8ms) frames per second at high settings. (You can see more details below)
````

## How Lumen works in this scene
```
Global Illumination (GI) & Reflections uses Lumen, Unreal Engine 5's new realtime/dynamic lighting, no baked lighting at all!
So, yes the sun can move and update every light source in the scene in realtime with decent frames!

By default all the settings are set to Epic. We can change between high & epic by using the buttons below.
Click  (1) - Sets the settings to Epic
Click  (2) - Sets the settings to High
Toggle (E) - Moves the sun in a 360 degree angle on the X axle, making it night/day in just a few seconds.

Lumen reflections uses Hardware Ray Tracing (HRT) at epic. Reflections will seem different in high settings.
Lumen's rays is set to only cast at the Surface Cache and not the Hit lighting. Hit Lighting is more realistic and gives a more accurate reflection, but comes at a higher price.

If you are on a none-RTX card that does not support Lumen/HRT you will only use Software Ray Tracing (SRT), which uses Global Tracing instad of Detail Tracing.
Global Tracing is more efficient and will provide with less details than Detail Tracing would have.

```
What is Lumen?: https://docs.unrealengine.com/5.1/en-US/lumen-global-illumination-and-reflections-in-unreal-engine/
#

## Benchmark tests
```
AMD 5600 XT @ Epic: 90fps (DX12, SM6, Accurate)
RTX 3070 Ti @ Epic: 150fps (DX12, SM6, Accurate)
GTX 1060    @ Epic: 50fps  (DX12, SM6, Accurate)

AMD 5600 XT @ High: 110fps (DX12, SM6, Accurate)
RTX 3070 Ti @ High: 200fps (DX12, SM6, Accurate)
GTX 1060    @ High: 70fps  (DX12, SM6, Accurate)
``` 


```This is the whole scene, from an outside perspective```
![image](https://user-images.githubusercontent.com/54723076/216193952-75d4fd06-4234-441a-9e24-2383d074c44c.png)
#
```This is the whole scene but in Wireframe viewmode, giving us an perspective of all the triangles```
![image](https://user-images.githubusercontent.com/54723076/216194039-80a0d13a-6eed-4696-b063-941538b0d569.png)
#

```Reflections in the windows (adjusted sun rotation*)```
![image](https://user-images.githubusercontent.com/54723076/216194224-a6f05ee8-fe17-4683-9b38-3a65e9c440de.png)
#

```An example of how Lumen/Global Illumination looks in realtime```

https://user-images.githubusercontent.com/54723076/216196957-09d76ccb-0159-491c-b33a-6e0f884f3b36.mp4


