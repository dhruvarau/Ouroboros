Team: Adan Abdullahi, Rong Hao, Dhruva Rau

This repository contains two complementary components: a web-based demonstration and the Python simulation that supplies its example data.

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

Open the local URL shown in your terminal (typically http://localhost:3000).

Python:
What the prototype demonstrates
- Monitor and explain: Visualizes simulated system metrics, alerts, and incidents; answers operator questions in natural language.
- Suggest, don't execute autonomously: Presents commands with risk labels and approval requirements.
- Role-based safeguards: Different permissions for junior and senior operators, with an audit trail.
- Preserve expertise: Expert-authored runbooks go through a second-senior review before approval.
- Detect anomalies: Python simulation includes rolling z-scores, Isolation Forest, and trend-based checks.

Run the web application
Requirements: Node.js and npm (or Bun). Internet access is needed to install dependencies.

cd app
npm install
npm run dev

Run the Python simulation
Requirements: Python 3 and the listed Python packages. From the repository root:
cd data-sim
python3 -m pip install numpy pandas scikit-learn matplotlib
python3 simulate_nonstop.py

The simulation generates 24 hours of minute-level synthetic metrics, with three example incidents (payment process issue, CPU failure, and disk filling), plus JSON outputs in data/.
For the exploratory analysis and evaluation, open CAIL_Relay_Data_Analysis.ipynb in Jupyter and run its cells.
Jupyter must be installed separately if needed.
Data flow: The web app currently reads its bundled files in app/src/data/; it does not automatically call the Python script. To reflect regenerated simulation data in the web app, copy the appropriate updated JSON outputs from data-sim/data/ into app/src/data/, checking filenames and schemas first.
