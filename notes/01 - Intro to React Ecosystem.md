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
    -
    ```javascript
$("tylers-btn").click(function() {
  $(this).toggleClass("highlight")
  $(this).text() === 'Add Highlight' ? $(this).text('Remove Highlight') : $(this).text('Add Highlight')
  })
  ```
  - React
    - Instead of how we are concerned what we want it to look like
    -
    ```javascript
  <TylersBtn
     onToggleHighling={this.handleToggleHighlight}
     highlight={this.state.highlight}>
    {this.state.buttonText}
   </TylersBtn>
  ```
    - State managment is seperated out eleswhere
      -
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
  -
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
  -
  ```javascript
  var ProfilePic = React.createClass({
    render: function() {
      return (
        <img src={'https://photo.fb.com/' + this.props.username} />
        )
    }
    })
  ```javascript
