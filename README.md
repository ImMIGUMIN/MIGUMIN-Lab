<table>
  <tr>
    <td width="230" align="center" valign="middle">
      <img src="./assets/migumin-mascot.webp" width="180" alt="MIGUMIN chibi assistant" />
    </td>
    <td align="left" valign="middle">
      <img src="https://readme-typing-svg.herokuapp.com?font=Cascadia+Code&weight=700&size=22&pause=1000&color=9ED7A7&center=false&vCenter=true&width=540&lines=Let%27s+learn+and+improve+together~" alt="Let's learn and improve together~" />
    </td>
  </tr>
</table>

<p align="center">
  <a href="https://github.com/Retourflow"><b>PROFILE</b></a> ·
  <a href="#map"><b>MAP</b></a> ·
  <a href="#unity"><b>UNITY</b></a> ·
  <a href="#blender"><b>BLENDER</b></a> ·
  <a href="#ae"><b>AE</b></a>
</p>

> **Core:** document what I actually learn and understand.  
> This repository is organized as **column → article**, not as a daily study diary.

<a id="map"></a>

## Map

| Column | Area | Articles |
| --- | --- | ---: |
| [UNITY](#unity) | Rendering / UI / NPR / PBR / Materials / Weather / Modeling / Water / Pipeline | 10 |
| [BLENDER](#blender) | Toon Shading / NPR / Hair Shader / Water Shader | 3 |
| [AE](#ae) | Motion / Wallpaper | 1 |

---

<a id="unity"></a>

## UNITY

### Rendering / UI

- [CanvasGroup 与透明渲染](./Unity/CanvasGroup-Alpha-Rendering.md)  
  这篇是我在研究角色淡出时整理出来的。原本只是觉得“把所有图层一起调透明就行”，后来才发现多层图片会互相透出来、叠色。最后把一个问题理清了：多层 UI / 角色图一起淡出时，问题不只是透明度本身，还和图层顺序、混合方式以及渲染流程有关，所以有时候应该用 Dissolve、Dither Fade 或 RenderTexture，而不是单纯把 Alpha 一起往下拉。

- [《终末地》3 渲 2 角色渲染与 Shader 通俗解释](./Unity/Endfield-3D-Toon-Rendering-and-Shader.md)  
  这篇算是我真正开始看懂 3 渲 2 的一篇笔记。以前更多是在看“效果好不好看”，整理完以后开始能分清阴影、脸部、头发高光、描边和后期分别在做什么。也理清了我之前最容易混在一起的问题：3 渲 2 不是一个单独的 Shader 效果，而是模型、贴图、光照、Mask、Render Pass 和后期一起工作的结果。

- [反光地面：Shader、反射、Roughness、Bump 与环境之间的关系](./Unity/Reflective-Floor-Shader-Reflection-Roughness-Bump.md)  
  这篇是我折腾反光地面时留下的笔记。过程中把 Light、Roughness、Bump 和环境之间的关系慢慢理顺了。最后主要理清了几个一直容易混的问题：Roughness 决定反射有多散，Bump 只是扰动表面，不负责“制造反射”；Shader 决定地面有多会反光，而环境里有没有真正可被反射的东西，才决定最后能不能看到倒影。

- [《终末地》雨雪天气与程序化 Mask](./Unity/Endfield-Weather-Procedural-Mask.md)  
  这篇是从《终末地》的雨雪效果一路整理下来的。最有意思的是发现雨、雪、灰尘和边缘磨损虽然看起来完全不同，但背后其实都可以用已有数据去生成 Mask。最后把“程序化 Mask 到底是什么”这件事理清了：Mask 不一定是一张手画的黑白图，它本质上只是 0～1 的权重，可以直接由 Normal、AO、Curvature、Roughness、Metallic、Noise 等数据算出来，再去决定雪、灰尘、湿润或磨损应该出现在哪里。

- [AO：从“角落为什么会变暗”到 Shader 里的实际用法](./Unity/AO-Ambient-Occlusion-Shader.md)  
  这篇是我把 AO 单独拎出来重新整理的一篇。之前总会把 AO、普通阴影和灰尘混在一起，看到角落变暗就很容易理解成“这里比较脏”。整理完以后终于理清了：AO 说的是周围空间有多封闭、环境光有多难进去；它本身不是灰尘，也不是普通 Shadow，但既能直接帮助表现空间感，也能作为 Dust / Dirt 这类程序化 Mask 的一份输入数据。

- [游戏角色模型：高模、动画模、游戏模，以及 Maya / 3ds Max 的位置](./Unity/Game-Character-Models-Highpoly-Animation-Game-ready.md)  
  这篇是我在看角色制作界面、判断眼前的模型到底算高模还是游戏模时整理出来的。一开始很容易把“用 Maya 做动画”“动画模”“高模”这些概念混在一起，甚至会觉得 Maya 更偏动画、3ds Max 才更像游戏建模。最后把它们的关系理清了：高模看的是几何细节，动画模看的是拓扑能不能自然变形，游戏模看的是能不能实时运行；它们不是固定的先后等级，而且很多游戏里动画模和游戏模本来就是同一个 Mesh。Maya、3ds Max、Blender 更像是制作工具，本身并不能决定一个模型属于哪一类。

- [PBR 中 Roughness、Specular 与 Metallic 的关系](./Unity/PBR-Roughness-Specular-Metallic.md)  
  这篇是我在看一个玩偶角色的眼睛材质时顺手复习整理出来的。最开始看到外层镜片反光很强，很容易直觉上把“很亮、很像镜子”和 Metallic 联系在一起。整理完以后把这三个参数真正分开了：Metallic 先决定它是不是按金属来算，Roughness 决定反射是清楚还是散开，Specular 主要决定非金属表面的镜面反射有多强。也因此理清了一个很实用的问题——玻璃、树脂、亚克力这类非金属完全可以非常亮、非常反光，低 Roughness 并不等于高 Metallic；像玩偶眼睛这种效果，更可能是低 Roughness 的非金属镜片，再配合 Specular 或 Clear Coat。

- [游戏水体 Shader：从经典结构到完整场景效果](./Unity/Game-Water-Shader.md)  
  这篇是我开始认真拆游戏里的水体效果时整理出来的。最开始会觉得“游戏里的水应该都有一套经典 Shader，换换参数就差不多了”，继续往下拆以后才发现这句话只对了一半。最后理清的是：水体确实反复使用 Wave、Depth、Normal、Fresnel、Reflection、Refraction、Foam、Ripple 这些经典模块，但真正决定最终效果的并不只是 Shader 本身，还包括水底、岸边地形、环境反射、灯光、Caustics、Bloom 和后处理。也开始能把一个完整水面拆成“大形由 Mesh / Wave 控制、小波纹由 Normal 控制、哪里出现效果由各种 Mask 决定、最后再由场景和渲染系统把它补完整”。

- [三渲二角色建模与 Toon Shader：Geometry、Normal 与光照的分工](./Unity/Geometry-driven-NPR-Toon-Shader.md)  
  这篇是我看一个三渲二角色制作短片时一路记下来的。刚开始最容易把“角色好看”直接归到 Shader 上，尤其看到头发和脸部的二次元明暗时，会下意识觉得一定用了很复杂的角色 Shader。把灰模、发束拓扑和不同灯光状态对着看以后，才慢慢理清这件事：很多二维感其实在建模阶段就已经被做进 Geometry 里了，Normal 再决定光照怎样理解这些表面，Toon Shader 最后只是把连续光照压成干净的二次元色块。也顺便理清了 Vertex Position、Vertex Normal、Normal Map 和 N·L 之间的关系——模型真实形状可以不变，但只要改变 Normal，最终看到的明暗和“形状感”就会跟着变化。

- [实时渲染与渲染管线：从 EEVEE 到 Redshift](./Unity/Real-Time-Rendering-and-Rendering-Pipeline.md)  
  这篇是我在比较 EEVEE、UE 和 Redshift 时整理出来的。一开始不太明白为什么 EEVEE 被叫作光栅化渲染引擎，Redshift 却主要使用路径追踪，也容易把 Shader 和渲染管线理解成前后独立的两步。一路梳理下来，终于分清了：光栅化主要负责确定几何体在屏幕上覆盖哪里，并不代表没有光照计算；路径追踪通过采样光线路径估算光的传播，同样需要 Shader 参与材质计算。Shader 是渲染管线中各个可编程阶段执行的程序，而不是管线之外的一道工序。也进一步理清了实时与离线描述的是时间要求，光栅化与路径追踪描述的才是算法选择。

---

<a id="blender"></a>

## BLENDER

### Toon Shading / NPR

- [三渲二二分阴影与头发高光](./Blender/Blender-Toon-Shading-Notes.md)  
  这篇是我在 Blender 里拆最基础的三渲二节点时整理出来的。最开始最容易混在一起的是“到底是谁在判断亮暗、谁在切二分、为什么明明没有进阴影头发还是会变深”。一路把 Diffuse BSDF、Shader to RGB、ColorRamp、Lit / Shadow Tint 和 Emission 分开以后，终于把这套逻辑理清了：Diffuse BSDF 负责算受光，Shader to RGB 把结果拿出来，ColorRamp 只负责按阈值分区，真正的亮部和暗部颜色则是后面自己设计的；所以亮部完全可以故意压成浅蓝灰，再给高光留空间。也顺便把 Hair Highlight 和物理 Anisotropic 的关系理顺了——二次元发丝高光会借用方向性原理，但最终形状通常会被进一步艺术化。

- [二次元头发：发束、法线、渐变 Base Color 与 Toon Shading](./Blender/Anime-Hair-Geometry-Color-Toon-Shading.md)  
  这篇是我看到一个白紫色头发的 Blender 模型以后，顺着“没有明显描边，为什么发束还是一缕一缕”和“颜色到底来自 Base Color 还是受光 Shader”两个问题整理的。发束感并不是因为拓扑边被画了出来，而是 Mesh 轮廓、法线、贴图和遮挡一起形成的。至于白到蓝紫的过渡，我最初考虑了渐变 Base Color，后来又想到原发色可能偏蓝紫，只是 NPR 把受光面映射成银白；这两种路线都能成立。没有工程文件就不能断言作者用了什么，因此我把 Eevee 的 Toon 节点、Generated Z / UV 渐变和排查思路都留下来了，配上原截图和节点示意图。

- [水面涟漪 Shader：从圆环动画到高度图与法线图](./Blender/Water-Ripple-Shader-Notes.md)  
  这篇是我在研究“水滴落下以后那一圈圈波纹到底怎么做”时整理出来的。刚开始很容易把颜色波纹、Height Map 和 Normal Map 当成差不多的东西，也会下意识觉得看起来有凹凸就说明水面真的变形了。一步步拆开以后才理清：Distance 负责生成圆，Time 让圆环向外扩散，Height 只是记录想象中的高低，而 Normal 才是在告诉光照系统表面朝哪个方向倾斜。也因此终于能分清“只是把波纹画出来”和“让波纹真正影响高光、反射、折射”之间的区别；如果还要改变水面的真实轮廓，则必须继续走到顶点位移或其他几何变形。

---

<a id="ae"></a>

## AE

### Motion / Wallpaper

- [终末地 Perlica 动态壁纸](./AE/Wallpaper-Engine-Production.md)  
  这是我做 Perlica 动态壁纸时留下的一次完整记录。光效从分形杂色开始，一层层叠 VR 色差和径向模糊，再用 Evolution 让它动起来。过程中也把一个之前比较模糊的问题理清了：这种会流动的丁达尔光并不是单靠某一个特效做出来的，而是先做出基础纹理，再通过色差、模糊、光源中心和时间变化把它一步步塑造成动态光束；另外也顺便把画幅、循环和 Wallpaper Engine 输出的问题踩了一遍。

  **Published work:** [Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=3804142795)

---

### Repository structure

```text
MIGUMIN-Lab/
├── README.md
├── assets/
├── Unity/
│   ├── CanvasGroup-Alpha-Rendering.md
│   ├── Endfield-3D-Toon-Rendering-and-Shader.md
│   ├── Reflective-Floor-Shader-Reflection-Roughness-Bump.md
│   ├── Endfield-Weather-Procedural-Mask.md
│   ├── AO-Ambient-Occlusion-Shader.md
│   ├── Game-Character-Models-Highpoly-Animation-Game-ready.md
│   ├── PBR-Roughness-Specular-Metallic.md
│   ├── Game-Water-Shader.md
│   ├── Geometry-driven-NPR-Toon-Shader.md
│   └── Real-Time-Rendering-and-Rendering-Pipeline.md
├── Blender/
│   ├── Blender-Toon-Shading-Notes.md
│   ├── Anime-Hair-Geometry-Color-Toon-Shading.md
│   ├── Water-Ripple-Shader-Notes.md
│   └── images/Anime-Hair-Shader/ (8 images)
└── AE/
    └── Wallpaper-Engine-Production.md
```

New columns are added only when there is real study content to place inside them.
