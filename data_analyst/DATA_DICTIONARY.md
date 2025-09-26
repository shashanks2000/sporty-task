# Data Dictionary and Business Context

## Business Context

This database represents a comprehensive **sports betting and gaming platform** with the following key business processes:

### Core Business Areas

1. **Sports Betting Operations**
   - Real sports betting (pre-match, live, mixed)
   - Various bet types (singles, multiples, system bets)
   - Comprehensive win/loss tracking

2. **Casino/Gaming Operations**
   - Multiple casino games (Red Black, Blackjack, Live Games)
   - Spin games (Spin2Win, Spin Da Bottle, Spin Match)
   - Specialty games (Sporty Hero, Galaxy Go, Sporty Jet)

3. **User Management & Campaigns**
   - User registration and lifecycle tracking
   - Marketing campaign participation and effectiveness

4. **Payment & Financial Operations**
   - Multi-type transactions (deposits, withdrawals, transfers)
   - Risk management and audit controls
   - Platform-specific payment processing

5. **Promotional System**
   - Sophisticated gift/bonus distribution
   - Multiple promotion types and redemption tracking
   - Loyalty rewards and incentives

## Field Value Interpretations

### t_order_record Business Classifications

**Order Types**:

- 0 = Singles (For Games Orders)
- 1 = Singles
- 2 = Multiples  
- 3 = System
- 4 = Flexible
- 5 = One_cut
- 6 = Anywin

**Business Types (Gaming Categories)**:

- 1 = Realsports (sports betting)
- 105 = Red Black
- 106 = Spin2Win
- 107 = Live Games  
- 108 = Blackjack
- 112 = Sporty Hero
- 113 = Even Odd
- 115 = Spin Da Bottle
- 116 = Spribe
- 121 = Rush
- 122 = Ping Pong
- 123 = Spin Match
- 130 = Pocket Rockets
- 131 = HubTech
- 133 = Special One
- 134 = Sporty Jet
- 136 = Galaxy Go

**Winning Status**:

- 0 = Not completed
- 10 = Part of order won
- 20 = All win  
- 30 = All lose
- 40 = Void bet
- 90 = Pending

### t_pocket_pay_record Transaction Types

**Payment Actions**:

- 10 = TRANSFER_IN (deposits)
- 20 = TRANSFER_OUT (withdrawals)
- 30 = INNER_TRANSFER
- 31 = INNER_TRANSFER_OUT
- 32 = INNER_TRANSFER_IN
- 40 = FROZEN
- 50 = UNFROZEN
- 60 = OFFLINE
- 95 = REVERSAL

**Payment Status**:

- 0 = INIT
- 10 = PROCESSING
- 20 = PAY_SUCC (success)
- 30 = PAY_FAIL (failed)
- 31 = PAY_AUDIT_FAIL
- 32 = PAY_RISK_FAIL
- 33 = PAY_MANUAL_FAIL
- 90 = PAY_UNKNOWN

### t_promotion_gift Promotion Types

**Gift Status**:

- 0 = INIT
- 10 = PRODUCED
- 20 = DELIVERED
- 30 = USABLE
- 40 = FULLY_USED
- 90 = EXPIRED
- 99 = RECYCLED

**Effort Types**:

- 1 = One-time cash deduction up to maximum amount
- 2 = Full reduction for every spending threshold
- 3 = Proportional discount
- 4 = With balance, multiple use up to maximum each time

### Platform Types

- `wap`: Mobile web application
- `android`: Native Android application
