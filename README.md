# Gurukul

AI-first immersive education platform that combines adaptive learning, VR classrooms, multiplayer quizzes, and blockchain-based rewards.

## Problem Statement

Modern digital education still struggles to deliver learning that is engaging, personalized, and motivating.

- Students often learn complex subjects like chemistry and biology through flat 2D content, even when the concepts need spatial understanding.
- Traditional quizzes usually measure right or wrong answers, but do not identify the exact misconception behind a wrong answer.
- Every learner receives the same pace and content, even though each student has different weak areas.
- Online learning platforms often lack social presence, immersion, and real-time classroom energy.
- Students have limited incentive to keep practicing beyond grades or exam pressure.

## Existing Solutions

Current education tools solve parts of the problem, but rarely address the full learning loop.

- LMS platforms such as Google Classroom and Moodle manage assignments and content, but are not deeply adaptive or immersive.
- Video platforms explain concepts visually, but remain passive and one-way.
- Quiz apps like Kahoot improve engagement, but mostly focus on scoring rather than long-term student profiling.
- AR/VR learning apps provide visualization, but are usually isolated experiences without personalized assessment.
- Reward systems motivate participation, but are often centralized and disconnected from actual learning performance.

## Our Solution

Gurukul brings these pieces together into one adaptive learning ecosystem.

- **AI diagnostic quizzes** generate fresh subject-specific questions using Gemini and attach signals to each option so incorrect answers reveal specific weak topics.
- **Adaptive student profiling** stores per-subject and per-topic mastery scores in MongoDB and updates them after every session using Exponential Moving Average.
- **Immersive VR learning** uses browser-based A-Frame/WebXR scenes for virtual classrooms, labs, lounges, and multiplayer quiz environments.
- **AI chatbot support** gives students instant doubt resolution with text, voice input, and text-to-speech output.
- **Gamified marketplace** rewards learning activity with points and EduTokens that can be redeemed for marketplace items.
- **Blockchain rewards** use smart contracts for token-based student incentives and marketplace purchases.

## Tech Stack

- **Frontend**: React 19, TypeScript, Vite, Tailwind CSS, Framer Motion, React Router, Capacitor
- **Backend**: Python, FastAPI, Beanie ODM, Motor, JWT authentication
- **Database**: MongoDB
- **AI**: Google Gemini via `google-genai` and `@google/genai`
- **VR and Realtime**: A-Frame, WebXR, Socket.IO, Networked-AFrame, EasyRTC
- **Blockchain**: Solidity, Hardhat, OpenZeppelin, Web3.py, viem
- **Core Modules**: `frontend`, `fastapiBackend`, `vr-kahoot`, `blockchain/student-reward-system`

## Workflow

1. A student registers or logs in through the React frontend.
2. The FastAPI backend manages authentication, courses, quizzes, marketplace data, wallet details, and MongoDB persistence.
3. The student enters learning spaces such as subject pages, the quiz room, marketplace, lounge, or VR Kahoot.
4. Gemini generates diagnostic quiz questions and maps answer options to topic-level learning signals.
5. Student answers are scored and converted into topic deltas.
6. The backend updates the student's adaptive learning profile in MongoDB.
7. Students receive points or EduTokens for learning activity and can redeem them in the marketplace.
8. VR Kahoot provides a multiplayer quiz flow with host controls, live player avatars, and real-time scoring.

## Setup

### Prerequisites

- Python 3.10+
- Node.js 18+
- MongoDB running locally or a MongoDB Atlas URI
- Google Gemini API key
- Optional: Hardhat local blockchain for token rewards

### Environment Variables

Create a `.env` file in `fastapiBackend` and, if needed, in `vr-kahoot`.

```env
GEMINI_API_KEY=your_gemini_api_key
MONGO_URI=mongodb://localhost:27017
DB_NAME=smartedu_db
SECRET_KEY=change-this-secret
RPC_URL=http://127.0.0.1:8545
EDU_TOKEN_ADDRESS=your_deployed_edu_token_address
MARKETPLACE_ADDRESS=your_deployed_marketplace_address
ADMIN_PRIVATE_KEY=your_admin_wallet_private_key
```

### Backend

```bash
cd fastapiBackend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

### VR Kahoot

```bash
cd vr-kahoot
pip install -r requirements.txt
cd avatar-server
npm install
node server.js
```

In another terminal:

```bash
cd vr-kahoot
python main.py
```

### Blockchain

```bash
cd blockchain/student-reward-system
npm install
npx hardhat node
```

In another terminal, deploy the contracts using the Hardhat Ignition module:

```bash
cd blockchain/student-reward-system
npx hardhat ignition deploy ignition/modules/EduSystem.ts --network localhost
```

### Run All Services

On Unix-like shells, the root script starts the backend, frontend, and VR Kahoot services together:

```bash
./run.sh
```

Default local URLs:

- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:8000`
- Backend docs: `http://localhost:8000/docs`
- VR Kahoot lobby: `http://localhost:8000/`
