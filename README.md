# Cloudinary SaaS (Next.js + Prisma)

A Next.js application that integrates Cloudinary for image and video uploads, with Prisma for database management. This project provides API routes for uploading media, a small UI for video and image uploads, simple auth pages, and social sharing pages.

## Features

- **Media Uploads:** Upload images and videos to Cloudinary via server-side API routes.
- **Video Library:** Browse uploaded videos with a simple `VideoCard` component.
- **Auth Pages:** Sign-in and sign-up flows (located under the `(auth)` app routes).
- **Social Sharing:** A social-share page template for sharing uploaded media.
- **Prisma ORM:** Uses Prisma for schema management and database access.
- **API Routes:** Lightweight serverless routes for handling uploads and listing videos.

## Tech Stack

- **Framework:** Next.js (App Router)
- **Database:** Prisma (generated client in `generated/prisma`)
- **Storage / CDN:** Cloudinary
- **Language:** TypeScript

## Repository structure (high level)

- app/: Next.js app pages and components
- api/: Serverless API routes (upload endpoints and video listing)
- components/: UI components (e.g. VideoCard)
- prisma/: Prisma schema and migrations
- generated/: Prisma client and generated types

## Quick start

Prerequisites:

- Node 18+ (or the version required by your environment)
- Yarn, npm, or pnpm
- A PostgreSQL (or other supported) database and a Cloudinary account

1. Install dependencies

```bash
npm install
# or yarn
# yarn
```

2. Create environment variables

Copy your environment file (example names shown) and set the values in `.env.local`:

- `DATABASE_URL` — your database connection string
- `CLOUDINARY_CLOUD_NAME` — your Cloudinary cloud name
- `CLOUDINARY_API_KEY` — your Cloudinary API key
- `CLOUDINARY_API_SECRET` — your Cloudinary API secret
- `NEXTAUTH_SECRET` — (if you use next-auth) secret for auth sessions
- `NEXTAUTH_URL` — base URL for your app (e.g., `http://localhost:3000`)

Place these variables in `.env.local` at the project root.

3. Prisma setup (generate client & run migrations)

```bash
npx prisma generate
npx prisma migrate deploy
# during development you may use:
npx prisma migrate dev
```

4. Run the app

```bash
npm run dev
```

Open `http://localhost:3000` to view the app.

## API routes overview

- Image upload: [api/image-upload/route.ts](api/image-upload/route.ts)
- Video upload: [api/video-upload/route.ts](api/video-upload/route.ts)
- Videos listing: [api/videos/route.ts](api/videos/route.ts)

Inspect these files for request payload expectations and response shapes.

## How uploads work

1. Client sends media to the API route (multipart/form-data or presigned upload payload).
2. Server-side route uploads the media to Cloudinary using official Cloudinary SDK or REST API.
3. Server persists metadata (URL, public_id, owner, etc.) to the database via Prisma.
4. Frontend lists media entries by calling the videos listing API.

## Deployment

This app is designed for deployment on Vercel, but any platform supporting Node.js and environment variables will work.

Typical steps to deploy to Vercel:

1. Connect the GitHub repository to Vercel.
2. Set the same environment variables in the Vercel project settings.
3. Deploy — Vercel will run the build and serve the Next.js app.

## Uploading this project to GitHub

Initialize a new repo and push your code (run from project root):

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

Replace `<your-github-repo-url>` with the URL for your GitHub repository (e.g., `https://github.com/username/repo.git`).

## Contributing

Contributions are welcome. Open an issue or submit a PR describing the change.

## Useful files

- [app/page.tsx](app/page.tsx) — main app entry
- [components/VideoCard.tsx](components/VideoCard.tsx) — video display component
- [prisma/schema.prisma](prisma/schema.prisma) — Prisma schema and models

## Troubleshooting

- If uploads fail, verify Cloudinary credentials and check server logs.
- If database issues arise, run `npx prisma migrate dev` to apply migrations locally.

## License

Specify a license for your project (e.g., MIT). Add a `LICENSE` file if desired.

---

If you want, I can also: add a `LICENSE` file, create a short `CONTRIBUTING.md`, or commit and push this README to a GitHub repo for you. What would you like next?
This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
