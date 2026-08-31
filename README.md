# beellama.cpp prebuilt CUDA binaries for Colab T4
Prebuilt `llama-server` from [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) with CUDA support for **sm_75 (NVIDIA T4)**.

## What is this?
A single GitHub Actions workflow builds beellama.cpp with CUDA for T4 GPUs (sm_75) and publishes the binary as a release asset. This avoids the 10-15 minute build step when running the Colab notebook.

## How to use
1. **Trigger a build**: go to Actions tab → "Build beellama CUDA sm_75" → Run workflow
2. **Download**: the tarball appears as a release asset on the Releases page
3. **In the notebook**: the download URL is set in `CONFIG`, and the notebook fetches it (~30 seconds) instead of building from source

## Manual trigger
You can manually trigger a rebuild (e.g. when beellama.cpp updates) from the Actions tab → "Run workflow".

## What's inside the tarball
```
dist/
├── llama-server       # the main binary
├── libllama.so        # llama core library
├── libggml*.so        # ggml computation backend (ggml, ggml-base, ggml-cuda)
└── ...
```
CUDA runtime, cuBLAS, and cuDNN are expected to be present on the system (Colab has them).

## Customization
Edit `build.yml` to change:
- `CUDA_ARCH`: GPU architecture (default: 75 for T4)
- `CUDA_VERSION`: CUDA toolkit version (default: 12.4.1)
- `BEE_REF`: beellama.cpp branch/tag to build (default: main)
