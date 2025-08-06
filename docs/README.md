# LAMBDA Docs

> This is the official document of LAMBDA - Multi-Agent Data Analysis System



# Quick Start

### Basic Requirements

> Basically, you should fulfill the [minimum requirements of the devices](device.md) to run Python. You should have Python with a version greater than 3.10 on your device.  If you already have it, you can skip this section. 

#### **Python Installation for Windows Users**

1. **Download the Installer**: Visit the [official Python downloads page](https://www.python.org/downloads/).

2. **Select a Version**: Find Python 3.10 and click "Download." Choose the "Windows installer" that matches your system (64-bit or 32-bit).

3. Run the Installer:

   - Double-click the downloaded `.exe` file.
   - **CRITICAL STEP**: At the bottom of the installer window, **check the box for "Add Python 3.x to PATH."** This automatically adds Python to your system's environment variables, allowing you to run it from any terminal.
   - Click "Install Now" for the default installation.

4. Verify the Installation: Once finished, open Command Prompt (CMD) or PowerShell and type the following command:

   ```
   python --version
   ```

   If you see the output below, the installation was successful.

   ```
   Python 3.10.x
   ```

    

#### **Python Installation for macOS Users**

macOS often includes an older, pre-installed version of Python. It's best to install a newer, cleaner version.

1. Install from the Official Website (Recommended):

   - Go to the [Python downloads page for macOS](https://www.python.org/downloads/macos/).
   - Download the "macOS 64-bit universal2 installer" for the latest version of Python 3.10.
   - Run the downloaded `.pkg` file and follow the installation prompts.

2. Install with Homebrew:

   - If you don't have Homebrew, install it from the [official Homebrew website](https://brew.sh/).

   - Open the Terminal app and run the following command:

     ```
     brew install python@3.10
     ```

3. Verify the Installation: Open a new Terminal window and type:

   ```
   python3 --version
   ```

   Seeing the version number confirms the installation. Note that on macOS and Linux, you typically use 

   ```
   python3
   ```

    to invoke the newly installed version.

#### **Python Installation For Linux Users**

Most Linux distributions (like Ubuntu) come with Python pre-installed. You can use the system's package manager to install or update it.

1. Open your terminal.

2. Update your package list:

   ```
   sudo apt update
   ```

3. Install Python 3.10:

   ```
   sudo apt install python3.10
   ```

4. Verify the Installation: In the terminal, type:

   ```
   python3.10 --version
   ```

   Seeing the corresponding version number means you're all set.

> Next, we will install and configure the LAMBDA system.

### LAMBDA Installation

With Python ready, you can now set up the LAMBDA environment.

#### Step 1: Clone the Repository

First, open your terminal, and use `git` to clone the LAMBDA repository to your local machine:

```
git clone https://github.com/AMA-CMFAI/LAMBDA.git
cd LAMBDA
```

#### Step 2: Create and Activate a Conda Environment (Optional)

Using a Conda environment is highly recommended to avoid package conflicts. If you don't have it, search for and install "Anaconda" or "Miniconda".

```bash
# Create a new environment named "lambda" with Python 3.10
conda create -n lambda python=3.10

# Activate the environment
conda activate lambda
```

Or, you can also create a virtual environment by Python:

```
# Create a new environment named "lambda"
python3 -m venv lambda

# Activate the environment
source venv/bin/activate
```

#### Step 3: Install Dependencies

Inside the LAMBDA project directory, you'll find a `requirements.txt` file listing all necessary Python libraries. Install them using `pip`:

```
pip install -r requirements.txt
```

#### Step 4: Install the Jupyter Kernel

LAMBDA uses Jupyter as its code interpreter. To ensure the project can call it correctly, install a local Jupyter kernel:

```
ipython kernel install --name lambda --user
```

### LAMBDA Configuration

After setting up the environment, the next crucial step is to configure the `config.yaml` file. This file acts as LAMBDA's control center, managing API keys, model selection, and working paths.

> There are two methods to use Large Language Models. First, buy an API Key from the providers. Second, deploy LLMs on your machine. We give an example of both methods.

#### 1. Obtaining API Keys

To use Large Language Models, you will need API keys from their respective providers. Below are some example providers you can use:

- [**OpenAI**](https://openai.com/api/pricing) 
- **[DeepSeek](https://api-docs.deepseek.com/zh-cn/quick_start/pricing)**
- **[OpenRouter](https://openrouter.ai/)**(free trial credits)
- **[SILICONFLOW](https://siliconflow.cn/)** (free trial credits)

Sign up to get your personal API key.

#### 2. Deploying LLMs on Your Machine

We support the OpenAI style interface. You can use any framework to deploy and use the LLMs if it supports the OpenAI style interface.

Here are some popular tools to use:

- [**Ollama**](https://ollama.com/)
- [**LLaMA-Factory**](https://github.com/hiyouga/LLaMA-Factory)
- [**LiteLLM**](https://docs.litellm.ai/docs/)

#### Modifying the `config.yaml` File

Find the `config.yaml` file in the root of the LAMBDA directory and open it with a text editor. You will need to modify the following sections:

```
#================================================================================================
#                                       Config of the LLMs
#================================================================================================
conv_model : "gpt-4.1-mini" # Choose the model you want to use. We highly recommned using the advanced model.
programmer_model : "gpt-4.1-mini" 
inspector_model : "gpt-4.1-mini"
api_key : "sk-xxxxxxx" # The API Keys you buy.
base_url_conv_model : 'https://api.openai.com/v1' # The base url from the provider.
base_url_programmer : 'https://api.openai.com/v1'
base_url_inspector : 'https://api.openai.com/v1'


#================================================================================================
#                                       Config of the system
#================================================================================================
streaming : True
project_cache_path : "cache/conv_cache/" # Local cache path
max_attempts : 5 # The max attempts of self-correcting
max_exe_time: 18000 # The maximum time for the execution

#knowledge integration
retrieval : False # Whether to start a knowledge retrieval. If you don't create your knowledge base, you should set it to False
```

If you have LLMs locally, for example, deployed by the [Ollama](https://ollama.com/):

From the documents:https://ollama.com/blog/openai-compatibility, you will find the corresponding configuration of base_url and api_key.

Here, the base_url is 'http://localhost:11434/v1', and api_key is 'ollama'

So the config should be:

```
conv_model : "deepseek-r1" # The model you deployed. We highly recommned using the advanced model.
programmer_model : "deepseek-r1" 
inspector_model : "deepseek-r1"
api_key : "ollama" # The API Key of ollama.
base_url_conv_model : 'http://localhost:11434/v1' # The base url of ollama
base_url_programmer : 'http://localhost:11434/v1'
base_url_inspector : 'http://localhost:11434/v1'
```

### Get Started!

Congratulations! After completing these steps, you can run LAMBDA with the following command:

```
python lambda_app.py
```

We hope this detailed guide helps you get started smoothly with LAMBDA. If you encounter any issues during setup, feel free to consult the official GitHub repository for more information.

------

**Official Repository Link:** https://github.com/AMA-CMFAI/LAMBDA

