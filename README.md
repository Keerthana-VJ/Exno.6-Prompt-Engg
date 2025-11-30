# Exno.6-Prompt-Engg
### NAME: KEERTHANA V
### REG NO: 212223220045
# Aim: Development of Python Code Compatible with Multiple AI Tools
To develop Python code that integrates with multiple AI tools via APIs, automates interaction, compares outputs, and generates actionable insights. This helps benchmark AI tools and determine the best one for a given task or use case.


# Algorithm: 
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights.

Step 1: Define the Use Case
Select a specific AI task to compare multiple tools (e.g., summarization, translation, sentiment analysis).
Example: Compare summarization capabilities of OpenAI’s ChatGPT and Cohere.

Step 2: Set Up API Access

Register for API keys for the chosen services.

Store keys securely using environment variables.

```python
import os

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
COHERE_API_KEY = os.getenv("COHERE_API_KEY")
```

Step 3: Write API Interaction Functions
Create functions to send standardized prompts and return outputs.

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

Step 4: Prepare a Prompt Dataset
Create a list of sample texts to be summarized by both tools.

```python
test_inputs = [
    "Artificial intelligence (AI) is rapidly evolving and...",
    "Climate change is one of the most pressing issues..."
]
```

Step 5: Collect and Compare Outputs
Loop through test inputs, gather results from both APIs, and store them.

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

Step 6: Generate Actionable Insights
Apply simple analysis such as word count, sentiment, or readability.

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

Step 7: Generate a Report
Export the comparative findings to a JSON file.

```python
import json

with open("summary_comparison.json", "w") as f:
    json.dump(results, f, indent=4)
```

# Conclusion:

This experiment shows how Python can integrate multiple AI tools to automate benchmarking and comparison. The approach helps identify the best-performing model for a given task, supports data-driven decision-making, and enhances productivity by combining model strengths. The system is flexible and scalable, making it applicable to tasks like multi-tool chatbots, creative workflows, research evaluation, and enterprise AI benchmarking.


# Result: 
The corresponding Prompt is executed successfully
