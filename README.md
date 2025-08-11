# ProofStake Protocol (PSP)

[![Clarity Version](https://img.shields.io/badge/Clarity-v3-blue.svg)](https://clarity-lang.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-Vitest-yellow.svg)](https://vitest.dev/)

## Next-Generation Staking Infrastructure on Stacks

ProofStake Protocol is an advanced decentralized finance primitive that combines Bitcoin's security model with Stacks' smart contract capabilities to deliver institutional-grade staking infrastructure. The protocol features algorithmic tier-based rewards, democratic governance mechanisms, and sophisticated risk management systems designed for maximum capital efficiency.

## 🌟 Key Features

### 🎯 Adaptive Tier System

- **Silver Tier**: Entry-level staking (1M+ STX) with 1x base rewards
- **Gold Tier**: Premium staking (5M+ STX) with 1.5x enhanced rewards  
- **Platinum Tier**: Institutional staking (10M+ STX) with 2x maximum rewards

### ⏰ Time-Weighted Rewards

- **Flexible Staking**: No lock commitment (1x multiplier)
- **30-Day Lock**: Enhanced commitment (1.25x multiplier)
- **60-Day Lock**: Maximum commitment (1.5x multiplier)

### 🏛️ Decentralized Governance

- Community-driven protocol evolution
- Weighted voting based on staking power
- Time-bound proposal lifecycle management
- Democratic decision-making processes

### 🔒 Security-First Design

- Multi-layered protection mechanisms
- Emergency circuit breakers
- Security cooldown periods for unstaking
- Parameter validation and access controls

## 📊 Protocol Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    ProofStake Protocol                      │
├─────────────────────────────────────────────────────────────┤
│  Intelligent Staking Engine                                │
│  ├─ Automated tier assignment                              │
│  ├─ Dynamic reward calculation                             │
│  └─ Compound interest mechanisms                           │
├─────────────────────────────────────────────────────────────┤
│  Governance Framework                                       │
│  ├─ Proposal lifecycle management                          │
│  ├─ Weighted voting system                                 │
│  └─ Democratic protocol evolution                          │
├─────────────────────────────────────────────────────────────┤
│  Risk Management                                            │
│  ├─ Emergency pause functionality                          │
│  ├─ Cooldown protection mechanisms                         │
│  └─ Parameter validation systems                           │
└─────────────────────────────────────────────────────────────┘
```

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks Wallet](https://wallet.hiro.so/) for testing

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/nkechi-okafor/proof-stake.git
   cd proof-stake
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Initialize the contract**

   ```bash
   clarinet check
   ```

### Development Setup

1. **Run tests**

   ```bash
   npm test
   ```

2. **Watch mode for development**

   ```bash
   npm run test:watch
   ```

3. **Generate test coverage reports**

   ```bash
   npm run test:report
   ```

## 📋 Contract Interface

### Core Staking Functions

#### `stake-stx`

Stake STX tokens with optional lock commitment period.

```clarity
(stake-stx (amount uint) (lock-period uint))
```

**Parameters:**

- `amount`: Amount of STX to stake (minimum 1M STX)
- `lock-period`: Lock commitment (0, 4320, or 8640 blocks)

**Returns:** `(response bool uint)`

#### `initiate-unstake`

Begin the unstaking process with security cooldown.

```clarity
(initiate-unstake (amount uint))
```

**Parameters:**

- `amount`: Amount of STX to unstake

**Returns:** `(response bool uint)`

#### `complete-unstake`

Complete unstaking after cooldown period expires.

```clarity
(complete-unstake)
```

**Returns:** `(response bool uint)`

### Governance Functions

#### `create-proposal`

Create a new governance proposal for protocol changes.

```clarity
(create-proposal (description (string-utf8 256)) (voting-period uint))
```

**Parameters:**

- `description`: Proposal description (10-256 characters)
- `voting-period`: Voting window (100-2880 blocks)

**Returns:** `(response uint uint)` - Returns proposal ID

#### `vote-on-proposal`

Cast a weighted vote on an active proposal.

```clarity
(vote-on-proposal (proposal-id uint) (vote-for bool))
```

**Parameters:**

- `proposal-id`: ID of the proposal to vote on
- `vote-for`: true for yes vote, false for no vote

**Returns:** `(response bool uint)`

### Administrative Functions

#### `initialize-contract`

Initialize the protocol with tier configurations (owner-only).

```clarity
(initialize-contract)
```

#### `pause-contract` / `resume-contract`

Emergency protocol controls (owner-only).

```clarity
(pause-contract)
(resume-contract)
```

### Read-Only Functions

- `get-user-position(user: principal)`: Get comprehensive user position
- `get-staking-position(user: principal)`: Get staking details
- `get-proposal-details(proposal-id: uint)`: Get proposal information
- `get-stx-pool()`: Get total value locked
- `is-contract-paused()`: Check pause status

## 💰 Reward Calculation

The protocol uses a sophisticated reward calculation system:

```
Rewards = (Stake × Base Rate × Tier Multiplier × Lock Multiplier × Blocks) / (100 × Blocks Per Year)
```

### Example Calculations

**Silver Tier (1M STX, No Lock)**

- Base Rate: 5% APY
- Tier Multiplier: 1x
- Lock Multiplier: 1x
- **Effective APY: 5%**

**Gold Tier (5M STX, 30-Day Lock)**

- Base Rate: 5% APY
- Tier Multiplier: 1.5x
- Lock Multiplier: 1.25x
- **Effective APY: 9.375%**

**Platinum Tier (10M STX, 60-Day Lock)**

- Base Rate: 5% APY
- Tier Multiplier: 2x
- Lock Multiplier: 1.5x
- **Effective APY: 15%**

## 🔧 Configuration Parameters

| Parameter | Value | Description |
|-----------|--------|-------------|
| `base-reward-rate` | 500 (5%) | Base annual percentage yield |
| `minimum-stake` | 1,000,000 | Minimum stake requirement (STX) |
| `cooldown-period` | 1,440 | Security cooldown (blocks ~24h) |
| `emergency-mode` | false | Emergency protocol state |

## 🧪 Testing

The protocol includes comprehensive test coverage using Vitest and Clarinet SDK:

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Categories

- **Unit Tests**: Individual function testing
- **Integration Tests**: Multi-function workflows
- **Edge Cases**: Boundary condition testing
- **Security Tests**: Attack vector validation

## 🔒 Security Considerations

### Audit Status

- [ ] Initial security review
- [ ] Formal audit pending
- [ ] Bug bounty program planned

### Security Features

- **Access Control**: Owner-only administrative functions
- **Input Validation**: Comprehensive parameter checking
- **Emergency Controls**: Circuit breaker mechanisms
- **Cooldown Periods**: Anti-manipulation protections

### Known Limitations

- Single owner model (multi-sig recommended for production)
- Fixed tier thresholds (governance upgrades planned)
- No slashing mechanisms (future enhancement)

## 🚢 Deployment Guide

### Testnet Deployment

1. **Configure Clarinet**

   ```toml
   # Clarinet.toml
   [network]
   name = "testnet"
   ```

2. **Deploy Contract**

   ```bash
   clarinet deploy --testnet
   ```

3. **Initialize Protocol**

   ```bash
   clarinet call initialize-contract --testnet
   ```

### Mainnet Deployment

⚠️ **WARNING**: Ensure thorough testing and security audits before mainnet deployment.

1. **Final testing on testnet**
2. **Security audit completion**
3. **Multi-signature wallet setup**
4. **Governance transition plan**

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch**
3. **Add comprehensive tests**
4. **Follow Clarity coding standards**
5. **Submit a pull request**

### Development Standards

- **Code Style**: Follow Clarity formatting conventions
- **Documentation**: Document all public functions
- **Testing**: Maintain >90% test coverage
- **Security**: Consider security implications

## 📚 Documentation

### Additional Resources

- [Clarity Language Guide](https://clarity-lang.org/)
- [Stacks Blockchain Documentation](https://docs.stacks.co/)
- [Clarinet Developer Guide](https://docs.hiro.so/clarinet/)
- [Protocol Whitepaper](./docs/whitepaper.md) *(coming soon)*

### API Reference

Detailed API documentation is available in the `/docs` directory:

- [Function Reference](./docs/api-reference.md)
- [Error Codes](./docs/error-codes.md)
- [Integration Guide](./docs/integration.md)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support & Community

- **Discord**: [Join our community](https://discord.gg/proofstake)
- **Twitter**: [@ProofStakeProtocol](https://twitter.com/proofstake)
- **Email**: <support@proofstake.com>
- **Documentation**: [docs.proofstake.com](https://docs.proofstake.com)

## 🗺️ Roadmap

### Phase 1 - Foundation ✅

- [x] Core staking mechanism
- [x] Tier-based reward system
- [x] Basic governance framework
- [x] Security controls

### Phase 2

- [ ] Advanced governance features
- [ ] Liquid staking tokens
- [ ] Yield optimization strategies
- [ ] Mobile wallet integration

### Phase 3

- [ ] Cross-chain compatibility
- [ ] Institutional features
- [ ] Advanced analytics
- [ ] DAO transition
