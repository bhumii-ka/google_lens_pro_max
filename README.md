# Google Lens Pro Max
## Image-Based Search Query Generator

This project implements a web application that generates a search query based on a combination of an uploaded image and a user-provided query. The application integrates several components, including **BLIP** for generating image captions, **LLaMA** for refining user queries, and **Zenserp API** for returning relevant search results.

## Table of Contents
1. [Problem Statement](#problem-statement)
2. [Solution](#solution)
3. [How it Works](#how-it-works)
4. [Dependencies](#dependencies)
5. [Installation and Setup](#installation-and-setup)
6. [Code Overview](#code-overview)
7. [Usage](#usage)

## Problem Statement
The goal is to develop an intelligent pipeline that takes an image of any object along with a user-defined prompt as input. The prompt specifies the user's requirement, such as finding similar objects or variations based on the image. For instance, if the input image is a towel, the prompt might request "show me a similar towel" or "show me towels of the same type but in different colors." The pipeline should then process the input image and prompt, and return relevant web search results that align with the user's specific needs. This system aims to enhance search efficiency by combining visual inputs with contextual user queries.

## Solution
This project addresses the problem by implementing:
1. **Image Captioning**: Uses the BLIP model to analyze the uploaded image and generate a relevant caption.
2. **Query Refinement**: Leverages the LLaMA model to refine the user’s text query by integrating the image caption and the user’s original prompt.
3. **Search Results**: Fetches results based on the refined query using the Zenserp API, providing a list of relevant websites.

## How it Works
- **User Input**: The user uploads an image and provides a query or prompt.
- **BLIP Model**: The application processes the uploaded image using the **BLIP (Bootstrapping Language-Image Pretraining)** model to generate a caption for the image.
- **LLaMA Model**: This caption is combined with the user’s query, and the **LLaMA** model refines the combined input to produce a single-line search query.
- **Zenserp API**: The refined query is then used to search for relevant web results through the **Zenserp API**.
- **Results Display**: The app displays the generated search query and provides a list of search results with clickable links.

## Dependencies
The project requires several Python libraries and external services:
- **PyTorch**: For working with machine learning models.
- **Transformers**: To load and interact with the BLIP and LLaMA models.
- **Gradio**: A simple UI framework to create the web interface.
- **Pyngrok**: To provide public access to the Gradio app.
- **Requests**: To handle API calls for fetching the image and querying Zenserp.
- **Zenserp API**: An external service to fetch search results based on a query.

## Installation and Setup

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/your-username/image-search-query-generator.git
    cd image-search-query-generator
    ```

2. **Install the Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Get API Keys**:
    - **Zenserp API Key**: Sign up at [Zenserp](https://zenserp.com) to get an API key and replace the placeholder in the code with your key.

4. **Ngrok Token (Optional)**: If you want to run the Gradio app publicly, sign up at [Ngrok](https://ngrok.com/) and set up your auth token using:
    ```bash
    ngrok config add-authtoken YOUR_AUTH_TOKEN
    ```

5. **Run the Application**:
    ```bash
    python app.py
    ```

## Code Overview

### `process_input` Function
- **Input**: The function takes two inputs:
  1. **Uploaded Image**: An image uploaded by the user (PIL format).
  2. **User Prompt**: A question or search query provided by the user.

- **Steps**:
  1. **Image Captioning (BLIP)**: 
     - The function uses the **BLIP processor** to convert the image into a caption. The caption provides contextual information about the image.
  
  2. **Query Refinement (LLaMA)**:
     - The BLIP-generated caption and user’s prompt are combined and passed to the **LLaMA model**.
     - The LLaMA model refines the input into a concise search query that integrates both the visual and text information.

  3. **Fetching Search Results**:
     - The refined query is sent to the **Zenserp API**, which returns search results (titles, URLs, etc.) in JSON format.
     - The function formats the results into a user-friendly output with clickable links.

  4. **Return**: The function returns the final refined query, search results, and image caption.

### Gradio Interface
- **Inputs**:
  - `gr.Image`: Allows the user to upload an image for analysis.
  - `gr.Textbox`: Lets the user input their search prompt or question.

- **Outputs**:
  - `gr.Markdown`: Displays the formatted search results as clickable links.
  - `gr.Textbox`: Shows the refined search query and the caption generated by BLIP.

### Ngrok Integration
- **Pyngrok**: Allows you to share the app publicly using Ngrok. After setting up the Ngrok token, the app can be accessed via a public URL.

## Usage
1. **Upload an Image**: Drag and drop an image or upload one from your device.
2. **Enter a Query**: Input a text query that you'd like to refine based on the image context.
3. **View Results**: The app will generate a search query based on the image and your text, then display relevant search results.

## Example
1. **Image**: An image of a black t-shirt with a Superman logo.
2. **User Prompt**: “Find similar t-shirts.”
3. **Refined Query**: “Black Superman logo t-shirt buy.”
4. **Search Results**: The app will return several links to stores or articles where similar t-shirts are available.
