# Rodan

Rodan is a modular real-time rendering engine built on the [Velos](https://github.com/LipskiDev/Velos) Render Hardware Interface (RHI), focusing on clean separation between GPU abstraction and high-level systems such as scene management, materials, and modern rendering techniques.

---

## Building

### Prerequisites

| Dependency | Link | Notes |
|---|---|---|
| CMake | [cmake.org](https://cmake.org/download/) | Required for assimp |
| Premake5 | [premake.github.io](https://premake.github.io/download) | Must be in PATH |
| Vulkan SDK | [vulkan.lunarg.com](https://vulkan.lunarg.com/sdk/home) | Sets `VULKAN_SDK` automatically |
| Visual Studio 2022 | [visualstudio.microsoft.com](https://visualstudio.microsoft.com/) | C++ desktop workload required |

On Windows, you can install Premake5 and the Vulkan SDK via winget:

```powershell
winget install Premake.Premake.5.Beta
winget install KhronosGroup.VulkanSDK
```

> Restart your terminal after installing so `PATH` and `VULKAN_SDK` are picked up.

### Clone

```bash
git clone --recursive https://github.com/LipskiDev/Rodan
cd Rodan
```

### Generate Project Files

**Windows**
```bash
premake5 vs2022
```

**Linux**
```bash
premake5 gmake
```

### Build

**Visual Studio** — Open `Rodan.sln`, set **Runtime** as the startup project, select **Release | x64**, and build.

**Command line (MSBuild)**
```powershell
msbuild Rodan.sln /p:Configuration=Release /p:Platform=x64 /m
```

**Command line (Make)**
```bash
make config=release_x86_64
```

> The Vulkan SDK only ships release-mode `shaderc_combined.lib`, so **Release** configuration is recommended on Windows. Debug builds may produce linker errors due to runtime library mismatches.

### Run

Launch from the Rodan root directory:

```powershell
./bin/Release-windows-x86_64/Runtime/Runtime
```

---

## Architecture

Rodan follows a layered architecture:

```
┌─────────────────────┐
│   Runtime / App     │
├─────────────────────┤
│ Renderer / Scene /  │
│ Assets / Materials  │
├─────────────────────┤
│ Graphics Abstraction│
├─────────────────────┤
│    Velos (RHI)      │
├─────────────────────┤
│      Vulkan         │
└─────────────────────┘
```

- **Velos** — low-level GPU abstraction (Vulkan backend)
- **Rodan** — high-level rendering engine

Rodan builds on top of Velos primitives and does not expose backend-specific APIs to higher-level systems.

### Velos (RHI)

Included as a submodule under `external/velos/`. Provides:

- Device and swapchain management
- Command lists and submission
- Buffers, images, pipelines
- Synchronization primitives

---

## Features

Rodan provides higher-level rendering systems including:

- Scene representation (meshes, cameras, lights)
- Material and shader systems
- GPU resource management
- Render pipeline orchestration
- Rendering techniques (forward, deferred, clustered, etc.)

### Current Status

Early development.

**Implemented / in progress:**
- Engine structure and module layout
- Integration with Velos RHI
- Basic rendering pipeline bootstrap

**Planned:**
- Mesh and material system
- Texture support
- Depth testing and render targets
- Camera and scene system
- Lighting (forward / clustered)
- Shadow mapping
- Render graph

---

## Goals

- Build a clean and extensible rendering architecture
- Explore modern real-time rendering techniques
- Maintain strict separation between API abstraction and rendering logic
- Serve as a foundation for experimentation (graphics research, engine design)
