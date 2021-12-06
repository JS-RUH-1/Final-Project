# Final Project 

![](tuwaiq1000-dark.svg)

## Overview: 

For your final project, you'll have the choice of building a MERN stack. Use your imagination! You get to create whatever you want for this app. 

Though, you'll need to run your user stories, wireframes, and database design by your instructors to get their feedback and approval before you begin coding! 

You will be woking as an individual for this project. 

## Prerequisite:
- Select a Project Idea of your own.
- User stories
- Wireframe 
- React Router Routes
- Components
- Models
- Backend routes



## Requirements:

- Build a full stack web application. Must be your own work.
    - back-end: Express, MongoDB  
    - front-end: React, NextJs
    - Connect the backend and frontend through the API
- Have at least 3 models (more if makes sense)
- Add authetication for Users
- Have multiple users roles and authorization for each role 
- Have full CRUD on at least one of your models
- Be able to Add/Delete on any remaining models
- Create database and connect it to the project.
- Use the MVC design pattern
- Be deployed on Heroku
- Readme 


## Additional Requirements & Bonus:
- Use a third-party APIs {SMS Message, Google Maps,…. ([Resource](https://any-api.com/), [Resource](http://apis.io/))
- SocketIO ([Resource](https://socket.io/))
- Authorization roles and groups
- Upload the images/files to : 
    - AWS S3 ([Resource](https://aws.amazon.com/s3/?nc2=h_ql_prod_st_s3))
    - Cloudinary ([Resource](https://cloudinary.com/)) 
- Make a  React-Native as front-end. 
- Use the unit-test (Mocha,Chai or Jest)


## Necessary Deliverables:
### Projects are due Wednesday, 22/12


- A link to your deployed application
- A link to your github repository
- A link of your presentation 

### The presentation must be a 8-10 minute presentation in which you answer the following questions:

- What is the application about?
- What are the user stories for your application?
- What API did you choose to use?
- Demo of the application
- Walk through a piece of code
- Answer some conceptual questions on your code
- What was the most difficult part of the project?
- What was your favorite part of the project?
- What is the thing your most proud of in the project?


## Useful Resources
- https://reactjs.org/docs/getting-started.html
- https://expressjs.com/


# Your prerequisite should be something like this:
*Note: add this to your final project Readme*

## User Stories
- **Signup:** As an anon I can sign up in the platform so that I can start playing into competition
- **Login:** As a user I can login to the platform so that I can log my exit points
- **Logout:** As a user I can logout from the platform so no one else can use it
- **Add Exit Points** As a user I can add an exit point
- **Edit Exit Points** As a user I can edit an exit point
- **Add PreOpp Checklist** As a user I can add players to a tournament
- **Edit PreOpp Checklist** As a user I can edit a player profile to fit into the tournament view
- **View Tournament Table** As a user I want to see the tournament table
- **Edit User** As a user I can edit my profile, add or substract exit points


## Client / Frontend

### React Router Routes (React App)

| Path             | Component            | Permissions                | Behavior                                                     |
| ---------------- | -------------------- | -------------------------- | ------------------------------------------------------------ |
| `/`              | SplashPage           | public `<Route>`           | Home page                                                    |
| `/signup`        | SignupPage           | anon only `<AnonRoute>`    | Signup form, link to login, navigate to homepage after signup |
| `/login`         | LoginPage            | anon only `<AnonRoute>`    | Login form, link to signup, navigate to homepage after login |
| `/exitpoint`     | TournamentListPage   | user only `<PrivateRoute>` | Shows all exit points in a list                              |
| `/exitpoint/add` | TournamentListPage   | user only `<PrivateRoute>` | Edits a exit points                                          |
| `/exitpoint/:id` | TournamentDetailPage | user only `<PrivateRoute>` | Details of a exit points to edit                             |
| `/exitpoint/:id` | n/a                  | user only `<PrivateRoute>` | Delete exit points                                           |

### Components

- LoginPage
- SplashPage
- ProfilePage
- SignupPage
- EditProfilePage
- EditExitPointPage
- ExitPointPage
- EditProfilePage
- Navbar

## Server / Backend

### Models

User model

```
{
  user: {type: String, required: true, unique: true},
  email: {type: String, required: true, unique: true},
  password: {type: String, required: true},
  favorites: [{type: Schema.Types.ObjectId,ref:'Exit'}]
  userAgreement: {type: boolean, required: true, default: false}
}
```

Exit model

```
 {
   name: {type: String, required: true},
   img: {type: String},
   aproachLat: {type: Number, required: true}
   aproachLong: {type: Number, required: true}
   aproachDescription: {type: String}
   exitLat: {type: Number, required: true}
   exitLong: {type: Number, required: true}
   exitDescription: {type: String}
   landiZoneLat: {type: Number, required: true}
   landingZoneLong: {type: Number, required: true}
   landingZoneDescription: {type: String}
   creator: {type: Schema.Types.ObjectId,ref:'User'}
   altitud: {type: number}
   
 }
```

### Backend routes

| HTTP Method | URL            | Request Body                                                 | Success status | Error Status | Description                                                  |
| ----------- | -------------- | ------------------------------------------------------------ | -------------- | ------------ | ------------------------------------------------------------ |
| GET         | `/auth/me`     |                                                              | 200            | 404          | Check if user is logged in and return profile page           |
| POST        | `/auth/signup` | {name, email, password}                                      | 201            | 404          | Checks if fields not empty (422) and user not exists (409), then create user with encrypted password, and store user in session |
| POST        | `/auth/login`  | {username, password}                                         | 200            | 401          | Checks if fields not empty (422), if user exists (404), and if password matches (404), then stores user in session |
| POST        | `/auth/logout` | (empty)                                                      | 204            | 400          | Logs out the user                                            |
| POST        | /api/exit      | {name, img, aproachLat, aproachLong, aproachDescription, exitLat, exitLong, exitDescription, landingZoneLat, landingZoneLong, landingZoneDescription, altitude} |                |              | Used to create one exit point document, using current logged in user id as a creator. |
| PUT         | /api/exit/:id  | {name, img, aproachLat, aproachLong, aproachDescription, exitLat, exitLong, exitDescription, landingZoneLat, landingZoneLong, landingZoneDescription, altitude} |                |              | Used to update one exit point document by id                 |
| GET         | /api/exit/:id  |                                                              |                |              | Used to get one exit point document by id                    |
| DELETE      | /api/exit/:id  |                                                              |                |              | Used to delete one exit point document by id                 |
| GET         | /api/user      |                                                              |                |              | Used to get current user's profile. Id of the user is coming form the req.session.currentUser |
| PUT         | /api/user      | {username, email, password}                                  |                |              | Used to update current user's profile. Id of the user is coming form the req.session.currentUser |


### Links

* Trello/Kanban

[Link to your trello board](https://trello.com/b/PBqtkUFX/curasan) or picture of your physical board

* Git

The url to your repository and to your deployed project

[Client repository Link](https://github.com/screeeen/project-client)

[Server repository Link](https://github.com/screeeen/project-server)

[Deployed App Link](http://heroku.com/)

* Slides

The url to your presentation slides

[Slides Link](http://slides.com/)
* Wireframe

The url to your Wireframe 

[Figma Link](http://www.figma.com/file/GNvDVBD1NPTydU2PJy4DDM/dataBASE?node-id=0%3A88)

