# BTC-Sovereign - Decentralized Staking Protocol for Bitcoin L2

A secure, tiered staking system for Bitcoin Layer 2 solutions with integrated governance and optimized reward mechanisms. Built on the Stacks blockchain, BTC-Sovereign combines Bitcoin's security with advanced DeFi capabilities while maintaining true decentralization.

## Table of Contents

- [BTC-Sovereign - Decentralized Staking Protocol for Bitcoin L2](#btc-sovereign---decentralized-staking-protocol-for-bitcoin-l2)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Key Features](#key-features)
    - [Tiered Staking System](#tiered-staking-system)
    - [Core Components](#core-components)
  - [Technical Architecture](#technical-architecture)
    - [Smart Contract Structure](#smart-contract-structure)
    - [System Parameters](#system-parameters)
  - [Installation \& Integration](#installation--integration)
    - [Requirements](#requirements)
  - [Usage Guide](#usage-guide)
    - [Staking Operations](#staking-operations)
    - [Governance Actions](#governance-actions)
  - [Governance System](#governance-system)
    - [Proposal Lifecycle](#proposal-lifecycle)
    - [Voting Power Calculation](#voting-power-calculation)
  - [Security Model](#security-model)
    - [Protocol Safeguards](#protocol-safeguards)
    - [Audit Considerations](#audit-considerations)
  - [Error Reference](#error-reference)
  - [Contributing](#contributing)

## Overview

BTC-Sovereign enables trustless participation in Bitcoin L2 ecosystems through:

- Multi-tiered STX staking with time-lock bonuses
- On-chain governance with BFT voting
- Dynamic reward distribution algorithm
- Non-custodial asset management
- Protocol-owned liquidity pool

Designed for institutional-grade security while maintaining accessibility for retail participants.

## Key Features

### Tiered Staking System

| Tier | Minimum STX | Multiplier | Features Enabled |
|------|-------------|------------|------------------|
| 1    | 1,000,000   | 1x         | Basic voting, Rewards |
| 2    | 5,000,000   | 1.5x       | Enhanced voting, Early提案 |
| 3    | 10,000,000  | 2x         | Protocol fees, Treasury access |

### Core Components

- **Time-Lock Multipliers**: 1.25x (30d), 1.5x (60d)
- **Cooldown Mechanism**: 24-hour security period for withdrawals
- **Adaptive Rewards**: `(base_rate × multiplier × blocks_staked) / 14400000`
- **Governance Engine**: Proposal-based DAO with stake-weighted voting

## Technical Architecture

### Smart Contract Structure

```clarity
(define-map UserPositions
  principal
  {
    stx-staked: uint,
    voting-power: uint,
    tier-level: uint,
    rewards-multiplier: uint
  }
)

(define-map StakingPositions
  principal
  {
    amount: uint,
    lock-period: uint,
    cooldown-start: (optional uint)
  }
)
```

### System Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Base Reward Rate | 5% | Annual percentage rate (APR) |
| Cooldown Period | 1440 blocks | ~24 hours |
| Minimum Stake | 1,000,000 uSTX | ~1 STX |
| Voting Period | 100-2880 blocks | 15m-48h |

## Installation & Integration

### Requirements

- Stacks Node
- Clarinet SDK
- Bitcoin testnet environment

## Usage Guide

### Staking Operations
**Stake STX with Time-Lock:**
```clarity
(contract-call? .btc-sovereign stake-stx u5000000 u8640)
```

**Initiate Unstaking:**
```clarity
(contract-call? .btc-sovereign initiate-unstake u2000000)
```

**Claim Rewards:**
```clarity
(contract-call? .btc-sovereign claim-rewards)
```

### Governance Actions
**Create Proposal:**
```clarity
(contract-call? .btc-sovereign create-proposal "Increase reward rate to 6%" u1440)
```

**Cast Vote:**
```clarity
(contract-call? .btc-sovereign vote-on-proposal u42 true)
```

## Governance System

### Proposal Lifecycle
1. **Creation**: 1M+ voting power required
2. **Voting**: 15m-48h duration
3. **Execution**: >50% approval with quorum
4. **Implementation**: Time-locked upgrades

### Voting Power Calculation
```
voting_power = staked_stx × tier_multiplier × time_boost
```

## Security Model

### Protocol Safeguards
- Emergency pause functionality
- Cooldown-protected withdrawals
- Tiered access control
- STX escrow verification
- Time-locked governance execution

### Audit Considerations
```clarity
(define-constant ERR-COOLDOWN-ACTIVE (err u1004))
(define-constant ERR-BELOW-MINIMUM (err u1006))
(define-constant ERR-PAUSED (err u1007))
```

## Error Reference

| Code | Error | Resolution |
|------|-------|------------|
| 1000 | Unauthorized | Verify sender permissions |
| 1002 | Invalid Amount | Check minimum requirements |
| 1004 | Cooldown Active | Wait 1440 blocks |
| 1006 | Below Minimum | Stake ≥1M uSTX |
| 1007 | Contract Paused | Check protocol status |

## Contributing

1. Fork repository
2. Create feature branch (`git checkout -b feature/improvement`)
3. Commit changes with Clarity linting
4. Push to branch
5. Submit PR with detailed documentation

**Built on Stacks Blockchain**  
*Bringing smart contracts to Bitcoin*
