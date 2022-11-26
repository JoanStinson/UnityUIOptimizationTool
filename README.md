# Unity UI Optimization Tool
A Unity Editor tool that automatically optimizes selected UI game objects (including Prefabs) to save you time.

<p align="center">
  <a>
    <img alt="Made With Unity" src="https://img.shields.io/badge/made%20with-Unity-57b9d3.svg?logo=Unity">
  </a>
  <a>
    <img alt="License" src="https://img.shields.io/github/license/JoanStinson/UnityUIOptimizationTool?logo=github">
  </a>
  <a>
    <img alt="Last Commit" src="https://img.shields.io/github/last-commit/JoanStinson/UnityUIOptimizationTool?logo=Mapbox&color=orange">
  </a>
  <a>
    <img alt="Repo Size" src="https://img.shields.io/github/repo-size/JoanStinson/UnityUIOptimizationTool?logo=VirtualBox">
  </a>
  <a>
    <img alt="Downloads" src="https://img.shields.io/github/downloads/JoanStinson/UnityUIOptimizationTool/total?color=brightgreen">
  </a>
  <a>
    <img alt="Last Release" src="https://img.shields.io/github/v/release/JoanStinson/UnityUIOptimizationTool?include_prereleases&logo=Dropbox&color=yellow">
  </a>
</p>

<p align="center">
  <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/preview.gif">
</p>

## 🖥️ How It Works
For starters, import the package located in the [Releases](https://github.com/JoanStinson/UnityUIOptimizationTool/releases) section into your project.

Now then, inside the Unity Editor, select any number of <i>game objects</i> anywhere: in the scene's <i>Hierarchy</i>, in the <i>Project</i> window or in <i>Prefab Edit Mode</i>.

Next, go to <i>Tools > JGM > Optimize Selected UI GameObjects</i> and press it.

It will automatically optimize the selected <i>game objects</i> (including <i>Prefabs</i>) with the supported techniques.
<p align="center">
  <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/tool usage.png">
</p>

## 🛠️ Unity UI Optimization Techniques
<details>
   <summary><b>🛠️ Using more Canvases</b></summary>
  
   ### Using more Canvases
   Every time a single UI element inside a Canvas changes (e.g. change 1 Text or Image), the whole Canvas has to generate the meshes and draw them all
over again (very costly).
</details>

<details>
   <summary><b>🛠️ Separating objects between static and dynamic Canvases</b></summary>
  
   ### Separating objects between static and dynamic Canvases
   * <b>Static Canvas</b>: contains UI elements that are <b>never</b> going to <b>change</b>; good examples of these are background images, labels, and so on.
   * <b>Incidental Dynamic Canvas</b>: contains UI elements that only <b>change in response</b> to something, such as a UI button press or hover action.
   * <b>Continuous Dynamic Canvas</b>: contains UI elements that <b>change regularly</b>, such as animated elements.
</details>

<details>
   <summary><b>🛠️ Disabling Raycast Target for non-interactive elements</b></summary>
  
   ### Disabling Raycast Target for non-interactive elements
   For all <b><i>Image</i></b> components that are not part of a <b><i>Button</i></b>, disable the <b><i>Raycast Target</i></b> (basically disable it in all images except for buttons).
   <br><br>
   Each time there is a UI input (click, tap, scroll, etc.) Unity's <i>GraphicsRaycaster</i> iterates over all the <i>Raycast Targets</i> in the scene, so the less we have the more processing we save.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/disable raycast target.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Hiding UI elements by disabling the parent Canvas component</b></summary>
  
   ### Hiding UI elements by disabling the parent Canvas component
   To avoid the <i>Canvas</i> regeneration, it's good habit to split the UI into different <i>Canvases</i>, and instead of disabling a <i>LayoutGroup</i>, disable an entire <i>Canvas</i>.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/hide canvas.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Avoiding Animator components</b></summary>
  
   ### Avoiding Animator components
   Unity's Animator components are meant for 3D avatar animations primarily. Using it for UI elements causes extra processing.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/animator.PNG">
   </p>
   Instead, the best approach is to use a custom tweening tool such as DOTween.<br><br>
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/dotween.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Explicitly defining the event camera for World Space Canvases</b></summary>
  
   ### Explicitly defining the event camera for World Space Canvases
   Always set the Event <i>Camera</i> in a <i>World Space Canvas</i> as if there is no <i>Camera</i> assigned, it will call <i>FindObjectWithTag("Main Camera")</i> on every single frame! ☠️
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/world space canvas.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Don't use alpha to hide UI elements</b></summary>
  
   ### Don't use alpha to hide UI elements
   Even though the <i>Image</i>'s color property is set to <i>alpha</i> 0, it will still cause a <i>draw call</i>.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/alpha.PNG">
   </p>
   Instead, disable the <i>game object</i> itself, or set the <i>alpha</i> of a <i>Canvas Group</i> to 0. This will prevent any <i>draw calls</i> from this object and its childs (0 <i>draw calls</i>).<br><br>
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/splash.PNG">
   </p>
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/canvas group.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Make sure to use a RectMask2D</b></summary>
  
   ### Make sure to use a RectMask2D
   Like this, any element that is not inside the <i>Scroll Rect</i>, will not be drawn saving plenty of <i>draw calls</i>.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/rectmask.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Disable Pixel Perfect for ScrollRects</b></summary>
  
   ### Disable Pixel Perfect for ScrollRects
   <i>Pixel Perfect</i> makes UI elements appear sharper, but since in a <i>Scroll Rect</i> there's going to be movement, we won't notice it and we'll save a lot of processing.
   <br><br>
   The <i>Scroll Rect</i> should be on a separate <i>Canvas</i> with this setting off and other UI elements appearing in the same screen, would be in another <i>Canvas</i> with this setting on.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/pixel perfect.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Manually stop ScrollRect motion</b></summary>
  
   ### Manually stop ScrollRect motion
   We can use <i>ScrollRect.StopMovement()</i> to stop the motion once the <i>ScrollRect.velocity</i> is below a certain threshold to reduce regeneration frequency.
</details>

<details>
   <summary><b>🛠️ Using empty UIText elements for full-screen interaction</b></summary>
  
   ### Using empty UIText elements for full-screen interaction
   For a <i>Button</i> that's going to be interactable full-screen, for the <i>Button's Target Graphic</i>, don't use an <i>Image</i> that fills the whole screen and has a <i>color alpha</i> set to 0 (as transparency breaks batching processes).
   <br><br>
   Instead, for the <i>Button's Target Graphic</i>, use a <i>Text</i> with no <i>Font</i> or <i>Text</i> defined.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/empty ui text for all screen.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Reduce Game Objects inside Prefabs</b></summary>
  
   ### Reduce Game Objects inside Prefabs
   Wherever possible, try to reduce the number of <i>game objects</i> inside of a <i>Prefab</i>, maybe in some occasions it's possible to merge 3 <i>game objects</i> with <i>Images</i> into 1 single <i>game object</i> with 1 <i>Image</i>.
</details>

<details>
   <summary><b>🛠️ Avoid Layout Groups when possible</b></summary>
  
   ### Avoid Layout Groups when possible
   Whenever possible, try to avoid using <i>Layout Groups</i>, specially nested <i>Layout Groups</i>, as it's very costly performance wise.
</details>

<details>
   <summary><b>🛠️ Adjust texture compression formats</b></summary>
  
   ### Adjust texture compression formats
   Always adjust texture compression formats for your UI Sprite assets, to reduce memory footprint. Available compression types can be found [here](https://docs.unity3d.com/Manual/class-TextureImporterOverride.html).
</details>

<details>
   <summary><b>🛠️ Use Sprite Atlases always</b></summary>
  
   ### Use Sprite Atlases always
   Use [Sprite Atlases](https://docs.unity3d.com/Manual/class-SpriteAtlas.html) for grouping single Sprites into one big texture to reduce the number of <i>draw calls</i>.
   <p align="center">
      <img src="https://github.com/JoanStinson/UnityUIOptimizationTool/blob/main/Images/sprite atlas.PNG">
   </p>
</details>

<details>
   <summary><b>🛠️ Take order into account to prevent Batch Breaks</b></summary>
  
   ### Take order into account to prevent Batch Breaks
   Order in UI hierarchies matters. If you have in a hierarchy this order: 
   * SpriteA1
   * SpriteB1
   * SpriteA2
   * SpriteB2
   * SpriteA3
   * SpriteB3 
   
   (meaning 'A' Sprites are from a specific Sprite Atlas and 'B' Sprite are from another one) it will issue 6 <i>draw calls</i> because the batches are breaking as all Sprites from one Atlas are not consecutively in line. To prevent this Batch Break, order them as in: 
   * SpriteA1
   * SpriteA2
   * SpriteA3
   * SpriteB1
   * SpriteB2
   * SpriteB3
   
   As a result, this will only issue 2 <i>draw calls</i>.
</details>

## 🧰 Tool Supported Techniques
✅ <b>Disabling Raycast Target for non-interactive elements</b><br>
✅ <b>Avoiding Animator components</b><br>
✅ <b>Make sure to use a RectMask2D</b><br>
✅ <b>Disable Pixel Perfect for ScrollRects</b>
    
## 📚 Bibliography
* [Unite '17 Seoul - Tips and Tricks for Optimising Unity UI](https://www.youtube.com/watch?v=eH-PdFKgctE)
* [Unite Europe 2017 - Squeezing Unity: Tips for Raising Performance](https://youtu.be/_wxitgdx-UI?t=1426)
* [Unity Game Optimization](https://www.amazon.com/Unity-Game-Optimization-Enhance-performance/dp/1838556516)
* [Optimizing Unity UI](https://learn.unity.com/tutorial/optimizing-unity-ui)
* [Optimization Tips for Unity UI](https://unity.com/how-to/unity-ui-optimization-tips#avoid-expensive-ui-elements)
* [Interactive Guide: Cross-Platform UI](https://assetstore.unity.com/packages/templates/tutorials/interactive-guide-cross-platform-ui-208063#description)
