Ouroboros is a working demonstration built around simulated HPE NonStop data, not a production integration with a bank. This is because data files required to run on real data are highly confidential and not feasible for our model. 
A real-life application of our proposed solution will not run on simulated data, but use real MOMI, ASAP, or other operations management software which works directly with bank/ATM/customer data.

Live demo: https://ouroboros-mission-control.lovable.app 
What it does
- Monitor: Displays simulated system health, events, and incidents.
- Explain: Lets operators ask troubleshooting questions in plain English.
- Guide safely: Suggests commands from an approved catalog, labels their risk, and requires operator approval or senior escalation.
- Preserve knowledge: Supports senior-authored troubleshooting guidance with a second-senior review step.
- Audit: Records actions in the demo interface.
Run locally

Using the demo
our live demo has AI-generated responses enabled, meaning what you type will not return scripted answers.
1. Open System Overview to inspect system health and an incident.
2. Ask the copilot a question such as “Why are transactions slow?”
3. Review the explanation, evidence, and proposed diagnostic command.
4. Explore the approval and escalation workflow for different risk levels.
5. Visit Knowledge to see how troubleshooting guidance is retained and reviewed, and Audit to inspect recorded activity

Project structure
Path	Purpose
src/routes/	Main pages and the /api/relay endpoint
src/components/	Dashboard, chat, incident, and UI components
src/data/	Simulated metrics, alerts, incidents, commands, users, and knowledge
src/lib/relay.server.ts	Server-side AI request and context assembly
src/lib/scripted.ts	Scripted responses used when AI is unavailable
src/lib/permissions.ts	Role and command-permission logic

Stack: React, TypeScript, TanStack Start, Vite, and Tailwind CSS. The interface was developed with Lovable

Environment configuration
The app can run without an API key using built-in scripted demo responses. To enable AI-generated responses, configure the server-side environment variable:
LOVABLE_API_KEY=your_key_here
Place it in a local .env file or your deployment platform's server-side environment settings. Do not commit API keys. The /api/relay endpoint uses this key to call Lovable's hosted AI gateway. If the AI request is unavailable, the chat uses scripted fallback responses.
Privacy note: The included web prototype is not an entirely local AI deployment when the hosted gateway is enabled. A future on-premises deployment would require a locally hosted model and supporting infrastructure.

Requirements: Node.js and npm (a recent Node.js LTS release is recommended).

git clone <repository-url>
cd <repository-folder>
npm install
npm run dev
Open the local URL shown in your terminal (typically http://localhost:3000).
