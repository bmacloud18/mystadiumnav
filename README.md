# My Stadium Navigator 

**Group N**: *Final Project* - 12/01/23

## MyStadiumNav  

Core functionality of our PWA works and major issues have been resolved. A user is able to sign-up, sign-in from a created account, edit profile settings, add event tickets to their account, send tickets across accounts, view all levels of information associated with their ticket(s), offline, and installable technology. These implementations have been accomplished through api requests and saving information to localStorage and the cache.  
Additionally, we believe that our interface is intuitive and visually appealing. The layout can be navigated by any user with minimal website usage experience. The target audience of this app are event-goes who would like their information saved in one place and offline.  
Authentication is done by saving a user to an account they created and authorized using JWT tokens, hashing, and secret keys. Through layering these technologies together, sending this information to the server is secure. Additionally, known password and salt saved in the database are hidden from the frontend. API request are make from the frontend to call differnt mysql queries to a database. This database contains initializaitons at the applications start up to establish objects. Addtionatlly, middleware is in place to allow required authentication to access pages within the applciation.  
At first we used cache-first implementation, however it was evident that our project needed to be fetch-first due to our application being highly dynamic. This allows the most up to date information to be saved in the cache, however this does minimally decrease the speed of the application, but this step is necessary. Caches are used with the help of service workers to save the cache when a service worker is installed. Throughout the usage of the application, the same service worker is used. Using caches effectively is what helps our application to work offline. LocalStorage is also used to lower the dependency on using API calls.   
In this milestone, we changed our implementation to work with an “active ticket” rather than having an “active event” associated with the subpages of the application. This is necessary because a user of a respective event can have multiple tickets for one event. Additionally, details of the event can be extrapolated from the contents of the ticket.  
With this change, users now have the ability to search for events and add tickets to their wallet from the homepage. In their wallet, they can delete their tickets or send them to another user by specifying the recipient's username.

| Pages  | Status | Decsription | Wireframe |
| ------------- | ------------- | ------------- |  ---------   |
| Home-guest  | ✅  |  |  [guest](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Welcome_Home.png)  |
| Home-user  | ✅  |  | [user](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Welcome_Home.png)   |
| SignIn  | ✅ |   |  [SignIn](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Sign_In_Up.png)  |
| SignUp  | ✅   |   |  [SignUp](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Sign_In_Up.png)  |
| Maps-Seat  | ✅  |    |  [Seat](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Maps_My_Seat.png)  |
| Maps-Bathroom  | ✅   |  |  [Bathroom](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Maps_Bathrooms.png)  |
| Maps-Parking  | ✅   |   |  [Parking](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Maps_Parking.png)  |
| Maps-Vendors  | ✅   |  |  [Vendors](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Maps_Food.png)  |
| Maps-EmergencyServices  | ✅    | |  [EmergencyServices](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Maps_Services.png)  |
| Details-Schedule  | 20%   |  no backend or functionality was implemented. only a "construction page" has been placed instead.  |  [Schedule](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Schedule.png)  |
| Details-Announcements  | 20%   |  no backend or functionality was implemented. only a "construction page" has been placed instead.  |  [Announcements](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Announcements.png)  |
| Details-GeneralInfo  | ✅   |  frontend only partially implemented  |  [GeneralInfo](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/General_Information.png)  |
| Account-Wallet  | ✅ |   |  [Wallet](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Wallet.png)  |
| Account-Profile  | ✅  |   |  [Profile](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Profile_Accessibility.png)  |
| Account-History  | ✅  |   |  [History](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Event_History.png)  |
| Support-Settings  |✅   |   |  [Settings](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/main/Proposal/Wireframes/Profile_Accessibility.png)  |
| Support-AboutUs  | ✅   |    |    |
| Support-Help  | ✅   |    |    |

## User Routes

These routes should be accessible to the user in order to provide a fully functional application

| Method  | Routes | Decsription | Status |
| ------------- | ------------- | ------------- |  ---------   |
|GET|/events/:eventId|returns an events object with the matching id field|✅|
|GET|/events/:eventId/details|returns the event details field of the matching event object - useful for home page|✅|
|GET|/events/venues/:venue|returns a list of events that are located at the specified venue|✅|
|GET|/events/upcoming|returns a list of events that have a date/time not past the current date - upcoming|✅|
|GET|/tickets/:ticketId|returns a list of all tickets in the database with a matching eventId|✅|
|GET|/tickets/events/:eventId|returns a list of all tickets in the database with a matching eventId|✅|
|GET|/tickets/venues/:venueId|returns a list of all tickets in the database with a matching venueId|✅|
|GET|/tickets/users/:ownerId|returns a list of all tickets in the database with a matching ownerId|✅|
|GET|/tickets/users/current/all|returns a list of all tickets in the database that the current user owns|✅|
|GET|/tickets/users/current/upcoming|returns a list of all tickets in the database that the current user owns and have a date/time ahead of the current date - upcoming|✅|
|GET|/tickets/users/current/history|returns a list of all tickets in the database that the current user owns but have past their date/time by 6 hours|✅|
|GET|/tickets/users/current/events/:eventId|returns a list of all tickets in the database that the current user owns with a matching eventId|✅|
|POST|/tickets|creates and adds a new ticket object to the database and to the user's 'wallet'|✅|
|PUT|/tickets|takes a ticket from the logged in users wallet and 'sends' it to another user by updating the ticket's usr_id|✅|
|POST|/register|this endpoint acts as a registration endpoint for adding new users to the database|✅|
|POST|/login|this endpoint will provide authentication for the provided user login information in the request body|✅|
|POST|/logout|this endpoint will provide a method for the current user to log out and clear their session|✅|
|GET|/users/:userId|returns the user object with a matching user id|✅|
|GET|/currentuser|returns the user object of the currently logged in user|✅|
|GET|/currentuser/tickets|retrieves the list of tickets owned by the currently logged in user|✅|
|PUT|/currentuser|logged in users will be able to update their user information such as names, username, etc. by reaching this endpoint|✅|
|PUT|/currentuser/password|logged in users will be able to update their user password by reaching this endpoint (must authenticate on this endpoint)|✅|
|PUT|/currentuser/settings|logged in users will be able to update their user settings by reaching this endpoint|✅|
|PUT|/currentuser/ticket|users can change their active ticket to another in their wallet by hitting this endpoint|✅|
|GET|/users/current/events|returns a list of the events that the current user has tickets to|✅|
|GET|/users/current/events/upcoming|returns a list of the upcoming events that the current user has tickets to|✅|
|GET|/users/current/events/history|returns a list of the past events that the current user has tickets to|✅|
|GET|/users/current/events/active|returns the user's 'active event' field, used to populate nav bar with event details|✅|
|GET|/venues|returns a list of all venue objects in the database|✅|
|GET|/venues/:venueId|returns the venue object with a matching venueId field|✅|
|GET|/venues?state=:state|returns a list of venues which are located in a certain state|✅|


Admin Routes: these routes should only be accessible to administration in the case of system wide changes to the database.
These new routes are unique to M2.

| Method  | Routes | Decsription | Status |
| ------------- | ------------- | ------------- |  ---------   |
|POST|/events|creates and adds a new event object to the database|✅|
|POST|/venues|creates and adds a new venues object to the database|✅|
- most admin routes were not implemented because we did not create an admin user role

The following ER tables were created in the database. This allows for persistance across webpages. Using the ID tag help to identify the particular object, therefore foreign keys were established in keys outside of the table.  
The database design has changed since M2 to allow saving a barcodes for a ticket. The following fields have been added to the ticket table, all else is unchanged:
    `tkt_qr_code` varchar(150) NOT NULL,
    `tkt_bar_code` varchar(150) NOT NULL,
PLEASE SEE : [ER Diagram](https://github.ncsu.edu/engr-csc342/csc342-2023Fall-GroupN/blob/dev/Milestone2/frontend/src/static/images/ER.pdf)    

---

## Team Contributions:  
#### M1
Evan Jonson: Frontend implementation. Backbone stucture for all pages. SignIn/SignUp Pages. Account Pages.<br>
Gabe Watts: Frontend implementation. Map pages nearly all implemented.<br>
Benjamin Abbott: Backend implementation. Creation of API routes and implementation in API folder.<br>
All: Report and review work.

##### M2
Evan: authentication, account creation, middleware, frontend (profile, support pages, events).<br>
Gabe: Map connect to backend, created map data, alter tables for map properites.<br>
Benjamin: general backend (api routes, DAO methods), database schema, connecting backend with DB and our frontend.  

##### M3
Evan: Tickets, frontend and backend (active, add, delete). Search, frontend and backend. User settings, frontend and backend. Service worker. Installable App, manifest and icons. Downloads and offline functionality.<br>
Gabe: maps calling and ui finlization, service workers and fixes, general information page, construciton pages.<br>
Benjamin: route updates, send ticket functionality (FE/BE)
