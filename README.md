# FakeProductDetectionUsingBlockchainFrontend

### Architecture Overview

1. **Client (Front-end)**
   - **Role:** Interface for users (consumers, manufacturers, distributors) to interact with the system.
   - **Technologies:** Web or mobile application, which includes user interfaces (UI) for scanning product identifiers, viewing product history, and submitting data.

2. **Backend Server**
   - **Role:** Acts as an intermediary between the client and the blockchain. Handles business logic, authentication, and data processing.
   - **Technologies:** A web server built using a framework like Django (Python) for handling API requests, user management, and interfacing with the blockchain.

3. **Blockchain Network**
   - **Role:** Provides a decentralized ledger for recording and verifying product transactions. Ensures data immutability and transparency.
   - **Technologies:** Blockchain platforms like Ethereum, Hyperledger, or a custom blockchain solution.

### Interaction Workflow

1. **Product Registration**
   - **Manufacturer registers a product:**
     - The client (mobile or web app) sends a product registration request to the backend server. This request includes product details like serial number, manufacturing date, and other relevant metadata.
     - The backend server processes this request, ensures the data is valid, and creates a transaction to add this product to the blockchain.
     - The transaction is sent to the blockchain network where it is verified and added to a new block.
     - A unique identifier (e.g., a QR code or NFC tag) is generated and linked to the blockchain record. This identifier is then sent back to the client and physically attached to the product.

2. **Product Verification**
   - **Consumer verifies a product:**
     - The consumer uses the client app to scan the product’s unique identifier (QR code/NFC tag).
     - The client app sends a request to the backend server to fetch the product's blockchain record.
     - The backend server retrieves the product’s transaction history from the blockchain.
     - The product’s history, including its origin, ownership changes, and any other relevant data, is sent back to the client app.
     - The client app displays this information to the consumer, enabling them to verify the product’s authenticity.

3. **Supply Chain Updates**
   - **Product changes hands (e.g., from manufacturer to distributor):**
     - The current owner scans the product and initiates a transfer request via the client app.
     - The client app sends the transfer request to the backend server, including details of the new owner.
     - The backend server processes this request, creates a new transaction reflecting the change of ownership, and sends it to the blockchain.
     - The blockchain network validates and records the transaction, updating the product’s ownership status.
     - Confirmation of the transfer is sent back to the client app.

### Detailed Interaction Flow

1. **Client to Backend Server Communication:**
   - **Protocol:** HTTPS for secure communication.
   - **Data Format:** JSON for structured data exchange.
   - **Authentication:** JWT (JSON Web Tokens) for user authentication and session management.
   - **Endpoints:** RESTful API endpoints for various operations (e.g., `/registerProduct`, `/verifyProduct`, `/transferOwnership`).

2. **Backend Server to Blockchain Interaction:**
   - **Blockchain Client:** Backend server uses a blockchain client (e.g., Web3.js for Ethereum, Hyperledger SDK) to interact with the blockchain network.
   - **Transaction Handling:**
     - The backend server constructs a transaction with the necessary data.
     - The transaction is signed using the server’s private key to ensure authenticity.
     - The signed transaction is sent to the blockchain network where it is broadcast to other nodes for validation.
     - Upon successful validation, the transaction is added to the blockchain, and a transaction hash is returned.
   - **Smart Contracts:** If using smart contracts, the backend server interacts with these contracts to execute predefined business logic.

3. **Blockchain to Backend Server Data Retrieval:**
   - **Querying Blockchain:** The backend server queries the blockchain for product data using the unique identifier.
   - **Data Parsing:** The raw blockchain data is parsed and formatted into a user-friendly structure before sending it to the client.
   - **Caching:** To improve performance, frequently accessed data may be cached temporarily in the backend server.

### Example Workflow

**1. Product Registration:**
   - **Step 1:** Client app sends product details to the backend server.
   - **Step 2:** Backend server validates the data, creates a blockchain transaction, and sends it to the blockchain.
   - **Step 3:** Blockchain validates and records the transaction. Backend server receives the transaction hash.
   - **Step 4:** Backend server generates a QR code, links it to the blockchain transaction, and sends it to the client app.

**2. Product Verification:**
   - **Step 1:** Consumer scans the product QR code using the client app.
   - **Step 2:** Client app sends a verification request to the backend server.
   - **Step 3:** Backend server queries the blockchain for the product’s history.
   - **Step 4:** Backend server retrieves and formats the data, sending it back to the client app.
   - **Step 5:** Client app displays the product history and authenticity status to the consumer.
