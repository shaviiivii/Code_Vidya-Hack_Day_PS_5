# aatmatoday Hobby Matchmaker<img width="720" height="1600" alt="Screenshot_2026-08-31-15-09-38-782_com android chrome" src="https://github.com/user-attachments/assets/9261a2ad-354e-4523-bdf2-81c2e4bda814" />


> Less directory. More nudge.

aatmatoday Hobby Matchmaker is a student-friendly discovery app that turns a free-form description of someone's interests into relevant campus communities, upcoming events, match reasoning, and a personalized icebreaker.

Instead of asking students to browse a long directory or choose from rigid dropdowns, the app lets them describe what they are curious about in their own words.

## Features

- **Natural-language hobby discovery** — describe an interest, mood, or activity in a sentence.
- **Live community suggestions** — matching clubs appear while the student types.
- **Transparent recommendations** — every result explains why it may be a good fit.
- **Upcoming event recommendations** — timely ways to try an interest in real life.
- **Personalized icebreakers** — each match includes a copyable opening line.
- **WhatsApp community access** — community and result cards link directly to the relevant WhatsApp group.
- **Responsive editorial interface** — designed for a warm, low-pressure campus experience across desktop and mobile.
- **Resilient states** — loading, validation, empty, API error, and retry states are included.
- **Duplicate protection** — communities and matches are deduplicated by their unique IDs.

## Communities

The MVP currently includes:

- Coding Club
- Robotics Club
- Cultural
- Literary
- Photography
- Fitness
- Fine Arts & Creative Club

The catalog is intentionally curated in the API server so the first version works without account setup, third-party AI credentials, or external service configuration.

## How it works

1. A student enters a free-form description such as:
   - `I want to learn photography and meet people who notice small details`
   - `I like building robots and working with Arduino`
   - `I want a low-pressure way to get fit`
2. The frontend displays live community suggestions based on searchable names, descriptions, tags, and keyword aliases.
3. Submitting the description calls `POST /api/match`.
4. The API detects interest themes, scores communities and events, and returns ranked matches.
5. The UI presents the match score, explanation, event details, icebreaker, tags, and WhatsApp link.

## Tech stack

- **Frontend:** React 19, TypeScript, Vite, React Hook Form, Zod, TanStack Query, Tailwind CSS
- **Backend:** Express 5, TypeScript, Zod
- **API contracts:** OpenAPI 3.1 with Orval-generated React Query hooks and Zod schemas
- **Workspace:** pnpm workspaces
- **Build tooling:** Vite for the frontend and esbuild for the API bundle
- **Runtime:** Node.js 24

## Project structure

```text
.
├── artifacts/
│   ├── aatmoday-matchmaker/       # React/Vite web application
│   ├── api-server/                # Express API and matching catalog
│   └── mockup-sandbox/            # Component preview tooling
├── lib/
│   ├── api-spec/                  # OpenAPI source of truth
│   ├── api-client-react/          # Generated React API client
│   ├── api-zod/                   # Generated validation schemas
│   └── db/                        # Shared database package for future persistence
├── scripts/                       # Workspace utility scripts
├── package.json                   # Root workspace scripts
└── pnpm-workspace.yaml            # Workspace and dependency configuration
```

## Getting started

### Prerequisites

- Node.js 24 or later
- pnpm

### Install dependencies

```bash
pnpm install
```

### Run the API server

The API requires a `PORT` environment variable:

```bash
PORT=8080 pnpm --filter @workspace/api-server run dev
```

The API will be available at:

```text
http://localhost:8080/api
```

### Run the web app

The Vite app requires both `PORT` and `BASE_PATH`:

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/aatmoday-matchmaker run dev
```

The frontend uses relative `/api` requests. In Replit, the included managed workflows route the web app and API server together. When running the services separately outside Replit, use a reverse proxy that forwards `/api/*` requests to the API server, or configure an equivalent Vite development proxy.

### Replit workflows

This repository includes these development workflows:

```text
API Server: pnpm --filter @workspace/api-server run dev
Web App:    pnpm --filter @workspace/aatmoday-matchmaker run dev
```

Start both workflows to use the complete experience in the Replit preview.

## API reference

The OpenAPI definition lives at [`lib/api-spec/openapi.yaml`](lib/api-spec/openapi.yaml).

### Health check

```http
GET /api/healthz
```

### List communities

```http
GET /api/communities
```

### List upcoming events

```http
GET /api/events
```

### Create matches

```http
POST /api/match
Content-Type: application/json
```

Request:

```json
{
  "interests": "I enjoy photography, visual storytelling, and meeting creative people"
}
```

Each returned match contains:

```json
{
  "id": "photography",
  "type": "community",
  "title": "Photography",
  "score": 92,
  "reason": "A strong fit for your interest in photography...",
  "icebreaker": "Hi! I’m interested in photography...",
  "communityLink": "https://chat.whatsapp.com/LuVKW6py3rQL4Mb7umJrFQ"
}
```

## Development commands

```bash
# Typecheck every workspace package
pnpm run typecheck

# Build the complete workspace
pnpm run build

# Typecheck only the web app
pnpm --filter @workspace/aatmoday-matchmaker run typecheck

# Typecheck only the API server
pnpm --filter @workspace/api-server run typecheck

# Build the web app
pnpm --filter @workspace/aatmoday-matchmaker run build

# Regenerate API clients and Zod schemas after editing OpenAPI
pnpm --filter @workspace/api-spec run codegen
```

## Matching approach

The MVP uses a deterministic, explainable matching approach:

- Natural-language input is normalized and checked against curated keyword aliases.
- Community and event tags contribute to relevance scores.
- Results are ranked by score and deduplicated by unique match ID.
- The detected interests are reused to generate the recommendation summary and icebreaker.
- If no specific interest is detected, the API still returns a gentle discovery path using the available catalog.

This keeps the experience fast and predictable while leaving room for a future personalized or AI-assisted matching layer.

## Contributing

1. Create a feature branch.
2. Make the smallest focused change possible.
3. Update the OpenAPI contract first when changing API response shapes.
4. Regenerate the API client and validation schemas when the contract changes.
5. Run `pnpm run typecheck` and `pnpm run build`.
6. Open a pull request describing the user-facing change.


