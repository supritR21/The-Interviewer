## The Interviewer (PrepWise)

AI-powered mock interview platform built with Next.js, Firebase, Gemini, and Vapi voice agents.

## Overview

PrepWise helps users practice interviews by generating role-specific interview questions, conducting real-time voice interview sessions, and producing structured feedback with scoring.

Core flow:

1. User signs up/signs in with Firebase Auth
2. User generates an interview set from role/level/tech stack inputs
3. Voice interview runs through Vapi
4. Transcript is analyzed with Gemini
5. Feedback is saved and displayed with scores + recommendations

## Features

- Email/password authentication with secure server session cookies
- Interview question generation via Gemini (`/api/vapi/generate`)
- Real-time voice interview sessions using Vapi Web SDK
- Transcript-based feedback scoring and analysis
- Dashboard with user interviews and latest interviews
- Tech stack logo rendering and role-based interview cards

## Tech Stack

- Next.js 15 (App Router)
- React 19 + TypeScript
- Tailwind CSS
- Firebase Auth + Firestore
- Firebase Admin SDK (server actions)
- Vapi Voice AI (`@vapi-ai/web`)
- AI SDK + Google Gemini (`@ai-sdk/google`)
- Zod + React Hook Form

## Project Structure

```text
The-Interviewer/
	app/
		(auth)/
		(root)/
		api/vapi/generate/route.ts
	components/
		Agent.tsx
		AuthForm.tsx
		InterviewCard.tsx
		ui/
	firebase/
		client.ts
		admin.ts
	lib/
		actions/
			auth.action.ts
			general.action.ts
		vapi.sdk.ts
		utils.ts
	constants/
		index.ts
	types/
	public/
	package.json
```

## Environment Variables

Create a `.env.local` file:

```env
# Firebase Client SDK
NEXT_PUBLIC_FIREBASE_API_KEY=
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=
NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=

# Firebase Admin SDK
FIREBASE_PROJECT_ID=
FIREBASE_CLIENT_EMAIL=
FIREBASE_PRIVATE_KEY=

# AI + Voice
GOOGLE_GENERATIVE_AI_API_KEY=
NEXT_PUBLIC_VAPI_WEB_TOKEN=
NEXT_PUBLIC_VAPI_WORKFLOW_ID=
```

Notes:

- `FIREBASE_PRIVATE_KEY` must preserve newlines. If storing as one line, use `\n` and code will convert it.
- Keep all secret values out of version control.

## Installation

```bash
npm install
```

## Run Locally

```bash
npm run dev
```

Open `http://localhost:3000`.

## Available Scripts

- `npm run dev` - start development server
- `npm run build` - production build
- `npm run start` - run production server
- `npm run lint` - lint project

## Key Routes

- `/sign-in` - sign in page
- `/sign-up` - registration page
- `/` - dashboard with interview lists
- `/interview` - interview generation voice flow
- `/interview/[id]` - interview session page
- `/interview/[id]/feedback` - interview feedback page
- `/api/vapi/generate` - API route to generate interview questions and persist interview record

## Data Collections (Firestore)

- `users`
	- `name`, `email`
- `interviews`
	- `role`, `type`, `level`, `techstack`, `questions`, `userId`, `finalized`, `coverImage`, `createdAt`
- `feedback`
	- `interviewId`, `userId`, `totalScore`, `categoryScores`, `strengths`, `areasForImprovement`, `finalAssessment`, `createdAt`

## Feedback Evaluation Categories

The feedback model scores:

1. Communication Skills
2. Technical Knowledge
3. Problem Solving
4. Cultural Fit
5. Confidence and Clarity

## Authentication Flow

- Client auth uses Firebase client SDK
- Server session cookie is created via Firebase Admin (`setSessionCookie`)
- Protected routes are enforced in layout files:
	- root routes require authentication
	- auth routes redirect authenticated users to dashboard

## Deployment

- Vercel config exists in `vercel.json`
- Ensure all required env vars are configured in deployment settings

## Author

Suprit Raj

