# Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce

## 📌 Project Overview

This project is a Salesforce-based customer support automation system that uses **Agentforce** to analyze support ticket descriptions, determine ticket priority, and automate assignment for high-priority tickets.

The system is designed to reduce manual ticket prioritization and help support teams respond to urgent customer issues more efficiently.

## 🎯 Objectives

- Analyze customer support ticket descriptions.
- Predict ticket priority as **High, Medium, or Low**.
- Automatically trigger backend automation for high-priority tickets.
- Assign high-priority tickets to an appropriate support agent.
- Provide a clear action message through Agentforce.
- Maintain ticket information in a custom Salesforce object.

## ✨ Key Features

### 1. Support Ticket Management

A custom Salesforce object named **Support Ticket Intelligence** stores support ticket information.

**API Name:** `Support_Ticket_Intelligence__c`

The object includes:

| Field | Purpose |
|---|---|
| Ticket Number | Auto-generated ticket number |
| Customer | Related customer account |
| Contact | Related contact |
| Issue Type | Technical, Billing, or General |
| Description | Customer's issue description |
| Priority Level | Low, Medium, or High |
| Status | New, In Progress, or Resolved |
| Created Date | Ticket creation date |
| Assigned To | Assigned Salesforce user |
| SLA Breach Risk | Indicates possible SLA breach |
| Resolution Time | Ticket resolution time |

## 🤖 Agentforce Integration

The project uses an Agentforce subagent named:

**Support Ticket Priority Analysis**

**API Name:** `Support_Ticket_Priority_Analysis`

The Agentforce action accepts an **Account Name** and analyzes the latest support ticket associated with that account.

### Agentforce Workflow

```text
User provides Account Name
          ↓
Agentforce retrieves latest ticket
          ↓
Reads ticket description
          ↓
Analyzes urgency keywords
          ↓
Determines priority
     ↙       ↓       ↘
   High    Medium    Low
     ↓       ↓       ↓
Trigger    Return    Return
Flow       result     result
     ↓
Create urgent task
     ↓
Assign support agent
     ↓
Return action message
```

## 🧠 Priority Prediction Logic

The current implementation uses keyword-based analysis of the ticket description.

### High Priority

The ticket is classified as **High** when the description contains keywords such as:

- `urgent`
- `not working`
- `failure`

### Medium Priority

The ticket is classified as **Medium** when the description contains keywords such as:

- `issue`
- `slow`
- `delay`

### Low Priority

If none of the defined priority keywords are detected, the ticket is classified as **Low**.

## ⚙️ Salesforce Flow Automation

The project contains an **Auto-Launched Flow**:

`Support_Ticket_Intellegence`

The flow:

1. Receives the Account Name.
2. Finds the corresponding Account.
3. Retrieves the latest support ticket.
4. Analyzes the ticket description.
5. Determines the priority level.
6. Assigns the appropriate support level.
7. For High-priority tickets, creates an urgent handling Task.
8. Returns the ticket ID, priority, assigned agent, and action message.

### High-Priority Automation

For a High-priority ticket, the Flow creates a Task:

**Subject:** `Urgent Ticket Handling`

The task is associated with the support ticket and configured with:

- Priority: High
- Status: Not Started

## 🔄 SLA Breach Risk

The Flow also supports an SLA breach check based on the ticket's created date.

Tickets older than the configured threshold can be identified as having an increased SLA breach risk.

## 🏗️ Salesforce Components

### Custom Object

`Support_Ticket_Intelligence__c`

### Flow

`Support_Ticket_Intellegence`

### Agentforce Subagent

`Support_Ticket_Priority_Analysis`

### Agentforce Planner Bundle

`EmployeeCopilotPlanner`

The repository also contains the Agentforce planner/action schema files retrieved from the Salesforce org.

## 🛠️ Technology Stack

- **Salesforce**
- **Agentforce**
- **Salesforce Flow**
- **Salesforce DX**
- **Git**
- **GitHub**
- **Metadata API**

## 📁 Project Structure

```text
Customer-Support-Ticket-Agentforce/
│
├── force-app/
│   └── main/
│       └── default/
│           ├── flows/
│           │   └── Support_Ticket_Intellegence.flow-meta.xml
│           │
│           ├── genAiPlannerBundles/
│           │   └── EmployeeCopilotPlanner/
│           │       ├── EmployeeCopilotPlanner.genAiPlannerBundle
│           │       └── ...
│           │
│           └── objects/
│               └── Support_Ticket_Intelligence__c/
│                   ├── object-meta.xml
│                   ├── fields/
│                   └── listViews/
│
├── config/
├── scripts/
├── .forceignore
├── .gitignore
├── package.json
├── sfdx-project.json
└── README.md
```

## 🚀 Setup / Deployment

This repository follows the Salesforce DX project structure.

### 1. Clone the repository

```bash
git clone https://github.com/Kazoli11/Customer-Support-Ticket-Agentforce.git
```

### 2. Open the project

```bash
cd Customer-Support-Ticket-Agentforce
```

### 3. Authenticate to a Salesforce org

```bash
sf org login web --alias MyAgentforceProject
```

### 4. Set the target org

```bash
sf config set target-org=MyAgentforceProject
```

### 5. Deploy the project

```bash
sf project deploy start
```

> Agentforce metadata availability can depend on the Salesforce org, API version, and Agentforce configuration.

## 🔍 Example

### Example 1 — High Priority

**Ticket Description:**

```text
The payment system is not working and this is urgent.
```

**Predicted Priority:**

```text
High
```

**Automation:**

```text
Urgent Ticket Handling Task
Priority: High
```

### Example 2 — Medium Priority

**Ticket Description:**

```text
The application is slow and there is a delay.
```

**Predicted Priority:**

```text
Medium
```

### Example 3 — Low Priority

**Ticket Description:**

```text
I would like general information about the service.
```

**Predicted Priority:**

```text
Low
```

## 📌 Project Benefits

- Reduces manual ticket prioritization.
- Provides consistent priority classification.
- Automates urgent-ticket handling.
- Helps support teams identify high-priority tickets quickly.
- Demonstrates the integration of Agentforce with Salesforce Flow and custom metadata.

## 🔮 Future Enhancements

Potential future improvements include:

- AI/ML-based priority prediction instead of keyword-only classification.
- More advanced SLA prediction.
- Automatic routing based on support-agent skills and workload.
- Customer sentiment analysis.
- Dashboard and reporting for ticket priority trends.
- Integration with notification systems for urgent tickets.

## 👩‍💻 Project

**Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce**

Built using Salesforce and Agentforce to demonstrate intelligent customer-support ticket analysis and automated workflow execution.

## 📄 License

This project is intended for educational and portfolio purposes.
