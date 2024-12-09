# Phase 2: Package Manager Project

![License](https://img.shields.io/badge/license-MIT-green)  
![TypeScript](https://img.shields.io/badge/typescript-v4.0.0+-blue)  
![React](https://img.shields.io/badge/react-v18.0.0+-brightgreen)

## Table of Contents

- [Project Overview](#project-overview)
- [Links](#links)
- [Endpoints Overview](#endpoints-overview)
- [Backend Repository](#backend-repository)
- [Frontend Repository](#frontend-repository)
- [Setup and Configuration](#setup-and-configuration)
- [Deployment](#deployment)
- [Interacting with the Application](#interacting-with-the-application)
- [Contributing](#contributing)
- [Contributors](#Contributors)
- [License](#license)

---

## Project Overview

The **Package Manager API** provides a trustworthy module registry to manage JavaScript packages. It allows for package ingestion, version control, rating, cost evaluation, and more. The API is designed to meet baseline requirements and Access Control track.

A **Package ID** is used as a unique identifier for a package and its version. Example IDs:
- PackageName: `Alpha`, Version: `1.1.1` → ID: `988645763`
- PackageName: `Alpha`, Version: `1.3.2` → ID: `357898765`

---

## Links

1. **API**:
   - [https://fuwwahpackreg.xyz/](https://fuwwahpackreg.xyz/)

2. **Website**:
   - [https://frontend-dev-packages-registry.vercel.app/](https://frontend-dev-packages-registry.vercel.app/)

---

## Endpoints Overview

### **Baseline Endpoints**

#### `/packages` - **Get Packages** (POST)
- **Purpose**: Retrieve a list of packages that fit a query.
- **Features**: Pagination via `offset` in headers.
- **Response**: List of package metadata.
- **Errors**: 
  - `400` – Missing/invalid fields.
  - `403` – Authentication failure.
  - `413` – Too many packages returned.

---

#### `/package/{id}` - **Get/Update Package**
- **GET**:
  - **Purpose**: Fetch details for a specific package by ID.
  - **Response**: Package metadata and content.
  - **Errors**:
    - `400` – Missing/invalid fields.
    - `403` – Authentication failure.
    - `404` – Package not found.

- **POST**:
  - **Purpose**: Update an existing package with a new version.
  - **Response**: Updated metadata.
  - **Errors**:
    - `400` – Invalid fields.
    - `403` – Authentication failure.
    - `404` – Package not found.

---

#### `/reset` - **Reset Registry** (DELETE)
- **Purpose**: Reset the registry to its default state.
- **Response**: Confirmation of reset.
- **Errors**:
  - `401` – Insufficient permissions.
  - `403` – Authentication failure.

---

#### `/package` - **Upload/Ingest Package** (POST)
- **Purpose**: Add a new package to the registry.
- **Options**:
  - Provide `Content` (Base64-encoded zip) or `URL`.
  - Enable `debloat` for storage optimization.
- **Response**: Metadata of the uploaded package.
- **Errors**:
  - `400` – Invalid fields or conflicting inputs (e.g., both `Content` and `URL` set).
  - `403` – Authentication failure.
  - `409` – Package already exists.
  - `424` – Package disqualified due to poor rating.

---

#### `/package/{id}/rate` - **Get Package Rating** (GET)
- **Purpose**: Retrieve the computed ratings for a package.
- **Response**: Ratings (e.g., RampUp, NetScore).
- **Errors**:
  - `400` – Invalid Package ID.
  - `403` – Authentication failure.
  - `404` – Package not found.
  - `500` – Rating system error.

---

#### `/package/{id}/cost` - **Get Package Cost** (GET)
- **Purpose**: Calculate the download cost (in MB) of a package and its dependencies.
- **Options**:
  - Include dependencies in the calculation via `dependency=true`.
- **Response**: Cost details.
- **Errors**:
  - `400` – Invalid Package ID.
  - `403` – Authentication failure.
  - `404` – Package not found.
  - `500` – Error in dependency resolution.

---

#### `/authenticate` - **Authenticate User** (PUT)
- **Purpose**: Obtain an access token for authenticated endpoints.
- **Response**: Authentication token (e.g., JWT).
- **Errors**:
  - `400` – Invalid fields in the request.
  - `401` – Incorrect user/password.
  - `501` – Authentication not implemented.

---

#### `/package/byRegEx` - **Search by Regular Expression** (POST)
- **Purpose**: Search for packages using a regex pattern over names and READMEs.
- **Response**: List of matching packages.
- **Errors**:
  - `400` – Invalid fields in regex query.
  - `403` – Authentication failure.
  - `404` – No packages found.

---

### **Access Control Endpoints**

#### `/logout` - **Logout User** (POST)
- **Purpose**: Logs out the authenticated user by invalidating their session or token.
- **Security**: Requires a valid `X-Authorization` header.
- **Responses**:
  - `200`: Logged out successfully.
  - `500`: Internal server error.

---

#### `/Access/{user_id}` - **Get/Update User Access**
- **GET**:
  - **Purpose**: Retrieve access permissions for a specific user. Admin only.
  - **Responses**:
    - `202`: Successfully retrieved user access.
    - `403`: Only admins can get user access.
    - `500`: Internal server error.

- **POST**:
  - **Purpose**: Update access permissions for a specific user. Admin only.
  - **Responses**:
    - `200`: User permissions updated successfully.
    - `403`: Only admins can update user access.
    - `500`: Internal server error.

---

### **Group Management Endpoints**

#### `/group` - **Create a New Group** (POST)
- **Purpose**: Creates a new user group. Admin only.
- **Responses**:
  - `202`: Group created successfully.
  - `403`: Only admins can create groups.
  - `500`: Internal server error.

---

#### `/add_user/{groupid}` - **Assign User to Group** (POST)
- **Purpose**: Assigns a user to a specific group. Admin only.
- **Responses**:
  - `201`: User added to the group successfully.
  - `403`: Only admins can assign users to groups.
  - `500`: Internal server error.

---

#### `/add_package/{groupid}` - **Assign Package to Group** (POST)
- **Purpose**: Assigns a specific package to a group. Admin only.
- **Responses**:
  - `200`: Package assigned to group successfully.
  - `403`: Only admins can assign packages to groups.
  - `500`: Internal server error.

---

#### `/groups` - **Get All Groups** (GET)
- **Purpose**: Retrieves a list of all user groups. Admin only.
- **Responses**:
  - `200`: List of all groups.
  - `403`: Only admins can view groups.
  - `500`: Internal server error.

---

#### `/groups/{groupid}` - **Get Users by Group** (GET)
- **Purpose**: Retrieves the list of users assigned to a specific group. Admin only.
- **Responses**:
  - `202`: Successfully retrieved users in the group.
  - `403`: Only admins can view users by groups.
  - `500`: Internal server error.

---

### **History Management**

#### `/history` - **Get Package History** (POST)
- **Purpose**: Retrieves the history of a specific package. Admin only.
- **Responses**:
  - `200`: Package history returned successfully.
  - `403`: Only admins can view package history.
  - `500`: Internal server error.

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

---

## Frontend Repository

The frontend provides an intuitive interface for interacting with the backend services.

### Key Features

- **User Interface**: Allows users to ingest, debloat, evaluate, and manage packages.
- **Visualization**: Displays package details, evaluation scores, and version history.

### Technologies Used

- **React** with **TypeScript**
- **Vite** for development server and bundling
- **Bootstrap** for styling
---

## Setup and Configuration

To set up the entire application locally:

### Clone the Repository

```bash
git clone https://github.com/AhmedShebl1/Phase_2.git
cd Phase_2
```

### Initialize Submodules

To ensure the backend and frontend repositories are included, initialize the submodules:

```bash
git submodule init
git submodule update
```

## Backend Setup

Navigate to the backend directory:

```bash
cd Package-manager-phase-2-
```

### Install Dependencies
```bash
npm install
```
### Set up environment variables:

Create a .env file in the root of the backend directory with the following:

```bash
DATABASE_URL=<Your PostgreSQL connection string>
AWS_ACCESS_KEY_ID=<Your AWS Access Key>
AWS_SECRET_ACCESS_KEY=<Your AWS Secret Key>
S3_BUCKET_NAME=<Your S3 Bucket Name>
PORT=3000
```
### Compile TypeScript code:
```bash
tsc
```

### Start the backend server:
```bash
node dist/index.js
```
---

## Frontend Setup

Navigate to the backend directory:

```bash
cd ../Frontend-Dev-Packages-Registry
```

### Install Dependencies
```bash
npm install
```
### Start the development server:
```bash
npm run dev
```
---
## Contributing

We welcome contributions to enhance this project. To contribute:

1. **Fork the repository.**

2. **Create a new branch:**
```bash
   git checkout -b feature-name
 ```

3. **Make your changes.**

4. **Commit your changes:**
 ```bash
   git commit -m "Description of changes"
```

5. **Push to your fork:**
 ```bash
   git push origin feature-name
```

6. **Open a pull request.**

---

## Deployment

The backend and frontend have Continuous Deployment (CD) pipelines set up.  
Simply pushing changes to their respective repositories will automatically trigger a deployment.

- **Backend Deployment**: The backend is deployed to [https://fuwwahpackreg.xyz/](https://fuwwahpackreg.xyz/).  
- **Frontend Deployment**: The frontend is hosted at [https://frontend-dev-packages-registry.vercel.app/](https://frontend-dev-packages-registry.vercel.app/).

---

## Interacting with the Application

The application can be accessed in two ways:

1. **Website**:  
   Use the frontend interface at [https://frontend-dev-packages-registry.vercel.app/](https://frontend-dev-packages-registry.vercel.app/) to interact with the application.

2. **Programmatically**:  
   Utilize the backend API at [https://fuwwahpackreg.xyz/](https://fuwwahpackreg.xyz/) for programmatic interaction. Refer to the API documentation for details on available endpoints.

---

## Contributors

- **Zeyad Ayman** - [zelafifi@purdue.edu](mailto:zelafifi@purdue.edu)
- **Ahmed Shebl** - [ashebl@purdue.edu](mailto:ashebl@purdue.edu)
- **Abdelrahman Ghania** - [aghania@purdue.edu](mailto:aghania@purdue.edu)
- **Ahmed Sayed** - [omar9@purdue.edu](mailto:omar9@purdue.edu)


---

## License

This project is licensed under the **MIT License**.

```text
MIT License

Copyright (c) 2024 Your Project Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.