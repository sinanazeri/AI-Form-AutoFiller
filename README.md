# AI-Form-AutoFiller
This project automates form-filling using LLM. It processes documents, extracts necessary information, and then intelligently fills out HTML forms based on this data. We use LLAMA2 hosted by IBM Watson's language model for text analysis and a Flask web app for easy access. The system efficiently handles form fields, streamlining the form-filling process with minimal manual input.


I hate forms, and they're everywhere—applying for a loan, a job, a visa, or funding. They waste so much time, even though the information is just sitting there (in the local storage). Our time is wasted just reading information and putting it into a form. In fact, the vast majority of government jobs involve form-filling. Workers read some information and fill out another form, and this process takes months and even years. What if we implemented AI that could read all the required information and automatically fill the forms and their fields, instantly and accurately?
well, this project does that. 

In this project, we use a simple tax form to showcase an AI form filler. We've provided a PDF with information about an imaginary person. The project reads the form fields and the AI fills them in, accordingly.


![](AI_form_fill.gif)

Here is the schema how it works:
![image](https://github.com/sinanazeri/AI-Form-AutoFiller/assets/121966646/8226f2d2-6c92-4c2d-a115-75618bb55f1d)


### Stage 1: Setting Up the Environment
**Why**: This stage involves preparing your Python environment with necessary libraries and configurations. It's essential for accessing IBM Watson's AI services and other functionalities needed in the project.
**How**:
- **Import Libraries**: Import libraries like `ibm_watson_machine_learning` for AI model integration, and `BeautifulSoup` for parsing HTML content.
- **API and Project IDs**: Initialize variables for API key and Project ID. These are crucial for authenticating and accessing IBM Watson's services. Alternatively, we can use OpenAI GPT models or any model available in huggingface.
**Code Snippet**:
```python
from ibm_watson_machine_learning.foundation_models.extensions.langchain import WatsonxLLM
# Other imports...
Watsonx_API = "YOUR_API_KEY"
Project_id= "YOUR_PROJECT_ID"
# or use OpenAI GPT models 
```

### Stage 2: Initializing the AI Model
**Why**: This step configures and initializes the AI model which will be used later to generate responses for form filling.
**How**:
- **Set Parameters**: Define parameters like `MAX_NEW_TOKENS` and `TEMPERATURE` which control the AI's text generation behavior.
- **Initialize Model**: Create an instance of the `WatsonxLLM` class with the provided model ID, credentials, and parameters.
**Code Snippet**:
```python
def get_llm():
    # Configuration parameters and credentials
    # ...
    llm = WatsonxLLM(model=LLAMA2_model)
    return llm
```

### Stage 3: Data Processing
**Why**: Processing the data involves loading, splitting, and indexing documents, making them searchable and retrievable for the AI model.
**How**:
- **Load Documents**: Use `PyPDFDirectoryLoader` to load PDF files from a directory.
- **Split Texts**: `RecursiveCharacterTextSplitter` splits the documents into smaller chunks for easier processing.
- **Create Index**: Use `FAISS` to create an index of these chunks, which allows efficient text retrieval later.
**Code Snippet**:
```python
def process_data():
    loader = PyPDFDirectoryLoader("info")
    # ...
    return db
```

### Stage 4: Form Field Identification
**Why**: To automate form filling, you first need to know what fields are present in the form and their characteristics.
**How**:
- **Parse HTML**: Read the HTML file and use `BeautifulSoup` to parse it.
- **Extract Form Fields**: Identify form elements like input boxes, dropdowns, and text areas, and extract their labels and IDs for identification.
**Code Snippet**:
```python
def get_form_field_descriptions(html_file_path):
    # ...
    return field_info
```

### Stage 5: Generating Responses
**Why**: This stage is where the AI model is utilized to fill in the form based on the content of the loaded documents.
**How**:
- **Retrieve Model and Data**: Call `get_llm()` and `process_data()` to get the AI model and processed data.
- **Generate Prompts and Responses**: For each form field, create a specific prompt and use the AI model to generate a corresponding response.
**Code Snippet**:
```python
def filling_form(form_fields_info):
    # ...
    return structured_responses
```

### Stage 6: Deploying the Web Server
**Why**: The web server acts as an interface between the user and the AI form filler, allowing users to access the functionality via API calls.
**How**:
- **Setup Flask**: Create a Flask app and configure CORS for cross-origin requests.
- **Create API Endpoint**: Define a route in Flask that will be called to get the filled form data.
- **Run Server**: Start the Flask server to make the API accessible.
**Code Snippet**:
```python
app = Flask(__name__)
CORS(app)

@app.route('/api/get_tax_form_data', methods=['GET'])
def get_tax_form_data():
    # ...
    return jsonify(response_data)

if __name__ == '__main__':
    app.run(debug=True, port=5055)
```

### Conclusion
Each stage builds upon the previous, creating a pipeline that goes from setting up the environment to deploying a server that provides AI-generated form data. This project offers a practical application of AI in automating tasks, integrating various tools and technologies. It's an excellent example for beginners to understand how different pieces of a project come together to create a functional AI application.

