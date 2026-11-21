# Springboard Capstone Ideas

These are three possible capstone project directions, each designed around a real-world problem and a practical API-driven solution.

1. U.S. National Park Explorer
   Planning a national park visit can require searching several pages to gather the information needed to make a decision. This app would help users discover parks by location and interests, explore available activities, and save places they want to visit. It would use the free [National Park Service API](https://www.nps.gov/subjects/developer/api-documentation.htm) to pull park descriptions, locations, activities, photos, and alerts.

2. City Travel Guide
   Travelers with limited time often struggle to decide which attractions are worth prioritizing. This app would let users enter a city and the length of their stay to receive suggested places to visit, organized into a manageable daily plan. It would use [Geoapify’s free API tier](https://www.geoapify.com/places-api/) for attractions and locations, while [openrouteservice](https://openrouteservice.org/) would provide travel-time data to help group nearby stops efficiently.

3. Word Explorer — My Preferred Project
   Looking up a word often requires visiting several websites to understand its meaning, pronunciation, and connections to other words. This app would bring that information together in one place, helping students, writers, and language learners explore and save vocabulary. It would use [WordsAPI’s free tier](https://www.wordsapi.com/), along with the [Free Dictionary API](https://dictionaryapi.dev/) and [Datamuse](https://www.datamuse.com/api/), to provide definitions, synonyms, rhymes, pronunciation, syllable counts, usage frequency, and word relationships. This is the idea I would most like to work on because it combines language exploration with a practical learning tool.


# Word Explorer

A full-stack web application for exploring English words and building a personal vocabulary collection.

> **Project status:** Capstone Step 2 — project proposal. The features below describe the planned application.

## Project overview

Word Explorer will bring English vocabulary information into one place so users can understand a word, discover related words, and save vocabulary for later. I chose this project because it combines language exploration with a practical learning tool.

## Technology stack, focus, and platform

| Layer | Technologies |
| --- | --- |
| Frontend | React, JavaScript, HTML, CSS |
| Backend | Node.js, Express, JavaScript |
| Database | MongoDB, Mongoose |

Word Explorer will be an evenly focused full-stack application. React will provide an accessible, responsive interface, while the backend will handle external API integration, authentication, and saved vocabulary. It will be a website usable on desktop and mobile browsers.

## Goal and intended users

The goal is to reduce the need to visit multiple websites when exploring a word and help users build a personal vocabulary collection. The primary users will be students, English-language learners, writers, and anyone interested in language. The first version will focus on English vocabulary.

## Data and collection

I will retrieve word information through API requests rather than web scraping. Free Dictionary API will provide definitions, parts of speech, example sentences, and phonetic text or audio when available. Datamuse will support related-word discovery, rhymes, and available syllable and frequency metadata. WordsAPI will supplement definitions and word relationships, subject to its available free plan. Users will supply their account details, saved words, and personal notes. External data will retain source attribution.

## Core functionality

Visitors will be able to search for a word without an account, read its definitions, play available pronunciation audio, and explore synonyms, rhymes, and related words. Syllable counts and usage frequency will appear when available. Registered users will be able to save words, view and search their vocabulary collection, edit personal notes, and remove saved words. Selecting a related word will open a new word detail view.

## User flow

1. Open the homepage and search for a word.
2. View definitions and available pronunciation, synonyms, rhymes, and other word information.
3. Select a related word to continue exploring.
4. Sign up or log in to save a word, then return to that word.
5. Visit **My Vocabulary** to search saved words, edit notes, remove entries, or reopen word details.

Loading, no-result, and partial-result states will explain what is happening.

## Proposed database schema

MongoDB will contain two main collections:

| Collection | Fields |
| --- | --- |
| `Users` | `_id`, `email` (unique), `passwordHash`, `createdAt` |
| `SavedWords` | `_id`, `userId` (reference to `Users`), `word`, `normalizedWord`, `notes`, `createdAt` |

A unique compound index on `userId` and `normalizedWord` will prevent duplicate saves. Word details will be fetched from providers when needed; saved entries will primarily store the word and user-written notes rather than copies of provider datasets.

## API integration and potential issues

The Express backend will request provider data and transform it into a consistent response for React. Challenges include missing definitions or audio, different response formats, conflicting word senses, request limits, and provider outages. I will validate input, apply request timeouts and rate limits, deduplicate related words, and return available sections even if one provider fails. Frequency will be labeled with its source and scale; provider ranking scores will not be treated as frequency. Before integration, I will verify WordsAPI access and plan limits. Datamuse announces an API-key requirement beginning February 1, 2027, so its credentials will be configurable on the server.

## Sensitive information and security

Email addresses, password hashes, and private vocabulary notes require protection. Passwords will be hashed with a suitable password-hashing library, and sessions will use secure, HTTP-only cookies. The backend will authorize each saved-word request against the logged-in user. API keys and database credentials will remain in server-side environment variables and will not be committed to GitHub. I will validate requests and use HTTPS in deployment.

## What makes this more than a CRUD app

The central feature is a word-exploration experience that combines multiple external data sources into one view. Users can move between words through meaning and sound relationships and hear pronunciation. This requires API orchestration, response normalization, and useful behavior when data is incomplete, in addition to creating, reading, updating, and deleting saved vocabulary.

## Implementation approach and validation

I will first confirm API access and design the schema and user flows. Next, I will build the Express API and database models, implement the React search and detail pages, and add authentication and saved vocabulary. I will test successful searches, unknown words, missing audio, provider failures, duplicate saves, and attempts to access another user's records. Finally, I will check mobile layouts and keyboard navigation, deploy the app, and document setup and API attribution in the repository.

## Stretch goals

After the core experience works, I would like to add flashcards and quizzes from saved vocabulary, custom word lists, and a visual map of word relationships. These features are optional and will not block completion of the initial version.

## Development checklist

These tasks can be created as GitHub issues. Suggested labels:

- **Difficulty:** `Easy`, `Medium`, `Hard`
- **Type:** `Frontend`, `Backend`, `Fullstack`
- **Scope:** `Must Have`, `Stretch Goal`

- [ ] **Confirm data sources** — `Medium` · `Backend` · `Must Have`
  Test sample queries with all three APIs; confirm credentials, quotas, attribution, and permitted caching. Record missing-data behavior.

- [ ] **Design database schema** — `Medium` · `Backend` · `Must Have`
  Define Users and SavedWords models, validation, references, and unique indexes.

- [ ] **Design user flows and wireframes** — `Easy` · `Frontend` · `Must Have`
  Sketch search, word details, signup/login, and My Vocabulary screens, including loading and error states.

- [ ] **Set up backend and MongoDB** — `Medium` · `Backend` · `Must Have`
  Create the Express server, environment configuration, database connection, and error handling. Keep secrets out of version control.

- [ ] **Set up React frontend** — `Easy` · `Frontend` · `Must Have`
  Create routes and shared layout; verify communication with the backend.

- [ ] **Implement word API integration** — `Hard` · `Backend` · `Must Have`
  Normalize provider responses, retain source information, deduplicate related words, and handle timeouts, rate limits, and partial failures.

- [ ] **Build search and word detail interface** — `Medium` · `Frontend` · `Must Have`
  Display definitions, available audio, synonyms, rhymes, related words, syllable counts, and labeled frequency data. Make related words clickable.

- [ ] **Implement authentication backend** — `Hard` · `Backend` · `Must Have`
  Add signup, login, logout, password hashing, session handling, and authentication middleware.

- [ ] **Build authentication screens** — `Medium` · `Frontend` · `Must Have`
  Create validated signup/login forms and preserve the word the visitor wanted to save.

- [ ] **Implement saved vocabulary endpoints** — `Medium` · `Backend` · `Must Have`
  Add save, list, update-note, and delete operations with ownership checks and duplicate prevention.

- [ ] **Build My Vocabulary page** — `Medium` · `Frontend` · `Must Have`
  Support saving words, searching saved entries, editing notes, removing entries, and reopening word details.

- [ ] **Test backend behavior** — `Hard` · `Backend` · `Must Have`
  Test API failures, malformed input, duplicate saves, authentication, and denial of access to another user's saved entries.

- [ ] **Validate usability** — `Medium` · `Frontend` · `Must Have`
  Check search-to-save flow, unknown words, missing audio, keyboard navigation, and responsive layouts.

- [ ] **Deploy and document** — `Medium` · `Fullstack` · `Must Have`
  Deploy frontend and backend, configure production secrets, verify the deployed flow, and document setup, features, and API attribution.

- [ ] **Add flashcards and quizzes** — `Hard` · `Fullstack` · `Stretch Goal`
  Create practice sessions using saved vocabulary and available definitions.

- [ ] **Add custom vocabulary lists** — `Medium` · `Fullstack` · `Stretch Goal`
  Allow users to organize words into named lists; extend the schema and authorization checks.

- [ ] **Add a visual word relationship map** — `Hard` · `Frontend` · `Stretch Goal`
  Show clickable connections between words using the existing related-word data.

## API references

- [Free Dictionary API](https://dictionaryapi.dev/)
- [Datamuse API](https://www.datamuse.com/api/)
- [WordsAPI](https://www.wordsapi.com/)
