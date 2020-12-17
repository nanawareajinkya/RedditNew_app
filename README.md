# react-reddit
Reddit clone written with [React](https://facebook.github.io/react) and bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).

## Overview
[react-reddit-jori.herokuapp.com](http://react-reddit-jori.herokuapp.com)
- Page is initially populated by a list of topics found in [database.js](src/database.js).
- Top 20 topics by points (upvotes minus downvotes) are displayed by default, sorted by points.
- You can select All to display all topics, so you can still see a topic even if it is downvoted to oblivion.
- Username is fixed to 'guest', and submitted topics and votes are done under this user.
- Newly submitted topics have one upvote when created.
- Repeated voting can be done.


1. Run npm install
```
cd react-reddit
npm install
``

2. To run tests, run npm test
```
npm start
```
