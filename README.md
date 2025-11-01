🎥 EchoFrame

EchoFrame is a lightweight, high-fidelity session replay SDK that lets you record and replay user sessions on your web application. Stop guessing what users are doing and start seeing exactly what they experience, helping you debug issues faster and understand user behavior.

This SDK is built to be minimal (15KB gzipped) and performance-first, using efficient batching and throttling to ensure it doesn't impact your site's load times.

✨ Core Features

⚡ Lightweight Footprint: Only 15KB gzipped, ensuring minimal impact on your site's performance.

📺 High-Fidelity Replay: Achieves 95% replay accuracy, capturing the DOM, user events (mouse, clicks, inputs), and dynamic mutations.

🚀 Performance Optimized: Uses the MutationObserver API with efficient event batching and throttling to prevent performance overhead, even on busy pages.

🏷️ Real-Time Session Tagging: Tag sessions with user IDs, emails, or custom metadata in real-time for easy filtering and debugging.

🔒 Secure & Scalable: Built with a secure API ingestion pipeline (Node.js) and a write-heavy NoSQL database structure, ready to support 100+ sessions per day and beyond.

💡 The Problem (Why EchoFrame?)

Analytics dashboards tell you what happened (e.g., "70% drop-off on checkout"). EchoFrame tells you why.

You can watch real user sessions to see where they get stuck, encounter bugs, or perform "rage clicks." It's an essential tool for product managers, engineers, and UX designers to build better products by eliminating guesswork.

🛠️ Tech Stack

SDK: TypeScript, MutationObserver API, Webpack (for optimized bundling)

Backend: Node.js (for the data ingestion API)

Database: NoSQL (e.g., MongoDB, Firestore), chosen for its ability to handle high-volume, unstructured event streams.

🏗️ How It Works: Architecture Overview

EchoFrame's architecture is simple and robust:

Record: The SDK is initialized on your site. It captures the initial DOM ("scaffolding") and then subscribes to all changes using the MutationObserver. It also records user events like mouse movements, clicks, and inputs.

Batch & Send: To protect your app's performance, these events are collected in a queue, batched, and throttled. They are then sent securely to your Node.js ingestion endpoint.

Store: The backend API validates the API key and session, then streams the events into a NoSQL database, optimized for fast, sequential writes.

Replay: A dashboard application (not included in this repo) can then fetch this stream of events, recreate the initial DOM in a sandboxed iframe, and apply each mutation and user event in sequence, perfectly replaying the session.

🚀 Getting Started (SDK Integration)

Integrating EchoFrame into your web application is straightforward.

1. Installation

npm install echoframe-sdk


2. Initialization

In your application's main entry point (e.g., index.js), initialize the SDK.

import EchoFrame from 'echoframe-sdk';

EchoFrame.init({
  apiKey: 'YOUR_PUBLIC_API_KEY',
  
  // Optional: If you are self-hosting the backend
  // ingestUrl: '[https://api.your-domain.com/v1/ingest](https://api.your-domain.com/v1/ingest)'
});


3. Tagging Sessions (Optional)

To easily find sessions belonging to a specific user, you can tag the session, typically after a user logs in.

EchoFrame.tag({
  userId: 'user-id-12345',
  email: 'user@example.com',
  plan: 'premium'
});


👨‍💻 Contributing (Project Setup)

Interested in contributing to EchoFrame itself? Here’s how to get the project running locally.

Prerequisites

Node.js (v18+)

npm

A NoSQL database (e.g., a local MongoDB instance or a free cloud account)

Installation

Clone the repository:

git clone [https://github.com/your-username/echoframe.git](https://github.com/your-username/echoframe.git)
cd echoframe


Install dependencies:
This project is likely a monorepo with sdk and server packages.

# Install root dependencies
npm install

# Install dependencies for SDK
cd packages/sdk
npm install

# Install dependencies for server
cd ../server
npm install
cd ../.. 


Set up Environment Variables:
Create a .env file in the packages/server directory.

# A secret key to validate API keys
API_SECRET_KEY=your-long-random-secret

# Your NoSQL database connection string
DATABASE_URL=mongodb://localhost:27017/echoframe


Run the application:

Build the SDK:

# In one terminal, build the SDK and watch for changes
cd packages/sdk
npm run build:watch


Run the server:

# In a second terminal, run the ingestion server
cd packages/server
npm run dev


🤝 Contributing

Contributions, issues, and feature requests are welcome! Please check the issues page to get started.

📄 License

This project is licensed under the MIT License. See the LICENSE file for details.