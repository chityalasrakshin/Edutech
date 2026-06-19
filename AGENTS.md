# MindFlix Academy Agent Instructions

## Setup
- Set `GEMINI_API_KEY` and `MONGODB_URI` or `MONGO_URI` in `.env`
- Install Python deps: `pip install -r requirements.txt`
- Install Node.js deps in frontend: `npm install`

## Run
- Backend: `cd fastapiBackend && uvicorn main:app --reload --port 8000`
- MindFlix Battle Royale API: `cd vr-kahoot && python main.py`
- MindFlix avatar server: `cd vr-kahoot/avatar-server && npm start`
- Build: `npm run build` in frontend

## Test
- Unit: `pytest backend/tests/`
- VR: `npm test` in vr-kahoot
- AI: `python -m pytest ai/`
