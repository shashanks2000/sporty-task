# Data Analyst Take Home Test

## Task

Create a comprehensive dashboard using the provided database to demonstrate your data analysis and visualization skills.

### Suggested Analysis Areas

Focus your analysis on key business modules and their related OKRs (Objectives and Key Results):

**Core Modules to Analyze:**

- `afbet_main` - Core platform metrics
- `afbet_marketing` - Marketing campaign effectiveness
- `afbet_patron` - Customer engagement and behavior
- `afbet_pocket` - Payment and transaction analysis

**Key Metrics & Topics to Consider:**

- **WAU (Weekly Active Users)** - User engagement and platform usage
- **Retention** - Customer loyalty and churn analysis
- **Payment** - Transaction patterns, payment success rates, revenue metrics
- **Campaign Performance** - Marketing ROI and conversion rates
- **User Lifecycle** - Acquisition, activation, and long-term value
- **Revenue Analysis** - Transaction volumes, payment methods

*Hint: Look for trends, patterns, and actionable insights that could inform business decisions in these areas.*

## Requirements

Before starting, ensure you have the following installed:

- **Docker Desktop** (for running Metabase)
- At least **2GB of available RAM**
- **Web browser** (Chrome, Firefox, Safari, or Edge)

## Environment Setup

This test uses a local Metabase instance connected to a SQLite database. We provide a simple Makefile to launch everything with a single command.

> **Note for Windows Users**: If you're using Windows, please refer to [WINDOWS_SETUP.md](WINDOWS_SETUP.md) for specific setup instructions and alternative commands.

## Quick Start

### Step 1: Navigate to the Project Directory

```bash
cd /path/to/data_analyst
```

### Step 2: Launch Metabase

Please open the Terminal in Docker Desktop.

```bash
make up        # Launch Metabase container
```

*Note: This will start Metabase on port 3002. Keep this terminal window open.*

### Step 3: Access Metabase

1. Open your web browser
2. Navigate to: **[http://localhost:3002](http://localhost:3002)**

### Step 4: Login to Metabase

Use these credentials to log in:

| User                   | Password   |
| ---------------------- | ---------- |
| `candidate@sporty.com` | `123admin` |

### Step 5: Create Your Dashboard

Using the `Data` database, create a dashboard in `Our analytics` that includes:

- Key business metrics and KPIs
- Meaningful visualizations (charts, graphs, tables)
- Clear insights and trends from the data
- Professional formatting and layout

## Stopping the Environment

When finished:

```bash
# Press Ctrl+C in the terminal where Metabase is running
# This will stop and remove the container automatically
```

## Submission Instructions

1. **Stop your Metabase container**
2. **Zip the entire folder data_analyst**
3. **Email the zip file** back to us

## Troubleshooting

- **Port already in use:** Make sure no other applications are using port 3002
- **Docker not found:** Install Docker from [docker.com](https://www.docker.com)
- **Container won't start:** Ensure Docker is running and you have sufficient RAM

## Data Information

The provided SQLite database contains business data for a **sports betting and gaming platform** with tables for:

- User campaigns and metrics
- Order records and transactions  
- Payment records
- Promotional gifts and rewards

### Documentation Resources

To help you understand the data structure and business context, we've provided comprehensive documentation:

- **[DATA_DICTIONARY.md](DATA_DICTIONARY.md)**: Complete business context, field value interpretations, and detailed explanations of all data codes and categories used across tables
- **[DATABASE_SCHEMA_DOCUMENTATION.md](DATABASE_SCHEMA_DOCUMENTATION.md)**: Technical database schema documentation with table structures, field descriptions, sample data, and relationship diagrams

**Recommendation**: Start by reviewing these documentation files to understand the business domain and data relationships before building your dashboard.

Explore the data structure to understand the relationships and build meaningful insights.
Good luck! May you create a dashboard that impresses us with your analytical skills and creativity.
