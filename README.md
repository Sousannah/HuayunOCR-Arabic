# **HunyuanOCR Arabic Demo**

A Gradio-based demonstration application for the Tencent HunyuanOCR model, focused on Arabic optical character recognition (OCR) tasks such as text detection, extraction, and recognition from images. Users can upload images, customize prompts optimized for Arabic text recognition, and generate structured outputs with advanced generation controls. The application is specifically configured to handle right-to-left (RTL) Arabic text with high accuracy.

## Features

- **Image Upload and Processing**: Supports direct upload or clipboard paste; processes images via PIL for text recognition.
- **Arabic-Optimized Prompts**: Default prompt configured for Arabic text recognition with bilingual instructions (Arabic and English) to ensure accurate RTL text extraction and character recognition.
- **Advanced Generation Controls**: Adjustable max new tokens (up to 8192) for handling complex documents.
- **Output Handling**: Cleaned text to remove repetitions; interactive textbox with copy button for easy use.
- **Custom Theme**: SteelBlueTheme with gradients and enhanced typography for a professional interface.
- **Examples Integration**: Built-in sample images for quick testing (e.g., documents, receipts).
- **Queueing Support**: Handles up to 10 concurrent inferences for smooth multi-user access.
- **Error Resilience**: Graceful handling of loading and generation errors with informative messages.

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (recommended for bfloat16; falls back to CPU with float32).
- Git for cloning submodules.
- Hugging Face account (optional, for model caching via `huggingface_hub`).

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/Sousannah/HuayunOCR-Arabic.git
   cd HuayunOCR-Arabic
   ```

2. Install dependencies:
   Create a `requirements.txt` file with the following content, then run:
   ```
   pip install -r requirements.txt
   ```
   **requirements.txt content:**
   ```
   git+https://github.com/huggingface/transformers@82a06db03535c49aa987719ed0746a76093b1ec4
   git+https://github.com/huggingface/accelerate.git
   git+https://github.com/huggingface/diffusers.git
   git+https://github.com/huggingface/peft.git
   huggingface_hub
   gradio==6.0.1
   qwen-vl-utils
   sentencepiece
   opencv-python
   torchvision
   supervision
   matplotlib
   easydict
   kernels
   einops
   addict
   hf_xet
   torch
   numpy
   av
   ```

3. Start the application:
   ```
   python app.py
   ```
   The demo launches at `http://localhost:7860` (or the provided URL if using Spaces).

## Usage

1. **Upload Image**: Drag-and-drop or paste an image containing Arabic text (e.g., scanned Arabic documents, signs, or multilingual text with Arabic content).

2. **Set Prompt**: Enter a custom query in the textbox. Default prompt: "قم باكتشاف وتعرّف على النص العربي في الصورة. استخرج جميع النصوص العربية بدقة مع الحفاظ على الاتجاه من اليمين إلى اليسار. Extract and recognize Arabic text in the image. Preserve right-to-left reading direction and maintain accurate Arabic character recognition."

3. **Configure Settings**:
   - Expand "Advanced Settings" to adjust max new tokens for longer outputs.

4. **Run Inference**: Click "Perform OCR" to process. Results appear in the output textbox.

5. **View Results**:
   - Text: Extracted Arabic text with proper right-to-left reading direction preserved.
   - Copy or edit the interactive output as needed.
   - The output maintains accurate Arabic character recognition and formatting.


## Troubleshooting

- **Model Loading Errors**: Verify CUDA setup; check console for `torch.version.cuda`. Use `attn_implementation="eager"` to avoid SDPA issues.
- **Out of Memory**: Reduce max new tokens or use CPU fallback; monitor with `nvidia-smi`.
- **Import Issues**: Install `spaces` only for Hugging Face Spaces deployment; it's mocked locally.
- **Repeated Output**: Automatically cleaned via `clean_repeated_substrings`; increase threshold if needed.
- **Generation Fails**: Ensure prompt is valid; test with default for baseline.
- **UI Launch**: If `ssr_mode=False` causes issues, set to `True` for server-side rendering.
