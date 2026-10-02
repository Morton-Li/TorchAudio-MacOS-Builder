# TorchAudio macOS Builder

> 🔧 自动构建 TorchAudio 官方发行版本的 macOS 平台兼容 `.whl` 安装包。
> 🔧 Automatically build official TorchAudio release `.whl` packages for macOS

---

## 📦 项目简介 Project Introduction

[本项目](https://github.com/Morton-Li/TorchAudio-MacOS-Builder) 通过 GitHub Actions 获取 [TorchAudio 官方仓库](https://github.com/pytorch/audio) 的发行版本，并自动构建适用于 **macOS** 的 Python wheel 安装包。

构建产物为 **多 Python 版本** 的 `.whl` 文件，便于在老款 Mac 上继续使用高版本 TorchAudio。

[This project](https://github.com/Morton-Li/TorchAudio-MacOS-Builder) uses GitHub Actions to fetch release versions from the [official TorchAudio repository](https://github.com/pytorch/audio), and automatically builds Python wheel packages for **macOS**.

The output includes `.whl` files for **multiple Python versions**, allowing users to continue using newer versions of TorchAudio on older Mac machines.

---

## 🛠 使用方式 How to Use

1. 从 [Releases 页面](../../releases) 下载你所需版本的 `.whl`：
   示例文件名：`torchaudio-2.11.0-cp313-cp313-macosx_11_0_x86_64.whl`
2. 使用 `pip` 安装：

   ```bash
   pip install torchaudio-2.11.0-cp313-cp313-macosx_11_0_x86_64.whl
   ```
3. 验证是否安装成功（需确保已安装兼容的 PyTorch）：

   ```bash
   python -c "import torchaudio; print(torchaudio.__version__)"
   ```

---

## 🔗 版本兼容 Compatibility

[TorchAudio 2.11.0 官方发布说明](https://github.com/pytorch/audio/releases/tag/v2.11.0)明确支持 PyTorch 2.11 及后续版本；其 C++ 扩展使用 PyTorch 稳定 ABI。因此，无需将 TorchAudio 版本号同步为 PyTorch 2.14.1。

本项目已有 TorchAudio 2.11.0 的 Python **3.11–3.14**、macOS 11.0+、x86_64 wheel，构建基线为 PyTorch 2.11.0。安装时请先安装相同 Python 与平台对应的[自建 PyTorch wheel](https://github.com/Morton-Li/PyTorch-MacOS-Builder/releases)。

The [official TorchAudio 2.11.0 release](https://github.com/pytorch/audio/releases/tag/v2.11.0) supports PyTorch 2.11 and later through PyTorch's stable ABI. The existing Intel macOS wheels cover Python **3.11–3.14** and were built against PyTorch 2.11.0; install the matching custom PyTorch wheel first.

可在 [Test TorchAudio Compatibility](../../actions/workflows/test-torchaudio-compatibility.yml) 中手动验证既有 wheel。默认组合为 **TorchAudio 2.11.0 + PyTorch 2.14.1**，检查导入、`lfilter`、`forced_align` 和 RNNT loss 的实际运行；该流程仅验证，不重新构建或发布 wheel。

Run **Test TorchAudio Compatibility** manually to validate existing wheels against a custom PyTorch release. Its default pair is **TorchAudio 2.11.0 + PyTorch 2.14.1**. It checks imports and native CPU operators without rebuilding or publishing wheels.

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
