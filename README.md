# lp1-cgo-lab1 **Granite Model Code Generation Lab in Google Colab**
Code Generation using IBM Granite Code

## Purpose
This lab provides guidance on using the IBM Granite Code base model on Google Colab to generate Jupyter Notebook `ipywidgets`-based UI components for an online bookstore. It demonstrates the use of various prompting techniques—Zero-Shot, Few-Shot, and Chain of Thought (CoT)—to refine code generation quality progressively.

## Prerequisites
- **Basic Knowledge of Python**: Familiarity with Python, especially `ipywidgets` in Jupyter Notebook, is recommended.
- **Replicate Account**: An account with Replicate for model inference calls.
- **REPLICATE_API_TOKEN**: Obtain an API token from Replicate, which will be stored as a Google Colab secret.

## Introduction
The [IBM Granite model cookbook on GitHub](https://github.com/ibm-granite-community/granite-kitchen) provides code-generation examples for various applications, including SQL, shell scripts, and UI design. This lab focuses on generating `ipywidgets`-based UI components for an online bookstore. Starting with Zero-Shot prompts, it progresses through Few-Shot examples and Chain of Thought to demonstrate prompt refinement.

## Model Overview
The lab uses the IBM Granite Code model hosted on Replicate to generate Python code that integrates `ipywidgets` for creating a bookstore UI. The generated code offers a customizable framework for real-world applications, highlighting the power of advanced prompt engineering in practical projects.

---

## Setting Up Google Colab

### Step 1: Set Up a Replicate Account
1. Create an account at [Replicate](https://replicate.com/).
2. Obtain your API token from Replicate.

### Step 2: Set Up REPLICATE_API_TOKEN and Configure the Colab Workspace
1. In Google Colab, go to “Secrets” on the left-hand panel.
2. Click on “Add new secret” and name it `REPLICATE_API_TOKEN`.
3. Paste your Replicate token into the value field.

```bash
# Install required packages
!pip install git+https://github.com/ibm-granite-community/utils \
            "langchain_community<0.3.0" \ 
            replicate
```

```python
# Initilize the Replicate & Colab Libraries

from ibm_granite_community.notebook_utils import get_env_var
from langchain_community.llms import Replicate
 
# Configure and load the IBM Granite model for code generation
model = Replicate(
    model="ibm-granite/granite-8b-code-instruct-128k",
    replicate_api_token=get_env_var('REPLICATE_API_TOKEN'),
    model_kwargs={"max_length": 100, "temperature": 0.2},
)
```