# OCRBill

This repository contains a Jupyter Notebook (`LLM_Ngok_API.ipynb`) designed to perform Optical Character Recognition (OCR) on bills and invoices using a Vision-Language Model (VLM), and expose the functionality via an API.

## Features

- **Advanced OCR using LLM:** Utilizes the `5CD-AI/Vintern-1B-v2` model from Hugging Face for powerful and accurate extraction of tabular data from bills and invoices.
- **Dynamic Image Preprocessing:** Includes robust image preprocessing to handle various aspect ratios and image resolutions gracefully.
- **Flask API:** Wraps the model in a Flask web service with a `/ocr` POST endpoint.
- **Public API Exposure:** Uses `pyngrok` to tunnel the local Flask server to a public URL automatically, making it ideal for testing on Google Colab and exposing the API to external clients.

## Requirements

The core dependencies for this project are listed below:

- `transformers`
- `bitsandbytes`
- `huggingface_hub`
- `flask`
- `flask-cors`
- `pyngrok`
- `flash_attn`
- `torch`
- `torchvision`
- `numpy`
- `Pillow`
- `requests`

## Usage (Google Colab Recommended)

The notebook is configured to run smoothly on Google Colab, utilizing its free GPUs.

1. **Open on Google Colab:** Upload the `LLM_Ngok_API.ipynb` file to your Google Colab workspace or open it directly.
2. **Configure Ngrok Token:** 
   - Sign up or log into [ngrok.com](https://ngrok.com/).
   - Copy your Authentication Token.
   - Go to Google Colab -> Secrets (the key icon in the left sidebar) and add a new secret named `ngrok_token` with your token value.
   - Toggle the "Notebook access" switch to allow the notebook to read the secret.
3. **Run the Cells:** Execute the cells sequentially. Ensure that your runtime type is set to **GPU** (e.g., T4 GPU).
4. **Access the API:** The final cell will start the Flask server and provide a public `ngrok.io` URL. 

### API Endpoint

- **Endpoint:** `POST /ocr`
- **Body structure (JSON):**
  ```json
  {
    "image_url": "URL_TO_YOUR_INVOICE_IMAGE"
  }
  ```
- **Response Structure (JSON):**
  ```json
  {
    "response_message": "Extracted text as a CSV/Markdown table format"
  }
  ```

## Model Information
This project relies on the **[Vintern-1B-v2](https://huggingface.co/5CD-AI/Vintern-1B-v2)** model by 5CD-AI. The notebook contains a prompt specifically designed for recognizing Vietnamese invoices and extracting columns such as Item Name, Quantity, Unit Price, and Total.
