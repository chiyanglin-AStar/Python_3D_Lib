# PyOpenGL_overview

[TOC]

## 請說明這專案,回答的輸出請用繁體中文及Markdown格式

# PyOpenGL 專案概述

PyOpenGL 是一個基於 ctypes 的 Python OpenGL 綁定函式庫，提供標準 OpenGL API 的 Python 介面 pyopengl:1-6 。

## 核心組件

### 主要套件
- **PyOpenGL**: 核心純 Python 套件，包含 OpenGL 綁定和包裝器 pyopengl:1-4 
- **PyOpenGL-accelerate**: Cython 編碼的效能加速器，提供 C 擴展來提升效能 pyopengl:1-4 

### 支援的 OpenGL 變體
專案支援多種 OpenGL 變體：
- 標準 OpenGL (GL)
- OpenGL ES 1.x (GLES1)
- OpenGL ES 2.x (GLES2)

## 安裝與使用

### 標準安裝
```bash
pip install PyOpenGL PyOpenGL_accelerate
```

### 開發環境安裝
```bash
cd pyopengl
pip install -e .
cd accelerate
pip install -e .
```
注意：編譯 PyOpenGL_accelerate 需要完整的 Python 擴展編譯環境 pyopengl:16-17 。

## 配置選項

PyOpenGL 提供多個配置變數來控制行為：

- **ERROR_CHECKING**: 控制錯誤檢查（預設：True） pyopengl:23-36 
- **ERROR_LOGGING**: 啟用錯誤日誌記錄（預設：False） pyopengl:38-50 
- **ERROR_ON_COPY**: 陣列操作時若需複製資料則引發錯誤（預設：False） pyopengl:52-67 
- **CONTEXT_CHECKING**: 每次呼叫前檢查 OpenGL 上下文（預設：False） pyopengl:69-79 

## 陣列處理支援

PyOpenGL 支援多種陣列格式：
- NumPy 陣列 pyopengl:335-354 
- ctypes 指標和參數 pyopengl:308-333 
- Python 緩衝區物件 pyopengl:355-364 
- VBO (頂點緩衝區物件) pyopengl:365-376 

## 擴展支援

專案包含豐富的 OpenGL 擴展支援，例如：
- **KHR.debug**: 提供調試和效能分析功能 pyopengl:7-17 
- **ARB.direct_state_access**: 直接狀態存取，避免綁定操作 pyopengl:9-24 
- **EXT.robustness**: 增強穩健性和安全性 pyopengl:9-21 

## 授權

專案採用 BSD 授權條款 pyopengl:23-24 。

## 測試

執行測試套件需要：
- git
- GLUT (FreeGLUT)
- GLExtrusion 函式庫 (libgle)
- GLU
- tox

```bash
tox
``` pyopengl:46-58 

---

## Notes

此專案是成熟的 Python OpenGL 綁定實作，提供完整的 OpenGL API 支援，包含效能優化選項和廣泛的擴展支援。適合需要 Python 中進行 3D 圖形開發的專案使用。

Wiki pages you might want to explore:
- [CI/CD and Distribution (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#8)
### Citations
**File:** OpenGL/__init__.py (L1-6)
```python
"""ctypes-based OpenGL wrapper for Python

This is the PyOpenGL 3.x tree, it attempts to provide
a largely compatible API for code written with the
PyOpenGL 2.x series using the ctypes foreign function
interface system.
```
**File:** OpenGL/__init__.py (L23-36)
```python
    ERROR_CHECKING -- if set to a False value before
        importing any OpenGL.* libraries will completely
        disable error-checking.  This can dramatically
        improve performance, but makes debugging far
        harder.

        This is intended to be turned off *only* in a
        production environment where you *know* that
        your code is entirely free of situations where you
        use exception-handling to handle error conditions,
        i.e. where you are explicitly checking for errors
        everywhere they can occur in your code.

        Default: True
```
**File:** OpenGL/__init__.py (L38-50)
```python
    ERROR_LOGGING -- If True, then wrap array-handler
        functions with  error-logging operations so that all exceptions
        will be reported to log objects in OpenGL.logs, note that
        this means you will get lots of error logging whenever you
        have code that tests by trying something and catching an
        error, this is intended to be turned on only during
        development so that you can see why something is failing.

        Errors are normally logged to the OpenGL.errors logger.

        Only triggers if ERROR_CHECKING is True

        Default: False
```
**File:** OpenGL/__init__.py (L52-67)
```python
    ERROR_ON_COPY -- if set to a True value before
        importing the numpy/lists support modules, will
        cause array operations to raise
        OpenGL.error.CopyError if the operation
        would cause a data-copy in order to make the
        passed data-type match the target data-type.

        This effectively disables all list/tuple array
        support, as they are inherently copy-based.

        This feature allows for optimisation of your
        application.  It should only be enabled during
        testing stages to prevent raising errors on
        recoverable conditions at run-time.

        Default: False
```
**File:** OpenGL/__init__.py (L69-79)
```python
    CONTEXT_CHECKING -- if set to True, PyOpenGL will wrap
        *every* GL and GLU call with a check to see if there
        is a valid context.  If there is no valid context
        then will throw OpenGL.errors.NoContext.  This is an
        *extremely* slow check and is not enabled by default,
        intended to be enabled in order to track down (wrong)
        code that uses GL/GLU entry points before the context
        has been initialized (something later Linux GLs are
        very picky about).

        Default: False
```
**File:** OpenGL/__init__.py (L308-333)
```python
FormatHandler(
    "ctypesparameter",
    "OpenGL.arrays.ctypesparameters.CtypesParameterHandler",
    [
        ("_ctypes" if sys.version_info[:2] >= (3,12) else _bi) + ".CArgObject",
        "ctypes.c_uint",
        "ctypes.c_int",
        "ctypes.c_float",
        "ctypes.c_double",
        "ctypes.c_ulong",
        "ctypes.c_long",
        "ctypes.c_longlong",
    ],
    isOutput=True,
)
FormatHandler(
    "ctypespointer",
    "OpenGL.arrays.ctypespointers.CtypesPointerHandler",
    [
        "ctypes.c_void_p",
        "_ctypes._Pointer",
        "ctypes.c_char_p",
        "_ctypes.pointer._Pointer",
    ],
    isOutput=False,
)
```
**File:** OpenGL/__init__.py (L335-354)
```python
    "numpy",
    "OpenGL.arrays.numpymodule.NumpyHandler",
    [
        "numpy.ndarray",
        "numpy.core.memmap.memmap",
        "numpy.uint8",
        "numpy.uint16",
        "numpy.uint32",
        "numpy.uint64",
        "numpy.int8",
        "numpy.int16",
        "numpy.int32",
        "numpy.int64",
        "numpy.float16",
        "numpy.float32",
        "numpy.float64",
        "numpy.float128",
    ],
    isOutput=True,
)
```
**File:** OpenGL/__init__.py (L355-364)
```python
FormatHandler(
    "buffer",
    "OpenGL.arrays.buffers.BufferHandler",
    [
        "OpenGL.arrays._buffers.Py_buffer",
        _bi + ".memoryview",
        _bi + ".bytearray",
    ],
    isOutput=True,
)
```
**File:** OpenGL/__init__.py (L365-376)
```python
FormatHandler(
    "vbo",
    "OpenGL.arrays.vbo.VBOHandler",
    ["OpenGL.arrays.vbo.VBO", "OpenGL_accelerate.vbo.VBO"],
    isOutput=False,
)
FormatHandler(
    "vbooffset",
    "OpenGL.arrays.vbo.VBOOffsetHandler",
    ["OpenGL.arrays.vbo.VBOOffset", "OpenGL_accelerate.vbo.VBOOffset"],
    isOutput=False,
)
```
**File:** pyproject.toml (L1-4)
```text
[project]
name="PyOpenGL"
dynamic=["version"]
description = "Standard OpenGL bindings for Python"
```
**File:** pyproject.toml (L23-24)
```text
    "License :: OSI Approved :: BSD License",
    "Programming Language :: Python",
```
**File:** accelerate/pyproject.toml (L1-4)
```text
[project]
name="PyOpenGL-accelerate"
dynamic=["version"]
description = "Cython-coded accelerators for PyOpenGL"
```
**File:** readme.rst (L16-17)
```text
Note that to compile PyOpenGL_accelerate you will need to have 
a functioning Python extension-compiling environment.
```
**File:** readme.rst (L46-58)
```text
You can run the PyOpenGL test suite from a source-code checkout, you will need:

* git (for the checkout)
* GLUT (FreeGLUT)
* GLExtrusion library (libgle)
* GLU (normally available on any OpenGL-capable machine)
* tox (`pip install tox`)

Running the test suite from a top-level checkout looks like::

    $ tox

The result being a lot of tests being run in a matrix of environments.
```
**File:** OpenGL/GL/KHR/debug.py (L7-17)
```python
Overview (from the spec)
	
	This extension allows the GL to notify applications when various events 
	occur that may be useful during application development, debugging and 
	profiling.
	
	These events are represented in the form of enumerable messages with a 
	human-readable string representation. Examples of debug events include 
	incorrect use of the GL, warnings of undefined behavior, and performance 
	warnings.
	
```
**File:** OpenGL/GL/ARB/direct_state_access.py (L9-24)
```python
	In unextended OpenGL, most mutation of state contained in objects is through
	an indirection known as a binding. Objects are attached to a context (either
	directly or indirectly via a container) and then commands to modify or
	query their state are issued on that context, indirecting through its
	attachments and into the underlying object. This is known as `bind-to-edit'.
	
	This extension derives from the GL_EXT_direct_state_access extension, which
	added accessors for most state on most objects, allowing it to be queried
	and modified without the object needing to be bound to a context. In cases
	where a single property of an object is to be modified, directly accessing
	its state can be more efficient than binding the object to the context and
	then indirecting through it. Further, directly accessing the state of
	objects through their names rather than by bind-to-edit does not disturb
	the bindings of the current context, which is useful for tools, middleware
	and other applications that are unaware of the outer state but it can also
	avoid cases of redundant state changes.
```
**File:** OpenGL/GLES1/EXT/robustness.py (L9-21)
```python
	Several recent trends in how OpenGL integrates into modern computer
	systems have created new requirements for robustness and security
	for OpenGL rendering contexts.
	
	Additionally GPU architectures now support hardware fault detection;
	for example, video memory supporting ECC (error correcting codes)
	and error detection.  OpenGL contexts should be capable of recovering
	from hardware faults such as uncorrectable memory errors.  Along with
	recovery from such hardware faults, the recovery mechanism can
	also allow recovery from video memory access exceptions and system
	software failures.  System software failures can be due to device
	changes or driver failures.
	
```
## 請說明這專案的程式架構與邏輯, 回答的輸出請用繁體中文及Markdown格式

Wiki pages you might want to explore:
- [Overview (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#1)

## 如何列出支援的GPU 型號 ,本地 GPU 能力, 內存及功耗,頻寬, 並給出如何監控的範例, 回答的輸出請用繁體中文及Markdown格式

# GPU 資訊查詢與監控

PyOpenGL 提供了多種方式來查詢 GPU 資訊和監控性能。以下是主要方法和範例：

## 基本資訊查詢

### 1. 使用 EGL 枚舉設備

```python
from OpenGL.EGL import *
from OpenGL.EGL.EXT.device_enumeration import eglQueryDevicesEXT

def enumerate_gpu_devices():
    devices = (EGLDeviceEXT * 10)()
    count = EGLint()
    
    if eglQueryDevicesEXT(10, devices, count):
        print(f"找到 {count.value} 個設備")
        for i, device in enumerate(devices[:count.value]):
            display = eglGetDisplay(device)
            if eglInitialize(display, EGLint(), EGLint()):
                vendor = eglQueryString(display, EGL_VENDOR)
                print(f"設備 #{i}: {vendor}")
``` pyopengl:11-33 

### 2. 查詢基本 GPU 資訊

```python
from OpenGL.GL import *

def get_basic_gpu_info():
    # GPU 廠商
    vendor = glGetString(GL_VENDOR).decode('utf-8')
    # GPU 型號/渲染器
    renderer = glGetString(GL_RENDERER).decode('utf-8')
    # OpenGL 版本
    version = glGetString(GL_VERSION).decode('utf-8')
    
    print(f"廠商: {vendor}")
    print(f"型號: {renderer}")
    print(f"版本: {version}")
```

## GPU 內存資訊

### 查詢 NVIDIA GPU 內存

```python
from OpenGL.GL import *

def get_nvidia_gpu_memory():
    # 檢查是否支援 NVX GPU 内存擴展
    try:
        # 當前可用視訊内存
        current_available = glGetIntegerv(0x9049)  # GL_GPU_MEMORY_INFO_CURRENT_AVAILABLE_VIDMEM_NVX
        # 專用視訊内存
        dedicated = glGetIntegerv(0x9047)  # GL_GPU_MEMORY_INFO_DEDICATED_VIDMEM_NVX
        # 總可用内存
        total_available = glGetIntegerv(0x9048)  # GL_GPU_MEMORY_INFO_TOTAL_AVAILABLE_MEMORY_NVX
        
        print(f"當前可用内存: {current_available} KB")
        print(f"專用視訊内存: {dedicated} KB")
        print(f"總可用内存: {total_available} KB")
    except:
        print("不支援 NVX GPU 内存查詢")
``` pyopengl:574-578 

## 性能監控

### AMD 性能監控擴展

```python
from OpenGL.GL.AMD.performance_monitor import *

def monitor_amd_performance():
    if not glInitPerformanceMonitorAMD():
        print("不支援 AMD 性能監控")
        return
    
    # 獲取性能監控組
    groups = GLint()
    num_groups = GLint()
    glGetPerfMonitorGroupsAMD(groups, 1, num_groups)
    
    print(f"找到 {num_groups.value} 個性能監控組")
    
    # 查詢每個組的詳細資訊
    for i in range(num_groups.value):
        group_string = glGetPerfMonitorGroupStringAMD(groups[i], 256, GLint())
        print(f"組 {i}: {group_string}")
``` pyopengl:27-43 

## 完整監控範例

```python
import logging
from OpenGL.EGL import *
from OpenGL.EGL.EXT.device_enumeration import eglQueryDevicesEXT
from OpenGL.GL import *

def comprehensive_gpu_monitoring():
    logging.basicConfig(level=logging.INFO)
    
    # 1. 枚舉所有 GPU 設備
    devices = (EGLDeviceEXT * 10)()
    count = EGLint()
    
    if not eglQueryDevicesEXT(10, devices, count):
        print("無法枚舉 GPU 設備")
        return
    
    for device_idx, device in enumerate(devices[:count.value]):
        print(f"\n=== GPU 設備 #{device_idx} ===")
        
        display = eglGetDisplay(device)
        try:
            if not eglInitialize(display, EGLint(), EGLint()):
                continue
                
            # 2. 基本資訊
            vendor = eglQueryString(display, EGL_VENDOR)
            print(f"廠商: {vendor}")
            
            # 3. 創建上下文以查詢更多資訊
            # 這裡需要實際的窗口系統設置，簡化示例
            
        except Exception as e:
            print(f"查詢設備 {device_idx} 時出錯: {e}")

if __name__ == "__main__":
    comprehensive_gpu_monitoring()
``` pyopengl:7-29 

## 注意事項

1. **權限要求**: 某些 GPU 資訊可能需要管理員權限
2. **平台差異**: 不同 GPU 廠商 (NVIDIA/AMD/Intel) 支援的擴展不同
3. **上下文依賴**: 大部分 GL 查詢需要有效的 OpenGL 上下文
4. **擴展檢查**: 使用前應檢查相關擴展是否可用

## Notes

PyOpenGL 本身是圖形 API 綁定庫，不是專門的 GPU 監控工具。上述方法主要依賴 OpenGL/EGL 擴展來獲取 GPU 資訊。對於更詳細的功耗、頻寬等硬體級資訊，建議使用專業的 GPU 監控工具如 NVIDIA-SMI、AMD ROCm 或 Intel GPU Tools。

Wiki pages you might want to explore:
- [Error Checking and Context Management (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#2.4)
- [OpenGL API Bindings (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#4)
### Citations
**File:** tests/check_egl_device_enumeration.py (L11-33)
```python
def main():
    devices = (EGLDeviceEXT * 10)()
    count = EGLint()
    major, minor = EGLint(), EGLint()
    if not eglQueryDevicesEXT:
        raise RuntimeError("No egl query devices extension available")
    if eglQueryDevicesEXT(10, devices, count):
        log.info("%s devices enumerated", count)
        for i, device in enumerate(devices[: count.value]):
            log.info("Describing device #%d: %s", i, device)
            display = eglGetDisplay(device)
            try:
                if not eglInitialize(display, major, minor):
                    log.info("Could not initialise, skipping")
                    continue
            except EGLError as err:
                log.warning("Unable to initialise EGL for display %d: %s", i, err)
            log.info("Display #%d, Version %s.%s", i, major.value, minor.value)
            for key in [
                EGL_VENDOR,
            ]:
                log.info(" Vendor: %s", eglQueryString(display, key))
            log.info("Finished device #%d", i)
```
**File:** OpenGL/raw/GL/_glgets.py (L574-578)
```python
_m[0x9049] = (1,) # GL_GPU_MEMORY_INFO_CURRENT_AVAILABLE_VIDMEM_NVX
_m[0x9047] = (1,) # GL_GPU_MEMORY_INFO_DEDICATED_VIDMEM_NVX
_m[0x904B] = (1,) # GL_GPU_MEMORY_INFO_EVICTED_MEMORY_NVX
_m[0x904A] = (1,) # GL_GPU_MEMORY_INFO_EVICTION_COUNT_NVX
_m[0x9048] = (1,) # GL_GPU_MEMORY_INFO_TOTAL_AVAILABLE_MEMORY_NVX
```
**File:** OpenGL/GL/AMD/performance_monitor.py (L27-43)
```python
def glInitPerformanceMonitorAMD():
    '''Return boolean indicating whether this extension is available'''
    from OpenGL import extensions
    return extensions.hasGLExtension( _EXTENSION_NAME )

glGetPerfMonitorGroupsAMD=wrapper.wrapper(glGetPerfMonitorGroupsAMD).setOutput(
    'groups',size=lambda x:(x,),pnameArg='groupsSize',orPassIn=True
).setOutput(
    'numGroups',size=(1,),orPassIn=True
)
glGetPerfMonitorCountersAMD=wrapper.wrapper(glGetPerfMonitorCountersAMD).setOutput(
    'counters',size=lambda x:(x,),pnameArg='counterSize',orPassIn=True
).setOutput(
    'maxActiveCounters',size=(1,),orPassIn=True
).setOutput(
    'numCounters',size=(1,),orPassIn=True
)
```
**File:** tests/egl_ext_enumerate.py (L7-29)
```python
def main():
    with egl_context(output=None, pbuffer=True) as context:
        display, context, surface = context
        print("Vendor: %s" % (EGL.eglQueryString(display, EGL.EGL_VENDOR)))
        print("Version: %s" % (EGL.eglQueryString(display, EGL.EGL_VERSION)))
        print("Extensions: %s" % (EGL.eglQueryString(display, EGL.EGL_EXTENSIONS),))
        print(
            "Client Extensions: %s"
            % (EGL.eglQueryString(display, EGL.EGL_CLIENT_APIS),)
        )
        if device_enumeration.eglQueryDevicesEXT:
            devices = (device_query.EGLDeviceEXT * 5)()
            count = GLint()
            device_enumeration.eglQueryDevicesEXT(
                5,
                devices,
                count,
            )
            for device in devices[: count.value]:
                print(device)
        else:
            print('No device_query extension available')
        print('OK')
```
## 請說明如何使用這專案 及安裝後的使用步驟 本專案有不同的典型使用情境的範例. 回答的輸出請用繁體中文及Markdown格式

# PyOpenGL 使用指南

## 安裝步驟

### 標準安裝
```bash
pip install PyOpenGL PyOpenGL_accelerate
```

### 開發環境安裝
```bash
cd pyopengl
pip install -e .
cd accelerate
pip install -e .
```
注意：編譯 PyOpenGL_accelerate 需要完整的 Python 擴展編譯環境 pyopengl:16-17 。

---

## 基本使用步驟

### 1. 初始化 OpenGL 上下文
```python
import pygame
from pygame.locals import *
from OpenGL.GL import *

# 初始化 pygame 和 OpenGL
pygame.init()
pygame.display.set_mode((800, 600), OPENGL | DOUBLEBUF)
```

### 2. 基本 OpenGL 設定
```python
# 設定清除顏色
glClearColor(0.0, 0.0, 0.0, 1.0)
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
```

---

## 典型使用情境範例

### 1. 基本圖形繪製
```python
from OpenGL.GL import *
from OpenGL.GLU import *

def draw_triangle():
    glBegin(GL_TRIANGLES)
    glVertex3f(0.0, 1.0, 0.0)
    glVertex3f(-1.0, -1.0, 0.0)
    glVertex3f(1.0, -1.0, 0.0)
    glEnd()
```

### 2. 使用 VBO (Vertex Buffer Object)
```python
from numpy import array
from OpenGL.arrays.vbo import VBO

# 創建 VBO
vertices = array([
    (0, 1, 0),
    (1, -1, 0),
    (-1, -1, 0),
], dtype='f')

vbo = VBO(vertices)

# 使用 VBO
with vbo:
    glVertexPointer(3, GL_FLOAT, 0, vbo)
    glEnableClientState(GL_VERTEX_ARRAY)
    glDrawArrays(GL_TRIANGLES, 0, 3)
``` pyopengl:1-24 

### 3. 著色器程式設計
```python
from OpenGL.GL import shaders

# 頂點著色器
vertex_shader = """
#version 330
attribute vec3 position;
void main() {
    gl_Position = vec4(position, 1.0);
}
"""

# 片段著色器
fragment_shader = """
#version 330
void main() {
    gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
}
"""

# 編譯著色器程式
program = shaders.compileProgram(
    shaders.compileShader(vertex_shader, GL_VERTEX_SHADER),
    shaders.compileShader(fragment_shader, GL_FRAGMENT_SHADER)
)
glUseProgram(program)
``` pyopengl:17-33 

### 4. EGL 設備枚舉與查詢
```python
from OpenGL.EGL import *
from OpenGL.EGL.EXT.device_enumeration import eglQueryDevicesEXT

def enumerate_gpu_devices():
    devices = (EGLDeviceEXT * 10)()
    count = EGLint()
    
    if eglQueryDevicesEXT(10, devices, count):
        for i, device in enumerate(devices[:count.value]):
            display = eglGetDisplay(device)
            if eglInitialize(display, EGLint(), EGLint()):
                vendor = eglQueryString(display, EGL_VENDOR)
                print(f"設備 #{i}: {vendor}")
``` pyopengl:11-33 

### 5. 幀緩衝區物件 (FBO) 使用
```python
from OpenGL.GL.EXT.framebuffer_object import *

# 創建紋理
tex = glGenTextures(1)
glBindTexture(GL_TEXTURE_2D, tex)
glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA8, 512, 512, 0, GL_RGBA, GL_UNSIGNED_BYTE, None)

# 創建 FBO
fbo = glGenFramebuffersEXT(1)
glBindFramebufferEXT(GL_FRAMEBUFFER_EXT, fbo)
glFramebufferTexture2DEXT(GL_FRAMEBUFFER_EXT, GL_COLOR_ATTACHMENT0_EXT, GL_TEXTURE_2D, tex, 0)
``` pyopengl:22-39 

### 6. 變換回饋 (Transform Feedback)
```python
# 設定變換回饋
buff = ctypes.c_char_p(b"outValue")
c_text = ctypes.cast(ctypes.pointer(buff), ctypes.POINTER(ctypes.POINTER(GLchar)))
glTransformFeedbackVaryings(program, 1, c_text, GL_INTERLEAVED_ATTRIBS)

# 重新連結程式
glLinkProgram(program)

# 執行變換回饋
glBeginTransformFeedback(GL_POINTS)
glDrawArrays(GL_POINTS, 0, len(data))
glEndTransformFeedback()
``` pyopengl:24-57 

### 7. 幾何著色器使用
```python
geometry_shader = """
#version 150 core
layout(points) in;
layout(triangle_strip, max_vertices = 3) out;

in float[] geoValue;
out float outValue;

void main() {
    for (int i = 0; i < 3; i++) {
        outValue = geoValue[0] + i;
        EmitVertex();
    }
    EndPrimitive();
}
"""
``` pyopengl:18-33 

---

## 測試與驗證

### 執行測試套件
```bash
# 需要安裝依賴
pip install tox

# 執行測試
tox
``` pyopengl:46-58 

### 基本功能測試
```python
from OpenGL.GL import *

# 測試基本常數
assert glGetString(GL_EXTENSIONS)

# 測試顏色設定
glColor4f(0, 1, 1, 1.0)

# 測試緩衝區操作
if glGenBuffers:
    buffer = glGenBuffers(1)
    glBindBuffer(GL_ARRAY_BUFFER, buffer)
``` pyopengl:120-143 

---

## Notes

- PyOpenGL 支援多種 OpenGL 變體：標準 OpenGL、OpenGL ES 1.x、OpenGL ES 2.x
- 使用 PyOpenGL_accelerate 可以顯著提升效能
- 不同平台可能需要特定的設定和依賴
- 建議在開發時啟用錯誤檢查，生產環境中可關閉以提升效能

Wiki pages you might want to explore:
- [Overview (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#1)
- [CI/CD and Distribution (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#8)

Wiki pages you might want to explore:
- [CI/CD and Distribution (mcfletch/pyopengl)](/wiki/mcfletch/pyopengl#8)
### Citations
**File:** OpenGL/arrays/vbo.py (L1-24)
```python
"""VertexBufferObject helper class

Basic usage:

    my_data = numpy.array( data, 'f')
    my_vbo = vbo.VBO( my_data )
    ...
    my_vbo.bind()
    try:
        ...
        glVertexPointer( my_vbo, ... )
        ...
        glNormalPointer( my_vbo + 12, ... )
    finally:
        my_vbo.unbind()
    
    or 
    
    with my_vbo:
        ...
        glVertexPointer( my_vbo, ... )
        ...
        glNormalPointer( my_vbo + 12, ... )        

```
**File:** tests/check_egl_es2.py (L17-33)
```python
    shader = shaders.compileProgram(
        shaders.compileShader(
            '''#version 130
    attribute vec3 position;
    void main() {
        gl_Position = vec4( position, 0 );
    }''',
            GL_VERTEX_SHADER,
        ),
        shaders.compileShader(
            '''#version 130
    void main() {
        gl_FragColor = vec4( 0,1,0,.5 );
    }''',
            GL_FRAGMENT_SHADER,
        ),
    )
```
**File:** tests/test_sf2946226.py (L22-39)
```python
    # setup a texture
    tex = glGenTextures(1)
    glBindTexture(GL_TEXTURE_2D, tex)
    glTexImage2D(
        GL_TEXTURE_2D, 0, GL_RGBA8, 512, 512, 0, GL_RGBA, GL_UNSIGNED_BYTE, None
    )
    glBindTexture(GL_TEXTURE_2D, 0)

    # setup teh fbo
    fbo = glGenFramebuffersEXT(1)
    glBindFramebufferEXT(GL_FRAMEBUFFER_EXT, fbo)
    glBindTexture(GL_TEXTURE_2D, tex)

    # this call produces an error!

    glFramebufferTexture2DEXT(
        GL_FRAMEBUFFER_EXT, GL_COLOR_ATTACHMENT0_EXT, GL_TEXTURE_2D, tex, 0
    )
```
**File:** tests/feedbackvarying.py (L24-57)
```python
    buff = ctypes.c_char_p(b"outValue")
    c_text = ctypes.cast(ctypes.pointer(buff), ctypes.POINTER(ctypes.POINTER(GLchar)))
    # modifies the state in the linking of the program
    glTransformFeedbackVaryings(program, 1, c_text, GL_INTERLEAVED_ATTRIBS)

    # so have to re-link
    glLinkProgram(program)
    glUseProgram(program)

    vao = glGenVertexArrays(1)
    glBindVertexArray(vao)

    data = (GLfloat * 5)(1.0, 2.0, 3.0, 4.0, 5.0)

    vbo = glGenBuffers(1)
    glBindBuffer(GL_ARRAY_BUFFER, vbo)
    glBufferData(GL_ARRAY_BUFFER, ctypes.sizeof(data), data, GL_STATIC_DRAW)

    inputAttrib = glGetAttribLocation(program, "inValue")
    glEnableVertexAttribArray(inputAttrib)
    # Note the need to cast 0 to a GLvoidp here!
    glVertexAttribPointer(inputAttrib, 1, GL_FLOAT, GL_FALSE, 0, GLvoidp(0))

    tbo = glGenBuffers(1)
    glBindBuffer(GL_ARRAY_BUFFER, tbo)
    glBufferData(GL_ARRAY_BUFFER, ctypes.sizeof(data), None, GL_STATIC_READ)

    glEnable(GL_RASTERIZER_DISCARD)

    glBindBufferBase(GL_TRANSFORM_FEEDBACK_BUFFER, 0, tbo)

    glBeginTransformFeedback(GL_POINTS)
    glDrawArrays(GL_POINTS, 0, len(data))
    glEndTransformFeedback()
```
**File:** tests/geomshader.py (L18-33)
```python
geometry_shader = """#version 150 core
    layout(points) in;
    layout(triangle_strip, max_vertices = 3) out;

    in float[] geoValue;
    out float outValue;

    void main() {
        for (int i = 0; i < 3; i++) {
            outValue = geoValue[0] + i;
            EmitVertex();
        }

        EndPrimitive();
    }
"""
```
**File:** readme.rst (L46-58)
```text
You can run the PyOpenGL test suite from a source-code checkout, you will need:

* git (for the checkout)
* GLUT (FreeGLUT)
* GLExtrusion library (libgle)
* GLU (normally available on any OpenGL-capable machine)
* tox (`pip install tox`)

Running the test suite from a top-level checkout looks like::

    $ tox

The result being a lot of tests being run in a matrix of environments.
```
**File:** tests/test_core.py (L120-143)
```python
    def test_getstring(self):
        assert glGetString(GL_EXTENSIONS)

    def test_constantPickle(self):
        """Test that our constants can be pickled/unpickled properly"""
        for p in pickle, cPickle:
            v = p.loads(p.dumps(GL_VERTEX_ARRAY))
            assert v == GL_VERTEX_ARRAY, (v, GL_VERTEX_ARRAY)
            assert v.name == GL_VERTEX_ARRAY.name, v.name

    def test_nonFloatColor(self):
        """Test that we handle non-floating-point colour inputs"""
        for notFloat, shouldWork in ((0, True), (object(), False), (object, False)):
            try:
                glColor4f(0, 1, 1, notFloat)
            except Exception:
                if shouldWork:
                    raise
            else:
                if not shouldWork:
                    raise RuntimeError(
                        """Expected failure for non-float value %s, succeeded"""
                        % (notFloat,)
                    )
```
