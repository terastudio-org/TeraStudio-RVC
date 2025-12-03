<div align="center">
  
# TeraStudio-RVC
A simple, high-quality and high-performance voice conversion tool.

[![TeraStudio-RVC](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/terastudio-org/TeraStudio-RVC)
[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/github/PhamHuynhAnh16/Vietnamese-RVC-ipynb/blob/main/Vietnamese-RVC.ipynb)

</div>

<div align="center">

</div>

## Description

This project is a simple, user-friendly voice conversion tool. Aiming to produce high-quality voice conversion products with optimal performance, the project allows users to change voices smoothly and naturally.

## Project Features

- Music Source Separation (MDX-Net / Demucs / VR)

- Voice Conversion (Single File Conversion / Batch Conversion / Conversion with Whisper / Text Conversion)

- Apply Audio Effects

- Generate Training Data (From URL)

- Model Training (v1 / v2, high-quality encoder, power training)

- Model Fusion

- Read Model Information

- Export Model to ONNX

- Download from Available Model Hub

- Search Models from Web

- Pitch Extraction

- Support ONNX Model Inference for Audio Conversion

- ONNX RVC models will also support index inference

- Real-time Voice Conversion

- Generate Training Reference

**Pitch Extraction Methods: `pm-ac, pm-cc, pm-shs, dio, mangio-crepe-tiny, mangio-crepe-small, mangio-crepe-medium, mangio-crepe-large, mangio-crepe-full, crepe-tiny, crepe-small, crepe-medium, crepe-large, crepe-full, fcpe, fcpe-legacy, fcpe-previous, rmvpe, rmvpe-clipping, rmvpe-medfilt, rmvpe-clipping-medfilt, harvest, yin, pyin, swipe, piptrack, penn, mangio-penn, djcm, djcm-clipping, djcm-medfilt, djcm-clipping-medfilt, swift, pesto`**

**Embedding Extraction Models: `contentvec_base, hubert_base, vietnamese_hubert_base, japanese_hubert_base, korean_hubert_base, chinese_hubert_base, portuguese_hubert_base, spin-v1, spin-v2, whisper-tiny, whisper-tiny.en, whisper-base, whisper-base.en, whisper-small, whisper-small.en, whisper-medium, whisper-medium.en, whisper-large-v1, whisper-large-v2, whisper-large-v3, whisper-large-v3-turbo`**

- **Embedding extraction models have available modes such as: fairseq, onnx, transformers, spin, whisper.**
- **All pitch extraction models have ONNX accelerated versions except for methods operating via wrapper.**
- **Pitch extraction models can be combined with weights to create new sensations, for example: `hybrid[rmvpe+harvest]`.**

## Usage Guide

**Will be added if I actually have free time...**

## Advanced Installation

Step 1: Install necessary dependencies

- Install Python from the official site: **[PYTHON](https://www.python.org/ftp/python/3.11.8/python-3.11.8-amd64.exe)** (Project tested on Python 3.10.x and 3.11.x)
- Install FFmpeg from source and add to system PATH: **[FFMPEG](https://github.com/BtbN/FFmpeg-Builds/releases)**

Step 2: Install the project (Using Git or simply download from GitHub)

For Git:
- git clone https://github.com/PhamHuynhAnh16/Vietnamese-RVC.git
- cd Vietnamese-RVC

Install via GitHub:
- Go to https://github.com/terastudio-org/TeraStudio-RVC
- Click the green `<> Code` button and select `Download ZIP`
- Extract `TeraStudio-RVC-main.zip`
- Navigate to the TeraStudio-RVC-main folder, type `cmd` in the address bar and press Enter

Step 3: Install required libraries:

Enter the command:
```
python -m venv env
env\\Scripts\\activate

python -m pip install uv
uv pip install six packaging python-dateutil platformdirs pywin32 onnxconverter_common wget
```

Installation for different devices

<details>
<summary>For CPU</summary>

```
uv pip install -r requirements.txt
```

</details>

<details>
<summary>For CUDA</summary>

Can replace cu118 with newer cu128 if GPU supports:
```
uv pip install numpy==1.26.4 numba==0.61.0
uv pip install torch torchaudio torchvision --index-url https://download.pytorch.org/whl/cu118
uv pip install -r requirements.txt
```

</details>

<details>
<summary>For OPENCL (AMD)</summary>

```
uv pip install numpy==1.26.4 numba==0.61.0
uv pip install torch==2.6.0 torchaudio==2.6.0 torchvision
uv pip install https://github.com/artyom-beilis/pytorch_dlprim/releases/download/0.2.0/pytorch_ocl-0.2.0+torch2.6-cp311-none-win_amd64.whl
uv pip install onnxruntime-directml
uv pip install -r requirements.txt
```

Note:
- It seems OPENCL support has been discontinued.
- Should only install on python 3.11 due to lack of builds for python 3.10 with torch 2.6.0.
- Demucs may cause overload and memory overflow on GPU (if you need to use demucs, open the config.json file in main\configs and change the demucs_cpu_mode argument to true).
- DDP does not support multi-GPU training for OPENCL.
- Some other algorithms must run on CPU so GPU performance may not be fully utilized.

</details>

<details>
<summary>For DIRECTML (AMD)</summary>

```
uv pip install numpy==1.26.4 numba==0.61.0
uv pip install torch==2.4.1 torchaudio==2.4.1 torchvision
uv pip install torch-directml==0.2.5.dev240914
uv pip install onnxruntime-directml
uv pip install -r requirements.txt
```

Note:
- Directml has stopped development for a long time.
- Directml does not support multi-threading tasks very well, so when running extraction it often gets locked to 1 thread.
- Directml partially supports fp16 but its use is not recommended as performance may be equivalent to fp32.
- Directml lacks a function to clean up memory; I've created a simple function for memory cleanup but it may not be very effective.
- Directml is designed for inference, not for training, although it can run training tasks, it is not recommended.

</details>

## Usage

**Using with Google Colab**
- Open Google Colab: [Vietnamese-RVC](https://colab.research.google.com/github/PhamHuynhAnh16/Vietnamese-RVC-ipynb/blob/main/Vietnamese-RVC.ipynb)
- Step 1: Run the Installation cell and wait for it to complete.
- Step 2: Run the Open Usage Interface cell (At this point, the interface will print two URLs: one is 0.0.0.0.7680 and one is a clickable gradio link; click the clickable link and it will take you to the interface).

**Run the run_app file to open the usage interface, run the tensorboard file to open the training monitoring chart. (Note: do not close the Command Prompt or Terminal)**
```
run_app.bat / tensorboard.bat
```

**Launch the usage interface. (Add `--allow_all_disk` to the command to allow gradio to access files outside the project)**
```
env\\Scripts\\python.exe main\\app\\app.py --open
```

**For using Tensorboard to monitor training**
```
env\\Scripts\\python.exe main/app/run_tensorboard.py
```

**Using via command syntax**
```
python main\\app\\parser.py --help
```

## Simple Installation and Usage

**Install the releases version from [Vietnamese_RVC](https://github.com/PhamHuynhAnh16/Vietnamese-RVC/releases)**
- Choose the correct version for you and download it.
- Extract the project.
- Run the run_app.bat file to open the operational interface.

**Using the run_install.bat file**
- Download the source code.
- Extract the project.
- Run the run_install.bat file to start installation.
- Run the run_app.bat file to open the operational interface.

## NOTES

- **Currently, new encoders like MRF HIFIGAN are still lacking complete pre-trained models.**
- **MRF HIFIGAN and REFINEGAN encoders do not support training when pitch is not being trained.**
- **Power training may improve model quality, but there are no pre-trained models specifically for this feature yet.**
- **Models in the Vietnamese-RVC repository are collected from various sources across AI Hub, HuggingFace, and other repositories. They may carry different licenses and copyrights.**

## Disclaimer

- **The Vietnamese-RVC project is developed for research, learning, and personal entertainment purposes. I do not encourage nor bear responsibility for any misuse of voice conversion technology for fraudulent purposes, identity impersonation, or violation of the privacy or copyrights of any individual or organization.**

- **Users must take full responsibility for their use of this software and commit to complying with the laws in effect in their country of residence or operation.**

- **The use of voices of celebrities, real people, or public figures must have permission or ensure no violation of law, ethics, and the rights of involved parties.**

- **The project author bears no legal responsibility for any consequences arising from the use of this software.**

## Terms of Use

- You must ensure that the audio content you upload and convert through this project does not infringe on the intellectual property rights of any third party.

- You are not permitted to use this project for any illegal activities, including but not limited to use for fraud, harassment, or causing harm to others.

- You are solely responsible for any damages resulting from improper use of the product.

- I will not be responsible for any direct or indirect damages arising from the use of this project.

## This project is built upon the following works

|                                                            Work                                                                 |         Author          |  License   |
|--------------------------------------------------------------------------------------------------------------------------------|-------------------------|------------|
| **[Applio](https://github.com/IAHispano/Applio/tree/main)**                                                                    | IAHispano               | MIT License |
| **[Python-audio-separator](https://github.com/nomadkaraoke/python-audio-separator/tree/main)**                                 | Nomad Karaoke           | MIT License |
| **[Retrieval-based-Voice-Conversion-WebUI](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/tree/main)**  | RVC Project             | MIT License |
| **[RVC-ONNX-INFER-BY-Anh](https://github.com/PhamHuynhAnh16/RVC_Onnx_Infer)**                                                  | Phạm Huỳnh Anh          | MIT License |
| **[Torch-Onnx-Crepe-By-Anh](https://github.com/PhamHuynhAnh16/TORCH-ONNX-CREPE)**                                              | Phạm Huỳnh Anh          | MIT License |
| **[Hubert-No-Fairseq](https://github.com/PhamHuynhAnh16/hubert-no-fairseq)**                                                   | Phạm Huỳnh Anh          | MIT License |
| **[Local-attention](https://github.com/lucidrains/local-attention)**                                                           | Phil Wang               | MIT License |
| **[TorchFcpe](https://github.com/CNChTu/FCPE/tree/main)**                                                                      | CN_ChiTu                | MIT License |
| **[FcpeONNX](https://github.com/deiteris/voice-changer/blob/master-custom/server/utils/fcpe_onnx.py)**                         | Yury deiteris           | MIT License |
| **[ContentVec](https://github.com/auspicious3000/contentvec)**                                                                 | Kaizhi Qian             | MIT License |
| **[Mediafiredl](https://github.com/Gann4Life/mediafiredl)**                                                                    | Santiago Ariel Mansilla | MIT License |
| **[Noisereduce](https://github.com/timsainb/noisereduce)**                                                                     | Tim Sainburg            | MIT License |
| **[World.py-By-Anh](https://github.com/PhamHuynhAnh16/world.py)**                                                              | Phạm Huỳnh Anh          | MIT License |
| **[Mega.py](https://github.com/3v1n0/mega.py)**                                                                                | Marco Trevisan          | No License  |
| **[Gdown](https://github.com/wkentaro/gdown)**                                                                                 | Kentaro Wada            | MIT License |
| **[Whisper](https://github.com/openai/whisper)**                                                                               | OpenAI                  | MIT License |
| **[PyannoteAudio](https://github.com/pyannote/pyannote-audio)**                                                                | pyannote                | MIT License |
| **[AudioEditingCode](https://github.com/HilaManor/AudioEditingCode)**                                                          | Hila Manor              | MIT License |
| **[StftPitchShift](https://github.com/jurihock/stftPitchShift)**                                                               | Jürgen Hock             | MIT License |
| **[Penn](https://github.com/interactiveaudiolab/penn)**                                                                        | Interactive Audio Lab   | MIT License |
| **[Voice Changer](https://github.com/deiteris/voice-changer)**                                                                 | Yury deiteris           | MIT License |
| **[Pesto](https://github.com/SonyCSLParis/pesto)**                                                                             | Sony CSL Paris          | LGPL 3.0    |

## Model Hub for the Model Search Tool

- **[VOICE-MODELS.COM](https://voice-models.com/)**

## Reporting Issues
- **If the system error reporting is not working, you can report issues to us vua [ISSUE](https://github.com/terastudio-org/TeraStudio-RVC/issues)**
