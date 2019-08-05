# documentation
## file Strucure
- client
    - Component
        - CommonComponent
            - Footer
                - index.js
                - style.css
            - Header
                - index.js
                - style.css
            - Loading
                - index.js
                - style.css
            - Menu
                - index.js
                - style.css
            - Button
                - index.js
                - style.css
            - Input
                - index.js
                - style.css
            - Textarea
                - index.js
                - style.css
            - DropdownMenu
                - index.js
                - style.css
            - HomeCard
                - index.js
                - style.css
            - JournalCard
                - index.js
                - style.css
        - Pages
            - Disclaimer
                - index.js
                - style.css
            - Landing
                - index.js
                - style.css
            - AboutUs
                - index.js
                - style.css
            - Signup
                - index.js
                - style.css
            - Login
                - index.js
                - style.css
            - Status
                - index.js
                - style.css
            - Home
                - index.js
                - style.css
            - PersonalSpace
                - index.js
                - style.css
            - Pictures
                - index.js
                - style.css
            - AddPicture
                - index.js
                - style.css
            - Journals
                - index.js
                - style.css
            - AddJournal
                - index.js
                - style.css
            - EditJournal
                - index.js
                - style.css
            - SingleJournal
                - index.js
                - style.css
            - Exercises
                - index.js
                - style.css
            - SingleExercises
                - index.js
                - style.css
            - Poems
                - index.js
                - style.css
            - SinglePoem
                - index.js
                - style.css
            - AddPoem
                - index.js
                - style.css
            - Information
                - index.js
                - style.css
            - Suggetion
                - index.js
                - style.css
            - Stories
                - index.js
                - style.css
            - SingleStory
                - index.js
                - style.css
            - AddStory
                - index.js
                - style.css
            - index.js
        - auth
            - protectRoute.js
        - assets
    - app.js
    - index.js
    - index.css
    - jsconfig.json
    - package.js
    - package-lock.js
    - .gitignore
- server
    - controller
        - signup
            - postUser.js
            - index.js
        - login
            - postLogin.js
            - index.js
        - journal
            - postJournal.js
            - getJournals.js
            - getSingleJournal.js
            - deleteJournal.js
            - index.js
        - picture
            - getPictures.js
            - PostPicture.js
            - deletePicture.js
            - index.js
        - logout.js
        - checkLogin.js
        - index.js
    - middleware
    - database
        - config
            - connection.js
            - dbBulid.js
            - dbBuild.sql
        - queries
            - insertUser.js
            - selectByEmail.js
            - selectJournals.js
            - selectJournal.js
            - updateJournal.js
            - deleteJournal.js
            - insertJournal.js
            - selectPictures.js
            - insertPicture.js
            - deletePicture.js
    - upload
    - app.js
    - index.js
- packgae.json
- package-lock.json
- .gitignore

_____

## Client Side 

| Page Name | Route | functions | DidMount | object format |
| ---- | ---- | ---- | ---- | ---- |
| Disclaimer | `/disclaimer` | btn : procceed ( redirect `/` ) ||
| Landing | `/` | btn : back ( redirect `back`), btn: login (redirect `/login`), btn: register (redirect `/register`), btn: about us ( redirect `/about-us`) |||
| about us | `/about-us` |btn: back ( redirect `back`) |||
| signup | `/register` | inputs: validation with ( `onBlure`) btn: sginup (validation, fetch(`/api/v1/signup`, {method: `post`}) => redirect (`/status`))|| `{data: {name, babyName, nickname, email, password}}`|
| login | `/login` | btn: send (validation(not empty, fetch(`/api/v1/login`, {method: `post`})))|| `{data: {email, password}}`|
| status | `/status` |btn: submit(validation not empty) btn: skip (redirect `/home`)|||
| home | `/home` |btn: information(redirect (`/information`)), btn: stories (redirect (`/stories`)), btn: personal space (redirect (`/personal-space`))|||
| information | `/information`| btn: next ( redirect(`/suggestion`)), btn: back( redirect(`back`))|||
| suggestion | `/suggestion` | btn: back (redirect `back`)|||
| personal space | `/personal-space` | btn: pictures (redirect `/pictures`), btn: poems (redirect `/poems`), btn: exciercises (redirect `/exirecises`), btn: journal (redirect `/journals`), btn: back (redirect `back`)|||
| journals | `/journals` |btn: add (redirect `/journals/new`), btn: edit (redirect `/journal/id`), btn: delete (show poup for delete if `ok` (fetch(`/api/v1/journals/id`, {method: `delete`}))), click card (redierct `/journals/id`)| fetch(`/api/v1/journals`, {method: `get`})||
| edit journal | `/edit-journal/id` |btn: edit (validation => fetch(`/api/v1/journals/id`, {method: `put`})), btn: back (redirect `back`)| fetch(`/api/v1/journals/id`, {method: `get`})||
| add journal | `/journal/new` | btn: save (validation, fetch(`/api/v1/journals/new`, {method: `post`})), btn: back (redirect `back`)||`{data: {title, content}}`|
| single journal | `/journal/id` | btn: back (redirect `back`), btn: edit & delete the same functionality in the journals page|||
| pictures | `/pictures` | btn: delete icon (display popup for delete if `ok` fetch(`/api/v1/pictures/id`, {method: `delete`})), btn: plus icon (redirect `/pictures/news`), btn: more pictures (render more photo add (10))| fetch(`/api/v1/pictures`, {method: `get`}) svae in state and first render just 10 photo||
| add picture | `/pictures/new`| btn: save ( validation => fetch(`/api/v1/pictures/new`, {method: `post`})), btn: cancel (redirect `back`)|| append file in `formData`|