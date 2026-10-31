# VendorBridge – RFQ & Quotation Management

A full-stack web application for creating Requests for Quotation (RFQs), inviting/allowing vendors to submit quotations, and comparing quotation responses.

## Tech stack
- Frontend: React + Vite
- Backend: Node.js + Express
- Database: MongoDB + Mongoose
- Authentication: JWT + bcrypt

## Features
- Register and login as a buyer or vendor
- JWT-protected API routes
- Buyers can create, view, update and delete RFQs
- Vendors can browse open RFQs and submit quotations
- Buyers can view quotations for an RFQ and award one
- Basic dashboard summaries
- Input validation and centralized error handling

## Requirements
- Node.js 18+
- MongoDB Community Server or MongoDB Atlas

## Run locally

### 1. Start MongoDB
Run MongoDB locally, or create a MongoDB Atlas database.

### 2. Backend
```bash
cd backend
cp .env.example .env
# Set MONGODB_URI and JWT_SECRET in .env
npm install
npm run dev
```
Backend runs at `http://localhost:5000`.

### 3. Frontend
Open a second terminal:
```bash
cd frontend
npm install
npm run dev
```
Open the URL printed by Vite (normally `http://localhost:5173`).

## Demo workflow
1. Register one account with role `buyer`.
2. Register another account with role `vendor`.
3. Log in as the buyer and create an RFQ.
4. Log in as the vendor and submit a quotation against the open RFQ.
5. Log back in as the buyer, open the RFQ and award a quotation.

## API overview
| Method | Endpoint | Access | Purpose |
|---|---|---|---|
| POST | `/api/auth/register` | Public | Create account |
| POST | `/api/auth/login` | Public | Login |
| GET | `/api/auth/me` | Authenticated | Current user |
| GET | `/api/rfqs` | Authenticated | List RFQs |
| POST | `/api/rfqs` | Buyer | Create RFQ |
| GET | `/api/rfqs/:id` | Authenticated | RFQ details |
| PUT | `/api/rfqs/:id` | Owner buyer | Update RFQ |
| DELETE | `/api/rfqs/:id` | Owner buyer | Delete RFQ |
| POST | `/api/rfqs/:id/quotations` | Vendor | Submit quotation |
| GET | `/api/rfqs/:id/quotations` | Owner buyer | View quotations |
| PATCH | `/api/rfqs/:id/award/:quotationId` | Owner buyer | Award quotation |

## Notes
- This is a portfolio/demo application. Before production use, add email verification, password reset, rate limiting, audit logs, file-upload scanning, stronger validation, automated tests and deployment secrets management.
- Never commit your real `.env` file or production credentials.
