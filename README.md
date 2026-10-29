# TorchAudio macOS Builder

> 🔧 通过 GitHub Actions 构建 TorchAudio 官方发行版本的 macOS 平台兼容 `.whl` 安装包。
> 🔧 Build official TorchAudio release `.whl` packages for macOS with GitHub Actions

---

## 📦 项目简介 Project Introduction

[本项目](https://github.com/Morton-Li/TorchAudio-MacOS-Builder) 通过 GitHub Actions 每日缓存 [TorchAudio 官方仓库](https://github.com/pytorch/audio) 最新稳定版本的源码，由维护者手动触发构建适用于 **macOS** 的 Python wheel 安装包。

构建产物为兼容 **多个 Python 版本** 的单个 `py3-none` wheel，便于在老款 Intel Mac 上继续使用高版本 TorchAudio。

[This project](https://github.com/Morton-Li/TorchAudio-MacOS-Builder) uses GitHub Actions to cache the source of the latest stable release from the [official TorchAudio repository](https://github.com/pytorch/audio) daily. Maintainers manually trigger builds of Python wheel packages for **macOS**.

The output is a single `py3-none` wheel for **multiple Python versions**, allowing users to continue using newer versions of TorchAudio on older Intel Macs.

---

## 🛠 使用方式 How to Use

当前构建目标为 **TorchAudio 2.11.1 + PyTorch 2.15.0**。截至 2026-10-29，以下是目标文件名，本项目尚未构建或发布 2.11.1；当前可下载版本为 2.11.0。请在新 Release 实际发布后使用示例，或按 Releases 中的真实文件名安装。

The build target is **TorchAudio 2.11.1 + PyTorch 2.15.0**. As of 2026-10-29, the new Intel macOS wheel has not been built or published; the available release is 2.11.0. Use the following examples after 2.11.1 is published.

1. 从 [Releases 页面](../../releases) 下载你所需版本的 `.whl`：
   示例文件名：`torchaudio-2.11.1-py3-none-macosx_11_0_x86_64.whl`
   同时从 [PyTorch macOS Builder Releases](https://github.com/Morton-Li/PyTorch-MacOS-Builder/releases/tag/v2.15.0) 下载对应 Python 版本的 PyTorch wheel。
2. 使用 `pip` 安装：

   ```bash
   pip install torch-2.15.0-cp313-cp313-macosx_11_0_x86_64.whl
   pip install torchaudio-2.11.1-py3-none-macosx_11_0_x86_64.whl
   ```
3. 验证是否安装成功（需确保已安装兼容的 PyTorch）：

   ```bash
   python -c "import torchaudio; print(torchaudio.__version__)"
   ```

---

## 🔗 版本兼容 Compatibility

[TorchAudio 2.11.1 官方发布说明](https://github.com/pytorch/audio/releases/tag/v2.11.1)明确支持 PyTorch 2.11 及后续版本，并采用跨 Python 版本的 `py3-none` wheel；[源码元数据](https://github.com/pytorch/audio/blob/v2.11.1/setup.py)声明 `torch>=2.11` 和 `python_requires>=3.10`。因此，TorchAudio 的版本号无需与 PyTorch 相同。

本项目使用 **Python 3.12 + PyTorch 2.15.0** 构建一次，目标为 **macOS 11.0+、x86_64**，然后在 **Python 3.11–3.14** 上安装同一个 wheel，检查依赖、导入、`lfilter`、`forced_align`、RNNT loss 和反向传播。所有测试成功后，只有 `main` 上的手动运行会发布 Release；每日定时工作流只缓存源码。

The [official TorchAudio 2.11.1 release](https://github.com/pytorch/audio/releases/tag/v2.11.1) supports PyTorch 2.11 and later and uses a `py3-none` wheel. This project builds once with **Python 3.12 + PyTorch 2.15.0**, targeting **macOS 11.0+, x86_64**, then tests the same wheel on **Python 3.11–3.14** with dependency checks and native CPU operators. Publishing requires all tests to pass and a manual run on `main`; the daily workflow only caches source.

可在 [Test TorchAudio Compatibility](../../actions/workflows/test-torchaudio-compatibility.yml) 中手动验证已发布 wheel。默认组合为 **TorchAudio 2.11.1 + PyTorch 2.15.0**，需先发布 2.11.1 wheel；也可将输入改回现有的 2.11.0，该流程同时识别旧的 `cpNNN` 和新的 `py3-none` 文件名，仅验证，不重新构建或发布。

Run **Test TorchAudio Compatibility** to validate published wheels. Its default pair is **TorchAudio 2.11.1 + PyTorch 2.15.0**, once 2.11.1 is available. The workflow also accepts existing 2.11.0 wheels and handles both legacy `cpNNN` and new `py3-none` filenames without rebuilding or publishing.

本次修改尚未执行 macOS 构建或运行测试；最低系统版本、Python 3.15 和 free-threaded Python 均未在本次验证。Python 3.15 测试需先有对应的自建 PyTorch `cp315` wheel，不能仅依据 `py3-none` 标签声称已验证兼容。

These changes still need macOS build and runtime validation. The minimum OS version, Python 3.15 and free-threaded Python have not been tested here. Testing Python 3.15 first requires a matching custom PyTorch `cp315` wheel; a `py3-none` tag alone does not establish tested compatibility.

`torchaudio.load()` 和 `torchaudio.save()` 另需兼容的 [TorchCodec](https://docs.pytorch.org/audio/stable/installation.html#optional-dependencies)，不在上述验证范围内。This workflow does not test audio file I/O, which requires a compatible TorchCodec installation.

---

## 💡 为什么需要这个项目 Why This Project Matters

TorchAudio 是 PyTorch 音频处理生态的重要组件，但其官方安装包亦不再为 Intel 架构的 macOS 提供支持。本项目旨在填补该缺口，**延续 TorchAudio 在旧款 Mac 上的使用寿命**，并确保其与非官方构建的 PyTorch 保持兼容。

TorchAudio, a core audio processing library in the PyTorch ecosystem, has also dropped support for Intel-based macOS in official binaries. This project fills the gap by **extending TorchAudio support for Intel Macs**, ensuring continued compatibility with custom-built PyTorch packages.

---

## 🤝 鸣谢 Acknowledgements

* [PyTorch](https://github.com/pytorch/pytorch)
* [TorchAudio](https://github.com/pytorch/audio)
* [GitHub Actions](https://github.com/features/actions)
