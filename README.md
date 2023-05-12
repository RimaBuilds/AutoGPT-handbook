# Autogpt: A  Guide to Prompt Engineering
Auto-GPT is an open-source AI tool that leverages the GPT-4 or GPT-3.5 APIs from OpenAI to accomplish user-defined objectives expressed in natural language. It does this by dissecting the main task into smaller components and autonomously utilizing various resources in a cyclic process.

In this guide, we'll explore the various features of Autogpt and outline the best practices and tips for utilizing Autogpt for coding. 

## Table of content 

- [Installation Guide to Autogpt](#-installation-guide-to-autogpt)
    - [API needed for Autogpt](#-api-needed-for-autogpt)
    - [Changes When Cloning The Github Repository](#-changes-when-cloning-the-github-repository)
- [Prompt Engineering Guide](#-prompt-engineering-guide)
- [Best Ways for Prompt Engineering](#-best-ways-for-prompt-engineering)    
     1. [Use Autogpt to execute code](#1-use-autogpt-to-execute-code)
     2. [Use Autogpt to execute shell](#2-use-autogpt-to-execute-shell)
     3. [Use Autogpt to analyze code](#3-use-autogpt-to-analyze-code)
     4. [Use Autogpt to improve code](#4-use-autogpt-to-improve-code)
     5. [Use Autogpt to generate documentation](#5-use-autogpt-to-generate-documentation)
     6. [Use Autogpt for debugging](#6-use-autogpt-for-debugging)
     7. [Use Autogpt for searching google](#7-use-autogpt-for-searching-google)
     8. [Use Autogpt for web scraping](#8-use-autogpt-for-web-scraping)
     9. [Use Autogpt for searching files](#9-use-autogpt-for-searching-files)
     10. [Use Autogpt for github cloning](#10-use-autogpt-for-github-cloning)
- [Best Use of Autogpt in Coding and Debugging Guide](#-best-use-of-autogpt-in-coding-and-debugging-guide)
- [Conclusion](#-conclusion)

## 🚀 Installation Guide to Autogpt

1. To install autogpt, we need to first clone the  [Github repository](https://github.com/Significant-Gravitas/Auto-GPT/releases/latest). 
2. you can find the latest version here:  https://github.com/Significant-Gravitas/Auto-GPT/releases/latest.
3. You can clone the repo using the command `git clone https://github.com/significant-gravitas/auto-gpt.git` on your terminal or by clicking on the "Code" button on the repository page and downloading the zip file.
4. follow the insallation guide from the auto-gpt repo  [installation guide](https://docs.agpt.co/setup/)
5. Verify that the installation was successful by running the command `autogpt --version`. You should see the version number displayed in the terminal.

You can also use a virtual environment to contain the installation of Autogpt, and to ensure you do not run into any errors when installing dependencies or running autogpt.

### 📌 API needed for Autogpt
Make sure to update '.env' with your own configurations and your own api keys. The file contains every api that you may need. you can ommit some if u wont use them such as for image generation however make sure you have: 

- **OpenAI API key**- this key is required to use the OpenAI API which autogpt is built on top of. You can get an API key by signing up for the OpenAI API program:

- **GITHUB_API_KEY**- this key is required to authorize your access to the GITHUB API. You can get this key by following the steps on the github website.
- your **GITHUB_USERNAME**

you can add all the apis here. the '.env' is self explanatory
Once you have obtained these keys, you need to edit the `.env` file in the repository and add the API keys listed above.

also pay attention to the below:
- **Allow local command execution** by changing to true if you want it to execute commands locally
- **Restrict to Workspace** - if you dont want to restrict it to workspace folder, change to false

### 📝 Changes When Cloning The Github Repository

1. You need to edit the `.env` file in the repository and add the API keys listed above. This is because the API keys are sensitive information that should not be hardcoded into the application. 

2. You also need to add your own prompts to the `prompts.json` file to make autogpt more useful for your particular use case. The prompts provided in the repository are general prompts that may not be applicable to your project. By adding your own prompts, you can train autogpt to generate responses that are tailored to your specific use case.

## 💻 Prompt Engineering Guide

1. To prompt autogpt, use the command `python -m autogpt` in your terminal. Make sure you are in the right path. if not, set it by ' cd Path'

2. For best results, make sure your prompts are specific and well-defined. This will give autogpt a clear understanding of what you are trying to achieve and help it generate more accurate responses.

3. When reviewing the model's responses, keep in mind that autogpt is a language model and not a human. As such, it may generate responses that are not entirely accurate or suitable for your use case. It is up to you to review the responses and make any necessary modifications.

4. Another way to use autogpt is by integrating it into your code. You can have a look at commands in the cloned folder and use it to generate responses programmatically. This can be useful if you want to generate responses in a specific context.

## 🔥 Best Ways for Prompt Engineering
Here are some of the best ways to use Autogpt for prompt engineering:

### 1. Use Autogpt to execute code:

The `@command` decorator is used to define custom commands. It takes three arguments:

- `name`: The name of the command.
- `description`: A brief description of the command.
- `params`: A string representing the expected parameters for the command.

Here's an example of using the `@command` decorator to define a custom command called `execute_python_file`:

```python
@command("execute_python_file", "Execute Python File", '"filename": "<filename>"')
def execute_python_file(filename: str) -> str:
    # Implementation of the command
```
### 2. Use Autogpt to execute shell

To execute shell commands, you can use the `subprocess` module. Here are two methods for running shell commands:

#### a) Using `subprocess.run()`:

This method runs the command and waits for it to complete. It returns the output (stdout and stderr) of the command.

```python
result = subprocess.run(command_line, capture_output=True, shell=True)
output = f"STDOUT:\n{result.stdout}\nSTDERR:\n{result.stderr}"
```

##### b) Using `subprocess.Popen()`:

This method launches the command as a separate process and returns immediately. It can be useful for running non-blocking commands.

```python
process = subprocess.Popen(
    command_line, shell=True, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL
)
return f"Subprocess started with PID:'{str(process.pid)}'"
```

To create a custom command that executes shell commands, you can use the `@command` decorator along with the `subprocess` methods:

```python
@command("execute_shell", "Execute Shell Command", '"command_line": "<command_line>"')
def execute_shell(command_line: str) -> str:
    result = subprocess.run(command_line, capture_output=True, shell=True)
    output = f"STDOUT:\n{result.stdout}\nSTDERR:\n{result.stderr}"
    return output
```

### 3. Use Autogpt to analyze code:

The `analyze_code` module is designed to analyze a given code snippet and provide suggestions for improvements. 
It uses the `@command` decorator to define a custom command called `analyze_code`. 
The function takes a string containing the code to be analyzed and returns a list of suggestions.

Here's a simplified explanation of the code:

- Define the `analyze_code` function with the `@command` decorator:

```python
@command("analyze_code", "Analyze Code", '"code": "<full_code_string>"')
def analyze_code(code: str) -> list[str]:
```

- Set up the function string, arguments, and description string for the AI function call:

```python
function_string = "def analyze_code(code: str) -> list[str]:"
args = [code]
description_string = (
    "Analyzes the given code and returns a list of suggestions for improvements."
)
```

-  Call the AI function to analyze the code and return suggestions:

```python
return call_ai_function(function_string, args, description_string)
```

### 4. Use Autogpt to improve code:

The `improve_code` function is designed to improve a given code snippet based on a list of provided suggestions. It uses the `@command` decorator to define a custom command called `improve_code`. The function takes a list of suggestions and a string containing the code to be improved, and it returns a new code string with the suggested improvements applied.

Here's a simplified explanation of the code:

- Define the `improve_code` function with the `@command` decorator:

```python
@command("improve_code", "Get Improved Code", '"suggestions": "<list_of_suggestions>", "code": "<full_code_string>"')
def improve_code(suggestions: list[str], code: str) -> str:
```

- Set up the function string, arguments, and description string for the AI function call:

```python
function_string = "def generate_improved_code(suggestions: list[str], code: str) -> str:"
args = [json.dumps(suggestions), code]
description_string = (
    "Improves the provided code based on the suggestions"
    " provided, making no other changes."
)
```

- Call the AI function to improve the code and return the improved version:

```python
return call_ai_function(function_string, args, description_string)
```

To use the `improve_code` function, pass a list of suggestions and a string containing the code snippet you want to improve:

```python
suggestions = [
    "Replace the print statement with a return statement.",
    "Add type hints to the function."
]

code_to_improve = '''
def some_function():
    print("Hello, World!")
'''

improved_code = improve_code(suggestions, code_to_improve)
print(improved_code)
```
The `improve_code` function will then call the AI function, which in turn uses the OpenAI API to apply the suggested improvements to the code and generate a new, improved version of the code. Note that the quality of the improvements depends on the language model's understanding of the suggestions and its ability to apply them correctly.

### 5. Use Autogpt to generate documentation:
   ```
   prompt = "Generate documentation for the function 'Function name'"

   generator =   response = openai.Completion.create(
            engine=engine,
            prompt=prompt,
            max_tokens=150,
            n=1,
            stop=None,
            temperature=1.2,
            presence_penalty=0.5,
            frequency_penalty=0.5,
        )
   ```

### 6. Use Autogpt for debugging:

use the `improve_code` function for debugging, you can follow the steps below:

- Identify the issues or bugs in your code. You can do this manually, or you can use tools like linters, static analyzers, or debuggers to help pinpoint the issues.

- Create a list of suggestions based on the identified issues. Each suggestion should describe how to fix a specific issue or bug in the code.

- Call the `improve_code` function, passing the list of suggestions and the code snippet with issues as arguments:

```python
suggestions = [
    "Fix the IndexError by using a conditional statement.",
    "Handle the ZeroDivisionError exception."
]

buggy_code = '''
def buggy_function(a, b):
    result = a / b
    return result

def another_buggy_function(lst):
    return lst[0]
'''

improved_code = improve_code(suggestions, buggy_code)
print(improved_code)
```

-  Review the improved code returned by the `improve_code` function. Make sure the AI-generated improvements align with your suggestions and correctly fix the identified issues. Verify that the improved code works as expected.

### 7. Use Autogpt for searching google
   ```
- Choose the search function: `google_search` for DuckDuckGo or `google_official_search` for the official Google API.

- Call the chosen function with your search query:

```python
query = "example search query"
num_results = 5

# Perform the search using DuckDuckGo
search_results = google_search(query, num_results)
print(search_results)

# Or, perform the search using the official Google API
# search_results = google_official_search(query, num_results)
# print(search_results)
```

The function returns a list of search result URLs that match the given query.
make sure you have the google api saved in secrets.json


### 8. Use Autogpt for web scraping

Call the `browse_website` function with the URL of the website you want to scrape and a question related to the content you're looking for:

```python
url = "https://example.com"
question = "What is the main purpose of the website?"

answer_and_links = browse_website(url, question)
print(answer_and_links)
```

The `browse_website` function uses `scrape_text_with_selenium` to scrape the text content of the website and `scrape_links_with_selenium` to extract the links. 

### 9. Use Autogpt for searching files

 - Call the `list_files` function with the directory you want to search:

```python
directory = "path/to/directory"
all_files = list_files(directory)
```

- Filter the results based on the file name or any other criteria you want to use:

```python
search_criteria = "example"
matching_files = [file for file in all_files if search_criteria in file]
print(matching_files)
```

In this example, `matching_files` will contain a list of all files in the specified directory (and its subdirectories) that have the `search_criteria` string in their names. Modify the filtering condition as needed to match your specific search requirements.

### 10. Use Autogpt for github cloning:

Autogpt has a function `clone_repository` that allows you to clone a Git repository from a given URL to a local directory on your machine. To prompt it for input and clone a Git repository using the `clone_repository` function, follow these steps:

- input the repo URL and clone path

```python
repo_url = "repository URL"
clone_path = "the path to clone the repository"
```

- Call the `clone_repository` function with the provided URL and path:

```python
result = clone_repository(repo_url, clone_path)
```

This code calls the `clone_repository` function, which clones the repository using the provided GitHub authentication credentials from the `Config` object.

## ✨ Best Use of Autogpt in Coding and Debugging Guide

1. Use autogpt to generate descriptive comments for your code automatically. This can help make your code more readable and easier to understand, especially for team members who may not be familiar with the codebase.

2. Use autogpt to generate boilerplate code for your project. For example, you can use autogpt to generate code for setting up logging, creating configuration files, or initializing the database.

3. Use autogpt to generate test cases for your code. This can help ensure that your code is working as expected and that any changes you make to the code do not introduce new bugs.

4. Use autogpt to generate documentation for your project. Autogpt can generate API documentation, user guides, and other types of documentation automatically, saving you time and effort.

## 📘 Conclusion
Autogpt is a powerful tool that can help you in coding and prompt engineering. It can generate code snippets, check code syntax, improve code, generate test cases, generate documentation and execute python files. By using Autogpt, you can save time and increase productivity.
