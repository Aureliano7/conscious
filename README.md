# 🚀 RiseUp

> **A decentralized platform for virtual rallies and direct democracy**  
> *A voice that cannot be silenced. A light that cannot be extinguished.*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status: MVP](https://img.shields.io/badge/Status-MVP%20Development-orange)](https://github.com/riseup-network/riseup/milestones)
[![PWA](https://img.shields.io/badge/PWA-Supported-brightgreen)](https://web.dev/progressive-web-apps/)
[![Decentralized](https://img.shields.io/badge/Architecture-P2P%20%2B%20libp2p-purple)](https://libp2p.io/)
[![TypeScript](https://img.shields.io/badge/TypeScript-Strict%20Mode-blue)](https://www.typescriptlang.org/)
[![Community](https://img.shields.io/discord/123456789?label=Discord&logo=discord)](https://discord.gg/riseup)

---

## 📋 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start)
- [Architecture](#-architecture)
- [Development](#-development)
- [Contributing](#-contributing)
- [Roadmap](#-roadmap)
- [Security](#-security)
- [License](#-license)
- [Contact](#-contact)

---

## 🌟 About

**RiseUp** is a decentralized digital platform that enables citizens to organize virtual rallies, express collective will, and visualize public opinion in real-time — without intermediaries, censorship, or geographic barriers.

### 🎯 Mission
> Restore every individual's ability to be heard, ensure the resilience of civic initiatives, and create a new language of political participation for the digital generation.

### 🔑 Core Principles
| Principle | Description |
|-----------|-------------|
| **Decentralization** | No single point of failure; P2P architecture with libp2p |
| **Privacy by Design** | Cryptographic identity; optional anonymity via zk-proofs (Phase 3) |
| **Transparency** | Open-source code; verifiable results; public audit trail |
| **Inclusivity** | Free access; mobile-first PWA; multi-language support |
| **Resilience** | Works offline; survives node failures; censorship-resistant |

---

## ✨ Features (MVP)

### 🗳️ Direct Democracy Tools
- **Create Initiatives**: Propose virtual rallies with topics, slogans, and geographic scope
- **Support & Vote**: Cryptographically signed voting with reputation-based weight
- **Threshold Activation**: Automatic event scheduling when support goals are met

### 👥 Identity & Reputation
- **Dual Mode**: Anonymous (zk-ready) or Verified (optional government ID integration)
- **Reputation System**: Earn XP for participation; levels affect vote weight
- **One-Time Pseudonyms**: Privacy-preserving participation per event

### 🌍 Real-Time Visualization
- **Interactive Map**: 2D Leaflet visualization of participant density (MVP)
- **Dynamic Slogans**: Live-updating slogan rankings with visual feedback
- **Event Pulse**: Real-time metrics: active users, messages, votes

### 💬 Communication
- **Signed Chat**: Moderated, cryptographically signed messages
- **"Shout" Feature**: Temporary full-screen announcements
- **Speaker Streaming**: WebRTC audio/video for organized presentations

### 📊 Reporting & Export
- **Auto-Generated Reports**: Participant stats, geographic distribution, slogan rankings
- **Verifiable Results**: Merkle-root proofs of event data
- **Multi-Format Export**: PDF, PNG, JSON, CSV for distribution and archival

---

## 🛠️ Tech Stack

### Frontend (PWA)
- ⚛️ React 18 + TypeScript + Vite
- 🧠 Redux Toolkit + Redux Saga (state management)
- 🎨 TailwindCSS + Headless UI (design system)
- 🗺️ Leaflet + OpenStreetMap (2D visualization)
- ✨ Three.js + Canvas (progressive 3D support)
- 🌐 Workbox (PWA offline support)

### P2P & Backend
- 🔗 libp2p (js) + WebRTC/WebSocket (network layer)
- 🗄️ OrbitDB + IndexedDB (decentralized storage)
- 🔐 WebCrypto API + noble-curves (cryptography)
- 📦 IPFS (optional media storage, Phase 2)

### DevOps & Testing
- 🧪 Vitest (unit) + Playwright (e2e) + k6 (load testing)
- 🔍 ESLint + Prettier + Husky (code quality)
- 🚀 GitHub Actions + Cloudflare Pages (CI/CD)
- 📊 Prometheus + Grafana (monitoring)

[View full `package.json`](package.json) • [Architecture Diagram](docs/ARCHITECTURE.md)

---

## ⚡ Quick Start

### Prerequisites
- Node.js ≥ 20 LTS
- npm ≥ 10 or pnpm ≥ 8
- Modern browser with WebCrypto support (Chrome 110+, Firefox 102+, Safari 16.4+)

### 1. Clone & Install
```bash
git clone https://github.com/riseup-network/riseup.git 
cd riseup
npm install  # or pnpm install
```

### 2. Environment Setup
```bash
cp .env.example .env.local
# Edit .env.local with your configuration:
# VITE_BOOTSTRAP_NODES=ns1.riseup.network,ns2.riseup.network
# VITE_SIGNALING_URL=wss://signal.riseup.network (optional fallback)
```

### 3. Run Development Server
```bash
npm run dev
# Open http://localhost:5173 in your browser
```

### 4. Build for Production
```bash
npm run build
npm run preview  # local preview of production build
```

### 5. Run Tests
```bash
npm run test          # unit tests
npm run test:e2e      # end-to-end tests (requires running app)
npm run test:load     # load testing with k6
npm run audit         # security audit
```

### 6. Bootstrap Node (Optional)
```bash
cd packages/bootstrap-node
npm run start
# Runs a libp2p bootstrap node for peer discovery
```

> 📚 **Full documentation**: [`/docs`](/docs) folder contains architecture specs, crypto protocols, and deployment guides.

---

## 🏗️ Architecture Overview

```text
┌─────────────────────────────────────┐
│         Client (Browser PWA)         │
│  ┌─────────────────────────────┐    │
│  │  React UI + Redux State     │    │
│  │  libp2p (P2P networking)    │    │
│  │  OrbitDB (local DB)         │    │
│  │  WebCrypto (signing)        │    │
│  └─────────────────────────────┘    │
└────────────┬────────────────────────┘
             │ WebRTC / WebSocket
             ▼
┌─────────────────────────────────────┐
│        P2P Network Layer             │
│  • Bootstrap Nodes (initial peer discovery)
│  • DHT for peer routing
│  • PubSub for event broadcasting
│  • CRDT for conflict-free replication
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│        Decentralized Data            │
│  • OrbitDB: profiles, initiatives, votes
│  • IPFS (Phase 2): media storage
│  • Local IndexedDB: offline cache
└─────────────────────────────────────┘
```

### Key Design Decisions
- **Optimistic UI**: Immediate feedback with background sync via CRDT
- **Signature-First**: All user actions signed before transmission
- **Progressive Decentralization**: MVP uses minimal bootstrap nodes with clear migration path
- **Performance Budget**: ≤200ms interaction latency at 500 concurrent users

[Read detailed architecture](docs/ARCHITECTURE.md) • [P2P Protocol Spec](docs/API_P2P.md)

---

## 👨‍💻 Development

### Project Structure
```text
riseup/
├── apps/
│   ├── web/                 # Main PWA application (React)
│   └── bootstrap-node/      # Libp2p bootstrap server (Node.js)
├── packages/
│   ├── crypto/              # Shared cryptography utilities
│   ├── p2p/                 # Libp2p configuration & protocols
│   ├── ui/                  # Reusable React components + Storybook
│   └── types/               # Shared TypeScript interfaces
├── docs/                    # Documentation (architecture, crypto, deployment)
├── scripts/                 # DevOps, testing, and utility scripts
├── .github/                 # CI/CD workflows, issue templates
├── package.json             # Root workspace config (Turborepo)
└── README.md                # You are here
```

### Essential Commands
```bash
# Development
npm run dev              # Start all apps in dev mode
npm run dev:web          # Start only the web app
npm run storybook        # Component library dev server

# Testing
npm run test             # Run unit tests (Vitest)
npm run test:watch       # Unit tests in watch mode
npm run test:e2e         # Playwright e2e tests
npm run test:load        # k6 load testing
npm run test:all         # Run all test suites

# Quality
npm run lint             # ESLint + TypeScript checks
npm run format           # Prettier formatting
npm run typecheck        # TypeScript compilation check
npm run audit            # Security audit (npm audit + custom checks)

# Build & Deploy
npm run build            # Build all apps for production
npm run build:web        # Build only web app
npm run preview          # Preview production build locally
```

### Cryptography Notes
```typescript
// All user actions MUST be signed:
import { signAction, verifySignature } from '@riseup/crypto';

const action = {
  type: 'vote',
  initiativeId: 'abc123',
  timestamp: Date.now(),
};

const signed = await signAction(action, privateKey);
// Returns: { data: {...}, signature: 'base64url...', publicKey: '...' }

// Verify before processing:
const isValid = await verifySignature(signed);
if (!isValid) throw new Error('Invalid signature');
```

[See crypto specification](docs/CRYPTO_SPEC.md)

---

## 🤝 Contributing

We welcome contributions from developers, designers, researchers, and activists!

### 🚀 Getting Started
1. Read our [Code of Conduct](CODE_OF_CONDUCT.md)
2. Check [open issues](https://github.com/riseup-network/riseup/issues) or create a new one
3. Fork the repo and create your branch: `git checkout -b feat/your-feature`
4. Follow our [Development Guidelines](docs/CONTRIBUTING.md)
5. Submit a pull request with clear description and tests

### 🎯 Good First Issues
Look for issues labeled:
- [`good first issue`](https://github.com/riseup-network/riseup/labels/good%20first%20issue) — beginner-friendly tasks
- [`help wanted`](https://github.com/riseup-network/riseup/labels/help%20wanted) — community contributions welcome
- [`documentation`](https://github.com/riseup-network/riseup/labels/documentation) — improve docs

### 🧭 Contribution Areas
| Area | Skills Needed | Resources |
|------|--------------|-----------|
| **Frontend** | React, TypeScript, Tailwind | [UI Components Guide](docs/UI_COMPONENTS.md) |
| **P2P/Backend** | libp2p, Node.js, OrbitDB | [P2P Protocol Spec](docs/API_P2P.md) |
| **Cryptography** | WebCrypto, ECDSA, zk-SNARKs | [Crypto Spec](docs/CRYPTO_SPEC.md) |
| **Design** | Figma, accessibility, UX research | [Design System](apps/web/src/design/) |
| **Testing** | Vitest, Playwright, k6 | [Testing Guide](docs/TESTING.md) |
| **Documentation** | Technical writing, i18n | [Docs Style Guide](docs/STYLE.md) |

### 📐 Code Standards
- TypeScript in strict mode
- ESLint + Prettier configuration enforced via Husky pre-commit hooks
- All new features require unit tests; critical paths require e2e tests
- Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/)

[Full contributing guide](docs/CONTRIBUTING.md)

---

## 🗓️ Roadmap

### ✅ Completed (Phase 0)
- [x] Project philosophy and visual language
- [x] Technical specification for MVP
- [x] Repository structure and CI/CD setup

### 🔄 Current (Phase 1: MVP — Q2-Q3 2024)
- [ ] Basic P2P network with libp2p (text data, voting)
- [ ] 2D map visualization (Leaflet + participant points)
- [ ] User identity module with cryptographic signing
- [ ] Initiative creation, voting, and threshold activation
- [ ] Synchronous event module (chat, slogans, reporting)
- [ ] Load testing for 1,000 concurrent users

### 📅 Planned (Phase 2: Visual Core — Q4 2024-Q1 2025)
- [ ] Three.js integration for 3D visualization modes
- [ ] Dynamic slogan rendering with particle effects
- [ ] Advanced reputation system with vote weighting
- [ ] Offline-first enhancements and background sync

### 🔮 Future (Phase 3+: Scaling & Ecosystem)
- [ ] zk-SNARKs integration for anonymous verification
- [ ] Government ID system integrations (by country)
- [ ] Tokenized participation economy and crowdfunding
- [ ] Public API for third-party developers and media

[View full roadmap with milestones](https://github.com/riseup-network/riseup/milestones)

---

## 🔒 Security

RiseUp handles sensitive civic participation data. Security is non-negotiable.

### Security Practices
- ✅ All user actions cryptographically signed and verified
- ✅ Private keys never leave user device; encrypted at rest
- ✅ Regular dependency audits (`npm audit`, `snyk`)
- ✅ Automated security scanning in CI pipeline
- ✅ Bug bounty program (coming soon)

### Reporting Vulnerabilities
If you discover a security issue, **do not open a public issue**.  
Please email: **security@riseup.network** with:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested mitigation (optional)

We aim to respond within 48 hours and coordinate responsible disclosure.

[Security policy details](SECURITY.md)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

**MIT License**

Copyright (c) 2024 RiseUp Network

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 📬 Contact

- 💬 **Discord Community**: [discord.gg/riseup](https://discord.gg/riseup)  
- 🐦 **Twitter/X**: [@RiseUpNetwork](https://twitter.com/RiseUpNetwork)  
- 📧 **Partnerships**: partner@riseup.network  
- 🔐 **Security Reports**: security@riseup.network  
- 🌐 **Website**: [riseup.network](https://riseup.network) (coming soon)

---

> **RiseUp is more than code.**  
> It's a commitment to building technology that amplifies human voice, protects dignity, and strengthens democracy.  
> Every contribution — code, design, documentation, or discussion — helps light another spark in the collective consciousness.  
>  
> *Join us. Build with purpose. RiseUp.* ✨

---

*Last updated: April 2024 • Version: MVP-1.0 • Status: Active Development*  
*Made with ❤️ by the RiseUp Community*
