React Redux Connectors and Providers
========================================

0. Write mapStateToProps

Reuse the latest dashboard project you worked on in the React course 0x09-React_Redux_reducer and install react-redux

Within the App/App.js file:

    Create a function named mapStateToProps. This should connect the uiReducer you created and the property isLoggedIn that your component is already using
    Import connect from Redux, and connect the mapStateToProps to the component

========================================

1. Create a small store

In the index.js file:

    Create a store using createStore from Redux that would contain the uiReducer state
    Implement a provider passing the store that you created to the main App

========================================

2. Test MapStateToProps

Export the mapStateToProps function you created if you haven’t already, and in the App.test.js file:

    Create a new suite to test the function
    Create a test that verify that the function returns the right object when passing the

========================================

3. Update mapStateToProps
mandatory

In the App.js file:

    Update the mapStateToProps function to also pass to the component the value for displayDrawer. It should be connected to the Reducer attribute isNotificationDrawerVisible
    Update the render function of the component to use the value displayDrawer coming from the props instead of the state

========================================

4. Connect your actions creators

In the App.js file:

    Connect to the component the actions creators displayNotificationDrawer and hideNotificationDrawer
    You should use the simplified version for the mapDispatchToProps. No need to import bindActionCreators
    Modify the render function of the component to use the functions passed within the props instead of the action within the Class component

========================================

5. Refactor your code

In the App.js file:

    You can delete the old function handleDisplayDrawer
    You can delete the old function handleHideDrawer
    Remove any state property related to the display of the drawer
    Remove any binding in the constructor
    You are now passing to your components props. You need to define propTypes and defaultProps

========================================

6. Update your tests

You can now refactor the App.test.js file:

    You don’t need to test the functions handleDisplayDrawer and handleHideDrawer since everything is already tested using the Redux mechanism
    You need to update the test you previously created to support the new attribute

Tips:

    At this point your app should be functional and able to display/hide the drawer using the Redux state
    Remember that the state of uiReducer is using Map from Immutable

========================================

7. Async actions & Thunk middleware

Let’s implement the LoginRequest / logout actions creators accross the entire application. LoginRequest is calling an API and is Async. Therefore, Redux will not support it. We will need to use a middleware

Install redux-thunk within your project. And in the index.js file, apply the middleware to your store

========================================

8. Connect LoginRequest to the App

Modify the file App/App.js:

    Connect the action creator loginRequest and map it to the login prop
    Modify the component to use the new login function from the props instead of the one within the class
    Refactor the component to remove any login or logout function and bind

========================================

9. Connect user state to the Footer

Modify the file Footer/Footer.js

    Create a mapStateToProps function
    Map the user props to the user within the Redux state
    Connect the Footer component to the function you created
    Modify the render function and remove any use of the Context. Instead use the user prop

========================================

10. Connect Logout action creator to the Header

Modify the file Header/Header.js

    Create a mapStateToProps function
    Map the user props to the user within the Redux state
    Connect the Header component to the function you created
    Connect the Header component to the logout action creator
    Modify the render function and remove any use of the Context. Instead use the user prop. When the user clicks on the link, it should now dispatch the logout action creator

========================================

11. Modify the uiReducer

Now that we can have the entire login request and the entire feedback loop, let’s modify a few things within the reducer:

    When the action LOGIN is passed, set the user within the state to the one passed within the action
    When the LOGOUT action is passed, make sure to set the user to null

========================================

12. Modify the test suites

Modify the test suites of the different components you modified:

    In the App.test.js, Footer.test.js, and Header.test.js to import the Stateless components instead of the connected component
    Remove any use of the mount function, and convert everything to use the shallow function
    You should remove any use of setState within the tests and pass directly the props to the stateless components
    Remove any test linked to the login, logout function within App, and Header
    Add a test in uiReducer to support the new action you just created

Tips:

    At this point your app should be functional and able to display/hide the drawer, login/logout using the Redux state
    Remember that the state of uiReducer is using Map from Immutable
    You can now see that your components logic is simplified. They only respond to props change. The logic is happening within the action creators

Requirements:

    Do not forget to add defaultProps and PropTypes to any component receiving props
    No error should be displayed within the console
    All the tests in the project should pass

========================================

13. Understand how to use the Redux Chrome extension

Install the Redux DevTools extension on your Chrome browser:

    Modify the index.js to support the extension
    Use the application and note the different actions being registered when you are logging in / logging out
    Note that a version of the state is saved along the different actions and you can jump at a different moment of the user journey

Tips:

    Read the documentation of the extension to learn how to support the Chrome extension as well as the Thunk middleware
    This extension can be one of the most powerful tool to debug an application. Make sure to become familiar with it

========================================

14. Combine store: Root reducer

Since you have more than one reducer for your application, you will need to combine them into the store.

Create a new file reducers/rootReducer.js, in this file, export a rootReducer:

    the root should contain every reducer
    courses maps to courseReducer
    notifications maps to notificationReducer
    ui maps to uiReducer

========================================

15. Combine store: modify the application

In the index.js, create the store using the root reducer instead of only the ui reducer:

    Any component connected to the state will probably need to be updated since you added a nested level

========================================

16. Combine store: write the tests

Modify the test suites:

    In the App.test.js, modify mapStateToProps to correctly work with the new format of the reducer
    Create a rootReducer.test.js file to test the root reducer’s initial state for the following structure:

{
  courses: Map {},
  notifications: Map {},
  ui: Map {}
}

Requirements:

    No errors in the browser’s console
    All tests should pass
    Use combineReducer to create the root reducer

========================================

17. Connect notifications: New Action Creator

We now know how to connect a simple component to a reducer. Let’s work on connecting a more complex component to the the entire API.

Add the following three action creators to notificationActionCreators.js

    setLoadingState whose parameter is a boolean. It will send the SET_LOADING_STATE action and the boolean.
    setNotifications whose parameter is an array. It will send the FETCH_NOTIFICATIONS_SUCCESS action with the data.
    fetchNotifications (which does not have a parameter). Calling it will dispatch setLoadingState with the boolean set to true
        It fetches /notifications.json
        Once the fetch is realized, it will dispatch setNotifications with the data
        At the end of the query it sets the loading state to false again

========================================

18. Connect notifications: Improve reducer

In the function notificationReducer within notificationReducer.js:

    Make sure to add a loading attribute to the initial state.
    Modify the notifications object to have the right initial state when merging the data coming from the API
    Create a SET_LOADING_STATE case and update the state accordingly
    Modify the FETCH_NOTIFICATIONS_SUCCESS case to perform a mergeDeep with the data


