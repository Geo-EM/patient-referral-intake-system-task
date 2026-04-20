
---

# Patient Referral Intake System

Full-stack TypeScript implementation of a Patient Referral Intake form for a pain management & neurology clinic.
Built with **Next.js, tRPC, Drizzle ORM, PostgreSQL (Neon), Zod, and React Hook Form**.

This project demonstrates an end-to-end type-safe architecture from UI → API → database.

---

## Tech Stack

* **Next.js (App Router)** – frontend + API routes
* **React + TypeScript** – UI layer
* **tRPC** – fully type-safe API layer
* **Drizzle ORM** – database layer
* **PostgreSQL (Neon)** – database
* **Zod** – shared validation schema (client + server)
* **React Hook Form** – form state management
* **Tailwind CSS** – UI styling
* **Vercel** – deployment
* **Neon** – serverless PostgreSQL

---

## Features

### Patient Referral Form

* Patient information (name, DOB, contact info)
* Referring attorney/law firm details
* Complaint description (max 500 chars)
* Preferred clinic location (California-based dropdown)
* Appointment type (In-Person / Telemedicine)
* Real-time validation using Zod

### Backend

* `submitReferral` tRPC mutation
* `getReferrals` query (admin view)
* Shared validation schema between frontend and backend
* Drizzle ORM schema with:

  * UUID primary key
  * timestamps
  * status tracking

### UX

* Mobile-first responsive UI
* Inline validation errors
* Success & error states
* Clean clinic-grade form design

---

## Project Structure

```
src/
├── app/                # Next.js App Router
│   ├── admin/          # Admin referrals list page
│   ├── api/trpc/       # tRPC endpoint handler
│   └── page.tsx        # main referral form page
│
├── components/         # UI components (Referral form)
├── lib/                # tRPC client setup
├── schemas/            # Zod shared validation schemas
├── server/
│   ├── api/            # tRPC routers
│   └── db/             # Drizzle DB + schema
```

---

## Architecture Decisions

### 1. End-to-end type safety

Zod schema is shared between frontend and backend to ensure:

* No duplicated validation logic
* Compile-time safety across API boundaries

### 2. tRPC instead of REST

Chosen for:

* Full type inference between client and server
* No manual DTO management
* Better developer experience

### 3. Drizzle ORM

* Lightweight and type-safe
* Explicit schema definition
* Better control over SQL structure compared to Prisma

### 4. Server-side validation

Even though frontend validates input, backend validation is enforced to ensure:

* Security
* Data integrity
* API safety

---

## Database Schema

Table: `referrals`

* id (UUID, primary key)
* patient_first_name
* patient_last_name
* dob
* phone
* email (optional)
* law_firm
* attorney_name
* attorney_email
* attorney_phone
* complaint (max 500 chars)
* location
* appointment_type
* status (default: "new")
* created_at (timestamp)

---

## Environment Variables

Create a `.env` file:

```env
DATABASE_URL=postgresql://<user>:<password>@<host>/<db>?sslmode=require
```

---

## Setup & Run Locally

### 1. Install dependencies

```bash
yarn install
```

### 2. Setup database

```bash
npx drizzle-kit push
```

### 3. Run development server

```bash
yarn dev
```

### 4. Open app

```
http://localhost:3000
```

---

## Deployment

### Frontend + API

* Hosted on **Vercel**

### Database

* Hosted on **Neon PostgreSQL (serverless)**

---

## API Endpoints

### Mutation: Submit Referral

```ts
referral.submitReferral
```

Returns:

```json
{
  "id": "uuid",
  "message": "Referral submitted successfully",
  "followUp": "Our team will contact the patient within 24 hours"
}
```

### Query: Get Referrals

```ts
referral.getReferrals
```

Returns list of submitted referrals (admin view).

---

## Tradeoffs / Notes

* Used Neon serverless PostgreSQL for simplicity and cloud-native setup
* No authentication layer (out of scope per spec)
* Focused on type safety and architecture over UI complexity
* Kept schema strictly aligned with business requirements
* Error handling is centralized in tRPC layer

---

## UI Philosophy

The UI is designed to mimic a **real medical intake system**:

* Clean and minimal
* Mobile-first layout
* Fast form completion flow
* No unnecessary UI complexity

---

## Optional Enhancements (Not Implemented)

* Authentication system
* Role-based admin dashboard
* Advanced Search/filter referrals
* Email notifications
* File uploads (medical documents)
* Audit logging

---

## Summary

This project demonstrates:

* Production-grade TypeScript architecture
* Type-safe full-stack communication (tRPC + Zod)
* Clean separation of concerns
* Real-world healthcare workflow modeling
* Scalable backend design using modern tools

---
