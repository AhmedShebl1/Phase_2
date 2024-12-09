# Phase 2: Package Manager Project

![License](https://img.shields.io/badge/license-MIT-green)  
![Node.js](https://img.shields.io/badge/node.js-v18.0.0+-brightgreen)  
![React](https://img.shields.io/badge/react-v18.0.0+-brightgreen)

## Project Overview

This repository serves as the central hub for the **Package Manager Project**, encompassing both the backend and frontend components. The project aims to provide a comprehensive solution for managing JavaScript packages, including:

- **Package Ingestion**: Add packages via NPM URLs.
- **Debloating**: Remove unnecessary files to optimize storage.
- **Package Evaluation**: Assess package quality using predefined metrics.
- **Version Control**: Track and manage different package versions.

### Components

1. **Backend**:
   - Handles API requests, package processing, and database interactions.
   - Repository: [Package Manager Backend](https://github.com/abdelrahmanHamdyG/Package-manager-phase-2-)

2. **Frontend**:
   - Provides a user-friendly interface for interacting with the backend services.
   - Repository: [Frontend Dev Packages Registry](https://github.com/zeyad7007/Frontend-Dev-Packages-Registry)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Backend Repository](#backend-repository)
- [Frontend Repository](#frontend-repository)
- [Setup and Configuration](#setup-and-configuration)
- [Deployment](#deployment)
- [Interacting with the Application](#interacting-with-the-application)
- [Contributing](#contributing)
- [License](#license)

---

## Backend Repository

The backend handles the core functionalities of the project, including:

### Key Features

- **API Endpoints**: Facilitate package ingestion, debloating, evaluation, and retrieval.
- **Database Management**: Utilize PostgreSQL for storing package metadata and related information.
- **AWS Integration**: Leverage AWS S3 for file storage and AWS RDS for database hosting.

### Technologies Used

- **Node.js** with **Express**
- **TypeScript**
- **PostgreSQL**
- **AWS S3** and **AWS RDS**

For detailed setup and configuration instructions, refer to the [backend repository's README](https://github.com/abdelrahmanHamdyG/Package-manager-phase-2-).

---

## Frontend Repository

The frontend provides an intuitive interface for interacting with the backend services.

### Key Features

- **User Interface**: Allows users to ingest, debloat, evaluate, and manage packages.
- **Visualization**: Displays package details, evaluation scores, and version history.

### Technologies Used

- **React** with **TypeScript**
- **Vite** for development server and bundling
- **Tailwind CSS** for styling
- **Redux Toolkit** for state management

For detailed setup and configuration instructions, refer to the [frontend repository's README](https://github.com/zeyad7007/Frontend-Dev-Packages-Registry).

---

## Setup and Configuration

To set up the entire application locally:

### Clone the Repository

```bash
git clone https://github.com/AhmedShebl1/Phase_2.git
cd Phase_2
