# Ontario Ranked Slippi Leaderboard

Code powering <https://rdrnt.github.io/canada-slippi-ranked-leaderboards/#/>

![image](https://github.com/rdrnt/canada-slippi-ranked-leaderboards/blob/master/demo.png)

[Submit your profile to the leaderboards](https://docs.google.com/forms/d/1hrqZNXV248bKtxPKVKQv1dlevI0_IPREkNypKmarVA8)

## Technologies

- Typescript
- [Webpack@5](https://webpack.js.org/) as module bundler
- [Eslint](http://eslint.org/) for linting
- [Tailwind](https://tailwindcss.com/) for css

Fork of [
CoSlippiLeaderboard](https://github.com/Grantismo/CoSlippiLeaderboard). This fork inludes:

- Visual styling changes
- Support for players province/city
- Prettier support
- Improved instructions for getting started with your own leaderboards

## How it works

The leaderboard is built from two programs:

- [[src/](https://github.com/rdrnt/canada-slippi-ranked-leaderboards/tree/master/src)] A static react website which displays player data.
- [[cron/](https://github.com/rdrnt/canada-slippi-ranked-leaderboards/tree/master/cron)] A cron job which pulls connect codes from a google sheet, player data from slippi, and writes that data to json files in `cron/data/`, and then redeploys the static site.

## Caveats

- The undocumented slippi api this depends on may break at any time
- This project takes extra consideration to avoid slamming the slippi servers with api calls, please be considerate of this. I recommend not using a cron job, but manually updating it every morning and night.
- Logic for determining ranks may become out of sync with the official slippi rank logic

## Getting started

- Clone this repo
- (Optional) Run `nvm use 18.12.0`. This will ensure that you are running the supported version of Node.js. You can nvm installation instructions [here](https://github.com/creationix/nvm).
- Install dependencies: `yarn`
- Run the project: `npm start`
- Set your repoPath in settings.js and "homepage" in package.json to your github pages url (e.g. <https://rdrnt.github.io/canada-slippi-ranked-leaderboards/#/>)
- Create a google form to collect player tags from your region. ![image](https://user-images.githubusercontent.com/911232/207989907-256100e3-c215-4699-9ae7-655d5345cbd4.png)
- Link your google form to a google sheet ![image](https://user-images.githubusercontent.com/911232/207990065-aadc0a30-2561-46b7-a46e-0742af601cec.png)
- Follow directions in <https://theoephraim.github.io/node-google-spreadsheet/#/getting-started/authentication?id=service-account> to create a service account and credentials to read from the google sheet. Save your creds json file to `secrets/creds.json`
- Change `spreadsheetID` in settings.js to your google sheet ID
- Edit your crontab to run the cron job every 30 minutes. On linux `crontab -e`

Example crontab:

```
# m h  dom mon dow   command
*/30 * * * * /bin/bash /home/grantismo/code/CoSlippiLeaderboard/cron/run.sh
```

## Settings

[settings.js](./settings.js) file includes all important settings that should be used to setup deployments to gh-pages:

- **title** – Base application title
- **cname** – Adds CNAME file that allows to use custom domain names with gh-pages
- **repoPath** – username.github.io/repoPath for react router to recognize gh-pages paths
- **spreadsheetID** - ID for google sheet containing player connect codes. `https://docs.google.com/spreadsheets/d/[YOUR ID]`

## scripts

- `npm start` – starts development server with webpack-dev-server
- `npm run build` – builds project to production
- `npm run deploy` – builds and deploys project to Github pages
- `./cron/run.sh` - manually runs the cron job

## Support me

☕ [Support the creator this work was based off of](https://www.buymeacoffee.com/blorppppp)
