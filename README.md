# PingBox 💬  
*A Real-Time Serverless Chat Application*

## 📖 Introduction
**PingBox** is a cloud-based real-time chat application designed to enable users to communicate instantly — without managing any servers.  
This project leverages **AWS serverless technologies** to provide scalability, reliability, and cost efficiency.  
By integrating services such as **AWS Lambda**, **API Gateway (WebSocket)**, **DynamoDB**, **IAM**, and **S3**, the system ensures smooth real-time communication between users with minimal latency.

## 🎯 Objective
The main objective of this project is to develop a **fully serverless chat system** that allows real-time message exchange between users while maintaining scalability, performance, and security.

### Key Goals
- Enable real-time messaging through **WebSocket connections**.  
- Store and retrieve chat data efficiently using **DynamoDB**.  
- Use **AWS Lambda** for backend logic — no servers required.  
- Secure access through **IAM roles and permissions**.  
- Host the frontend interface using **Amazon S3** for easy deployment.

## 🏗️ System Architecture

### Components & Responsibilities

#### 🖥️ Frontend (Amazon S3)
- Hosts the user interface (HTML, CSS, JavaScript).  
- Opens and maintains a WebSocket connection to the WebSocket API endpoint.  
- Sends events (e.g., connect, sendMessage, disconnect).  
- Displays incoming messages and user presence.

#### 🌐 API Gateway — WebSocket API
- Acts as the WebSocket endpoint for all clients.  
- Routes messages to corresponding **Lambda functions** based on route keys (`$connect`, `$disconnect`, `sendMessage`).  
- Provides the **Management API** for backend-to-client communication.

#### ⚙️ AWS Lambda (Backend Handlers)
- **$connect**: Authenticates (optional) and registers the connection in DynamoDB.  
- **$disconnect**: Cleans up user connection and updates presence.  
- **sendMessage**: Validates and stores the message, then broadcasts it to all connected users.

#### 🧩 DynamoDB
- Stores all chat messages (partitioned by roomId or conversationId).  
- Maintains connection and presence data (`connectionId`, `userId`, `lastSeen`, `currentRoom`).  
- Uses optimized keys and indexes for efficient queries.

#### 🔒 IAM
- Provides fine-grained roles for Lambda with permissions to access DynamoDB and call the API Gateway Management API.  
- Follows the principle of **least privilege** for secure operations.

## 🪜 Steps Involved in the Project

### **Step 1: Setup DynamoDB**
- Created two DynamoDB tables:  
  - **Connections Table** – stores user connection details.  
  - **Messages Table** – stores chat history and metadata.

### **Step 2: Create IAM Role for Lambda**
Created a Lambda execution role with permissions to:
- Access DynamoDB tables.
- Invoke APIs and write logs.

**Attached Policies:**
- `AmazonDynamoDBFullAccess`  
- `AWSLambdaBasicExecutionRole`  
- `AmazonAPIGatewayInvokeFullAccess`

### **Step 3: Create Lambda Functions**
Implemented Lambda functions in **Python** to handle:
- **ConnectLambda**
- **DisconnectLambda**
- **MessageLambda**

Each function performs a specific event-driven task in the WebSocket lifecycle.

### **Step 4: Create WebSocket API**
Configured **AWS API Gateway (WebSocket)**:
- Created a WebSocket API named **ServerlessChatAPI**.  
- Added the following routes:
  - `$connect`
  - `$disconnect`
  - `sendMessage` (custom route)

Each route is linked to the respective Lambda function.

### **Step 5: Host Frontend on Amazon S3**
- Created an S3 bucket for static web hosting.  
- Enabled **Static Website Hosting**.  
- Uploaded frontend files (HTML, CSS, JS).  
- Connected the frontend to the WebSocket API endpoint.

## 📊 Architecture Diagram
![Chat_app](https://github.com/user-attachments/assets/031e87ae-6730-472c-8bd7-cbada2385980)

- Users connect via WebSocket → API Gateway routes messages → Lambda processes → DynamoDB stores data.  
- Responses are pushed back to connected clients via the API Gateway Management API.

## 🧠 Technologies Used
- **AWS Lambda** – backend compute layer.  
- **Amazon DynamoDB** – data storage.  
- **API Gateway (WebSocket)** – real-time connection management.  
- **IAM** – role-based access control.  
- **Amazon S3** – frontend hosting.  
- **Python / JavaScript** – Lambda and frontend code.

## ✅ Final Output
PingBox provides a working example of a **real-time chat application** where multiple users can send and receive messages instantly — with zero server maintenance.

## 🏁 Conclusion
This project demonstrates the power of **AWS Serverless Architecture** in building scalable, cost-efficient, and reliable real-time applications.  
By combining **Lambda**, **API Gateway**, **DynamoDB**, **IAM**, and **S3**, PingBox achieves instant, persistent communication — without traditional servers.  

The result is a **lightweight, flexible, and future-ready chat platform** perfect for learning, demos, or extending into production-scale applications.


## 👥 Authors
Developed by a group of friends who wanted a simple, fun, and cloud-based way to chat online —  
and turned that idea into **PingBox**, a real-time serverless chat app.

## 🏷️ Tags
`#AWS` `#Serverless` `#Lambda` `#WebSocket` `#DynamoDB` `#S3` `#CloudComputing` `#ChatApp` `#RealTime`
