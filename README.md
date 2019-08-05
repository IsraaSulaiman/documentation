# Documentation for Nova App for Developers

### All User Stories/Backlog Items
- As a user, I want to see a disclaimer before I proceed to navigate the page. 
- As a user, I want to know what Nova is about.
- As a user, I want to create a new account in Nova app.
- As a user, I want to login to my account.
- As a user, I want to navigate through the pages easily on my mobile. 
- As a user, I want to feel not alone and like somebody cares by asking me about my feelings/thoughts.
- As a user, I want to know what kind of support Nova provides to make me feel better.
- As a user, I want to find good resources of information and suggestions to help me let go of negative feelings/trauma.
- As a user, I want to have a non-judmental space where I write my diaries during trigger times.
- As a user, I want to view all my diaries.
- As a user, I want all of my diaries to be private.
- As a user, I want to delete any diary that makes me feel bad.
- As a user, I want to edit any diary any time.
- As a user, I want to have a place to save lillies/pictures for my loved ones.
- As a user, I want to delete any picture any time I want.
- As a user, I want to see all the pictures I save in my personal corner.
- As a user, I want to do some exercises when I feel overwhelmed/bereaved.
- As a user, I want to find some distractions, like reading poems.
- As a user, I want to add a poem that helped me/that I love.
- As a user, I want to read the stories of other people who experienced loss of loved ones.
- As a user, I want to be able to share my story when I feel I am ready for that.

______________

### Main Features:
The features we will work on during this sprint are:
1. Information & Suggestions
2. Personal Space
    - Journal
    - Pictures

### Stretch Goals
1. Continue Personal Space:
    - Exercises
    - Poems
2. Other Stories & Share Your Story

_______________

### Call Stack:
- **FrontEnd**: Reactjs
- **BackEnd**: Nodejs
- **Server**: Expressjs
- **Database**: PostgreSQL? MongoDB?

________________

### Components:
#### Pages:
1. LandingPage
2. Login
3. Signup
4. AboutUs
5. Status
6. HomePage
7. Journals
8. Journal
9. EditJournal
10. NewJournal
11. Pictures
12. NewPicture
  
#### Common Components:
1. Header
2. Footer
3. Loading
4. Menu
5. DropDown
6. Button
7. JournalCard
8. ServiceCard
9. Input
10. TextArea

______________

### Analysis

#### Header
  - Function component
  - props: `{isLogged, className}`<br>
  
  Since we have 4 headers, we need the `className` property to style the component as we want depending on the page.<br>
  `isLogged` property will be passed from the app to this component since it will be needed in the menu to determine what navlinks to display.
  - All props are required

#### Menu
  - Function component
  - props: `{isLogged}`<br>
  
  `isLogged` is needed to determine what navlinks would appear on the menu component. <br>
  Here is an idea of what could be done here:
  ```javascript
  //if logged in
  const navLinksForUsers = [
    {text: 'Nova Home', path: '/home'},
    {text: 'Nova Information', path: '/information'},
    {text: 'Nova Stories', path: '/stories'},
    {text: 'Personal Space', path: '/personal-space'},
    {text: 'Logout', path: '/logout'},
  ]
  //if not logged in
  const navLinksForVisitors = [
    {text: 'Nova Home', path: '/'},
    {text: 'About US', path: '/about-us'},
  ]
  ```
   - Map through one of these arrays to create a list of items(`li` or `button`)
   - `redirectOnClick(path)`:
   When the user clicks on one of these buttons/items, it redirects him to the required page. This could be done using `Redirect` component from `react-dom-router` but I prefer `props.history.push(path)` to maintain our router history. Either way is okay after all!
   - All props are required

#### Button
  - Function component
  - props: `{className, action, text`<br>
  
  className is needed because we have different styles for buttons.
```js
  <Button className='login__button' action={this.submitForm} text='Login'/>
```
  - All props are required

#### Input
   - props: `{label,placeholder,type,action }`<br>
   
   Label and placeholder properties are optional. Other props are required.

  - One style for all inputs :).
  - This component includes label and input elements

```js
  <Input label='Your Email' type='email' placeholder='person@example.com' action={this.validateInput}/>
```
The action function will be called not on each change, rather after blur. So, the event will be `onBlur` to minimize rendering the component as possible. Cool?

#### TextArea
  - Function component
  - props: `{placeholder, action}`

Same thing here, action function will be triggered when `onBlur` event is fired. 
 - All textAreas in the app has the same design.
 - Props are required

#### JournalCard
- Function component
- props: `{id, action}`
- This component inclues the following elements:
  1. h3
  2. p
  3. delete icon (`id` will be passed here)
  4. edit icon (`id` will be passed here)
- `deleteJournal(e)`: when clicking on delete icon
- `redirectOnEdit(e)`: when clicking on edit icon, redirection will happen, using `props.history.push('/edit-journal/:id')`

#### ServiceCard 
  - Function component
  - props: `{icon, title, description, action}`
  - action: when clicking on the card, it redirects to the service page. Use `props.history.push(destination)`

#### DropDown
- This includes a select element with 3 options: stories, information & suggestions, what people said.

- `redirectOnSelect()`: when selecting an option, it redirects to the right page.

__________________

### Routes 

### Server Routes:

| Page | Method | Endpoint | Functionality | Request Body | Response Body|
  | ----- | ---- | ---- | ---- | ----| ----|
  | Signup | POST | `api/v1/signup` | 1.Validation <br> 2.Cryption <br> 3.Database: `insertUser(userName, babyName, nickname, email, password)`<br> 4. `createCookie()` | `{data: {userName, nickname, babyName, email, password}` | `{data: {id},error:undefined}` |
  | Login | POST  | `api/v1/login`  | 1.Database: `selectUser()`<br> 2.Compare Password <br> 3.Create Cookie | `{data: {email, password}}` |`{data:{id}, error:unefined}`  |
  | Journals | GET | `api/v1/journals` | 1. Database: `selectJournals(userId)`| - | `{data:{journals: [{id, title, content}, {id, title, content}]}, error:undefined}` |
  | Journals | DELETE | `api/v1/journals/:id`|1.Database: `deleteJournal(id, userId)`| - | `{data: {id}, error:undefined}` |
 | Journal | PUT | `api/v1/journals/:id`| 1.Validation <br> 2.Database: `updateJournal(id, userId)`| `{data: {title, content}}`| `{data: {id}, error:undefined}` |
  | Journal | GET | `api/v1/journals/:id` |1.Database: `selectJournal(id, userId)` | - |`{data:{id, title, content}, error:undefined}` |
  | Journal |POST | `api/v1/journal` |1.Database: `insertJournal(title, content, userId)`|`{data: {title, content}}`| `{data: {id}, error:undefined}`|
 | Pictures | GET | `api/v1/pictures` | 1.Database: `selectPictures(userId)`| - | `{data: {pictures:[{id, imgSrc, title}, {id, imgSrc, title}]}, error:undefined}` |
  | Pictures | POST  | `api/v1/pictures` |1.Validate the image size (not over than 500 kb) <br> 2.Database: `insertPicture(title, imgSrc, userId)`| `{files: {imgSrc}}` |`{data: {id}, error:undefined}`|
  | Logout | GET |`api/v1/logout`| 1.`clearCookie()` | - | `{data:{message:'success'}, error:undefined}` |

_____

### Client Side 

| Page Name | Route | functions | DidMount | object format |
| ---- | ---- | ---- | ---- | ---- |
| Disclaimer | `/disclaimer` | btn : procceed ( redirect `/` ) ||
| Landing | `/` | btn : back ( redirect `back`), btn: login (redirect `/login`), btn: register (redirect `/register`), btn: about us ( redirect `/about-us`) |||
| about us | `/about-us` |btn: back ( redirect `back`) |||
| signup | `/register` | inputs: validation with ( `onBlure`) btn: sginup (validation, fetch(`/api/v1/signup`, {method: `post`}) => redirect (`/status`))|| `{data: {name, babyName, nickname, email, password}}`|
| login | `/login` | btn: send (validation(not empty, fetch(`/api/v1/login`, {method: `post`})))|| `{data: {email, password}}`|
| status | `/status` |btn: submit(validation not empty) btn: skip (redirect `/home`)|||
| home | `/home` |btn: information(redirect (`/information`)), btn: stories (redirect (`/stories`)), btn: personal space (redirect (`/personal-space`))|||
| information | `/information`| btn: next ( redirect(`/suggestions`)), btn: back( redirect(`back`))|||
| suggestion | `/suggestions` | btn: back (redirect `back`)|||
| personal space | `/personal-space` | btn: pictures (redirect `/pictures`), btn: poems (redirect `/poems`), btn: exciercises (redirect `/exercises`), btn: journal (redirect `/journals`), btn: back (redirect `back`)|||
| journals | `/journals` |btn: add (redirect `/journals`), btn: edit (redirect `/journals/id`), btn: delete (show poup for delete if `ok` (fetch(`/api/v1/journals/id`, {method: `delete`}))), click card (redierct `/journals/id`)| fetch(`/api/v1/journals`, {method: `get`})||
| edit journal | `/edit-journal/id` |btn: edit (validation => fetch(`/api/v1/journals/id`, {method: `put`})), btn: back (redirect `back`)| fetch(`/api/v1/journals/id`, {method: `get`})||
| add journal | `/journals` | btn: save (validation, fetch(`/api/v1/journals`, {method: `post`})), btn: back (redirect `back`)||`{data: {title, content}}`|
| single journal | `/journals/id` | btn: back (redirect `back`), btn: edit & delete the same functionality in the journals page|||
| pictures | `/pictures` | btn: delete icon (display popup for delete if `ok` fetch(`/api/v1/pictures/id`, {method: `delete`})), btn: plus icon (redirect `/pictures`), btn: more pictures (render more photo add (10))| fetch(`/api/v1/pictures`, {method: `get`}) svae in state and first render just 10 photo||
| add picture | `/pictures`| btn: save ( validation => fetch(`/api/v1/pictures`, {method: `post`})), btn: cancel (redirect `back`)|| append file in `formData`|

_____

### Database

![Nova Schema](databaseSchema.png)
<br>
  To Edit, [click here]('https://dbdesigner.page.link/LkJEzgpgUMsVZnfy6')

_____________

