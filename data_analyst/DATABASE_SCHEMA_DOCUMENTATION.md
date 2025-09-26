# Database Schema Documentation

## Overview

This document provides comprehensive documentation for the SQLite database used in the BI Hiring Test. The database contains business data for a **sports betting and gaming platform** with comprehensive user management, order processing, payment handling, and promotional systems.

## Database Information

- **Database Type**: SQLite
- **File Location**: `data/data.db`
- **Total Tables**: 6
- **Total Records**: ~39,667 across all tables
- **Business Domain**: Sports betting, casino games, and promotional gaming
- **Data Period**: February 2025 - July 2025

## Table Structure and Descriptions

### 1. patron_user_campaigns

**Purpose**: Tracks user participation in marketing campaigns

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "patron_user_campaigns" (
    "user_id" text,
    "campaign_id" integer,
    "campaign_metric_date" text,
    "register_time" text
);
```

**Record Count**: 5,827

**Field Descriptions** (Official Schema):

- `user_id` (STRING): Unique identifier for the user
- `campaign_id` (BIGINT): Numerical identifier for the marketing campaign associated with the user
- `campaign_metric_date` (DATETIME): Timestamp of when the campaign metric was recorded
- `register_time` (DATETIME): Timestamp of when the user registered

**Sample Data**:

```text
bT250218230021puid21847538|22210658326|2025-02-18 23:00:22|2025-02-18 23:00:42
eh250220140427puid26676500|22210658326|2025-02-20 14:04:27|2025-02-20 14:04:57
```

---

### 2. t_patron_user

**Purpose**: Master table for user information and login activity

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "t_patron_user" (
    "user_id" text,
    "create_time" text,
    "last_login_time" text
);
```

**Record Count**: 5,828

**Field Descriptions** (Official Schema):

- `user_id` (STRING): Unique identifier for the user
- `create_time` (DATETIME): Timestamp of when the user account was created
- `last_login_time` (DATETIME): Timestamp of the most recent user login

**Sample Data**:

```text
RV250213020225puid05207974|2025-02-13 2:02:26|2025-02-13 2:13:26
YN250217130538puid17706444|2025-02-17 13:05:38|2025-02-17 13:07:01
```

---

### 3. t_order_record

**Purpose**: Transaction records for all user orders (sports betting and gaming)

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "t_order_record" (
    "order_id" text,
    "user_id" text,
    "order_type" integer,
    "biz_type" integer,
    "sub_biz_type" integer,
    "pay_amount" integer,
    "favor_amount" integer,
    "bonus_amount" float,
    "taxable_prize" integer,
    "winning_status" integer,
    "create_time" text,
    "update_time" text
);
```

**Record Count**: 10,283

**Field Descriptions** (Official Schema):

- `order_id` (STRING): Unique identifier for the order
- `user_id` (STRING): Unique identifier for the user
- `order_type` (INTEGER): Type of order
  - 1 = Singles
  - 2 = Multiples
  - 3 = System
  - 4 = Flexible
  - 5 = One_cut
  - 6 = Anywin
- `biz_type` (INTEGER): Business category of the order
  - 1 = Realsports
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
- `sub_biz_type` (INTEGER): Subcategory within the business type
  - If biz_type = 1: 1=pre-match, 2=live, 3=mixture
  - If biz_type ≠ 1: same value as biz_type
- `pay_amount` (FLOAT): Actual amount paid by the user
- `favor_amount` (FLOAT): Discount or promotion amount applied
- `bonus_amount` (FLOAT): Potential bonus - additional winning amount before tax
- `taxable_prize` (FLOAT): Actual amount won by the user
- `winning_status` (INTEGER): Status of the order
  - 0 = Not completed
  - 10 = Part of order won
  - 20 = All win
  - 30 = All lose
  - 40 = Void bet
  - 90 = Pending
- `create_time` (DATETIME): Timestamp when the order was created
- `update_time` (DATETIME): Timestamp of the most recent update to the order

**Sample Data**:

```text
250401001422ord03434703|CG250322110208puid12244106|2|1|1|0|10|636266.7408|0|30|2025-04-01 0:14:22|2025-04-05 17:14:38
```

---

### 4. t_pocket_pay_record

**Purpose**: Payment transaction records for deposits, withdrawals, and transfers

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "t_pocket_pay_record" (
    "user_id" text,
    "pay_action" integer,
    "trade_code" text,
    "status" integer,
    "amount" integer,
    "platform" text,
    "create_time" text,
    "update_time" text
);
```

**Record Count**: 16,395

**Field Descriptions** (Official Schema):

- `user_id` (STRING): Unique identifier for the user
- `pay_action` (INTEGER): Encoded type of payment action
  - 10 = TRANSFER_IN
  - 20 = TRANSFER_OUT
  - 30 = INNER_TRANSFER
  - 31 = INNER_TRANSFER_OUT
  - 32 = INNER_TRANSFER_IN
  - 40 = FROZEN
  - 50 = UNFROZEN
  - 60 = OFFLINE
  - 95 = REVERSAL
- `trade_code` (STRING): Identifier for the type of transaction
  - DP0001 = user deposit
  - CB0006 = compensation after negative caused by rollback
  - AD0001 = adjust balance in
- `status` (INTEGER): Status of the payment transaction
  - 0 = INIT
  - 10 = PROCESSING
  - 20 = PAY_SUCC
  - 30 = PAY_FAIL
  - 31 = PAY_AUDIT_FAIL
  - 32 = PAY_RISK_FAIL
  - 33 = PAY_MANUAL_FAIL
  - 90 = PAY_UNKNOWN
- `amount` (INTEGER): Amount of the transaction
- `platform` (STRING): Source platform for the transaction (e.g., wap, android)
- `create_time` (DATETIME): Timestamp when the payment record was created
- `update_time` (DATETIME): Timestamp when the payment record was last updated

**Sample Data**:

```text
vH250407190008puid69304090|10|DP0001|0|10|wap|2025-05-19 16:50:12|2025-05-19 16:50:12
```

---

### 5. t_promotion_gift

**Purpose**: Promotional gifts and rewards management system

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "t_promotion_gift" (
    "gift_id" text,
    "plan_id" integer,
    "user_id" text,
    "status" integer,
    "effort_type" integer,
    "plan_name" text,
    "init_bal" integer,
    "cur_bal" integer,
    "delivery_time" text,
    "usable_time" text,
    "used_time" text,
    "expire_time" text
);
```

**Record Count**: 949

**Field Descriptions** (Official Schema):

- `gift_id` (STRING): Unique identifier for the gift assigned to the user
- `plan_id` (BIGINT): Identifier of the promotional plan associated with the gift
- `user_id` (STRING): Unique identifier for the user
- `status` (INTEGER): Status code of the gift
  - 0 = INIT
  - 10 = PRODUCED
  - 20 = DELIVERED
  - 30 = USABLE
  - 40 = FULLY_USED
  - 90 = EXPIRED
  - 99 = RECYCLED
- `effort_type` (INTEGER): Type/category of promotion
  - 1 = One-time cash deduction up to the maximum amount
  - 2 = Full reduction for every spending threshold
  - 3 = Proportional discount
  - 4 = With balance, can be used multiple times up to the maximum each time
- `plan_name` (STRING): Human-readable name of the promotional campaign or plan
- `init_bal` (INTEGER): Initial balance or value of the gift
- `cur_bal` (INTEGER): Current remaining balance of the gift
- `delivery_time` (DATETIME): Timestamp when the gift was delivered
- `usable_time` (DATETIME): Timestamp from when the gift becomes usable
- `used_time` (DATETIME): Timestamp when the gift was actually used
- `expire_time` (DATETIME): Timestamp when the gift expires

**Sample Data**:

```text
250501000042gift482878330|2024112711420602952|ws250329180421puid36187242|40|4|Sportybet Is The Best|10|0|2025/5/1 0:00:43|2025/4/30 21:00:00|2025/5/1 5:45:46|2025/5/15 20:59:59
```

---

### 6. t_promotion_gift_acc_log

**Purpose**: Accounting log for promotional gift transactions and usage tracking

**Schema**:

```sql
CREATE TABLE IF NOT EXISTS "t_promotion_gift_acc_log" (
    "gift_id" text,
    "plan_id" integer,
    "user_id" text,
    "order_id" text,
    "amount" integer,
    "create_time" text
);
```

**Record Count**: 385

**Field Descriptions** (Official Schema):

- `gift_id` (STRING): Unique identifier of the gift being used (links to t_promotion_gift)
- `plan_id` (BIGINT): Identifier of the promotional plan associated with the gift
- `user_id` (STRING): Unique identifier for the user
- `order_id` (STRING): Unique identifier for the order (links to t_order_record)
- `amount` (INTEGER): Amount of gift used in the transaction
- `create_time` (DATETIME): Timestamp when the gift usage record was created

**Sample Data**:

```text
250623083138gift463241680|2025061108000272236|jQ250516090547puid04396642|250623184337ord08991502|3|2025-06-23 18:43:38
```

## Data Relationships

### Primary Relationships

1. **t_patron_user.user_id** ↔ **patron_user_campaigns.user_id**
2. **t_patron_user.user_id** ↔ **t_order_record.user_id**
3. **t_patron_user.user_id** ↔ **t_pocket_pay_record.user_id**
4. **t_patron_user.user_id** ↔ **t_promotion_gift.user_id**
5. **t_promotion_gift.gift_id** ↔ **t_promotion_gift_acc_log.gift_id**
6. **t_order_record.order_id** ↔ **t_promotion_gift_acc_log.order_id**

## Data Insights and Observations

### Time Period Coverage

- **Data Range**: February 2025 - July 2025
- **Active Users**: 5,828 total users
- **Campaign Participation**: 5,827 campaign registrations
- **Order Activity**: 10,283 total orders
- **Payment Transactions**: 16,395 payment records

### Data Quality Notes

- User IDs follow consistent naming patterns
- Timestamps are in YYYY-MM-DD HH:MM:SS format
- Some monetary values are stored as integers, others as floats
- Status codes are used throughout (need business context for interpretation)
