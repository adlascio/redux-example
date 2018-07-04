## React + Redux

- create-react-app redux-example
- create folder components
- create files Posts.js and Postform.js
- import Posts and Postform in app.js
- make fetch request in posts.js and map through
- create form in Postform.js

- install redux, react-redux and redux-thunk
- wrap whole return in app.js using tag Provider
<Provider store={store}>

- create store.js in src

## store.js
- import createStore and applyMiddleware from redux
- import thunk form redux-thunk
- create store = createStore(rootReducer, initialState, applyMiddleware(...middleware))
middleware = [thunk]
- export store

## app.js
- import store from store.js

- create folder reducers, file index.js and postReducer.js

## app.js
- import rootReducer from reducers

## reducers/index.js
- import combineReducers from redux
- import postReducer from postReducer
- export combineReducers({posts: postReducer});

- create folder actions and file types.js

## types.js
- export fetch_posts and new_post

## postReducer.js
- import fetch_posts and new_post from types
- create initialState
- export function(state = initialState, action) {
  switch (action.type) {
    case fetch_posts:
    return {
      ...state,
      items: action.payload
    }
    default:
    return state;
  }
}

- create postActions.js in actions folder

## postActions.js
- import fetch_posts and new_post
- export const fetchPosts = () => dispatch => {
    <!-- fetch posts (cut from posts.js) -->
    data => dispatch({
      type: fetch_posts,
      payload: data
    })
}

## Posts.js
- import connect form react-redux
- import fetchPosts from postActions
- export connect(mapStateToProps, {fetchPosts} )(Posts);
- call fetchPosts in componentDidMount
- create mapStateToProps = state => ({
  posts: state.posts.items
  });
- change state to props in postItems
- import PropTypes from prop-types
- Posts.propTypes = {
  fetchPosts: PropTypes.func.isRequired,
  posts: PropTypes.array.isRequired
}

## postActions.js
- create new action named createPost
- cut fetch from Postform.js
- post => dispatch({
      type: new_post,
      payload: post
    })
- change post to postData on stringify

## postReducer.js
- create new case for new_post copying from fetch_post and change items to item

## Postform.js
- import connect from react-redux and proptypes from prop-types
- import createPost from postActions
- call createPost giving post
- export connect(null, {createPost})(PostForm);
- PostForm.propTypes = {
  createPost: PropTypes.func.isRequired
};

## Posts.js
- add newPost to mapStateToProps and propTypes
- create componentWillReceiveProps(nextProps) {
  if(nextProps.newPost) {
    this.props.posts.unshift(nextProps.newPost);
  }
}

