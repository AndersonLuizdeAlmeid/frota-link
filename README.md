<div align="center">

# FrotaLink

**Enterprise fleet management platform — multi-company SaaS built with Clean Architecture, .NET, and PostgreSQL.**

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-messaging-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)](https://www.rabbitmq.com/)

</div>

---

## About

FrotaLink is a production-grade SaaS platform that enables companies to manage their vehicle fleets end-to-end — from travel requests and driver assignment to financial reporting and real-time notifications.

The system supports multiple companies on a single installation, each with full data isolation. Roles are separated across three levels: global administrator, company manager, and driver.

> This repository is a public showcase. The source code is proprietary and kept in a private repository.

---

## Key Features

- **Multi-company tenancy** — each company operates in full isolation with hash-based access control
- **Complete travel lifecycle** — request → confirm → assign driver → start → complete → report
- **Real-time push notifications** — passengers and drivers notified at each travel status change via Web Push + RabbitMQ
- **Financial reporting** — costs by period, cost center, and requester; exportable as CSV
- **Fleet analytics** — driver performance, fleet utilization rate, and peak hour analysis
- **Gantt view** — visual scheduling of travels and driver availability
- **Cost centers** — full cost attribution per department or business unit
- **Toll management** — register and track toll costs per route
- **Password security** — Argon2 hashing with custom salt

---

## Architecture
FrotaLink
├── FrotaLink.WebApi # REST API — controllers, DI, filters, middlewares
├── FrotaLink.Application # Business logic — handlers, queries, repositories, domain
├── FrotaLink.Common # Cross-cutting — JWT, encryption, DB connection, validators
└── FrotaLink.NotificationWorker # Background service — RabbitMQ consumer + Web Push dispatcher

The project follows **Clean Architecture** with a custom Handler pattern:
Request → Controller → IHandler → Handler → IRepository → PostgreSQL
↘ IQuery (read side)

Each domain module is fully self-contained:
Cars/
├── Domain/ Car.cs
├── Dtos/ CarDto.cs
├── Handlers/ CreateCar/ ChangeCar/ ActivateCar/ DeactivateCar/
├── Queries/ ICarQuery.cs CarQuery.cs
└── Repositories/ ICarRepository.cs CarRepository.cs

---
## Tech Stack
| Layer | Technology |
|---|---|
| API | ASP.NET Core 8, C# |
| ORM / Query | Dapper (raw SQL, no EF Core) |
| Database | PostgreSQL 16 |
| Messaging | RabbitMQ |
| Push Notifications | Web Push Protocol |
| Frontend | Next.js 15, TypeScript |
| Auth | JWT + Argon2 password hashing |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions → Docker Hub |
| Migrations | Versioned SQL scripts (v1.sql, v2.sql, ...) |
---
## System Roles
| Role | Access |
|---|---|
| **Administrator** | Full platform access — companies, users, cars, routes, tolls, reports |
| **Company Manager** | Manages travel requests, cost centers, and views company-scoped reports |
| **Driver** | Views assigned travels, starts and completes trips, receives push notifications |
---
## Domain Modules
| Module | Responsibilities |
|---|---|
| `Companies` | Company registration, hash-based access for company views |
| `Users` | User lifecycle — create, activate, deactivate, permission control |
| `Cars` | Vehicle registration, activation, and driver association |
| `Routes` | Route definition with ordered waypoints |
| `TravelRequests` | Request creation, approval workflow, cost assignment |
| `Travels` | Driver assignment, trip execution, passenger notifications |
| `Reports` | Financial, utilization, performance, and peak hour reports |
| `Dashboard` | KPIs — completed travels, revenue by day, top drivers and vehicles |
| `CostCenters` | Department-level cost attribution |
| `Tolls` | Toll registration and cost tracking per route |
| `Tracking` | Audit log for all domain events |
| `Subscriptions` | Web Push subscription management |
---
## Infrastructure

```yaml
# Automated CI/CD on every push to main
- Build .NET solution
- Docker image build
- Push to Docker Hub
- Deploy to production
Docker Compose for local dev and production
Multi-environment config — Development / Production separation
Versioned SQL migrations applied in order at startup
API Overview
POST   /auth/login
POST   /auth/register
GET    /companies
POST   /companies
GET    /cars
POST   /cars/{id}/activate
POST   /travel-requests
PUT    /travel-requests/{id}/confirm
PUT    /travel-requests/{id}/cancel
POST   /travels/{id}/assign-driver
PUT    /travels/{id}/start
PUT    /travels/{id}/complete
GET    /reports/costs-by-period
GET    /reports/driver-performance
GET    /reports/fleet-utilization
GET    /dashboard 
```
## Contact

**Anderson Luiz de Almeida** — Backend Developer | .NET · Clean Architecture · Docker

<a href="https://linkedin.com/in/anderson-luiz-almeida">
  <img src="https://img.shields.io/badge/LinkedIn-anderson_luiz_almeida-0A66C2?style=flat-square&logo=linkedin&logoColor=white" />
</a>
&nbsp;
<a href="https://github.com/AndersonLuizdeAlmeid">
  <img src="https://img.shields.io/badge/GitHub-AndersonLuizdeAlmeid-181717?style=flat-square&logo=github&logoColor=white" />
</a>
