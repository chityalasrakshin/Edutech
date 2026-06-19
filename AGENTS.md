# MindFlix Academy Agent Instructions

## Setup
- Set `GEMINI_API_KEY` and `MONGODB_URI` in `.env`
- Install Python deps: `pip install -r requirements.txt`
- Install Node.js deps in frontend: `npm install`

## Run
- Backend: `uvicorn main:app --reload`
- MindFlix Battle Royale: `cd vr-kahoot && npm run dev`
- Build: `npm run build` in frontend

## Test
- Unit: `pytest backend/tests/`
- VR: `npm test` in vr-kahoot
- AI: `python -m pytest ai/`
