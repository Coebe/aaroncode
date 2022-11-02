---
title: Unity Note
date: "2022-11-01 17:40:08"
tags:
top_img: https://s2.loli.net/2022/11/01/34Nx9ZQyfaViMCd.jpg
cover: https://s2.loli.net/2022/11/01/34Nx9ZQyfaViMCd.jpg
updated: 
type: 
comments: 
description: 
keywords: 
mathjax: 
katex: 
aside: 
aplayer: 
highlight_ shrink: 
---

## 知识点

### 操作

#### Hierarchy

如果父节点与子节点的**缩放**不一致（非等比缩放）时，子物体旋转会让缩放产生异常变化，因为基于非等比坐标系做出的变化，会导致子物体的位置、朝向计算错误。  
如果对象的各个组件局部坐标系不一致，在执行某些旋转变换的时候会产生意料之外的变化。**要注意统一**  

`Alt`+`Shift`+`A` 激活 gameObject 快捷键

[Unity常用[xxx]用法、特性](https://blog.csdn.net/FifthGently/article/details/78363364)

### 旋转 Rotation

[Unity transform.rotation和四元数的基本理解应用](https://taikr.com/article/3945)

### Material & Shader

#### 3D Text

GUI/Text Shader是一种可以穿透的 shader，如果不想让3D文字穿透就得自己建一个shader来使用  
> 这里**需要注意**的地方就是原始改颜色的位置已经不起作用了，因为已经替换了原始材质，所以需要改变自己新建的材质颜色  

`Shader Code:`  

``` Shader
Shader "Custom/NewSurfaceShader"
{
    // 变量属性
    Properties
    {
        _Color ("Color", Color) = (1,1,1,1)
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        // 只是命名不同，作用其实都相同
        //_MainTex ("Font Texture", 2D) = "white" {}
        //_Color ("Text Color", Color) = (1,1,1,1)
    }
    SubShader
    {
        Tags
        {
            // TODO: understand
            "Queue" = "Geometry"
            //"IgnoreProjector"="True" 
            //"RenderType"="Transparent"
        }
        // 表象理解：控制单面显示，像 Plane 一样
        Lighting Off Cull Off ZWrite On Fog 
        { 
            Mode Off
        }
        // 字面解释：用1减去源 α 值，想要的字体就会显现出来
        Blend SrcAlpha OneMinusSrcAlpha
        Pass 
        {
            Color [_Color]
            SetTexture [_MainTex] 
            {
                combine primary, texture * primary
            }
        }
    }
}
```

然后搭配字体以及其自带的 Texture 来配置 material，其中shader属性选择自己新建的 `Custom/[NewSurfaceShader]`

## 工具

### UI

当画布没有正对着相机时，对应上面的按钮之类的交互控件则不会被触发

### DOTween

**待查证：**  
`Sequence`对象好像只能作为函数作用域的变量，一旦提升到类域就不能用了  
**~结论：~**  
对象变量所处作用域没有关系，只是初始化的时间不对，`Sequence`初始化不能在 `Awake`、`Start`函数里面 ==至于为什么需要再探查一下== ，要在使用前一刻初始化。  

### VR

思考使用射线拖拽物体，因为射线本身只有三种激发状态，并没有持续状态在[Unity使用SteamVR2.0实现基本功能(瞬移,抓取物品,射线点击,UI交互等)](https://blog.csdn.net/Liu_ChangC/article/details/124816737?spm=1001.2101.3001.6650.10&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-10-124816737-blog-124718564.pc_relevant_aa_2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-10-124816737-blog-124718564.pc_relevant_aa_2&utm_relevant_index=11)得到了使用一个`isActive`布尔变量来获得状态属性,但是行不通

参考，了解了“append”脚本 ~通俗说就是在不修改官方（SteamVR_LaserPointer）情况下添加功能~  
[SteamVR 2.x 手柄射线与3D物体交互（9）](https://blog.csdn.net/weixin_38484443/article/details/124718969?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-6-124718969-blog-124718564.pc_relevant_aa_2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-6-124718969-blog-124718564.pc_relevant_aa_2&utm_relevant_index=7)  

## Unity编译原理

[Unity - 深度理解C# 的执行原理及Unity跨平台 - 笔记](https://www.cnblogs.com/Jaysonhome/articles/13218403.html)  

```text
    编译成中间语言                                            运行它的虚拟机
C# ---------------> CIL(Common Intermidiate Language)||MCIL ---------------> CLR(Common Language Runtime) } 统称为 .Net Framework
```

## 卡顿/BUG

---
About Build  

> Internal build system error. Backend exited with code -1073740791.
tundra: error: Couldn't launch process
errno: 2 (No such file or directory) GetLastError: 1455 (0x000005AF):  

**解决：**  

1. 重启Unity  
2. 删除`Library/` 下对应项目名的文件（未尝试）

---
About Package  

> 错误 CS0234 命名空间“UnityEngine.XR”中不存在类型或命名空间名“Management”(是否缺少程序集引用?) Assembly-CSharp D:\Aaron\Proj\Metaverse_Project\MetaverseProject\Assets\HTC.UnityPlugin\VRModule\Modules\SteamVRv2Module.cs 18 活动

**解决：**  
在`Package Manager-Unity Registry`安装 `AR Fundation`

> Cinemachine 相关错误  
在`Package Manager-Unity Registry`安装 `Cinemachine`
---

> 偶尔UnityEditor出现未响应的情况，只能强制结束，重启后发现一直进不去，但后台进程是有Unity.exe的。  
> Internal build system error. Backend exited with code -1073741819.  

**解决方案：**  
删除以下文件夹，重启Unity  
C:\Users\用户名\AppData\Local\Unity  
C:\Users\用户名\AppData\LocalLow\Unity  
~理解:应该是把缓存清理一下就好了~

---

### About XR

> InvalidOperationException: You are trying to read Input using the UnityEngine.Input class, but you have switched active Input handling to Input System package in Player Settings.  

**解决办法：**  
setting->player->Active Input Handling[both]  

> 开启VR  

Project Setting->XR Plug-in Management->勾选OpenXR && [OpenVR Loader]  

OpenVR->Application Type==Scene  
~这里如果是Display就会进入VR的黑色世界~  

### 脚本

**Tip：** 删除不必要的事件函数。如果有空函数建议删除，因为在编译器执行空函数时也会消耗CPU的性能  

> 如果脚本出现错误，Unity 编辑器会因为检查到出错而**无法进入运行模式**，这时可以在项目视图中新建文件夹 WebplayerTemplates，然后将出错的脚本拖入此文件夹下，所有位于该文件夹下的文件都会被识别为一般文件从而**不会被当作脚本编译**，这样就可以运行游戏了。

[Unity常用[xxx]用法、特性](https://blog.csdn.net/FifthGently/article/details/78363364)

- C#脚本代码不执行
  1. 对象没有绑定对应C#脚本，**可能是脚本名称和里面类的名称不一致**，导致的“脚本脱落”
- 射线检测  

```C#
        if (Input.GetMouseButtonDown(0))
        {
            ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            if (Physics.Raycast(ray, out hit))//使用默认射线长度和其他默认参数
            {
                //Debug.DrawLine(transform.position, hitInfo.point, Color.yellow);
                Debug.DrawRay(ray.origin, hit.point, Color.green);
                var other = hit.collider.GetComponent<VideoScreen>();
                if (other)
                {
                    TriggerPlay();
                }

            }
        }
```

### 音效

~~衰减的计算方式~~ ~移到TODO~  

### 文件

刚开始出现了图片比例被扭曲了，**不知道**怎么解决，但是通过将图片直接导入Unity**误打误撞**了解到了Unity对导入图片的格式要求（1:1, 1:2, 2:1）

- 加载文件夹的文件到Unity  
  - `var texture = Resources.Load(texPath) as Texture;`  
  > 有限制，必须在`Resources`文件目录下
  - 使用文件流

```C#
    // 将文件转化为二进制形式重构（自己理解）
    FileStream fileStream = new     FileStream(texPath, FileMode.Open,     FileAccess.Read);
    
    byte[] bytes = new     byte[fileStream.Length];
    // 可以理解成复制吧
    fileStream.Read(bytes, 0,     (int)fileStream.Length);
    // 或许是文件流的正确操作流程?
    fileStream.Close();
    // 文件流释放
    fileStream.Dispose();
    // 设置图片大小
    int width = 400;
    int height = 400;
    // 创建texture2D
    Texture2D texture = new Texture2D(width, height);
    // 加载图片流
    texture.LoadImage(bytes);
    // 将材质的第一个贴图重新赋值
    mat.mainTexture = texture;
```

[unity 动态加载本地图片及排版功能](https://www.dounaite.com/article/628d1d41f8519f4c0cd325e9.html)  

---

<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    /*
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://aaroncode-1.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>