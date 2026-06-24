# Dynamic QR Code Analytics Platform

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)

A full-stack web application designed to generate, manage, and track dynamic QR codes. Built for businesses that need to update physical marketing materials in real-time while gathering scan analytics.

## 🚀 The Problem
Static QR codes require re-printing whenever a destination URL changes. Furthermore, businesses lack visibility into when and where their codes are being scanned. This project solves that by creating an intermediary routing layer where the physical QR code never changes, but the destination URL and tracking metrics are fully manageable via a web dashboard.

## 🛠️ The Stack & Architecture
- **Frontend:** React.js (Provides a responsive, client-side dashboard for managing campaigns).
- **Backend API:** FastAPI (Python) chosen for its high performance, asynchronous capabilities, and auto-generated Swagger documentation.
- **Database:** PostgreSQL for robust relational data integrity (mapping users to QR campaigns and storing high-volume scan logs).
- **Deployment:** Containerized using Docker and Docker Compose for seamless environment replication.

## 🧠 Technical Challenges Overcome

**1. High-Concurrency Scan Logging**
*Challenge:* Ensuring that redirecting a user to the destination URL happens in milliseconds, without being delayed by the database write operation for analytics.
*Solution:* Leveraged FastAPI's `BackgroundTasks`. The API instantly returns a `307 Temporary Redirect` to the user, while the scan metadata (timestamp, user-agent, IP) is inserted into the PostgreSQL database asynchronously in the background.

**2. State Management & Authentication**
*Challenge:* Securing the dashboard so users can only view and edit their own QR codes.
*Solution:* Implemented JWT (JSON Web Token) authentication within FastAPI, passing the token securely to the React frontend to maintain session state and protect API routes.

## 💻 Running the Project Locally

