# Exno.6-Prompt-Engg

### Date: 
### Register no.: 212222100059
### VARSHINI S A


# Aim: 
Development of Python Code Compatible with Multiple AI Tools

# Objective:
Design a Python-based solution that:

-Connects to multiple AI services via APIs

-Sends standardized prompts or inputs

-Collects and stores the responses

-Evaluates outputs based on quality, tone, or accuracy

-Produces reports or logs for analysis

This enables benchmarking of AI tools and helps in identifying the most suitable tool for a specific task.




# Algorithm: 
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights.

### Step 1: Define the Use Case
Choose a task that is common across AI tools, such as:

-Text summarization

-Translation

-Sentiment analysis

-Text generation

Example: Compare summarization by ChatGPT (OpenAI) and Cohere.

### Prompt:
"Write Python code that uses OpenAI and Cohere APIs to summarize a list of texts.For each text, get summaries from both APIs, analyze word count and sentiment using TextBlob, and save the combined results as a JSON file.Use environment variables for API keys and keep the code clean and well-structured."

### Step 2: Configure API Access
Register for the respective API services and store the API keys securely using environment variables:
```python
import os

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
COHERE_API_KEY = os.getenv("COHERE_API_KEY")

```
### Step 3: Define API Interaction Functions
Create functions to connect and send prompts to each AI tool:
```python
import openai
import cohere

def get_openai_summary(text):
    openai.api_key = OPENAI_API_KEY
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": f"Summarize this: {text}"}]
    )
    return response['choices'][0]['message']['content']

def get_cohere_summary(text):
    co = cohere.Client(COHERE_API_KEY)
    response = co.summarize(text=text)
    return response.summary


```

### Step 4: Provide Input Data
```python
test_inputs = [
    "Artificial intelligence (AI) is rapidly evolving and...",
    "Climate change is one of the most pressing issues..."
]


```
### Step 5: Collect and Compare Outputs
```python
results = []

for text in test_inputs:
    openai_output = get_openai_summary(text)
    cohere_output = get_cohere_summary(text)

    results.append({
        "input": text,
        "openai_summary": openai_output,
        "cohere_summary": cohere_output
    })


```
### Step 6: Analyze Outputs
```python

from textblob import TextBlob

def analyze_summary(summary):
    blob = TextBlob(summary)
    return {
        "word_count": len(summary.split()),
        "sentiment": blob.sentiment.polarity,
        "readability": blob.sentiment.subjectivity
    }

for result in results:
    result["openai_analysis"] = analyze_summary(result["openai_summary"])
    result["cohere_analysis"] = analyze_summary(result["cohere_summary"])

```

### Step 7: Generate Summary Report
```python
import json

with open("summary_comparison.json", "w") as f:
    json.dump(results, f, indent=4)


```

# Result: 
 The Python script was successfully executed to:
Connect to multiple AI tools using APIs
Send uniform prompts
Collect and compare responses using analysis metrics
Export structured reports for evaluation
