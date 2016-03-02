### Imperative vs Declarative Code:
- Imperative
  - Explicitly telling a program how to do something
- Declarative
  - More concerned about what we want our code to do rather than how it does it
  - Reduce Side Effects
  - Minimize mutability
  - More readable code
  - Less Bugs

### Is React Declarative?
- For the most part
  - Comes from the components rather than state
- Example highlight button on click
  - Imperative in jquery
  ```javascript
    $("tylers-btn").click(function() {
      $(this).toggleClass("highlight")
      $(this).text() === 'Add Highlight' ? $(this).text('Remove Highlight') : $(this).text('Add Highlight')
    })
  ```
  - React
    - Instead of how we are concerned what we want it to look like
    ```jsx
    <TylersBtn
      onToggleHighling={this.handleToggleHighlight}
      highlight={this.state.highlight}>
        {this.state.buttonText}
    </TylersBtn>
    ```
    - State managment is seperated out eleswhere
    ```javascript
      this.setState({
        highlight: !this.state.highlight,
        buttonText: this.state.buttonText === 'Add Highlight' ? 'Remove Highlight' : 'Add Highlight'
      })
      ```

### Composition
- How do you break down an app into different components
  - ![Instagram](01-Instagram.png)
  - Compose larger components from smaller components
  - Same with building functions
  - React returns html elements or other react components
  - Javascript functions
  ```javascript
  var getProfilePic = function(username) {
      return "https://photo.fb.com" + username
  }

  var getProfileLink = function(username) {
      return "https://www.fb.com" + username
  }

  var getProfileData = function (username) {
      return {
        pic: getProfilePic(username),
        link: getProfileLink(username)
      }
  }
  ```
  - React
  ```jsx
  var ProfilePic = React.createClass({
    render: function() {
      return (
        <img src={'https://photo.fb.com/' + this.props.username} />
      )
    }
  })

  var ProfileLink = React.createClass({
    render: function() {
      return (
        <a href={'https://www.fb.com/' + this.props.username}>
          {this.props.username}
        </a>
      )
    }
  })

  var Avatar = React.createClass({
    render: function() {
      return (
        <div>
          <ProfilePic username={this.props.username} />
          <ProfileLink username={this.props.username} />
        </div>
      )
    }
  })

  <Avatar username="tylermcginnis" />
  ```

### Explicit Mutations
- Explicitly call `setState` to get the view to rerender

### "It's just JavaScript"
- People getting grumpy when using it, but it's largely just a limitation of their knowledge of JavaScript.
```jsx
var listItems = this.props.items.map(function(item, index){
  return (
    <li style={styles.listGroup}>
      <button
        style={styles.removeItem}
        onClick={this.props.remove.bind(null, index)} />
      <span>
        {item}
      </span>
    </li>
  )
}.bind(this))
```

### Piecing the Puzzle
- API is pretty small
- Ecosystem is pretty big
  - Covering in this course
    - React
    - React Router
    - Webpack
    - Babel
    - Axios
    - 
### React Router
```jsx
  <Router history={hashHistory}>
    <Route path='/' component={Main}>
      <IndexRoute component={Home} />
      <Route path='playerOne' header='Player One' component={PromptContainer} />
      <Route path='playerTwo/:playerOne' component={PromptContainer} />
      <Route path='battle' component={ConfirmBattleContainer} />
      <route path='results' component={ResultsContainer} />
    </Route>
  </Router>
```
  - Allows us to map different components to different URLs
     - Example:

| __URL__              | __Active Component__           |
|----------------------|--------------------------------|
| foo.com              | Maine -> Home                  |
| foo.com/playerOne    | Main -> PrompContainer         |
| foo.com/playerTwo/tm | Main -> PromptContainer        |
| foo.com/battle       | Main -> ConfirmBattleContainer |
| foo.com/results      | Main -> ResultsContainer       |
