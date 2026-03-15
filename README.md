# NightVault-
NightVault Hotel Management Infrastructure on Stellar Open-source, programmable hospitality payments and operations — built for the world, powered by Stellar.
What is NightVault ?
NightVault  is an open-source, Web3-native hotel management system built on the Stellar blockchain. It replaces traditional opaque hospitality payment rails — nightly billing, deposit holds, staff payroll, multi-currency settlement — with transparent, low-cost, programmable flows.
NightVault is not just a booking app. It is open financial infrastructure for hospitality, designed to serve boutique hotels, hostels, and lodging operators across emerging markets and beyond.


Why NightVault ?
Hotel management today suffers from:
Fragmented payment flows — deposits, nightly charges, F&B, extras, and refunds are siloed across systems
Settlement delays — revenue reaches owners days or weeks late, filtered through acquirers and PSPs
Opaque deposit handling — guests have no verifiable proof of how their deposit is held or released
High cross-border fees — international bookings lose 3–7% to currency conversion and wire charges
No programmable commissions — OTA and agent commissions are tracked manually and disputed frequently
Exclusion of unbanked operators — small lodges in emerging markets lack access to global payment rails
NightVault solves this by combining Stellar's payment rails with a clean, open-source hotel operations layer.

Why Stellar?
NightVault is designed specifically for Stellar, not merely deployed on it.
Stellar FeatureNightVault  Use CaseFast finality (2–5 seconds)Real-time nightly charge settlementUltra-low feesMicro-transactions for extras, tips, room serviceBuilt-in DEXMulti-currency booking without external bridgesAnchor fiat on/off-rampsLocal currency check-in/check-outMulti-sig & pre-auth transactionsEscrow-style deposit holdsClaimable balancesRefund flows that guests can claim on departureStellar Asset IssuanceHotel loyalty tokens & 

Core Features
💳 Programmable Payments
Nightly charges settle instantly to hotel owners
Automatic splits between property owner, manager, and franchise
OTA and agent commissions distributed at booking time — no manual reconciliation

🔒 Deposit Escrow
Guest deposits locked on-chain using Stellar multi-sig or pre-authorised transactions
Released automatically on checkout approval or held for damage deductions
Fully transparent and auditable by all parties

🌍 Multi-Currency Settlement
Accept USDC, local fiat-backed tokens via Stellar Anchors, or native XLM
Stellar DEX handles currency conversion at best available rate
No wire fees for international guests or cross-border owner distributions

🏷️ Hotel Loyalty Tokens
Issue property-specific tokens redeemable for nights, upgrades, or F&B
Transferable on Stellar DEX — guests can trade or gift loyalty credits
Transparent supply and redemption records on-chain

📋 Operations Layer (Off-Chain)
Room inventory and availability management
Guest profiles and reservation records
Staff scheduling and task management
Housekeeping and maintenance tracking
Reporting and analytics dashboards

Architecture
NightVault  uses a hybrid architecture — decentralising what matters (money, trust, agreements) while keeping complex business logic off-chain for usability and scale.

┌─────────────────────────────────────────────┐
│              FRONTEND LAYER                 │
│  apps/web      — Guest & Booking Portal     │
│  apps/dashboard — Hotel Manager Dashboard  │
│  apps/mobile   — Staff & Guest Mobile App  │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│               BACKEND LAYER                 │
│  apps/api      — REST + WebSocket API       │
│  apps/indexer  — Stellar Event Indexer      │
│  apps/worker   — Background Job Runner      │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│             SHARED PACKAGES                  │
│  packages/stellar  — Stellar SDK wrapper    │
│  packages/db       — Prisma schema & client │
│  packages/types    — Shared TypeScript types│
│  packages/ui       — Component library      │
│  packages/config   — Shared configs         │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│            STELLAR NETWORK                  │
│  · Booking deposit escrow                   │
│  · Nightly charge settlement                │
│  · Commission distribution                 │
│  · Loyalty token issuance & redemption      │
│  · Refund claimable balances                │
│  · Immutable transaction records            │
└─────────────────────────────────────────────┘

On-Chain (Stellar)
Booking deposit holds and releases
Nightly revenue settlement to owners
Automatic OTA/agent commission splits
Loyalty token issuance and redemption
Refund claimable balances
Immutable payment audit trail

Off-Chain
Room inventory and rate management
Guest reservations and profiles
Housekeeping and maintenance workflows
Staff management and scheduling
Analytics and reporting
Compliance and KYC hooks
Messaging and notifications


NightVault/
├── apps/
│   ├── web/              # Guest-facing booking portal (Next.js)
│   ├── dashboard/        # Hotel manager operations dashboard (Next.js)
│   ├── mobile/           # Staff & guest mobile app (React Native / Expo)
│   ├── api/              # Core REST + WebSocket API (Fastify / Node.js)
│   ├── indexer/          # Stellar horizon event indexer
│   └── worker/           # Background jobs (deposits, commissions, alerts)
│
├── packages/
│   ├── stellar/          # Stellar SDK wrapper & payment primitives
│   ├── db/               # Prisma schema, migrations, seed data
│   ├── types/            # Shared TypeScript types and Zod schemas
│   ├── ui/               # Shared component library (Tailwind + Radix)
│   └── config/           # ESLint, TypeScript, Tailwind base configs
│
├── contracts/            # Stellar smart contract experiments (Soroban)
├── docs/                 # Protocol documentation & architecture guides
├── scripts/              # Dev tooling, deploy scripts, anchor integration
├── turbo.json            # Turborepo pipeline config
├── pnpm-workspace.yaml   # pnpm workspace definition
└── README.md

Tech Stack
LayerTechnologyMonorepo toolingTurborepo + pnpm workspacesFrontendNext.js 14, Tailwind CSS, Radix UIMobileExpo (React Native)Backend APIFastify, Node.js, TypeScriptDatabasePostgreSQL via Prisma ORMBlockchainStellar (Horizon API + Soroban)Stellar SDK@stellar/stellar-sdkPaymentsUSDC, fiat anchors, XLMBackground jobsBullMQ + RedisAuthPasskey / wallet-based + JWTHostingDocker-composable, cloud-agnostic

Payment Flows

Booking Deposit
Guest → [USDC/fiat token] → NightVault  Escrow Account (multi-sig)
                                    │
               ┌────────────────────┴──────────────────┐
           On Checkout                          On Dispute/Damage
        Release to Guest                    Partial/Full → Hotel

Nightly Charge Settlement
Guest Wallet → Payment TX on Stellar
                     │
          ┌──────────┴──────────┐
     Hotel Owner (70%)    Manager Fee (15%)
                               │
                      Agent/OTA Commission (15%)

Loyalty Token Flow
Hotel issues NightVaultToken (custom Stellar asset)
     │
Guest earns tokens on stay / spend
     │
Redeem at property OR trade on Stellar DEX

Roadmap
Phase 1 — Foundation
 Monorepo scaffold with Turborepo
 Stellar SDK integration package
 Basic booking deposit escrow flow
 Hotel manager dashboard (MVP)
 Guest booking portal (MVP)

Phase 2 — Core Payments
 Nightly charge automation
 Commission split logic
 Multi-currency support via Stellar anchors
 Refund claimable balance flows
 Stellar Horizon indexer for payment events

Phase 3 — Operations
 Housekeeping and maintenance module
 Staff management and scheduling
 Room inventory and rate management
 Reporting and analytics

Phase 4 — Loyalty & Ecosystem
 Hotel loyalty token issuance (custom Stellar asset)
 DEX-tradeable loyalty credits
 OTA partner integration hooks
 Soroban smart contract experiments
 Multi-property / franchise support

 Open Source & Contribution
NightVault  is being built fully open-source. We welcome:
🛠️ Engineers — frontend, backend, Stellar/blockchain
🎨 Designers — UX/UI for hospitality workflows
📖 Technical writers — protocol and API documentation
🔗 Anchor operators — fiat on/off-ramp integration
🏨 Hospitality operators — domain expertise and feedback

# Clone the repo
git clone https://github.com/your-org/NightVault.git
cd NightVault

# Install dependencies (requires pnpm)
pnpm install

# Copy environment variables
cp .env.example .env

# Start all services in development
pnpm dev

License
MIT ©NightVault  Contributors
NightVault  is not just a hotel booking app.
It is open financial infrastructure for hospitality — built on Stellar, designed to scale across borders, currencies, and communities.


        

