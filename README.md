Phase 2: Package Manager Project
This repository serves as the central hub for the Package Manager Project, encompassing both the backend and frontend components. The project aims to provide a comprehensive solution for managing JavaScript packages, including ingestion, debloating, evaluation, and version control.

Table of Contents
Project Overview
Backend Repository
Frontend Repository
Setup and Configuration
Deployment
Interacting with the Application
Contributing
License
Project Overview
The Package Manager Project is designed to streamline the management of JavaScript packages by offering:

Package Ingestion: Add packages via NPM URLs.
Debloating: Remove unnecessary files to optimize storage.
Package Evaluation: Assess package quality using predefined metrics.
Version Control: Track and manage different package versions.
The project is divided into two main components:

Backend: Handles API requests, package processing, and database interactions.
Frontend: Provides a user-friendly interface for interacting with the backend services.
Backend Repository
The backend component is available at: Package Manager Backend

Key Features
API Endpoints: Facilitate package ingestion, debloating, evaluation, and retrieval.
Database Management: Utilize PostgreSQL for storing package metadata and related information.
AWS Integration: Leverage AWS S3 for file storage and AWS RDS for database hosting.
Technologies Used
Node.js with Express
TypeScript
PostgreSQL
AWS S3 and AWS RDS
For detailed setup and configuration instructions, refer to the backend repository's README.

Frontend Repository
The frontend component is available at: Frontend Dev Packages Registry

Key Features
User Interface: Allows users to ingest, debloat, evaluate, and manage packages.
Visualization: Displays package details, evaluation scores, and version history.
Technologies Used
React with TypeScript
Vite for development server and bundling
Tailwind CSS for styling
Redux Toolkit for state management
For detailed setup and configuration instructions, refer to the frontend repository's README.

Setup and Configuration
To set up the entire application locally:

Clone the Phase_2 Repository:

bash
Copy code
git clone https://github.com/AhmedShebl1/Phase_2.git
cd Phase_2
Initialize Submodules:

bash
Copy code
git submodule init
git submodule update
Backend Setup:

Navigate to the backend directory:

bash
Copy code
cd Package-manager-phase-2-
Follow the setup instructions provided in the backend repository's README.

Frontend Setup:

Navigate to the frontend directory:

bash
Copy code
cd ../Frontend-Dev-Packages-Registry
Follow the setup instructions provided in the frontend repository's README.

Deployment
For deployment instructions, refer to the respective READMEs of the backend and frontend repositories.

Interacting with the Application
Once both backend and frontend are set up and running:

Access the frontend application in your browser (default: http://localhost:5173).
Use the interface to ingest packages, view details, debloat, evaluate, and manage versions.
Contributing
We welcome contributions to enhance this project. To contribute:

Fork the repository.

Create a new branch:

bash
Copy code
git checkout -b feature-name
Make your changes.

Commit your changes:

bash
Copy code
git commit -m "Description of changes"
Push to your fork:

bash
Copy code
git push origin feature-name
Open a pull request.

License
This project is licensed under the MIT License.

