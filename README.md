# NOVAE: Democratizing Agentic Voice AI 🎙️🤖

**NOVAE** is an open-source, multi-tenant AI infrastructure platform designed to democratize access to state-of-the-art conversational voice agents. Built for SMEs, grassroots tech agencies, and the open-source community, NOVAE eliminates exorbitant SaaS paywalls, removes the developer bottleneck, and guarantees data privacy through a strict **"Bring-Your-Own-Key" (BYOK)** model.

---

## 🌍 Hackathon Context: HackGit V2

This project was developed for the **HackGit V2 Agentic AI Hackathon** to directly address two Sustainable Development Goals (SDGs):

- **SDG 8: Decent Work and Economic Growth**
- **SDG 9: Industry, Innovation, and Infrastructure**

By providing scalable AI infrastructure, NOVAE empowers local economies (like dental clinics, distribution centers, and gyms) to automate their workflows without vendor lock-in.

---

## ✨ Core Features

- **Multi-Tenant Dashboard**: A secure, intuitive UI for businesses to manage multiple agents, users, and call logs without writing code.

- **Ultra-Low Latency**: Utilizes Twilio Media Streams (Websockets) to pass bidirectional audio directly to AWS Bedrock's Nova Sonic 2 model.

- **Agentic Autonomy (Live Tool Use)**: Agents actively listen, reason, and autonomously trigger webhooks (e.g., updating a CRM) or execute SIP network escalations to human agents.

- **Bring-Your-Own-Key (BYOK)**: Users plug in their own AWS and Twilio API keys, ensuring zero platform markup and complete data ownership.

- **Custom Configurations**: Tenants can inject custom system prompts and Knowledge Base (KB) guardrails for isolated, context-aware agents.

---

## 🛠️ Tech Stack

- **Frontend/Dashboard**: Next.js
- **Authentication & Security**: JWT + bcrypt for strict tenant isolation
- **Voice Routing**: Twilio Programmable Voice & Media Streams
- **Agentic Engine**: AWS Bedrock (Nova Sonic 2)

---

## 🚀 Getting Started

### Prerequisites

- **Node.js 18+**
- A **Twilio Account** with a provisioned phone number
- An **AWS Account** with an IAM profile configured for Amazon Bedrock (us-east-1 recommended)
- **localtunnel** or **ngrok** to expose your local server to Twilio webhooks

### 1. Environment Variables

Create a `.env.local` file in the root directory and add the following:

```env
# Database
DATABASE_URL="file:./dev.db"

# JWT Secret
JWT_SECRET="your-super-secret-jwt-key-change-this-in-production"

# AWS Configuration
AWS_ACCESS_KEY_ID="your-aws-access-key"
AWS_SECRET_ACCESS_KEY="your-aws-secret-key"
AWS_REGION="us-east-1"

# Twilio Configuration
TWILIO_ACCOUNT_SID="your-twilio-account-sid"
TWILIO_API_SID="your-twilio-api-sid"
TWILIO_API_SECRET="your-twilio-api-secret"

# Application
NEXT_PUBLIC_BASE_URL="http://localhost:3000"
```

### 2. Local Development Setup

Clone the repository and install dependencies:

```bash
git clone https://github.com/saadhaniftaj/novae.git
cd novae
npm install
```

Run database migrations:

```bash
npx prisma migrate dev
npm run seed
```

Start the Next.js development server:

```bash
npm run dev
```

### 3. Exposing the Webhook

In a new terminal, run **localtunnel** (or **ngrok**) to expose your local port (default is 3000):

```bash
npx localtunnel --port 3000
```

Copy the generated public URL (e.g., `https://random-domain.loca.lt`).

### 4. Twilio Configuration

1. Go to your active phone number in the [Twilio Console](https://console.twilio.com/)
2. Under the **Voice Configuration** tab, set the "A CALL COMES IN" webhook to your public URL path:
   ```
   https://random-domain.loca.lt/api/incoming-call
   ```
3. Save the configuration

---

## 📞 Usage & Call Flow

### Inbound Calling (The Receptionist)

1. Dial your Twilio phone number
2. Twilio hits the `/api/incoming-call` webhook, which returns TwiML instructing Twilio to open a Websocket connection
3. The app streams audio to AWS Bedrock. The Nova Sonic model responds in real-time
4. Try saying: **"I need to cancel my reservation"** or **"Book an appointment"** to test Live Tool Use

### Call Escalation (The SIP Transfer)

If the user says, **"I want to speak to a human,"** the agent utilizes its tool set to update the current call leg and dials the configured `SIP_ENDPOINT`. If you have a softphone (like Zoiper) connected to that SIP domain, it will ring instantly.

---

## 🔐 Default Login Credentials

After running the seed script, you can log in with:

- **Email**: `admin@novae.vanguard.com`
- **Password**: `vanguardnovae1`

---

## 📊 Project Structure

```
novae/
├── app/                    # Next.js app directory
│   ├── (auth)/            # Authentication pages
│   ├── api/               # API routes
│   └── dashboard/         # Dashboard pages
├── src/
│   ├── components/        # React components
│   ├── hooks/             # Custom hooks
│   └── lib/               # Utility functions
├── prisma/                # Database schema & migrations
├── scripts/               # Database seed scripts
└── public/                # Static assets
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📄 License

This project is licensed under the MIT License.

---

## 🎯 Hackathon Goals Achieved

✅ **SDG 8 & 9 Alignment**: Democratizing AI infrastructure for economic growth  
✅ **Open Source**: Fully transparent codebase  
✅ **BYOK Model**: Zero vendor lock-in, complete data ownership  
✅ **Production-Ready**: Multi-tenant architecture with JWT authentication  
✅ **Agentic AI**: Real-time voice agents with autonomous tool use

---

**Built with ❤️ for HackGit V2 by Vanguard**
