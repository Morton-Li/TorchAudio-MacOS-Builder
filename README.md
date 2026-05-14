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
   示例文件名：`torchaudio-2.12.0-cp313-cp313-macosx_11_0_x86_64.whl`
2. 使用 `pip` 安装：

   ```bash
   pip install torchaudio-2.12.0-cp313-cp313-macosx_11_0_x86_64.whl
   ```
3. 验证是否安装成功（需确保已安装兼容的 PyTorch）：

   ```bash
   python -c "import torchaudio; print(torchaudio.__version__)"
   ```

---

## 💡 为什么需要这个项目 Why This Project Matters

TorchAudio 是 PyTorch 音频处理生态的重要组件，但其官方安装包亦不再为 Intel 架构的 macOS 提供支持。本项目旨在填补该缺口，**延续 TorchAudio 在旧款 Mac 上的使用寿命**，并确保其与非官方构建的 PyTorch 保持兼容。

TorchAudio, a core audio processing library in the PyTorch ecosystem, has also dropped support for Intel-based macOS in official binaries. This project fills the gap by **extending TorchAudio support for Intel Macs**, ensuring continued compatibility with custom-built PyTorch packages.

---

## 🤝 鸣谢 Acknowledgements

* [PyTorch](https://github.com/pytorch/pytorch)
* [TorchAudio](https://github.com/pytorch/audio)
* [GitHub Actions](https://github.com/features/actions)
