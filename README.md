# ARVIN — Real Estate & Office Management System

### A purpose-built Windows desktop application for real estate and construction operations.

<p align="center">
  <img src="assets/dashboard.png" alt="Arvin Dashboard" width="900">
</p>

<p align="center">
  <strong>Real-world workflow · Offline-first · Persian RTL · Desktop-native · SQLite</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/PySide6-Desktop%20UI-41CD52?style=flat-square&logo=qt&logoColor=white">
  <img src="https://img.shields.io/badge/SQLite-Local%20Database-003B57?style=flat-square&logo=sqlite&logoColor=white">
  <img src="https://img.shields.io/badge/Windows-Desktop-0078D6?style=flat-square&logo=windows&logoColor=white">
  <img src="https://img.shields.io/badge/PyInstaller-Packaging-FFD343?style=flat-square">
</p>

---

## Overview

**Arvin** is a custom-built Windows desktop management system developed for a real-world real estate and construction office.

The application centralizes property records, customer-related information, partnership files, advanced search, operational tasks, scheduling, and calendar-based planning into a single offline-first workflow.

The project was designed around the actual operational requirements of its target environment rather than around a generic CRUD template.

That distinction shaped the entire system — from the data model and category-specific forms to the Persian RTL interface, responsive desktop layout, task calendar, record lifecycle management, and Windows deployment workflow.

---

## Product Showcase

<table>
<tr>
<td width="50%">

### Dashboard

Centralized operational overview with statistics, recent records, notifications and calendar access.

<img src="assets/dashboard.png" alt="Dashboard">

</td>
<td width="50%">

### Property Management

Dedicated workflows for managing real estate records across multiple business categories.

<img src="assets/property-management.png" alt="Property Management">

</td>
</tr>

<tr>
<td width="50%">

### Advanced Search

Category-aware filtering for quickly locating relevant records.

<img src="assets/advanced-search.png" alt="Advanced Search">

</td>
<td width="50%">

### Work Calendar

Persian calendar with holidays, occasions and task indicators.

<img src="assets/work-calendar.png" alt="Work Calendar">

</td>
</tr>

<tr>
<td width="50%">

### Task Management

Internal office tasks connected directly to calendar dates.

<img src="assets/task-management.png" alt="Task Management">

</td>
<td width="50%">

### Data Entry

Dynamic forms adapted to the selected business workflow.

<img src="assets/property-form.png" alt="Property Form">

</td>
</tr>
</table>

---

# Why This Project?

The original workflow relied heavily on manually maintained records.

The objective was to create a focused desktop system that could:

* centralize operational data
* reduce repetitive manual work
* provide faster record retrieval
* separate different real-estate workflows
* introduce internal task management
* provide calendar-based planning
* work completely offline
* remain usable on different desktop screen sizes
* be packaged as a standalone Windows application

The result is a domain-specific application rather than a generic database interface.

---

# Core Product Areas

## 01 — Property Management

The application separates the primary real-estate workflows into dedicated categories:

| Category         | Purpose                          |
| ---------------- | -------------------------------- |
| **For Sale**     | Properties available for sale    |
| **For Rent**     | Properties available for rent    |
| **Buy Request**  | Customer requests to purchase    |
| **Rent Request** | Customer requests to rent        |
| **Partnership**  | Partnership / investment records |

Each workflow exposes fields appropriate to its business context.

Property records can contain information including:

* Region
* Property type
* Usage
* Area
* Address
* Construction year
* Rooms
* Floor
* Units
* Direction
* Price per square meter
* Total price
* Deposit
* Monthly rent
* Customer / owner information
* Phone number
* Registration date
* Additional notes

---

# 02 — Dynamic Data Entry

Instead of using one oversized form for every record type, the application dynamically adapts the data-entry workflow according to the selected category.

This allows the interface to remain focused while preventing irrelevant fields from appearing in unrelated workflows.

### Design principle

```text
Selected Business Type
          │
          ▼
Category-specific fields
          │
          ▼
Validated input
          │
          ▼
Persistent SQLite record
```

This approach keeps the UI aligned with the underlying domain model.

---

# 03 — Partnership Management

Partnership records use their own dedicated workflow.

The module supports separate information for:

* Property owner
* Investor
* Owner contact information
* Investor contact information
* Partnership role
* Property location
* Dimensions
* Direction
* Registration date
* Additional notes

Dedicated list, form and details views keep partnership workflows independent from standard property records.

---

# 04 — Search & Discovery

The system provides multiple levels of record discovery.

### Standard search

Search through commonly used fields such as:

* Name
* Phone
* Region
* Address
* Property type

### Advanced search

Category-specific filters allow records to be narrowed using numerical criteria.

Depending on the selected workflow, users can filter by:

* Price range
* Budget range
* Deposit range
* Monthly rent range
* Area range
* Room count

The search interface is therefore driven by the business context rather than exposing every possible filter at once.

---

# 05 — Work Calendar

The **Work Calendar** is an internal operational planning module.

It combines Persian date handling with office task management.

### Calendar capabilities

* Jalali / Persian calendar
* Hijri date information
* Month navigation
* Today navigation
* Current-date highlighting
* Weekend indication
* Official holiday indication
* Occasion display
* Task-day indicators
* Selected-date state
* Integrated task display

The dashboard also contains a compact calendar representation that connects directly to the full work-calendar workflow.

---

# 06 — Task Management

Tasks are designed for internal office operations rather than customer-facing scheduling.

Each task can contain:

* Title
* Date
* Time
* Type
* Priority
* Related property/customer
* Description
* Completion state

### Task types

* Contact
* Property Visit
* Document Follow-up
* Meeting

### Priority levels

* Low
* Medium
* High

Tasks can be created, edited, completed and removed directly through the calendar workflow.

---

# 07 — Dashboard & Operational Overview

The dashboard provides a high-level view of the current state of the office.

It brings together:

* Category statistics
* Recent records
* Upcoming tasks
* Relevant notifications
* Calendar information
* Task counts
* Quick navigation

The goal is to make the dashboard an **operational starting point**, rather than simply a collection of statistics.

---

# 08 — Record Lifecycle Automation

The system includes automated lifecycle handling for standard property records.

Records are evaluated based on their Persian registration date.

The application can:

* identify aging records
* surface upcoming expiration states
* notify about records approaching expiration
* automatically remove records that exceed the configured lifecycle threshold

The current implementation uses a **91-day lifecycle** for standard property records.

Partnership records are handled separately and are excluded from this automatic cleanup mechanism.

---

# Architecture

The application follows a modular desktop architecture with clear separation between UI, data access, models and services.

```text
                         ARVIN
                           │
             ┌─────────────┴─────────────┐
             │                           │
        Presentation                 Application
             │                           │
      ┌──────┼──────┐             ┌──────┴──────┐
      │      │      │             │             │
   Dashboard Forms Calendar    Models       Services
      │      │      │             │             │
      └──────┴──────┘             │       Lifecycle Logic
             │                    │
             └──────────┬─────────┘
                        │
                  Database Layer
                        │
                ┌───────┴───────┐
                │               │
           Property DB       Task DB
                │               │
                └───────┬───────┘
                        │
                     SQLite
```

### Main layers

**UI Layer**

PySide6-based desktop interface containing dashboards, forms, lists, dialogs, calendar and search interfaces.

**Model Layer**

Domain objects representing property and application data.

**Database Layer**

SQLite persistence with dedicated data-access logic for property and task data.

**Service Layer**

Application-level logic such as automatic record cleanup.

**UI Infrastructure**

Reusable formatting, responsive sizing and centralized design-system utilities.

---

# Data Architecture

The application uses local SQLite persistence.

Two databases are maintained:

### Property Database

Responsible for:

* Property records
* Partnership records
* CRUD operations
* Category queries
* Region queries
* Schema initialization / migration

### Task Database

Responsible for:

* Office tasks
* Task status
* Task dates
* Task priorities
* Task relationships
* Calendar retrieval

This separation keeps task operations independent from the primary property-data lifecycle.

---

# Persian RTL Engineering

The application was built specifically for a Persian-language office environment.

RTL behavior is considered across:

* Navigation
* Forms
* Dialogs
* Tables
* Calendar
* Task cards
* Details pages
* Menus
* Labels
* Numeric fields

Special handling is used for mixed Persian/Latin content such as phone numbers, timestamps and numerical values.

This makes RTL part of the application's interaction model rather than simply a translated UI layer.

---

# Responsive Desktop UI

The interface was designed to remain usable across different desktop environments.

A dedicated responsive layer provides:

* Screen-profile detection
* Dimension scaling
* Responsive window sizing
* Minimum size handling
* Scrollable forms
* Adaptive dialogs
* Resolution-aware styling
* Shared UI scaling

The objective is to preserve the application's visual hierarchy while avoiding oversized fixed layouts on smaller displays.

---

# Design System

The visual language is centralized rather than independently styled screen by screen.

The design system manages:

* Colors
* Dimensions
* Typography scaling
* Component sizing
* QSS processing
* Screen profiles
* Shared UI behavior

This provides consistency across the dashboard, forms, lists, dialogs and calendar.

---

# Windows Deployment

The application includes a dedicated Windows build workflow based on **PyInstaller**.

The deployment configuration supports:

* Standalone `.exe` generation
* Custom ARVIN application icon
* Bundled application assets
* Resource resolution in packaged mode
* Persistent data directories
* Maximized application startup

The build process is documented separately within the original development project.

---

# Technology Stack

| Technology          | Role                         |
| ------------------- | ---------------------------- |
| **Python**          | Core application logic       |
| **PySide6**         | Desktop UI framework         |
| **SQLite**          | Local persistence            |
| **jdatetime**       | Persian/Jalali date handling |
| **hijri-converter** | Hijri calendar conversion    |
| **persiantools**    | Persian utilities            |
| **PyInstaller**     | Windows packaging            |
| **Qt Style Sheets** | Application styling          |

---

# Engineering Highlights

### Domain-specific design

The application was modeled around actual office workflows instead of a generic CRUD abstraction.

### Context-aware forms

Data-entry interfaces adapt to the selected business category.

### Offline-first architecture

Core functionality does not depend on a cloud service, remote server or external API.

### Local persistence

SQLite provides lightweight and reliable storage for a single-office desktop environment.

### Dual-database strategy

Property data and task data are persisted separately.

### Lifecycle automation

Property records can be automatically evaluated and cleaned according to their registration age.

### Calendar integration

Tasks are connected directly to calendar dates and reflected throughout the dashboard.

### RTL-first interface

Persian interaction requirements were considered throughout the application architecture.

### Responsive desktop engineering

A reusable sizing and styling layer prevents each screen from becoming dependent on a single display resolution.

### Windows packaging

The project includes a reproducible path toward a standalone Windows executable.

---

# Project Structure

The original application is organized into dedicated modules:

```text
RealEstateManager/
│
├── main.py
│
├── models/
│   └── property.py
│
├── database/
│   ├── db_manager.py
│   └── task_db.py
│
├── services/
│   └── auto_cleanup.py
│
├── ui/
│   ├── dashboard.py
│   ├── main_window.py
│   ├── property_list.py
│   ├── property_form.py
│   ├── property_details.py
│   ├── partnership_list.py
│   ├── partnership_form.py
│   ├── partnership_details.py
│   ├── advanced_search.py
│   ├── add_task_dialog.py
│   ├── work_calendar.py
│   ├── responsive.py
│   ├── design_system.py
│   ├── formatters.py
│   └── styles/
│       └── main.qss
│
└── assets/
```

> The source tree above documents the architecture of the application.
> The public showcase repository intentionally does not contain the application source code.

---

# Portfolio Scope

This repository is intentionally structured as a **visual and technical showcase** rather than a source-code distribution.

### Included

* Project documentation
* Architecture overview
* Technical overview
* UI screenshots
* Selected animated demonstrations

### Not included

* Application source code
* Executable binaries
* SQLite databases
* Customer information
* Property records
* Private office documents
* Development-only files

The purpose is to demonstrate the engineering and product-design work while keeping the underlying application and real-world data private.

---

# What This Project Demonstrates

This project demonstrates an end-to-end software development workflow:

```text
Real-world requirements
        ↓
Domain analysis
        ↓
Data modeling
        ↓
Application architecture
        ↓
UI / UX design
        ↓
Database implementation
        ↓
Workflow automation
        ↓
Responsive desktop engineering
        ↓
Windows packaging
        ↓
Real-world deployment
```

The emphasis is not only on writing code, but on translating a real operational problem into a maintainable software product.

---

# Role & Contribution

**Arian Shayestehfard — Design & Development**

Responsibilities included:

* Requirements analysis
* Workflow design
* Domain modeling
* Database design
* SQLite implementation
* PySide6 UI development
* Persian RTL engineering
* Responsive UI implementation
* Calendar and task management
* Lifecycle automation
* Application styling
* Windows packaging
* Deployment preparation
* Product customization

---

# Repository Purpose

This repository exists as a **portfolio case study** for the Arvin Real Estate Manager project.

It is intended to demonstrate:

* Desktop application development
* Python engineering
* UI architecture
* Database design
* Product-oriented development
* Real-world requirements analysis
* RTL interface engineering
* Software packaging and deployment

---

<p align="center">

### Built for a real workflow, not a tutorial.

**Python · PySide6 · SQLite · Windows**

**Arian Shayestehfard**

</p>
