# ⚠️ WIP – Work In Progress

> **🚧 WARNING: Use at Your Own Risk**
>
> This project is a **work in progress**. Things might break, behave unexpectedly, or not work at all.
>
> ⚠️ **No guarantees. No support. No refunds.**
>
> Proceed only if you're comfortable debugging on your own and willing to loose marks if this does nto work for you
>
> I am using openai/gpt-5 so your milage will vary. You can use any OpenAi compatible API with this, update your env files as you wish with your models

---



## Working Features
- Accepts file uploads including text files, images, ZIP archives, and TAR archives.
- Extracts and processes files from ZIP and TAR archives.
- Analyzes questions provided in a `questions.txt` file.
- Generates Python code to answer the questions based on the uploaded data.
- Returns the generated code and information about the processed files.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn
- OpenAI Python client
- python-dotenv

## Installation

1. Clone the repository:

```sh
git clone https://github.com/23f3004008/p2_IDK.git
cd p2_IDK
```

2. Install the required packages:

```sh
pip install fastapi uvicorn openai python-dotenv
```

3. Create a `.env` file in the root directory and add your OpenAI API key and base URL from [OpenAI Platform](https://platform.openai.com/docs/overview):

```env
OPENAI_API_KEY=your_openai_api_key
OPENAI_BASE_URL=your_openai_base_url
LLM_MODEL=your_llm_model
```

## Usage

1. Run the FastAPI application:

```sh
uvicorn main:app --host 0.0.0.0 --port 8000
```

2. Send a POST request to the `/api/` endpoint with the necessary files and questions. The `questions.txt` file is required.

Example using `curl`:

```sh
curl "http://127.0.0.1:8000/api/" -F "questions.txt=@questions.txt"
```

## API Endpoint

- **POST /api/**: Upload files and get the generated Python code to answer the questions.

## Response

The API returns a JSON response with the following structure:

```json
{
  "files_processed": {
    "questions.txt": {
      "filename": "questions.txt",
      "content_preview": "Preview of the questions content..."
    },
    "data.zip": {
      "filename": "data.zip",
      "extracted_files": [
        {
          "filename": "file1.csv"
        },
        {
          "filename": "file2.csv"
        }
      ]
    }
  },
  "generated_code": "# Generated Python code to answer the questions..."
}
```


- The API expects the `questions.txt` file to be included in the request.
- The generated Python code is designed to be executable and will print the final answers to standard output.
- If the question requires creating a plot or image, the code will save it to a file and print its base64 data URI to standard output.
