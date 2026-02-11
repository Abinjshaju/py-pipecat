# Baines AI Voice Service

FastAPI + Pipecat + Gemini Live + Twilio voice agent. Users select a persona, enter a phone number, and receive a real-time AI voice call.

## MVC Structure

```
app/
├── main.py              # FastAPI app wiring
├── config.py            # Environment configuration
├── models/              # Data layer
│   └── persona.py       # Persona loading, system instruction builder
├── services/            # Business logic
│   ├── twilio_service.py   # Twilio calls, TwiML generation
│   └── bot_service.py      # Pipecat Gemini Live pipeline
├── controllers/         # Request handlers
│   ├── web_controller.py    # GET /
│   ├── api_controller.py    # GET /api/personas, POST /call
│   ├── twiml_controller.py  # POST /twiml (Twilio webhook)
│   └── websocket_controller.py  # WebSocket /ws
├── views/
│   └── index.html       # Static UI
└── data/
    └── persona.json     # Persona definitions
```

## Run locally

```bash
uv sync
uv run python main.py
```

Runs on port 8520. Set `DOMAIN` to your ngrok URL, configure `.env` from `.env.example`.

## Run with Docker (uv)

```bash
# Build
docker build -t py-pipecat .

# Run
docker run -p 8520:8520 --env-file .env py-pipecat
```

Or with docker-compose:

```bash
docker compose up --build
```
