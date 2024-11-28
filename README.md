# StreamLedger

**StreamLedger** is a decentralized invoicing platform that integrates with Request Network to create and display transparent, immutable invoices for Sablier streams. This app allows users to generate invoices for their Sablier streams, track payments, and view them in a secure, easily accessible format, all while ensuring compliance with blockchain’s transparency and immutability principles.

## Overview

In the decentralized finance (DeFi) world, managing invoices for ongoing payment streams can be cumbersome and prone to disputes. **StreamLedger** simplifies this by allowing users to create a decentralized paper trail for Sablier streams. Using Request Network's underlying infrastructure, invoices are stored securely on IPFS, ensuring that they are tamper-proof and always accessible. 

The app provides an interface for users to create, track, and display invoices tied to their Sablier streams, making it the ideal solution for anyone using decentralized streams for payments.

## Key Features

- **Create Invoices:** Automatically generate invoices for active Sablier streams.
- **Immutable Records:** Invoices are stored on IPFS, ensuring transparency and tamper-proof records.
- **Data Consumption:** Display real-time data from the Request Network, showing invoice details in a user-friendly interface.
- **Multiple Chains Supported:** Supports networks like Sepolia Testnet for easy access and testing.

## How It Works

1. **Create Request:** Users can create a request to generate an invoice for their ongoing Sablier stream. The request is stored on Request Network and linked to the user's stream data.
2. **Immutable Storage:** Invoice data is stored on IPFS, ensuring that no one can alter or manipulate the information.
3. **Display Invoices:** Users can view and track their invoices through an intuitive interface. The app fetches and displays data from the Request Network, ensuring seamless integration with other decentralized financial systems.

## Tech Stack

- **Frontend:** JavaScript, React
- **Blockchain Integration:** Request Network, IPFS
- **Smart Contracts:** Interaction with Sablier Streams
- **Deployment:** Vercel (for web app hosting)

## Code Overview

The app integrates with the Request Network for invoice creation and management, utilizing two main modules: `RequestHandler.js` and `WithdrawalHandler.js`.

### **RequestHandler.js**
This file is responsible for interacting with the Request Network to create and manage requests for invoices. It utilizes the `Web3SignatureProvider` to sign requests and the `RequestNetwork` client to handle transaction creation and management.

```javascript
import { Web3SignatureProvider } from '@requestnetwork/web3-signature';
import { RequestNetwork, Types, Utils } from '@requestnetwork/request-client.js';

// Initialize Request Network and Signature Provider
const provider = new Web3SignatureProvider('your-wallet-provider');
const requestNetwork = new RequestNetwork(provider);

// Function to create a request for an invoice
async function createInvoice(amount, payeeAddress) {
  const requestData = {
    amount: amount, 
    payee: payeeAddress,
    // other required data for the request
  };

  // Creating the request
  const request = await requestNetwork.createRequest(requestData);
  
  return request;
}
```

### **WithdrawalHandler.js**
This file manages the withdrawal process by interacting with the Request Network to fetch invoice details, validate payments, and allow for withdrawals once the conditions are met.

```javascript
import { RequestNetwork, Types } from '@requestnetwork/request-client.js';

// Initialize Request Network
const requestNetwork = new RequestNetwork(provider);

// Function to handle withdrawals after the invoice has been settled
async function handleWithdrawal(requestId) {
  // Fetch the request based on the request ID
  const request = await requestNetwork.getRequestById(requestId);
  
  // Ensure that the invoice has been paid and then allow withdrawal
  if (request.status === 'paid') {
    // Proceed with the withdrawal logic
    const withdrawalData = await processWithdrawal(request);
    return withdrawalData;
  }

  throw new Error('Invoice not paid yet');
}
```

These files utilize the core functionality of `Request Network` to create and manage decentralized invoices, as well as to facilitate the withdrawal process when conditions are met.

## Installation

To run this project locally, clone the repository and follow these steps:

1. Clone the repo:
   ```bash
   git clone https://github.com/yourusername/StreamLedger.git
   cd StreamLedger
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   - Copy `.env.example` to `.env` and configure your settings.

4. Run the application:
   ```bash
   npm run dev
   ```

5. Visit `http://localhost:3000` to view the app.

## Future Enhancements

- **Grant Program Integration:** Apply for and support the Request Network Foundation’s grants program to expand the app’s features.
- **Additional Blockchain Support:** Integrate with other chains to increase compatibility and scalability.
- **Mobile Application:** Develop a mobile version for easier access on the go.

