# jax-ml/jax Overview

[TOC]

## 請說明這專案,回答的輸出請用繁體中文及Markdown格式

# JAX 專案概述

JAX 是一個用於陣列導向數值計算的 Python 函式庫，具有自動微分和即時編譯功能，專為高效能機器學習研究而設計 jax:15-15 。

## 核心特性

### 1. NumPy 相容的 API
JAX 提供與 NumPy 高度相容的介面，透過 `jax.numpy` 模組實現 jax:68-68 。與 NumPy 不同的是，JAX 陣列是不可變的 jax:61-61 。

### 2. 程式轉換功能
- **JIT 編譯**：透過 Open XLA 進行即時編譯，提升執行效能 jax:25-25 
- **自動微分**：支援前向模式和反向模式的自動微分 jax:26-26 
- **向量化**：自動將函式向量化以處理批次輸入 jax:27-27 

### 3. 跨平台支援
JAX 提供統一的介面，可在 CPU、GPU 或 TPU 上執行，支援本地和分散式環境 jax:24-24 。

## 專案架構

### 模組化設計
JAX 採用模組化技術堆疊，核心專注於基礎功能，鼓勵周邊生態系統的發展 jax:16-30 。

### 核心組件
1. **JAX 核心函式庫**：專注於機器學習和數值計算的基礎 jax:12-14 
2. **編譯器和執行時後端**：模組化設計以支援不同的加速器 jax:24-30 
3. **擴展 API**：提供客製化和擴展功能 jax:82-88 

## 開發模式

### 開源協作
JAX 由 JAX 核心團隊領導，採開放式開發，歡迎社群貢獻 jax:5-10 。日常開發在 GitHub 上進行，使用 pull requests、issue 追蹤和討論 jax:42-49 。

### 持續整合系統
JAX 具有完善的 CI 系統，包含：
- 預提交檢查（Presubmits）
- 持續建置（Continuous builds）
- 夜間建置和測試（Nightly builds）
- 發布流程 jax:18-21 

支援的平台包括 Linux x86、Linux aarch64、Windows x86 和 Mac Arm64 jax:26-29 。

## 生態系統

JAX 鼓勵基於其核心函式庫建構特定領域的函式庫和工具 jax:71-75 。許多函式庫已經圍繞 JAX 發展，提供更高階的功能和擴展 jax:73-75 。

## 學習資源

JAX 提供豐富的學習資源：
- **Autodidax 教學**：從零開始理解 JAX 核心系統 jax:44-46 
- **Thinking in JAX**：JAX 快速入門指南 jax:9-9 
- **進階指南**：涵蓋效能分析、外部回呼等主題 jax:61-110 

---

## Notes

JAX 是 Apache 2.0 授權的開源專案，由 Google 和其他機構共同貢獻。專案設計強調可組合性和可擴展性，使其成為現代機器學習研究的重要工具。如需了解更多技術細節，可以參考專案文件中的 Autodidax 教學，該教學詳細解釋了 JAX 的內部實作原理。
### Citations
**File:** docs/notebooks/thinking_in_jax.ipynb (L9-9)
```text
    "# Quickstart: How to think in JAX\n",
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L15-15)
```text
    "**JAX is a library for array-oriented numerical computation (*à la* [NumPy](https://numpy.org/)), with automatic differentiation and JIT compilation to enable high-performance machine learning research**."
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L24-24)
```text
    "* JAX provides a unified NumPy-like interface to computations that run on CPU, GPU, or TPU, in local or distributed settings.\n",
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L25-25)
```text
    "* JAX features built-in Just-In-Time (JIT) compilation via [Open XLA](https://github.com/openxla), an open-source machine learning compiler ecosystem.\n",
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L26-26)
```text
    "* JAX functions support efficient evaluation of gradients via its automatic differentiation transformations.\n",
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L27-27)
```text
    "* JAX functions can be automatically vectorized to efficiently map them over arrays representing batches of inputs."
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L61-61)
```text
    "- Unlike NumPy arrays, JAX arrays are always immutable."
```
**File:** docs/notebooks/thinking_in_jax.ipynb (L68-68)
```text
    "NumPy provides a well-known, powerful API for working with numerical data. For convenience, JAX provides [`jax.numpy`](https://docs.jax.dev/en/latest/jax.numpy.html) which closely mirrors the NumPy API and provides easy entry into JAX. Almost anything that can be done with `numpy` can be done with `jax.numpy`, which is typically imported under the `jnp` alias:"
```
**File:** docs/about.md (L5-10)
```markdown
The JAX project is led by the JAX core team. We develop in the open,
and welcome open-source contributions from across the community. We
frequently see contributions from [Google
DeepMind](https://deepmind.google/), Alphabet more broadly,
[NVIDIA](https://docs.nvidia.com/deeplearning/frameworks/jax-release-notes/overview.html),
and elsewhere.
```
**File:** docs/about.md (L12-14)
```markdown
At the heart of the project is the [JAX
core](https://github.com/jax-ml/jax) library, which focuses on the
fundamentals of machine learning and numerical computing, at scale.
```
**File:** docs/about.md (L16-30)
```markdown
When [developing](#development) the core, we want to maintain agility
and a focused scope, so we lean heavily on a surrounding [modular
technology stack](#components). First, we design the `jax` module
to be
[composable](https://github.com/jax-ml/jax?tab=readme-ov-file#transformations)
and
[extensible](https://docs.jax.dev/en/latest/jax.extend.html), so
that a wide variety of domain-specific libraries can thrive outside of
it in a decentralized manner. Second, we lean heavily on a modular
backend stack (compiler and runtime) to target different
accelerators. Whether you are [writing a new domain-specific library
built with JAX](#upstack), or looking to [support
new hardware](#downstack), you can often
contribute these with *minimal to no modifications* to the JAX core
codebase.
```
**File:** docs/about.md (L42-49)
```markdown
JAX's day-to-day development takes place in the open on GitHub, using
pull requests, the issue tracker, discussions, and [JAX Enhancement
Proposals
(JEPs)](https://docs.jax.dev/en/latest/jep/index.html). Reading
and participating in these is a good way to get involved. We also
maintain [developer
notes](https://docs.jax.dev/en/latest/contributor_guide.html)
that cover JAX's internal design.
```
**File:** docs/about.md (L71-75)
```markdown
While the JAX core library focuses on the fundamentals, we want to
encourage domain-specific libraries and tools to be built on top of
JAX. Indeed, [many
libraries](https://docs.jax.dev/en/latest/#ecosystem) have
emerged around JAX to offer higher-level features and extensions.
```
**File:** docs/about.md (L82-88)
```markdown
handful of more advanced APIs for
[customization](https://docs.jax.dev/en/latest/notebooks/Custom_derivative_rules_for_Python_code.html)
and
[extensibility](https://docs.jax.dev/en/latest/jax.extend.html). Libraries
can [lean on these
APIs](https://docs.jax.dev/en/latest/building_on_jax.html) in
order to use JAX as an internal means of implementation, to integrate
```
**File:** ci/README.md (L18-21)
```markdown
nightly and release flows. It encompasses several distinct workflows, including
comprehensive presubmit checks triggered on pull requests and branch pushes,
bi-hourly continuous builds, extensive nightly builds with broad platform
coverage, and a controlled release process that culminates in PyPI publication.
```
**File:** ci/README.md (L26-29)
```markdown
*   **Linux x86:** CPU, TPU, CUDA
*   **Linux aarch64:** CPU, CUDA
*   **Windows x86:** CPU
*   **Mac Arm64:** CPU
```
**File:** docs/autodidax.md (L44-46)
```markdown
Ever want to learn how JAX works, but the implementation seemed impenetrable?
Well, you're in luck! By reading this tutorial, you'll learn every big idea in
JAX's core system. You'll even get clued into our weird jargon!
```
**File:** docs/advanced_guides.rst (L61-110)
```text
.. toctree::
   :maxdepth: 1
   :caption: Performance benchmarking and profiling

   benchmarking
   profiling
   device_memory_profiling

.. toctree::
   :caption: Non-functional programming
   :maxdepth: 1

   array_refs

.. toctree::
   :caption: External Callbacks
   :maxdepth: 1

   external-callbacks

.. toctree::
   :caption: FFI
   :maxdepth: 1

   ffi

.. toctree::
   :caption: Modeling workflows
   :maxdepth: 1

   gradient-checkpointing
   aot
   export/index

.. toctree::
   :caption: Example applications
   :maxdepth: 1

   notebooks/neural_network_with_tfds_data
   notebooks/Neural_Network_and_Data_Loading
   notebooks/vmapped_log_probs

.. toctree::
   :caption: Deep dives
   :maxdepth: 1

   notebooks/convolutions
   xla_flags
   jax-primitives
   jaxpr
```
## 請說明這專案的程式架構與邏輯, 回答的輸出請用繁體中文及Markdown格式

# JAX 專案程式架構與邏輯

## 核心架構概覽

JAX 的程式架構基於**可組合的函數轉換系統**，核心概念是將數值計算分解為基本操作（primitives），然後透過解釋器堆疊來應用各種轉換 jax:55-78 。

### 1. 基本運算單元系統

JAX 將所有計算操作抽象為 **Primitive** 物件，這是系統的最小運算單元 jax:87-90 。

```python
class Primitive(NamedTuple):
  name: str
```

每個 primitive 都有對應的轉換規則，透過 `bind` 函數來調用 jax:127-131 。

### 2. 追蹤與解釋器系統

JAX 使用 **Tracer** 物件來追蹤函數執行過程，並維護一個解釋器堆疊來處理不同的轉換 jax:141-159 。

```python
class MainTrace(NamedTuple):
  level: int
  trace_type: type['Trace']
  global_data: Any | None

trace_stack: list[MainTrace] = []
```

## 程式執行流程

### 階段一：函數追蹤

當 JAX 轉換函數被調用時，系統會：
1. 建立新的 MainTrace 並加入堆疊
2. 使用 Tracer 物件替換實際輸入
3. 執行函數並記錄所有 primitive 操作
4. 生成 Jaxpr 中間表示

### 階段二：Jaxpr 生成

Jaxpr 是 JAX 的中間表示，類似於一個小型函數式語言 jax:974-989 ：

```
jaxpr ::=
  { lambda <binder> , ... .
    let <eqn>
        ...
    in ( <atom> , ... ) }
```

### 階段三：編譯與執行

生成的 Jaxpr 會被轉換為 MLIR/StableHLO，然後透過 XLA 編譯器進行優化並在目標硬體上執行 jax:103-117 。

## 轉換系統架構

### 自動微分系統

JAX 實作了前向模式（JVP）和反向模式（VJP）自動微分 jax:39-42 。

### JIT 編譯系統

`jax.jit` 透過 XLA 編譯器將函數編譯為高效能的機器碼 jax:35-37 。

### 向量化系統

`jax.vmap` 自動將函式向量化以處理批次輸入 jax:27-27 。

## 模組化設計原則

JAX 採用高度模組化的設計 jax:16-30 ：

1. **核心模組**：專注於基礎數值計算和機器學習功能
2. **擴展 API**：提供客製化和擴展功能
3. **後端系統**：模組化的編譯器和執行時支援不同硬體

## 生態系統架構

JAX 鼓勵在核心之上建構特定領域的函式庫 jax:71-75 ，形成分層的生態系統架構。

---

## Notes

JAX 的架構設計強調**可組合性**和**可擴展性**，透過統一的 primitive 系統和解釋器堆疊，實現了各種函數轉換的無縫組合。這種設計使得 JAX 能夠支援從簡單的數值計算到複雜的機器學習模型的各種應用場景。如需深入理解實作細節，建議參考 Autodidax 教學文件 jax:44-46 。

Wiki pages you might want to explore:
- [Compilation Pipeline (jax-ml/jax)](/wiki/jax-ml/jax#2.3)
### Citations
**File:** docs/autodidax.md (L44-46)
```markdown
Ever want to learn how JAX works, but the implementation seemed impenetrable?
Well, you're in luck! By reading this tutorial, you'll learn every big idea in
JAX's core system. You'll even get clued into our weird jargon!
```
**File:** docs/autodidax.md (L55-78)
```markdown
## Part 1: Transformations as interpreters: standard evaluation, `jvp`, and `vmap`

We want to transform functions that look like this:

```python
def f(x):
  y = sin(x) * 2.
  z = - y + x
  return z
```

Think of functions like `sin` and the arithmetic operations underlying the
infix operators (`mul`, `add`, and `neg`) as primitive operations, meaning
atomic units of processing rather than compositions.

"Transform" means "interpret differently." Instead of standard interpretation
where we apply primitive operations to numerical inputs to produce numerical
outputs, we want to override primitive application and let different values
flow through our program. For example, we might want to replace the
application of every primitive with an application of [its JVP
rule](https://docs.jax.dev/en/latest/notebooks/autodiff_cookbook.html),
and let primal-tangent pairs flow through our program. Moreover, we want to be
able to compose multiple transformations, leading to stacks of interpreters.

```
**File:** docs/autodidax.md (L87-90)
```markdown
```{code-cell}
from typing import NamedTuple

class Primitive(NamedTuple):
```
**File:** docs/autodidax.md (L127-131)
```markdown
A `Primitive` is just an object with a name, to which we attach our
interpretation rules (one for each transformation). The `bind` function is our
interception point: it'll figure out which transformation rule to apply, based
on how the arguments are boxed in tracers and what interpreters are active.

```
**File:** docs/autodidax.md (L141-159)
```markdown
We represent active interpreters as a stack. The stack is just a simple
`list`, and each element is a container with an integer level (corresponding
to the element's height in the stack), an interpreter type (which we'll call a
`trace_type`), and an optional field for any global data the interpreter
needs. We call each element a `MainTrace`, though maybe "Interpreter" would be
more descriptive.

```{code-cell}
from collections.abc import Sequence
from contextlib import contextmanager
from typing import Any

class MainTrace(NamedTuple):
  level: int
  trace_type: type['Trace']
  global_data: Any | None

trace_stack: list[MainTrace] = []
dynamic_trace: MainTrace | None = None  # to be employed in Part 3
```
**File:** docs/autodidax.md (L974-989)
```markdown
The jaxpr term syntax is roughly:

```
jaxpr ::=
  { lambda <binder> , ... .
    let <eqn>
        ...
    in ( <atom> , ... ) }

binder ::= <var>:<array_type>
var ::= a | b | c | ...
atom ::= <var> | <literal>
literal ::= <int32> | <int64> | <float32> | <float64>

eqn ::= <binder> , ... = <primitive> [ <params> ] <atom> , ...
```
```
**File:** docs/about.md (L16-30)
```markdown
When [developing](#development) the core, we want to maintain agility
and a focused scope, so we lean heavily on a surrounding [modular
technology stack](#components). First, we design the `jax` module
to be
[composable](https://github.com/jax-ml/jax?tab=readme-ov-file#transformations)
and
[extensible](https://docs.jax.dev/en/latest/jax.extend.html), so
that a wide variety of domain-specific libraries can thrive outside of
it in a decentralized manner. Second, we lean heavily on a modular
backend stack (compiler and runtime) to target different
accelerators. Whether you are [writing a new domain-specific library
built with JAX](#upstack), or looking to [support
new hardware](#downstack), you can often
contribute these with *minimal to no modifications* to the JAX core
codebase.
```
**File:** docs/about.md (L71-75)
```markdown
While the JAX core library focuses on the fundamentals, we want to
encourage domain-specific libraries and tools to be built on top of
JAX. Indeed, [many
libraries](https://docs.jax.dev/en/latest/#ecosystem) have
emerged around JAX to offer higher-level features and extensions.
```
**File:** docs/about.md (L103-117)
```markdown
To manage hardware devices and memory, and for compilation to such
devices, JAX calls out to the open [XLA
compiler](https://openxla.org/) and the [PJRT
runtime](https://github.com/openxla/xla/tree/main/xla/pjrt/c#pjrt---uniform-device-api). Both
of these are projects external to the JAX core, governed and
maintained by OpenXLA (again, with frequent contributions from and
discussion with the JAX core developers).

XLA aims for interoperability across accelerators (e.g. by ingesting
[StableHLO](https://openxla.org/stablehlo) as input) and PJRT offers
extensibility through a plug-in device API. Adding support for new
devices is done by implementing a backend lowering for XLA, and
implementing a plug-in device API defined by PJRT. If you're looking
to contribute to compilation, or to supporting new hardware, we
encourage you to contribute at the XLA and PJRT layers.
```
**File:** docs/glossary.rst (L35-37)
```text
    JIT
      Short for *Just In Time* compilation, JIT in JAX generally refers to the compilation of
      array operations to :term:`XLA`, most often accomplished using :func:`jax.jit`.
```
**File:** docs/glossary.rst (L39-42)
```text
    JVP
      Short for *Jacobian Vector Product*, also sometimes known as *forward-mode* automatic
      differentiation. For more details, see :ref:`jacobian-vector-product`. In JAX, JVP is
      a :term:`transformation` that is implemented via :func:`jax.jvp`. See also :term:`VJP`.
```
## 如何列出支援的GPU 型號 ,本地 GPU 能力, 內存及功耗,頻寬, 並給出如何監控的範例, 回答的輸出請用繁體中文及Markdown格式

# JAX GPU 資訊查詢與監控指南

## 列出支援的 GPU 型號與基本資訊

### 使用 JAX 內建函數查詢設備

```python
import jax

# 列出所有可用設備
print("所有設備:", jax.devices())

# 列出本地設備
print("本地設備:", jax.local_devices())

# 獲取設備數量
print("設備總數:", jax.device_count())
print("本地設備數量:", jax.local_device_count())
```

### 獲取詳細 GPU 資訊

JAX 提供了 `print_environment_info()` 函數來顯示環境資訊，包括 GPU 詳細資訊 jax:34-63 ：

```python
from jax._src.environment_info import print_environment_info

# 打印完整的環境資訊，包括 nvidia-smi 輸出
print_environment_info()
```

## GPU 能力、內存及硬體資訊查詢

### NVIDIA GPU 查詢範例

從 CI 腳本中可以看到如何使用 `nvidia-smi` 獲取詳細資訊 jax:59-67 ：

```bash
# 獲取 GPU 數量
gpu_count=$(nvidia-smi --query-gpu=name --format=csv,noheader | wc -l)

# 獲取 GPU 型號
gpu_name=$(nvidia-smi --query-gpu=name --format=csv,noheader --id=0)

# 獲取 GPU 記憶體總量 (MiB)
memory_per_gpu_mib=$(nvidia-smi --query-gpu=memory.total --format=csv,noheader,nounits --id=0)

# 完整的 GPU 資訊
nvidia-smi
```

### AMD GPU (ROCm) 查詢範例

對於 AMD GPU，可以使用 `rocm-smi` 工具 jax:55-64 ：

```bash
# 獲取 GPU 數量
gpu_count=$(rocminfo | egrep -c "Device Type:\s+GPU")

# 獲取 GPU 記憶體資訊
memory_per_gpu_mib=$(rocm-smi -d 0 --showmeminfo vram | grep -i "vram total" | awk '{print int($NF/1024/1024)}' | head -1)

# 完整的 ROCm 資訊
rocm-smi
```

## GPU 監控範例

### 設備內存監控

JAX 提供了設備內存分析工具 jax:47-60 ：

```python
import jax
import jax.numpy as jnp
import jax.profiler

def func1(x):
  return jnp.tile(x, 10) * 0.5

def func2(x):
  y = func1(x)
  return jnp.sum(y)

# 創建一些數據
x = jnp.ones((1000, 1000))

# 執行並保存內存分析檔案
result = func2(x)
jax.profiler.save_device_memory_profile("memory_profile.prof")
```

### 性能監控與分析

使用 JAX profiler 進行詳細的性能監控 jax:353-383 ：

```python
import jax.profiler

# 基本性能分析
with jax.profiler.trace("./profile_dir"):
    # 執行你的 JAX 程式碼
    result = some_jax_function()

# 進階 GPU 監控選項
options = jax.profiler.ProfileOptions()
options.advanced_configuration = {
    "gpu_max_callback_api_events": 2048,
    "gpu_max_activity_api_events": 2048,
    "gpu_enable_nvtx_tracking": True,
    "gpu_pm_sample_counters": "sm__cycles_active.avg.pct_of_peak_sustained_elapsed",
    "gpu_pm_sample_interval_us": 500
}

with jax.profiler.trace("./profile_dir", profiler_options=options):
    result = some_jax_function()
```

## GPU 記憶體管理配置

JAX 預設會預分配 75% 的 GPU 記憶體，可以透過環境變數調整 jax:4-28 ：

```bash
# 禁用預分配
export XLA_PYTHON_CLIENT_PREALLOCATE=false

# 設定預分配比例為 50%
export XLA_PYTHON_CLIENT_MEM_FRACTION=0.5

# 使用平台分配器（按需分配）
export XLA_PYTHON_CLIENT_ALLOCATOR=platform
```

## 完整的 GPU 監控腳本範例

```python
import jax
import subprocess
import json

def get_gpu_info():
    """獲取 GPU 詳細資訊"""
    info = {
        'jax_devices': str(jax.devices()),
        'local_devices': str(jax.local_devices()),
        'device_count': jax.device_count(),
        'local_device_count': jax.local_device_count(),
        'platform': jax.default_backend()
    }
    
    # 嘗試獲取 nvidia-smi 資訊
    try:
        nvidia_smi_output = subprocess.check_output(['nvidia-smi', '--query-gpu=name,memory.total,memory.used,memory.free,utilization.gpu,temperature.gpu,power.draw', '--format=csv,noheader,nounits']).decode()
        info['nvidia_smi'] = nvidia_smi_output.strip().split('\n')
    except:
        info['nvidia_smi'] = 'N/A'
    
    return info

def monitor_gpu_usage():
    """監控 GPU 使用情況"""
    import time
    
    while True:
        try:
            # 使用 nvidia-smi 持續監控
            subprocess.run(['nvidia-smi', '-l', '1'])
            time.sleep(1)
        except KeyboardInterrupt:
            break
        except Exception as e:
            print(f"監控錯誤: {e}")
            break

if __name__ == "__main__":
    # 顯示 GPU 資訊
    gpu_info = get_gpu_info()
    print("=== GPU 資訊 ===")
    for key, value in gpu_info.items():
        print(f"{key}: {value}")
    
    # 可選：啟動持續監控
    # monitor_gpu_usage()
```

---

## Notes

- JAX 支援 NVIDIA GPU（透過 CUDA）和 AMD GPU（透過 ROCm）
- `nvidia-smi` 和 `rocm-smi` 是獲取硬體詳細資訊的主要工具
- JAX 的 profiler 提供了詳細的性能和記憶體分析功能
- 記憶體預分配行為可以透過環境變數調整以適應不同的使用場景
- 對於生產環境，建議使用 XProf 進行更詳細的設備記憶體分析 jax:6-10 

Wiki pages you might want to explore:
- [Overview (jax-ml/jax)](/wiki/jax-ml/jax#1)
### Citations
**File:** jax/_src/environment_info.py (L34-63)
```python
def print_environment_info(return_string: bool = False) -> str | None:
  """Returns a string containing local environment & JAX installation information.

  This is useful information to include when asking a question or filing a bug.

  Args: return_string (bool) : if True, return the string rather than printing
  to stdout.
  """
  from jax import version  # pytype: disable=import-error

  # TODO(jakevdp): should we include other info, e.g. jax.config.values?
  python_version = sys.version.replace('\n', ' ')
  info = textwrap.dedent(f"""\
  jax:    {version.__version__}
  jaxlib: {lib.version_str}
  numpy:  {np.__version__}
  python: {python_version}
  device info: {xb.devices()[0].device_kind}-{xb.device_count()}, {xb.local_device_count()} local devices"
  process_count: {xb.process_count()}
  platform: {platform.uname()}""")
  for key, value in os.environ.items():
    if key.startswith(("JAX_", "XLA_")):
      info += f"\n{key}={value}"
  nvidia_smi = try_nvidia_smi()
  if nvidia_smi:
    info += '\n\n$ nvidia-smi\n' + nvidia_smi
  if return_string:
    return info
  else:
    return print(info)
```
**File:** ci/run_pytest_cuda.sh (L59-67)
```shellscript
export gpu_count=$(nvidia-smi --query-gpu=name --format=csv,noheader | wc -l)
echo "Number of GPUs detected: $gpu_count"

echo "Assuming all GPUs are the same model and have the same amount of memory"
export gpu_name=$(nvidia-smi --query-gpu=name --format=csv,noheader --id=0)
echo "Detected GPU type: $gpu_name"

export memory_per_gpu_mib=$(nvidia-smi --query-gpu=memory.total --format=csv,noheader,nounits --id=0)
echo "Reported memory per GPU: $memory_per_gpu_mib MiB"
```
**File:** ci/run_pytest_rocm.sh (L55-64)
```shellscript
export gpu_count=$(rocminfo | egrep -c "Device Type:\s+GPU")
echo "Number of GPUs detected: $gpu_count"

# Query GPU 0 memory using rocm-smi
export memory_per_gpu_mib=$(rocm-smi -d 0 --showmeminfo vram | grep -i "vram total" | awk '{print int($NF/1024/1024)}' | head -1)
echo "Reported memory per GPU: $memory_per_gpu_mib MiB"

# Convert effective memory from MiB to GiB.
export memory_per_gpu_gib=$((memory_per_gpu_mib / 1024))
echo "Effective memory per GPU: $memory_per_gpu_gib GiB"
```
**File:** docs/device_memory_profiling.md (L6-10)
```markdown
June 2025 update: we recommend using [XProf
profiling](xprof-profiling) for device memory analysis. After taking a
profile, open the `memory_viewer` tab of the Tensorboard profiler for more
detailed and understandable device memory usage.
```
```
**File:** docs/device_memory_profiling.md (L47-60)
```markdown
To capture a device memory profile to disk, use
{func}`jax.profiler.save_device_memory_profile`. For example, consider the
following Python program:

```python
import jax
import jax.numpy as jnp
import jax.profiler

def func1(x):
  return jnp.tile(x, 10) * 0.5

def func2(x):
  y = func1(x)
```
**File:** docs/profiling.md (L353-383)
```markdown
##### GPU options

The following options are available for GPU profiling:

*   `gpu_max_callback_api_events`: Sets the maximum number of events collected
    by the CUPTI callback API. Defaults to `2*1024*1024`.
*   `gpu_max_activity_api_events`: Sets the maximum number of events collected
    by the CUPTI activity API. Defaults to `2*1024*1024`.
*   `gpu_max_annotation_strings`: Sets the maximum number of annotation
    strings that can be collected. Defaults to `1024*1024`.
*   `gpu_enable_nvtx_tracking`: Enables NVTX tracking in CUPTI. Defaults to
    `False`.
*   `gpu_enable_cupti_activity_graph_trace`: Enables CUPTI activity graph
    tracing for CUDA graphs. Defaults to `False`.
*   `gpu_pm_sample_counters`: A comma-separated string of GPU
    Performance Monitoring metrics to collect using CUPTI's PM sampling feature
    (e.g. `"sm__cycles_active.avg.pct_of_peak_sustained_elapsed"`). PM sampling
    is disabled by default. For available metrics, see
    [NVIDIA's CUPTI documentation](https://docs.nvidia.com/cupti/main/main.html#metrics-table).
*   `gpu_pm_sample_interval_us`: Sets the sampling interval in microseconds
    for CUPTI PM sampling. Defaults to `500`.
*   `gpu_pm_sample_buffer_size_per_gpu_mb`: Sets the system memory buffer size
    per device in MB for CUPTI PM sampling. Defaults to 64MB. The maximum
    supported value is 4GB.
*   `gpu_num_chips_to_profile_per_task`: Specifies the number of GPU devices to
    profile per task. If not specified, set to 0, or set to an invalid value,
    all available GPUs will be profiled. This can be used to decrease the trace
    collection size.
*   `gpu_dump_graph_node_mapping`: If enabled, dumps CUDA graph node
    mapping information into the trace. Defaults to `False`.

```
**File:** docs/gpu_memory_allocation.rst (L4-28)
```text
**JAX will preallocate 75% of the total GPU memory when the first JAX
operation is run.** Preallocating minimizes allocation overhead and memory
fragmentation, but can sometimes cause out-of-memory (OOM) errors. If your JAX
process fails with OOM, the following environment variables can be used to
override the default behavior:

``XLA_PYTHON_CLIENT_PREALLOCATE=false``
  This disables the preallocation behavior.  JAX will instead allocate GPU
  memory as needed, potentially decreasing the overall memory usage.  However,
  this behavior is more prone to GPU memory fragmentation, meaning a JAX program
  that uses most of the available GPU memory may OOM with preallocation
  disabled.

``XLA_PYTHON_CLIENT_MEM_FRACTION=.XX``
  If preallocation is enabled, this makes JAX preallocate XX% of
  the total GPU memory, instead of the default 75%. Lowering the
  amount preallocated can fix OOMs that occur when the JAX program starts.

``XLA_PYTHON_CLIENT_ALLOCATOR=platform``
  This makes JAX allocate exactly what is needed on demand, and deallocate
  memory that is no longer needed (note that this is the only configuration that
  will deallocate GPU memory, instead of reusing it). This is very slow, so is
  not recommended for general use, but may be useful for running with the
  minimal possible GPU memory footprint or debugging OOM failures.

```
## 請說明如何使用這專案 及安裝後的使用步驟 本專案有不同的典型使用情境的範例. 回答的輸出請用繁體中文及Markdown格式

# JAX 專案使用指南

## 安裝指南

### 基本安裝

JAX 需要安裝兩個套件：`jax`（純 Python）和 `jaxlib`（編譯二進位檔） jax:6-8 。

#### CPU 版本（適用於所有平台）
```bash
pip install --upgrade pip
pip install --upgrade jax
``` jax:57-60 

#### NVIDIA GPU 版本
```bash
pip install --upgrade "jax[cuda13]"
``` jax:106-108 

#### Google Cloud TPU 版本
```bash
pip install --upgrade "jax[tpu]"
``` jax:225-227 

### 支援平台

| 平台 | CPU | NVIDIA GPU | Google TPU | AMD GPU | Apple GPU |
|------|-----|------------|------------|---------|-----------|
| Linux x86_64 | ✓ | ✓ | ✓ | ✓ | ✗ |
| Linux aarch64 | ✓ | ✓ | ✗ | ✗ | ✗ |
| Mac aarch64 | ✓ | ✗ | ✗ | ✗ | 實驗性 |
| Windows x86_64 | ✓ | ✗ | ✗ | ✗ | ✗ | jax:31-38 

## 基本使用步驟

### 1. 導入 JAX

```python
import jax
import jax.numpy as jnp
from jax import grad, jit, vmap
``` jax:64-66 

### 2. 基本陣列操作

JAX 提供與 NumPy 相容的 API jax:62-62 ：

```python
# 創建陣列
x = jnp.linspace(0, 10, 1000)
y = 2 * jnp.sin(x) * jnp.cos(x)

# 基本運算
result = jnp.dot(x, x)
``` jax:73-75 

### 3. 設備管理

```python
# 查看可用設備
print("所有設備:", jax.devices())
print("本地設備:", jax.local_devices())
print("設備數量:", jax.device_count())
```

## 典型使用情境範例

### 1. 自動微分

```python
def tanh(x):
  y = jnp.exp(-2.0 * x)
  return (1.0 - y) / (1.0 + y)

# 計算梯度
grad_tanh = grad(tanh)
print(grad_tanh(1.0))  # 輸出: 0.4199743
``` jax:78-88 

### 2. JIT 編譯加速

```python
def predict(params, inputs):
  for W, b in params:
    outputs = jnp.dot(inputs, W) + b
    inputs = jnp.tanh(outputs)
  return outputs

def loss(params, inputs, targets):
  preds = predict(params, inputs)
  return jnp.sum((preds - targets)**2)

# 編譯函數以提升效能
grad_loss = jit(grad(loss))
``` jax:46-56 

### 3. 向量化處理

```python
# 對批次數據進行向量化處理
perex_grads = jit(vmap(grad_loss, in_axes=(None, 0, 0)))
``` jax:57-57 

### 4. 神經網路訓練

```python
import jax.random

# 初始化參數
key = jax.random.PRNGKey(0)
params = jax.random.normal(key, (10, 5))

# 定義簡單的神經網路
def neural_network(params, x):
  return jnp.tanh(jnp.dot(x, params))

# 計算損失和梯度
def compute_loss(params, x, y):
  preds = neural_network(params, x)
  return jnp.mean((preds - y)**2)

# 編譯訓練步驟
train_step = jit(grad(compute_loss))
```

### 5. 科學計算應用

```python
# 微分方程求解
def ode_system(state, t):
  x, y = state
  dx_dt = -y
  dy_dt = x
  return jnp.array([dx_dt, dy_dt])

# 使用自動微分進行 Jacobian 計算
jacobian_fn = jit(jacfwd(ode_system))
```

## 進階使用模式

### 1. 與其他函式庫整合

JAX 可以與多個領域特定函式庫結合使用 jax:54-63 ：

- **Flax**：神經網路建構
- **Optax**：優化器
- **Dynamax**：狀態空間模型
- **BlackJAX**：MCMC 採樣

### 2. 效能優化

```python
# 使用 JIT 編譯提升效能
@jit
def fast_matrix_multiply(A, B):
  return jnp.dot(A, B)

# 使用 vmap 進行批次處理
batched_multiply = vmap(fast_matrix_multiply, in_axes=(0, None))
```

### 3. 分散式計算

```python
# 多設備平行處理
from jax import pmap

@pmap
def parallel_function(x):
  return jnp.sum(x**2)

# 在多個 GPU 上執行
devices = jax.devices()
```

## 重要注意事項

### JAX 陣列的特性

- **不可變性**：JAX 陣列總是不可變的 jax:58-58 
- **函數式編程**：避免副作用和就地修改
- **隨機數生成**：使用 `jax.random.PRNGKey` 而非 NumPy 的隨機數

### 記憶體管理

JAX 預設預分配 75% 的 GPU 記憶體，可透過環境變數調整：

```bash
export XLA_PYTHON_CLIENT_MEM_FRACTION=0.5  # 預分配 50%
export XLA_PYTHON_CLIENT_PREALLOCATE=false  # 禁用預分配
```

---

## Notes

JAX 的設計理念是提供可組合的函數轉換，讓你能夠輕鬆地組合自動微分、JIT 編譯和向量化等功能。開始使用時建議先從簡單的 NumPy 相容操作開始，然後逐步學習如何使用 `jit`、`grad` 和 `vmap` 等轉換功能來提升效能。對於複雜的機器學習項目，建議使用基於 JAX 建構的高階函式庫如 Flax 或 Equinox。

Wiki pages you might want to explore:
- [Getting Started with JAX (jax-ml/jax)](/wiki/jax-ml/jax#4.1)
- [JAX 101 Tutorials (jax-ml/jax)](/wiki/jax-ml/jax#4.2)

Wiki pages you might want to explore:
- [Overview (jax-ml/jax)](/wiki/jax-ml/jax#1)
### Citations
**File:** docs/installation.md (L6-8)
```markdown
Using JAX requires installing two packages: `jax`, which is pure Python and
cross-platform, and `jaxlib` which contains compiled binaries, and requires
different builds for different operating systems and accelerators.
```
**File:** docs/installation.md (L31-38)
```markdown
|                  | Linux, x86_64                         | Linux, aarch64                  | Mac, aarch64                          | Windows, x86_64          | Windows WSL2, x86_64                     |
|------------------|---------------------------------------|---------------------------------|---------------------------------------|--------------------------|------------------------------------------|
| CPU              | {ref}`yes <install-cpu>`              | {ref}`yes <install-cpu>`        | {ref}`yes <install-cpu>`              | {ref}`yes <install-cpu>` | {ref}`yes <install-cpu>`                 |
| NVIDIA GPU       | {ref}`yes <install-nvidia-gpu>`       | {ref}`yes <install-nvidia-gpu>` | n/a                                   | no                       | {ref}`experimental <install-nvidia-gpu>` |
| Google Cloud TPU | {ref}`yes <install-google-tpu>`       | n/a                             | n/a                                   | n/a                      | n/a                                      |
| AMD GPU          | {ref}`yes <install-amd-gpu>`          | no                              | n/a                                   | no                       | {ref}`experimental <install-amd-gpu>`                             |
| Apple GPU        | n/a                                   | no                              | {ref}`experimental <install-mac-gpu>` | n/a                      | n/a                                      |
| Intel GPU        | {ref}`experimental <install-intel-gpu>`| n/a                            | n/a                                     | no                       | no                                       |
```
**File:** docs/installation.md (L57-60)
```markdown
```bash
pip install --upgrade pip
pip install --upgrade jax
```
```
**File:** docs/installation.md (L106-108)
```markdown
# NVIDIA CUDA 13 installation
# Note: wheels only available on linux.
pip install --upgrade "jax[cuda13]"
```
**File:** docs/installation.md (L225-227)
```markdown
```bash
pip install "jax[tpu]"
```
```
**File:** docs/notebooks/thinking_in_jax.md (L58-58)
```markdown
- Unlike NumPy arrays, JAX arrays are always immutable.
```
**File:** docs/notebooks/thinking_in_jax.md (L62-62)
```markdown
NumPy provides a well-known, powerful API for working with numerical data. For convenience, JAX provides [`jax.numpy`](https://docs.jax.dev/en/latest/jax.numpy.html) which closely mirrors the NumPy API and provides easy entry into JAX. Almost anything that can be done with `numpy` can be done with `jax.numpy`, which is typically imported under the `jnp` alias:
```
**File:** docs/notebooks/thinking_in_jax.md (L64-66)
```markdown
```{code-cell} ipython3
import jax.numpy as jnp
```
```
**File:** docs/notebooks/thinking_in_jax.md (L73-75)
```markdown
x_jnp = jnp.linspace(0, 10, 1000)
y_jnp = 2 * jnp.sin(x_jnp) * jnp.cos(x_jnp)
plt.plot(x_jnp, y_jnp);
```
**File:** README.md (L46-56)
```markdown
def predict(params, inputs):
  for W, b in params:
    outputs = jnp.dot(inputs, W) + b
    inputs = jnp.tanh(outputs)  # inputs to the next layer
  return outputs                # no activation on last layer

def loss(params, inputs, targets):
  preds = predict(params, inputs)
  return jnp.sum((preds - targets)**2)

grad_loss = jax.jit(jax.grad(loss))  # compiled gradient evaluation function
```
**File:** README.md (L57-57)
```markdown
perex_grads = jax.jit(jax.vmap(grad_loss, in_axes=(None, 0, 0)))  # fast per-example grads
```
**File:** README.md (L78-88)
```markdown
```python
import jax
import jax.numpy as jnp

def tanh(x):
  y = jnp.exp(-2.0 * x)
  return (1.0 - y) / (1.0 + y)

grad_tanh = jax.grad(tanh)
print(grad_tanh(1.0))
# prints 0.4199743
```
**File:** docs/building_on_jax.md (L54-63)
```markdown
### Composable domain specific libraries with JAX exposed
Another common approach are packages that provide prebuilt functionality,
whether it be model definition, or computation of some type.
Combinations of these packages can then be mixed and matched for a full
end to end workflow where a model is defined and its parameters are estimated.

One example is [Flax](https://github.com/google/flax) which simplifies the construction of Neural Networks.
Flax is then typically paired with [Optax](https://github.com/deepmind/optax)
where Flax defines the neural network architecture
and Optax supplies the optimization & model-fitting capabilities.
```
## 請給  繁體中文的 JAX 101 Tutorials

# JAX 101 教學指南（繁體中文）

## JAX 101 教學結構概覽

JAX 101 是一套完整的教學系列，旨在幫助用戶從基礎到進階掌握 JAX 的核心概念和功能 jax:14-30 。

### 教學主題列表

#### JAX 101 核心教學
- **關鍵概念** (key-concepts) - 介紹 JAX 的基本概念如轉換、追蹤、jaxpr 和 pytrees jax:21-21 
- **JIT 編譯** (jit-compilation) - 學習如何使用即時編譯提升效能 jax:22-22 
- **自動向量化** (automatic-vectorization) - 掌握 vmap 轉換的使用 jax:23-23 
- **自動微分** (automatic-differentiation) - 深入了解 JAX 的自動微分功能 jax:24-24 
- **除錯** (debugging) - 學習 JAX 程式的除錯技巧 jax:25-25 
- **隨機數** (random-numbers) - 理解 JAX 的隨機數生成機制 jax:26-26 
- **Pytrees** - 掌握 JAX 的樹狀結構數據處理 jax:27-27 
- **分片計算** (sharded-computation) - 學習分散式計算概念 jax:28-28 
- **有狀態計算** (stateful-computations) - 處理有狀態的計算模式 jax:29-29 
- **簡單神經網路** (simple-neural-network) - 實作基礎神經網路 jax:30-30 

#### JAX 201 進階教學
- **平行處理** (parallelism) - 進階平行計算技術 jax:39-39 
- **進階除錯** (advanced-debugging) - 複雜程式的除錯方法 jax:40-40 
- **效能分析** (profiling-and-performance) - 效能優化和分析工具 jax:41-41 

#### JAX 301 專家教學
- **進階編譯** (advanced-compilation) - 深度編譯技術 jax:47-47 

## 學習路徑建議

### 初學者路徑
1. 從 **Thinking in JAX** 開始，了解 JAX 的基本概念和與 NumPy 的差異 jax:8-9 
2. 學習 **關鍵概念**，建立 JAX 的核心思維模式 jax:13-13 
3. 掌握 **JIT 編譯** 和 **自動向量化** 提升程式效能
4. 深入 **自動微分**，理解 JAX 的核心優勢

### 進階學習路徑
1. 完成所有 JAX 101 主題
2. 進入 JAX 201 學習平行處理和效能分析
3. 挑戰 JAX 301 的進階編譯技術

## 重要注意事項

### 文件更新狀態
JAX 101 教學目前處於最終確定階段，但部分內容仍在開發中 jax:8-12 。

### 舊版文件重定向
舊的 JAX 101 文件路徑已經重定向到新的文件結構 jax:380-389 ：
- `jax-101/01-jax-basics.md` → `key-concepts.md`
- `jax-101/02-jitting.md` → `jit-compilation.md`
- `jax-101/03-vectorization.md` → `automatic-vectorization.md`
- `jax-101/04-advanced-autodiff.md` → `automatic-differentiation.md`

## 學習資源

### 官方文件
- JAX 101 教學是官方推薦的深度學習資源 jax:49-53 
- 可從官方網站的首頁直接訪問 JAX 101 區塊

### 補充資源
- **Autodidax** - 從零開始理解 JAX 核心系統的進階教學
- **Building on JAX** - 學習如何基於 JAX 建構應用程式

---

## Notes

JAX 101 教學系列提供了從基礎到專家的完整學習路徑。建議按照順序學習，特別是對於初學者，應先掌握關鍵概念再進入實際應用。教學內容涵蓋了 JAX 的所有核心功能，包括陣列操作、函數轉換、自動微分、平行處理等主題。對於中文用戶，可以結合英文原文和中文說明進行學習，以獲得最佳效果。

Wiki pages you might want to explore:
- [Getting Started with JAX (jax-ml/jax)](/wiki/jax-ml/jax#4.1)
- [Overview (jax-ml/jax)](/wiki/jax-ml/jax#1)
### Citations
**File:** docs/_tutorials/index.rst (L8-12)
```text
.. note::

   The tutorials below are a work in progress; for the time being, please refer
   to the older tutorial content, including :ref:`beginner-guide`,
   :ref:`jax-101`, and the now-deleted *JAX 101* tutorials.
```
**File:** docs/_tutorials/index.rst (L14-30)
```text
JAX 101
-------
Mostly finalized at :ref:`jax-101`!

.. toctree::
   :maxdepth: 1

   ../key-concepts
   ../jit-compilation
   ../automatic-vectorization
   ../automatic-differentiation
   ../debugging
   ../random-numbers
   ../pytrees
   ../sharded-computation
   ../stateful-computations
   simple-neural-network
```
**File:** docs/_tutorials/index.rst (L39-39)
```text
   parallelism
```
**File:** docs/_tutorials/index.rst (L40-40)
```text
   advanced-debugging
```
**File:** docs/_tutorials/index.rst (L41-41)
```text
   profiling-and-performance
```
**File:** docs/_tutorials/index.rst (L47-47)
```text
   :maxdepth: 1
```
**File:** docs/beginner_guide.rst (L8-9)
```text
:doc:`notebooks/thinking_in_jax` is the easiest place to jump in and get an overview of the JAX project, its execution
model, and differences with NumPy.
```
**File:** docs/beginner_guide.rst (L13-13)
```text
- :doc:`key-concepts` introduces the key concepts of JAX, such as transformations, tracing, jaxprs and pytrees.
```
**File:** docs/conf.py (L380-389)
```python
  "jax-101/01-jax-basics.md": "key-concepts.md",
  "jax-101/02-jitting.md": "jit-compilation.md",
  "jax-101/03-vectorization.md": "automatic-vectorization.md",
  "jax-101/04-advanced-autodiff.md": "automatic-differentiation.md",
  "jax-101/05-random-numbers.md": "random-numbers.md",
  "jax-101/05.1-pytrees.md": "pytrees.md",
  "jax-101/06-parallelism.md": "sharded-computation.md",
  "jax-101/07-state.md": "stateful-computations.md",
  "jax-101/08-pjit.rst": "sharded-computation.md",
  "jax-101/index.rst": "jax-101.rst",
```
**File:** docs/index.rst (L49-53)
```text
    .. grid-item-card:: :material-regular:`library_books;2em` JAX 101
      :columns: 12 6 6 4
      :link: jax-101
      :link-type: ref
      :class-card: jax-101
```
