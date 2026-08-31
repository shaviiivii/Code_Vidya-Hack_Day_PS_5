# Aatmoday Hobby Matchmaker

Find the Aatmoday hobby community that fits your interests, understand why it matches, and start a natural first conversation.

Live published website: [Aatmoday Hobby Matchmaker](https://aatmoday-hobby-matchmaker--baunime22.replit.app)

## What it does

Students can describe what they enjoy or want to try in plain language. The app matches their input to the most relevant Aatmoday community and provides:
- A clear club recommendation
- A short explanation of why the club fits
- A match signal
- A personalized icebreaker
- Alternate icebreakers
- A direct link to the Aatmoday WhatsApp community
- A searchable and filterable directory of all available clubs

## Available communities

- Coding Club
- Robotics Club
- Cultural Club
- Literary Club
- Photography Club
- Fitness Club
- Fine Arts & Creative Club
- Gardening Club
- Cooking Club

## Tech stack

- React
- TypeScript
- Vite
- Tailwind CSS
- Lucide React icons
- pnpm workspace

The MVP uses a local, explainable keyword-matching system. It does not require an API key, database, authentication, or external AI service to run.

## Run locally

Install dependencies from the repository root:


```bash
pnpm install
```

Start the development server:

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/aatmoday-hobby-matchmaker run dev
```

Then open `http://localhost:5173`.

## Build for publishing

```bash
pnpm --filter @workspace/aatmoday-hobby-matchmaker run build
```

The production files are generated in:

```text
artifacts/aatmoday-hobby-matchmaker/dist/public
```
## Published website address

The currently verified live website address is:

```text
https://aatmoday-hobby-matchmaker--baunime22.replit.app
```

The requested custom domain is `aatmoday.hobbymatchmaker.club`. It is not included as the live link because it has not completed DNS verification and may not open yet.

## WhatsApp community

All club recommendations use the Aatmoday community link:

https://chat.whatsapp.com/LuVKW6py3rQL4Mb7umJrFQ

## License

This project is available for personal and educational use.
