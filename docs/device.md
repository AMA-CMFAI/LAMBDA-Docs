

### **Minimum Device Configuration Requirements**



>  This section outlines the minimum hardware and software configurations required to run this framework. The requirements are divided into two scenarios based on your use case:



#### **1. Using an API Key (Recommended)**



If you have an API key for a large language model service (e.g., OpenAI, Anthropic, Google Gemini), you will not need to run the entire LLM locally. This significantly lowers the configuration requirements. Essentially, any modern laptop capable of running Python and Jupyter Notebook smoothly will suffice.

- **Operating System**:
  - Windows 7 or later
  - macOS 10.11 or later (64-bit)
  - Linux (e.g., RHEL 6/7, Ubuntu 18.04+)
- **Hardware**:
  - **RAM**: A minimum of 4 GB is recommended.
  - **Processor**: Any modern processor with a clock speed of 2 GHz or higher.
  - **Disk Space**: At least 5 GB of free space for installing Python, Jupyter, and related dependencies.

The advantage of using an API Key is its low hardware requirements, allowing you to easily leverage state-of-the-art, powerful LLMs without worrying about hardware costs and maintenance.



#### **2. Running a Large Language Model Locally (Example: Ollama)**



If you wish or need to run an LLM in your local environment, the configuration requirements will be higher, primarily depending on the size of the model you plan to run and the deployment framework you use. Using the popular [Ollama](https://ollama.com/) framework as an example, here are the minimum requirements for different model sizes (All estimates are theoretically calculated based on the minimum quantization precision, such as INT4. For a better experience, it is recommended to use a higher configuration in practice. ):

- **For running small models (e.g., 3B to 7B parameters)**:
  - **RAM**: At least 8 GB
  - **VRAM (Video RAM)**: At least 8 GB is recommended.
  - **Processor**: A modern CPU with at least 4 cores.
- **For running medium-sized models (e.g., 13B parameters)**:
  - **RAM**: At least 16 GB
  - **VRAM**: At least 16 GB is recommended.
  - **Processor**: A modern CPU with at least 8 cores.
- **For running large models (e.g., 70B parameters or larger)**:
  - **RAM**: 32 GB or more
  - **VRAM**: 24 GB or more (e.g., NVIDIA RTX 3090, 4090, or professional-grade cards).
  - **Processor**: A powerful multi-core CPU.

**Important Notes**:

- **Graphics Card (GPU)**: While some models can run in a CPU-only environment, the performance will be very slow. To achieve usable inference speeds, using a supported NVIDIA GPU is highly recommended.
- **Disk Space**: In addition to the framework itself, each model file will occupy several to tens of gigabytes of space. Please ensure you have sufficient disk capacity.

Running models locally gives you the ability to work offline and provides better control over data privacy. However, the drawbacks include high hardware costs and the need for some technical expertise for deployment and maintenance.

Here is an example config for using LAMBDA by deploying gpt-oss locally using Ollama. The detail of deploying can be find in Ollama's [documents](https://ollama.com/library/gpt-oss):

```yaml
programmer_model : "gpt-oss" 
inspector_model : "gpt-oss"
api_key : "ollama" # The API Key of ollama.
base_url_conv_model : 'http://localhost:11434/v1' # The base url of ollama
base_url_programmer : 'http://localhost:11434/v1'
base_url_inspector : 'http://localhost:11434/v1'
```



| Feature / Scenario   | Using an API Key (Recommended)  | Running LLM Locally (Ollama Example)                         |
| -------------------- | ------------------------------- | ------------------------------------------------------------ |
| **Operating System** | Windows 7+, macOS 10.11+, Linux | Windows, macOS, Linux                                        |
| **Processor (CPU)**  | Modern Processor (>= 2 GHz)     | **Small Models (3-7B):** 4+ cores <br> **Medium Models (13B):** 8+ cores <br> **Large Models (70B+):** Powerful multi-core CPU |
| **System RAM**       | 4+ GB Recommended               | **Small Models (3-7B):** 8+ GB <br> **Medium Models (13B):** 16+ GB <br> **Large Models (70B+):** 32+ GB |
| **GPU VRAM**         | N/A                             | **Small Models (3-7B):** 8+ GB Recommended <br> **Medium Models (13B):** 16+ GB Recommended <br> **Large Models (70B+):** 32+ GB |
| **Disk Space**       | 5+ GB of free space             | 5+ GB for framework + additional storage for each model      |



------



### **About the OpenAI-Style API**



The `OpenAI-Style API` has become an industry standard, referring to an interface specification that is compatible with the OpenAI API format. This standardized design has greatly facilitated the development of the Large Language Model (LLM) ecosystem by allowing developers to use a single, unified codebase to interact with a wide variety of LLMs.



#### **Why is it Important?**



By adopting the OpenAI-Style API, our framework (and many other tools) can easily "plug and play" with LLMs from various sources, whether they are official models from OpenAI or open-source models deployed locally via frameworks like Ollama, vLLM, etc. This gives developers immense flexibility to freely switch and test different models based on cost, performance, and specific needs.



#### **Model Selection Recommendations**



While the API format can be unified, the inherent capabilities of models vary greatly. This is mainly due to differences in their training data and methodologies. To get the best experience within our framework, we **strongly recommend using models that have undergone Instruction Tuning**.

These types of models are specially trained to better understand and follow user instructions. They typically possess the following advanced capabilities, which are crucial for building complex and reliable AI applications:

- **Structured Outputs**: The ability of the model to generate output in a predefined format (like JSON), which makes it easy for programs to parse and process.
- **Function Calling / Tool Use**: The model can understand when and how to use external tools or functions to retrieve information or perform actions, greatly expanding its capabilities.
- **Chain of Thought (CoT)**: The model can show its reasoning process, solving complex problems step-by-step. This not only improves the accuracy of the answer but also makes its decision-making process more transparent.

Of course, a fundamental principle applies: **the more advanced and powerful the model, the better your experience will generally be**. Newer, larger models tend to perform better at understanding complex instructions, generating high-quality content, and utilizing advanced capabilities.