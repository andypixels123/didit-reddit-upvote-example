## Upvote

Upvote is a Reddit-esque web application that allows users to create posts, upvote and downvote posts, and comment on posts in a multi-threaded, nested list.

The project is built using Next.js with the /app router and [Tailwind CSS](https://tailwindcss.com/), and uses [Auth.js (formerly Next Auth)](https://authjs.dev/) for user authentication. The data is stored in a Postgres database, which is created and accessed with raw SQL queries using the `pg` package.

The project is a work in progress and is not yet complete.

## Features

- [x] View a list of posts
- [x] View a single post
- [x] Create a post
- [x] Upvote and downvote posts
- [x] Pagination of posts
- [x] Comment on posts
- [x] Nested comments (recursive lists)
- [x] User authentication

## Setup instructions

1. Fork the repository (check "copy the main branch only") and clone your fork to your local machine
2. Run `npm install`
3. Create a `.env.local` file in the root directory and add the following environment variables:
   - `DATABASE_URL` - the URL of your Postgres database (eg. the Supabase connection string)
   - `AUTH_SECRET` - the Next Auth secret string (this can be anything at all like a password, but keep it secret!)
   -  UPDATE... You can type npx auth secret in your VsCode terminal to automatically create and add the secret to your .env.local file
   -  Read more: https://cli.authjs.dev
   - `AUTH_GITHUB_ID` - the GitHub OAuth client ID (create yours in [Github developer settings](https://github.com/settings/developers)
   - `AUTH_GITHUB_SECRET` - the GitHub OAuth client secret (create this in [Github developer settings](https://github.com/settings/developers))
4. Create the database schema by running the SQL commands in `schema.sql` in your database (eg. by running the commands in Supabase Query Editor)
5. Run `npm run dev` to start the development server
6. Open [http://localhost:3000](http://localhost:3000) with your browser to see the site

## Potential future features

- [ ] User profiles
- [ ] Sorting posts by recent (date posted), top (most upvotes), and most controversial (most upvotes _and_ downvotes)
- [ ] User karma scores
- [ ] User badges / trophies (awards for achievements like number of posts, years on the site, etc.)
- [ ] User settings (eg. number of posts per page, theme, etc.)
- [ ] Moderation tools / reporting or flagging objectionable comments for removable by admins
- [ ] Searching posts (possibly using simple SQL LIKE '%some search%', or [Postgres text search](https://www.crunchydata.com/blog/postgres-full-text-search-a-search-engine-in-a-database))
- [ ] Subreddits (separate communities, that isn't just one big list of posts, that can be created by users)
- [ ] User notifications
- [ ] User private messaging
- [ ] User blocking
- [ ] User following
- [ ] User feed (posts from users you follow)
- [ ] User flair


---------------- REFLECTION -----------------------------

I successfully deployed to Vercel.
I had issues with npm dependencies on the first try... I read a recommendation to use Yarn instead as it doesn't cause issues such as this. I tried re-installing node modules locally but this did not fix the errors.
My fix was to add npm i --legacy-peer-deps to the deployment settings - 'Install Command'.
It seems ESlint was causing the problems... but why do we need a linter on a deployed app?

Perhaps this is a workaround?:
Deploying to Vercel Without Any Checks By default,
Vercel runs type and lint checks before building your app. The deployment will fail if there are any type or lint errors. If your repo is connected to Vercel, you can set NEXT_PUBLIC_IGNORE_BUILD_ERROR to true in an environment variable.


I still got this error when the deployment was successful:

 ⨯ ESLint: Cannot read config file: /vercel/path0/node_modules/eslint-config-next/dist/core-web-vitals.js
   - Error: Cannot find module 'typescript
   - Require stack:
   - /vercel/path0/node_modules/@typescript-eslint/typescript-estree/dist/create-program/getWatchProgramsForProjects.js
   - /vercel/path0/node_modules/@typescript-eslint/typescript-estree/dist/clear-caches.js
   - /vercel/path0/node_modules/@typescript-eslint/typescript-estree/dist/index.js
   - /vercel/path0/node_modules/eslint-config-next/node_modules/typescript-eslint/node_modules/@typescript-eslint/parser/dist/parser.js
   - /vercel/path0/node_modules/eslint-config-next/node_modules/typescript-eslint/node_modules/@typescript-eslint/parser/dist/index.js
   - /vercel/path0/node_modules/eslint-config-next/node_modules/typescript-eslint/node_modules/@typescript-eslint/eslint-plugin/dist/raw-plugin.js
   - /vercel/path0/node_modules/eslint-config-next/node_modules/typescript-eslint/node_modules/@typescript-eslint/eslint-plugin/dist/index.js
   - /vercel/path0/node_modules/eslint-config-next/node_modules/typescript-eslint/dist/index.js
   - /vercel/path0/node_modules/eslint-config-next/dist/index.js
   - /vercel/path0/node_modules/eslint-config-next/dist/core-web-vitals.js
   - /vercel/path0/node_modules/@eslint/eslintrc/dist/eslintrc.cjs
   - /vercel/path0/node_modules/eslint/lib/cli-engine/cli-engine.js
   - /vercel/path0/node_modules/eslint/lib/eslint/eslint.js
   - /vercel/path0/node_modules/eslint/lib/eslint/index.js
   - /vercel/path0/node_modules/eslint/lib/api.js
   - /vercel/path0/node_modules/next/dist/lib/eslint/runLintCheck.js
   - /vercel/path0/node_modules/next/dist/compiled/jest-worker/processChild.js
   - Referenced from: /vercel/path0/.eslintrc.json

   I had no issues with following the README and I found that you can create a Next Auth secret string from the terminal by typing - npx auth secret . This will automatically add the string to the .env.local file.

  I have the app running and I'm able to login using my Github account. I have changed the 'homepage url' and 'authorization callback url' in Github -> settings -> developer settings -> OAuth Apps
