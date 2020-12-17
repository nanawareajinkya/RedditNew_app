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

## Approach
React was chosen because of its functional and component-based approach. You break down an app into smaller, reusable, composable components, making your app easier to maintain and reason about.

Functional programming is the main approach here. I used pure functions as much as possible to avoid shared mutable state. Functions with side effects and that mutate state is a source of a lot of bugs and :rage1:.

[TopicUtil.js](src/TopicUtil.js) has pure functions that return new objects instead of mutating existing ones:
```
addTopic(topics, topic) {
    return topics.concat([topic]);
}
```

Higher-order functions, currying, and partial application were used to break down functions into smaller, composable, and reusable ones:
```
// Curried function that returns a function to sort topics.
const getSortedTopics = comparison =>
    topics => {
        const sortedTopics = [...topics].sort(comparison);
        return sortedTopics;
    };
...

// Partially apply getSortedTopics to return a function that returns the sorted topics.
const getTopicsSortedByVotes = getSortedTopics(compareTopicVotes);

...
    getTop20TopicsSortedByVotes(topics) {
        const sortedTopics = getTopicsSortedByVotes(topics);
        return sortedTopics.slice(0, 20);
    },

    getAllTopicsSortedByVotes(topics) {
        return getTopicsSortedByVotes(topics);
    },
```

Apart from the libraries included in Create-react-app, I eschewed other libraries (such as Redux for state management and ImmutableJS for immutable data structures) to demonstrate that good coding practices can be done without them for this exercise.

## Files
### Components
- [App](src/App.js): the parent component. It is only used as the container for the child components, and does not have any application logic.
- [UserProfile](src/UserProfile.js): displays username
- [SubmitTopicForm](src/SubmitTopicForm.js): for submitting new topic
- [TopicList](src/TopicList.js): displays list of topics
- [TopicItem](src/TopicItem.js): displays individual item
- [DisplayType](src/DisplayType.js): controls whether to display top or all topics

[withDataStore.js](src/withDataStore.js) contains the app logic. It wraps the App component in a higher-order component that has the API to the data store.

[TopicUtil.js](src/TopicUtil.js) contains utility functions for sorting topics and manipulating them - create new topic, upvote, and dowvote.

[database.js](src/database.js) contains list of initial topics to display. Everytime `loadInitialTopics()` is called, a new copy of the topic list is created.

[.eslintrc](.eslintrc) is for code linting in the text editor.

Since there are a few styles, all of them are in [index.css](src/index.css), for simplicity.

### Tests
Each component has its own unit test file, named [Component].test.js. The test files are in the same folder as the component so that they are immediately visible, and to avoid nested directories when importing the component in the test.

Tests include rendering using Enzyme's `shallow()`, prop checking, and event simulation.

Tests follow [Arrange-Act-Assert pattern](http://wiki.c2.com/?ArrangeActAssert).

Jest and Enzyme are used for testing.

## Development
1. Clone the repo
```
https://github.com/joriguzman/react-reddit.git
```

2. Run npm install
```
cd react-reddit
npm install
```

3. Run npm start. App will run at [http://localhost:3000/](http://localhost:3000/).

4. To run tests, run npm test
```
npm test
```

## Deployment
This app is deployed to Heroku.<br>
To push to Heroku: `git push heroku master`

## Sending Feedback
Please send [your feedback](https://github.com/joriguzman/react-reddit/issues).

Thanks for reading! :squirrel:
