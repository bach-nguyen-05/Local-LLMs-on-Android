# Local LLMs on Android
## This is a tutorial on how you can set up local LLMs on your phone using llama.cpp
I will use llama.cpp in this tutorial, and create a UI using llama-server. Ollama can also do the same thing, and the models must be in gguf format.

1.	Download Termux from Google Play <br>
Before proceeding, you have to initiate your storage:
```bash
termux-setup-storage
```
For further understanding termux, please visit [this video](https://www.youtube.com/watch?v=Uj21Kz-BsTs) <br>
2.	Update and install all needed packages
```bash
pkg update && pkg upgrade
pkg install cmake clang make git wget
```

3.	Install llama.cpp by cloning the following GitHub Repository <be>
Note that this may take around 10-20 minutes, depending on your connection and hardware.
```bash
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp
```

4.	Build the system

```bash
mkdir build
cd build
cmake ..
cmake  - -build . - -config Release
```
5.	Make a Models folder inside Build if not available
```bash
mkdir models
cd models
```
6.	You can use any gguf models on huggingface or the models that you fine-tuned on your own (must be in gguf format). <br>
<strong>Note:</strong> The model should be less than 8B parameters to run on your phone because llama.cpp does not support running for inference using NPU. <br>
Below is an example Qwen2.5-1.5B quantized model but you can substitute it by any other gguf models. <br>
https://huggingface.co/mradermacher/DeepSeek-R1-Distill-Qwen-1.5B-i1-GGUF/resolve/main/DeepSeek-R1-Distill-Qwen-1.5B.i1-IQ1_M.gguf <br>

7.	Download the LLM to the models folder
This will download the model, it may take some time if you want to download heavier models.
```bash
wget https://huggingface.co/mradermacher/DeepSeek-R1-Distill-Qwen-1.5B-i1-GGUF/resolve/main/DeepSeek-R1-Distill-Qwen-1.5B.i1-IQ1_M.gguf
```
<br>

8.	Rename the GGUF to a short name (optional)
```bash
mv https://huggingface.co/mradermacher/DeepSeek-R1-Distill-Qwen-1.5B-i1-GGUF/resolve/main/DeepSeek-R1-Distill-Qwen-1.5B.i1-IQ1_M.gguf?download=true qwen.gguf
```
9.	Come back to build folder
a.	Since you are in models/ folder, type
```bash
cd ..
```
to come back to the build folder. <be>

10.	Serve your LLM model <br>
We use llama-server to run the UI for model's inference
```bash
./bin/llama-server –model models/qwen.gguf
```
11.	Go to localhost:8080 for testing the model <br>
The link to your local host is provided within some last lines in your terminal

## Use your own fine-tuned model
llama.cpp does provide a python file code "convert_hf_to_gguf.py" that can help you transform your own model into gguf format
For further understanding, please refer this link where you have many options <br>
https://github.com/ggml-org/llama.cpp
