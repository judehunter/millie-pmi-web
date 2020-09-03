# MILLIE PMI Project (WEB)
#### Prerequisites
- `node v12.18.3+`
- `yarn` (optional)

#### Setup
Clone the repo:

```bash
git clone https://github.com/judehunter/millie-pmi-web .
```

Download dependencies:

```bash
yarn
```

Create a `.env` file in project root and paste:

```dotenv
API_URL=http://localhost:4000/
```

Run the app in development mode. This will start the web app on port `3333`:

```bash
yarn dev
```

#### The available routes are:
##### /
The sign up form.

##### /admin
The admin page.
