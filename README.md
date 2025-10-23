# Weekly Budget Report automation generator

## About

This fork of [n8n-workflows](https://github.com/adomas399/n8n-workflows) generates a weekly budger report generation workflow to n8n.
The workflow:

- Connects to an [actual-mcp](https://github.com/adomas399/actual-mcp) instance to extract the users budget data
- Generates a report based on prompt `input/budgetReviewPrompt.txt`
- Sends said report via email to the recipient

All necessary setup can be made from the terminal or by manually setting the envirnoment variables – no coding needed! For a more tailored report, customize the prompt.

> ℹ️ Supported LLM providers: OpenRouter, OpenAi, Anthropic, GoogleGemini, MistralCloud, DeepSeek, Groq, XAiGroq, AzureOpenAi, Ollama, AwsBedrock

## Usage

### Prerequisities

- [n8n](https://n8n.io)
- [Node.js](https://nodejs.org/en/download)
- [Docker Desktop](https://www.docker.com/products/docker-desktop) (optional)
- [actual-mcp](https://github.com/adomas399/actual-mcp)

### Before you start

⚠️ Make sure that:

1.  Your n8n instance is up and running.

2.  Your actual-mcp SSE server is running and accesible from n8n.

3.  You have set up the required credentials in n8n:

    a) For Resend and actual-mcp, use generic Bearer credentials.

    b) For the LLM provider, use their specific credential type.

### Execution

1.  Clone the repository:

    ```bash
    git clone https://github.com/adomas399/budget-report-generator.git
    cd budget-report-generator
    ```

2.  Install dependencies:

    ```bash
    npm install
    ```

3.  Configure envirnonment variables:

    You can do this either automatically or manually:

- Option A: Guided setup

  ```bash
  npm run setup
  ```

- Option B: Manual setup

  ```bash
  cp .env.example .env
  ```

  ```bash
  # --- Required ---
  N8N_URL=https://your.n8n.url
  N8N_API_KEY=your-n8n-api-key
  LLM_PROVIDER_CREDENTIAL_ID=id-from-n8n
  RESEND_CREDENTIAL_ID=id-from-n8n
  MAIL_FROM=send@email.example
  MAIL_TO=receive@email.example
  OVERWRITE=true/false
  MCP_ENDPOINT=https://your-actual-mcp-url/sse

  # --- Optional ---
  MCP_AUTHENTICATION=brearerAuth/headerAuth/empty
  MCP_CREDENTIAL_ID=id-from-n8n

  # --- Optional with defaults in code ---
  LLM_PROVIDER=OpenRouter
  CHAT_MODEL=anthropic/claude-3.7-sonnet
  WORKFLOW_NAME="Weekly Budget Report"
  WEEK_DAY=Sunday
  HOUR=21
  ```

4.  Executing

    You can push the workflow to n8n in several ways:

    a) Using Node.js

        ```bash
        npm run start
        ```

    b) Using Docker

    1. Build the image:

    ```bash
    docker build -t local-image . --load
    ```

    2. Run the image:

    ```bash
    docker run local-image
    ```

    c) Using GitHub Actions

    Run Action 'Push N8N Workflow' on Github

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
