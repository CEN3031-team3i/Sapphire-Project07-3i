# CaSMM

> Computation and Science Modeling through Making

Cloud-based programming interface

![Deploy Staging](https://github.com/STEM-C/CaSMM/workflows/Deploy%20Staging/badge.svg)
![Deploy Production](https://github.com/STEM-C/CaSMM/workflows/Deploy%20Production/badge.svg)

<br/>

## Application

### `client` 
[client](/client#client) is the frontend of the application. It is powered by [React](https://reactjs.org/) and [Blockly](https://developers.google.com/blockly).

### `server`

[server](/server#server) is the web server and application server. It is powered by [Node](https://nodejs.org/en/) and [Strapi](https://docs-v3.strapi.io/developer-docs/latest/getting-started/introduction.html).

### `compile`

  [compile](/compile#compile) is an arduino compiler service. It is an unofficial fork of [Chromeduino](https://github.com/spaceneedle/Chromeduino).

<br/>

## Environments

> The project is divided into three conceptual environments.

### Development
#### Structure

The development environment is composed of five servers. The first one is run with the [Create React App](https://create-react-app.dev/docs/getting-started/) dev server. The later four are containerized with docker and run with [docker compose](https://docs.docker.com/compose/).

* `casmm-client-dev` - localhost:3000

* `casmm-server-dev` - localhost:1337/admin

* `casmm-compile-dev` 

* `casmm-db-dev` - localhost:5432

  > The first time the db is started, the [init_db.sh](/scripts/init_db.sh) script will run and seed the database with an environment specific dump. Read about Postgres initialization scripts [here](https://github.com/docker-library/docs/blob/master/postgres/README.md#initialization-scripts). To see how to create this dump, look [here](https://github.com/DavidMagda/CaSMM_fork_2023/blob/develop/scripts/readme.md).

* `casmm-compile_queue-dev`

#### Running

`casmm-client-dev`

1. Follow the [client](/client#setup) setup
2. Run `yarn start` from `/client`

`casmm-server-dev`, `casmm-compile-dev`, `casmm-db-dev`, and `casmm-compile_queue-dev`

1. Install [docker](https://docs.docker.com/get-docker/)

2. Run `docker compose up` from `/`

   > Grant permission to the **scripts** and **server** directories if you are prompted
   

### Staging

#### Structure

The staging environment is a Heroku app. It is composed of a web dyno, compile dyno, Heroku Postgres add-on, and Heroku Redis add-on.

* `casmm-staging` - [casmm-staging.herokuapp.com](https://casmm-staging.herokuapp.com/)
  * The web dyno runs `server`
  * The compile dyno runs `compile`

#### Running

`casmm-staging` is automatically built from the latest commits to branches matching `release/v[0-9].[0-9]`. Heroku runs the container orchestration from there.

### Production

#### Structure

The production environment is a Heroku app. It is composed of a web dyno, compile dyno, Heroku Postgres add-on, and Heroku Redis add-on.

* `casmm` - [www.casmm.org](https://www.casmm.org/)
  * The web dyno runs `server`
  * The compile dyno runs `compile`

#### Running

`casmm` is automatically built from the latest commits to `master`. Heroku runs the container orchestration from there.

<br/>

## Maintenance

All three components of the application have their own dependencies managed in their respective `package.json` files. Run `npm outdated` in each folder to see what packages have new releases. Before updating a package (especially new major versions), ensure that there are no breaking changes. Avoid updating all of the packages at once by running `npm update` because it could lead to breaking changes. 

### Strapi

This is by far the largest and most important dependency we have. Staying up to date with its [releases](https://github.com/strapi/strapi/releases) is important for bug/security fixes and new features. When it comes to actually upgrading Strapi make sure to follow the [migration guides](https://docs-v3.strapi.io/developer-docs/latest/update-migration-guides/migration-guides.html#v3-guides)!

<br/>

## CI/CD

All of the deployments and releases are handled automatically with [GitHub Actions](https://docs.github.com/en/actions). The workflows implement custom [Actions](https://github.com/STEM-C/CaSMM/actions) that live in the [auto](https://github.com/STEM-C/auto) repo.

<br/>

## Contributing

### Git Flow 

> We will follow this git flow for the most part — instead of individual release branches, we will have one to streamline staging deployment 

![Git Flow](https://nvie.com/img/git-model@2x.png)

### Branches

#### Protected

> Locked for direct commits — all commits must be made from a non-protected branch and submitted via a pull request with one approving review

- **master** - Production application

#### Non-protected

> Commits can be made directly to the branch

- **release** - Staging application
- **develop** - Working version of the application
- **feature/<`scaffold`>-<`feature-name`>** - Based off of develop
  - ex. **feature/cms-strapi**
- **hotfix/<`scaffold`>-<`fix-name`>** - Based off of master
  - ex. **hotfix/client-cors**

### Pull Requests

Before submitting a pull request, rebase the feature branch into the target branch to resolve any merge conflicts.

- PRs to **master** should squash and merge
- PRs to all other branches should create a merge commit

## Project Features Implemented

Version History Modal:
- Description: Implemented a version history modal to track and display changes made by team members.
- Screenshots:
  
<img width="688" alt="Screenshot 2023-12-10 at 3 54 33 PM" src="https://github.com/camcimber/Nutritional-Facts/assets/89543442/02cb9b21-c402-4895-8d60-6c7a0dd76ad5">
  
Rename Save Feature:
- Description: Added a feature allowing users to rename specific saves for improved project organization.
- Screenshots:
  
<img width="552" alt="Screenshot 2023-12-10 at 4 02 23 PM" src="https://github.com/camcimber/Nutritional-Facts/assets/89543442/d7cf3d3f-378a-4a0d-a97b-ff4494f27224">

Save Pop-up for Non-Logged-in Users:
Description: Added a pop-up for non-logged-in users, prompting them to log in before saving their work.
Screenshots: 

<img width="520" alt="Screenshot 2023-12-10 at 3 54 19 PM" src="https://github.com/camcimber/Nutritional-Facts/assets/89543442/1c73b6bf-e2e4-4a41-95ed-a70dca71e8c2">

## Outstanding Work

User Stories

1. As a new user, I want to access a gallery of other users' work so that I can get inspiration for what I want to create and learn from others. [1]
Completed:
- As a new user, I want to be able to code in the workspace and have my progress be saved, even without creating an account. Once I close out of the tab and come back, I want my work to still be there, as long as I have cookies allowed on my browser. [1]

Outstanding:
- As a new user, I want to access a gallery of other users' work so that I can get inspiration for what I want to create and learn from others. [1]

- As a member of a team, I want access to a gallery shared by the members where each person's changes get saved in a different gallery entry, so everyone has access to their contributions. [8]

- As a student, I want to be able to access the gallery with code examples from the home screen, make a copy for myself, to aid in my learning Ardublocky. [2]


2. As a member of a large team, I want to be able to view my teammates' changes and be able to restore previous history so that I can achieve full awareness of what's going on and fix possible mistakes. [8]
Completed:
-As a member of a large team, I want to be able to view my teammates' changes and be able to restore previous history so that I can achieve full awareness of what's going on and fix possible mistakes. [8]

-As a student, I want to be able to see a history of my saves and be able to revert my project to one of them if needed, so I can easily undo any work that I’ve done. [8]

- Link to our project board: https://github.com/orgs/CEN3031-team3i/projects/1/views/1

## Built Upon
The project is built upon the following technologies and frameworks:

- React for front-end development
- JavaScript, CSS, HTML for UI updates
- Docker for efficient containerization

## Credits
We would like to credit the following people/organizations for their contributions:

- Bootstrap: Used for styling and layout components.
- YouTube Tutorial on Modals in ReactJS: Referenced for implementing the version history modal.

