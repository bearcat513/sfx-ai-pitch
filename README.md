# Snowfox AI Pitch (Not a Hackathon)

## Use Case
Fix shitty client data.

## System Setup
- Download [Ollama](https://ollama.com)
- Download the model of your choosing. [Available Ollama Model](https://ollama.com/search)
- Update the `.env` file with a LLM model that you already have downloaded
- Ensure ollama is running and you have node.js installed
- Clone the repo and run the following commands:
  ```
    cd sfx-ai-pitch
    npm install
    npm run dev
  ```

## How does it all work?
- Take shitty client data (text, spreadsheet) and input it into app
- Tell the app how much you love it or hate it in order to GLAZE the AI model
- Enter in any additional prompt information (what to exactly do with the data)