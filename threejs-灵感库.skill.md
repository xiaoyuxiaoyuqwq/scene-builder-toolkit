# Three.js 场景灵感库 · 优秀案例集

## 一、必看参考站点

### Awwwards / FWA 获奖作品

| 站点 | 风格 | 核心技法 |
|------|------|----------|
| **Oryzo** (oryzo.com) | 极简产品展示 | 惯性 3D 渲染 + Z 轴景深滚动，**一个物体做到极致** |
| **IVRESS** (ivress.com) | 暗色调叙事 | WebGPU + TSL 双后端着色器，7 场景连续滚动故事 |
| **Hubtown** | B2B 品牌站 | 3D 单体 + 鼠标揭示交互（cursor 扫过显露细节） |
| **Sleep Well Creative** | 手绘编辑风 | 滚动驱动插画 3D 场景，叙事与视觉同步 |
| **Explore Primland** | 自然风光 | 航拍式 3D 景观飞越，雾效 + 地形 |
| **Cartier Watches** | 奢侈品 | 每只表一个独立 3D "房间"，滚动在房间间切换 |
| **Shopify Editions** | 产品发布 | 滚动触发分节 reveal，打字散开 + 重构 |
| **Lacoste Ace Breaker** | 品牌游戏 | 浏览器内 3D 微游戏作为 campaign |
| **ZERO** (zero.university) | 叙事交互 | 故事线 + 可交互城市地图，1GB 资源压缩至 10MB |
| **Shader.se** | 80s 科技 | WebGPU 无缝场景过渡，frustum-matched 平面转场 |

### 值得研究的个人站

| 站点 | 风格 | 核心技法 |
|------|------|----------|
| **Joseph Santamaria** | 建筑空间 | 滚动驱动相机 + 空间排版 + 场景连续运镜 |
| **Jordan Breton** | 浮空岛屿 | 草地/瀑布/火/风/树/蝴蝶，细节丰富的小世界 |
| **Thibault Introvigne** | 科幻探索 | WASD 控制宇航员 + 收集品揭示履历 |
| **WoraWork** | 塞尔达风 | 角色控制 + 温馨小场景 + 交互物 |
| **Samsy** | 赛博朋克 | WebGPU 120+fps 霓虹城市，第一人称 |
| **Corentin Bernadou** | 瑞士风格 | WebGL 几何 + 极简橙白黑配色 |
| **Mousham Singh** | 3D 简历 | 滚动触发 + 空间转换 |
| **Giulio Collesei** | 赛博朋克叙事 | 4 场景 + Dolly Zoom 转场 + 雨中泪致敬 |

### 中国古风 / 文化类

| 项目 | 内容 | 地址 |
|------|------|------|
| **tang-changan** | 大唐长安城微缩沙盘，1200+ 网格，217 NPC | github: andyhuo520/tang-changan |
| **Lonely City Dream** | 古诗词意境 3D 叙事 | github: zym9863/Lonely-City-Dream |
| **谪仙风流** | 李白主题 3D 探索 | github: zym9863/Chronicles-of-the-Banished-Immortal-s-Elegance |
| **筑韵千年** | 古建筑六屏可视化 + 太和殿 3D | github: 3502687683-web/zhuyun-heritage |
| **china-heritage-3d** | 7 座古建筑交互展示 | github: xyiqq/china-heritage-3d |
| **MetaPalace** | 数字故宫文物 | github: Selen-Suyue/MetaPalace |
| **Tekton** | 南禅寺大殿程序化重建 | github: tangxiya-star/Tekton |
| **古园奇梦** | 宋代园林 + 榫卯互动 | TRAE 社区案例 |

---

## 二、风格分类与参考配色

### 暖金暮色（光遇/艾尔登法环风）
`#0a0018` `#2a0a30` `#dd6644` `#ffaa66` `#ffcc88` `#ffe0b0`
- 深紫向暖橙渐变天空
- 暖色 DirectionalLight + 冷色 rim light
- 对象 emissive 微光 + Bloom

### 深蓝灵境（Ori 风）
`#080418` `#2233aa` `#6644ff` `#ffaa44` `#88ddff`
- 深蓝紫背景 + 暖金主光
- 大量半透发光粒子 + 浮动轨迹
- 强 Bloom (0.7+)

### 赛博霓虹（赛博朋克风）
`#0a0a1a` `#ff00ff` `#00ffff` `#ff4400`
- 暗底色 + 高饱和霓虹光
- 反射面 + 发光边缘
- Bloom 加 chromatic aberration

### 极简白（Swiss / Apple 风）
`#ffffff` `#f5f2ee` `#c4975a` `#1a1a1a`
- 大面积留白
- 单个 3D 物体作为视觉重心
- 极淡阴影 + 细腻材质

### 玻璃质感（现代高端）
`MeshTransmissionMaterial` 参数：
- transmission: 0.95
- chromaticAberration: 0.04
- ior: 1.5
- roughness: 0.1
- metalness: 0

---

## 三、核心技法速查

### 场景类型速查

| 类型 | 适用场景 | 实现方式 |
|------|----------|----------|
| 俯瞰沙盘 | 城市/地图 | OrthographicCamera + 大量小网格 |
| 第一人称 | 探索 | PointerLockControls + WASD |
| 第三人称跟随 | RPG | lerp 插值相机到角色后方 |
| 滚动驱动 | 叙事 | GSAP ScrollTrigger + 相机沿路径 |
| 轨道环绕 | 展示 | OrbitControls + autoRotate |
| 浮空岛 | 小世界 | 单场景 + 可交互元素 |

### 后期处理组合

```
Bloom 强度指南：
  0.15-0.25   — 自然微光（古风/写实）
  0.3-0.5     — 温暖氛围（光遇/暮色）
  0.6-0.9     — 梦幻/灵境（Ori/赛博）
  1.0+        — 超现实（仅特定元素）

常用 Pass 组合：
  基础三件套：RenderPass + UnrealBloomPass + 自定义 Pass
  高配：+ OutlinePass(悬停高亮) + SMAAPass(抗锯齿)
```

### 性能基线

```
1200+ 网格 + 200+ NPC → 移动端 30fps
做法：全程序化几何体 + InstancedMesh + 屏幕空间查询
关键：不引入外部模型文件，不每帧全量距离计算
```

### 相机转场技巧

```
三种模式平滑过渡：
  1. 每帧 lerp 插值 position + target
  2. GSAP 动画 timeline
  3. 自定义 CameraPath 插件

Dolly Zoom (Vertigo Effect)：
  相机向前移动 + FOV 同步增宽
  背景"呼吸"而前景不动
```

---

## 四、搜索关键词

### 灵感搜索（中文）
```
Three.js 案例 精选
Three.js 古风 场景 3D 可视化
Three.js 获奖网站 awwwards
Three.js 建筑 漫游 交互
Three.js 粒子 特效 梦幻
Three.js 地圖 数据 可视化 大屏
Three.js WebGPU 优秀案例
three.js 滚动 叙事 交互动画
```

### 英文搜索
```
best three.js websites showcase 2026
three.js awwwards site of the day
three.js portfolio inspirational
three.js creative coding environment
three.js chinese architecture procedural
three.js scroll driven narrative GSAP
three.js WebGPU production example
three.js React Three Fiber production site
three.js low poly world procedural generation
three.js particle system creative
```

### GitHub 搜索
```
three.js chinese architecture scene
three.js ancient city procedural
three.js portfolio R3F
three.js creative coding
three.js dataviz map
```

### 学习资源
```
threejs.org/examples/ — 官方示例（最权威）
threejs-journey.com — Bruno Simon 付费课程
codrops.net — 技术教程 + 案例分析
tympanus.net/codrops — 同上
awwwards.com websites three-js — 获奖作品
threejsresources.com/showcase — 案例展示
```

---

## 五、常见陷阱

1. **材质太多** → 用 MAT 对象统一管理，不超过 15 种
2. **场景太杂** → 聚焦一个视觉中心（树/建筑/雕塑），其他做陪衬
3. **Bloom 过度** → 先设 0.3，逐步增加，不要超过 1.0
4. **比例失调** → 人物/建筑/树的比例保持 1:3:2
5. **阴影丢失** → 记得设置 `renderer.shadowMap` + `light.castShadow` + `mesh.castShadow`/`receiveShadow`
6. **颜色太脏** → 用 ACESFilmicToneMapping，exposure 0.8-1.2
7. **屋顶不对** → 中式屋顶 = ConeGeometry 多层堆叠，不是 ExtrudeGeometry
8. **忘记雾效** → FogExp2 可以让远景自然隐去
9. **粒子太多** → 超过 2000 个考虑 InstancedMesh
