# Enterprise Banking System

## Overview

The Enterprise Banking System is a full-stack financial web application
designed to address security vulnerabilities and promote financial
discipline in modern digital banking environments. The system enables
secure and reliable digital transactions while incorporating advanced
mechanisms such as automated savings management, milestone-based service
contracts, and continuous fraud risk monitoring.

The platform ensures secure fund transfers using ACID-compliant database
transactions and integrates an asynchronous fraud detection mechanism
that evaluates transaction risks without interrupting the user
experience.

## Core Features

### Asynchronous Fraud Detection Engine

The system includes a background fraud detection engine implemented
using Celery and Redis. When a transaction is initiated, the engine
analyzes transaction velocity, geographic anomalies, and unusual
transaction amounts to generate a risk score. Transactions identified as
suspicious are automatically frozen and flagged for administrative
review.

### Keeper Vaults (Smart Savings)

Keeper Vaults function as algorithmic savings accounts that restrict
withdrawals until predefined conditions are satisfied. These conditions
may include reaching a specified target date or maintaining a minimum
balance in the primary wallet. This mechanism encourages disciplined
savings behavior.

### Milestone Contracts

The platform allows users to create milestone-based service agreements.
These agreements support two operational modes. In Escrow Mode, funds
are locked in advance until milestones are completed. In Credit Mode,
payments are executed incrementally as milestones are fulfilled.

### ACID-Compliant Transactions

All financial transfers are executed using PostgreSQL atomic
transactions to ensure data integrity and reliability. This guarantees
that no partial updates occur and prevents inconsistencies in the
financial ledger.

### Role-Based Access Control

The system provides separate interfaces and privileges for standard
users and administrators. Users can manage accounts, perform transfers,
create vaults, and manage contracts. Administrators are responsible for
tasks such as Know Your Customer verification, fraud review, and overall
system monitoring.

## Technology Stack

### Frontend

React.js\
Tailwind CSS or a similar user interface framework\
Axios for API communication

### Backend

Python 3.x\
Django\
Django REST Framework

### Database and Asynchronous Processing

PostgreSQL as the primary relational database\
Redis as the message broker\
Celery for asynchronous task processing

## System Architecture

### Frontend Layer

The frontend is implemented using React and is responsible for managing
the user interface, handling user interactions, and communicating with
backend APIs.

### Backend Layer

The backend is built with Django and Django REST Framework. It manages
business logic, authentication, authorization, and interaction with the
database through the ORM.

### Data Layer

PostgreSQL is used to store system data including user information,
wallet balances, vault records, milestone contracts, and an immutable
transaction ledger.

### Asynchronous Processing Layer

When a transaction request is initiated, the backend sends a task
message to Redis. A Celery worker retrieves the message, processes the
fraud risk evaluation, and updates the database accordingly. This
process occurs asynchronously so that the main application remains
responsive.

## Local Setup and Installation

### Prerequisites

Python 3.10 or later\
Node.js and npm\
PostgreSQL\
Redis running locally on port 6379

### Clone the Repository

``` bash
git clone https://github.com/kpradyun/Banking_system.git
cd Banking_system
```

### Backend Setup

``` bash
cd backend
python -m venv venv
```

Linux or macOS

``` bash
source venv/bin/activate
```

Windows

``` bash
venv\Scripts\activate
```

Install dependencies

``` bash
pip install -r requirements.txt
```

Create `.env` file

    DB_NAME=banking_db
    DB_USER=postgres
    DB_PASSWORD=yourpassword
    REDIS_URL=redis://localhost:6379/0

Apply migrations

``` bash
python manage.py migrate
```

Run Django server

``` bash
python manage.py runserver
```

Backend will run on http://localhost:8000

### Start Celery Worker

``` bash
celery -A your_project_name worker --loglevel=info
```

### Frontend Setup

``` bash
cd frontend
npm install
npm start
```

Frontend runs on http://localhost:3000 and communicates with
http://localhost:8000

## Contributors

K. Pradyun\
K. Uday Kumar

## Project Objective

The objective of this project is to develop a secure and scalable
digital banking platform that integrates disciplined savings mechanisms,
reliable transaction processing, milestone-based financial agreements,
and real-time fraud detection into a unified full-stack system.
