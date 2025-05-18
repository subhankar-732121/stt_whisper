[Audio Transcription Project
This project uses the transformers library and OpenAI's Whisper model to transcribe audio files into text, with support for timestamps. The code is designed to run in a Google Colab environment and processes MP3 audio files.
Prerequisites

Python 3.11 or higher
Google Colab environment (for file upload functionality)
FFmpeg installed for audio processing
CUDA-compatible GPU (optional, for faster processing)

Installation

Install the required Python packages:
pip install transformers


Install FFmpeg:
apt-get update && apt-get install -y ffmpeg



Dependencies
The following Python packages are automatically installed with transformers:

filelock
huggingface-hub>=0.30.0
numpy>=1.17
packaging>=20.0
pyyaml>=5.1
regex!=2019.12.17
requests
tokenizers>=0.21
safetensors>=0.4.3
tqdm>=4.27

Usage

Upload Audio File:

Use Google Colab's file upload widget to upload an MP3 audio file:from google.colab import files
uploaded = files.upload()




Set Up Transcription Pipeline:

Initialize the Whisper model (openai/whisper-tiny) for automatic speech recognition:import torch
from transformers import pipeline
import os

device = "cuda" if torch.cuda.is_available() else "cpu"
pipe = pipeline(
    "automatic-speech-recognition",
    model="openai/whisper-tiny",
    device=device
)




Transcribe Audio:

Specify the path to the uploaded MP3 file and transcribe it with timestamps:audio_path = "/content/your_audio_file.mp3"
if not os.path.exists(audio_path):
    raise FileNotFoundError(f"Audio file {audio_path} not found.")
result = pipe(audio_path, return_timestamps=True)
print("Transcription:")
print(result["text"])





Example Output
For an input MP3 file, the transcription might look like:
Transcription:
DJ Unrealer. DJ Unrealer. Thomas Smith Records. Thomas Smith Records. This is Thomas Smith Records. Are you ready? Are you ready? Get ready. Are you ready? This is an unrel exclusive. This is an unrel exclusive. This is an unreal exclusive. This is an unreal exclusive. This is an unreal exclusive. This is an unreal exclusive. This is an unreal exclusive. This is an unreal exclusive. You're in the mix with an unreal exclusive. Thomas Smith Records.

Notes

The script checks for CUDA availability and defaults to CPU if no GPU is available.
Ensure the audio file path is correct to avoid FileNotFoundError.
The openai/whisper-tiny model is lightweight but may have lower accuracy compared to larger models like whisper-base or whisper-large. Adjust the model in the pipeline for better results if needed.
A FutureWarning about deprecated input names (inputs vs. input_features) may appear but does not affect functionality.

Troubleshooting

FileNotFoundError: Verify the audio file is uploaded to the correct path in Colab (e.g., /content/).
FFmpeg not found: Ensure FFmpeg is installed using the provided apt-get command.
Memory issues: If using a larger Whisper model, ensure sufficient RAM/GPU memory is available in Colab.


](https://grok.com/share/c2hhcmQtMg%3D%3D_f886f3e8-6e8a-4333-9a3e-b0964b9fe4ea)
