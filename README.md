# Unity UI Optimization Tool
This is a compilation of useful tips and tricks we can use in order to optimize the performance of our games' UI.
Here is the list of tips and tricks and here is the list of supported features by the tool:

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
Each time there is a UI input (click, tap, scroll, etc.) Unity's <i>GraphicsRaycaster</i> iterates over all the <i>Raycast Targets</i> in the scene, so the less we have the
more processing we save.
</details>

## 📚 Bibliography
* [Unite Europe 2017 - Squeezing Unity: Tips for raising performance](https://youtu.be/_wxitgdx-UI?t=1426)
* [Unity Game Optimization: Enhance and extend the performance of all aspects of your Unity games](https://www.amazon.com/Unity-Game-Optimization-Enhance-performance/dp/1838556516)
* [Unity Learn - Optimizing Unity UI](https://learn.unity.com/tutorial/optimizing-unity-ui)
