# Website Analyzer and Brochure Generator

A Python script that analyzes websites and generates marketing brochures using AI. This tool can scrape website content, extract links, and create professional brochures for businesses.

## Features

- **Website Content Analysis**: Extracts and summarizes website content
- **Link Extraction**: Finds and categorizes all links on a website
- **AI-Powered Brochure Generation**: Creates marketing brochures using Ollama AI
- **Streaming Response**: Real-time generation with live updates
- **Flexible Input**: Works with any website URL

## Requirements

```python
pip install requests beautifulsoup4 IPython
```

You'll also need:
- Ollama installed locally (running on `localhost:11434`)
- A compatible model (script uses "llama3.2")

## Code Structure

### Cell 1: Import and Configuration
```python
import json, requests
from bs4 import BeautifulSoup
from IPython.display import Markdown, display
```

Sets up the required libraries and defines:
- `OLLAMA_API`: Local Ollama API endpoint
- `HEADERS`: HTTP headers for web requests
- `MODEL`: AI model name for text generation

### Cell 2: Simple Chat Function
```python
def simple_chat(message, model="llama3.2"):
```

Basic function to communicate with Ollama AI:
- Sends messages to the AI model
- Returns AI responses
- Handles network and JSON parsing errors

### Cell 3: User Prompt Generator
```python
def user_prompt_for(website):
```

Creates dynamic prompts for website analysis:
- Takes website object as input
- Generates contextual instructions for AI
- Includes website content and specific formatting requirements

### Cell 4: Website Class
```python
class Website:
```

Main class for website analysis with methods:
- `__init__(self, url)`: Initializes with URL and fetches content
- `get_contents(self)`: Returns formatted website information

**Key features:**
- Fetches website content using requests
- Parses HTML with BeautifulSoup
- Extracts title, body text, and links
- Removes script, style, and input tags for cleaner content
- Handles missing titles gracefully

### Cell 5: Testing Basic Functionality
```python
ed = Website("https://edwarddonner.com")
```

Tests the Website class:
- Creates instance for Edward Donner's website
- Displays extracted links
- Shows various website URLs found

### Cell 6: Summarization Function
```python
def summarize(url):
```

Complete website summarization workflow:
- Creates Website instance
- Generates appropriate user prompt
- Gets AI summary using simple_chat
- Returns formatted response

### Cell 7: Testing Summarization
```python
result = summarize("https://www.google.com")
```

Demonstrates the summarization feature:
- Analyzes Google's website
- Shows structured markdown output with sections like:
  - Overview of services
  - News/Announcements
  - Language Options
  - Notable Features

### Cell 8: Link System Prompt
```python
link_system_prompt = "You are provided with a list of links..."
```

Defines AI instructions for link analysis:
- Explains how to categorize links
- Provides JSON response format
- Gives examples of link classification

### Cell 9: Link Analysis Functions
```python
def get_links_user_prompt(website):
def get_links(url):
```

Functions for extracting and analyzing website links:
- `get_links_user_prompt`: Creates prompts for link analysis
- `get_links`: Full pipeline for link extraction and AI analysis
- Returns structured JSON with link categories

### Cell 10: Link Analysis Testing
```python
print(get_links_user_prompt(ed))
```

Tests link analysis functionality:
- Shows the generated prompt for Edward Donner's website
- Demonstrates link categorization format

### Cell 11: Advanced Link Extraction
```python
huggingface = Website("https://huggingface.co")
```

Tests with HuggingFace website:
- More complex website with many links
- Shows comprehensive link extraction
- Demonstrates scalability

### Cell 12: Complete Website Analysis
```python
def get_all_details(url):
```

Comprehensive analysis function:
- Combines content summary and link analysis
- Returns complete website profile
- Useful for thorough website understanding

### Cell 13: Brochure Generation System
```python
system_prompt = "You are an assistant that analyzes..."
def get_brochure_user_prompt(company_name, url):
def create_brochure(company_name, url):
```

Professional brochure generation:
- Takes company name and website URL
- Creates marketing-focused content
- Generates structured brochures for business use
- Includes company culture, customers, and career information

### Cell 14: Streaming Brochure Generation
```python
def stream_brochure(company_name, url):
```

Enhanced version with real-time streaming:
- Shows generation progress live
- Uses streaming API for better user experience
- Processes response chunks in real-time
- Displays formatted markdown output

## Usage Examples

### Basic Website Summary
```python
summary = summarize("https://example.com")
display(Markdown(summary))
```

### Link Analysis
```python
links = get_links("https://example.com")
print(json.dumps(links, indent=2))
```

### Generate Business Brochure
```python
brochure = create_brochure("Company Name", "https://company.com")
display(Markdown(brochure))
```

### Streaming Brochure Generation
```python
result = stream_brochure("Company Name", "https://company.com")
```

## Error Handling

The script includes robust error handling for:
- Network connection issues
- Invalid URLs
- JSON parsing errors
- Missing website elements
- AI API communication problems

## Customization

You can customize:
- **AI Model**: Change the `MODEL` variable to use different Ollama models
- **Prompts**: Modify system and user prompts for different analysis styles
- **Output Format**: Adjust markdown formatting and structure
- **Website Parsing**: Modify the Website class for specific content extraction needs

## Tips for Best Results

1. **Ensure Ollama is Running**: Make sure Ollama is installed and running locally
2. **Model Selection**: Choose appropriate models based on your needs (llama3.2 works well)
3. **Website Accessibility**: Some websites may block automated requests
4. **Content Quality**: Results depend on the quality and structure of the target website
5. **Prompt Engineering**: Adjust prompts for better results with specific website types

## Troubleshooting

- **Connection Errors**: Check if Ollama is running on localhost:11434
- **Empty Results**: Some websites may have anti-scraping protection
- **Slow Performance**: Large websites may take longer to process
- **JSON Errors**: AI responses might occasionally be malformed

This tool is perfect for market research, competitive analysis, and automated content generation for business development.