# Web Chat App
This repository contains a real-time web chat application implemented using Node.js, Express, Socket.IO, RxJS and Angular. It contains users and admins with groups and channels.
## Angular Architecture
The Angular application contains _components_, _services_ and _routes_.

### Components
There were four components that were used in this application. 
- channel
- dashboard
- group
- login

#### Channel
The Channel component contains all the user-interface features of a chat channel. It contains a list of users, the current channel name, the chat box and the textfield and button to send messages. 

#### Dashboard
The Dashboard component contains all the groups available to the user, their username, their current email, an input field to update their email and a log out button. 

For Group admins, there's a form to create new groups and buttons to remove groups. Note that default groups _newbies_ and _general_ cannot be removed. 

For a Super admin, they can see the entire list of users in the system. Super admins can remove users from the system (except the persistent _Super_ user) and assign Group or Super admin roles to existing users. 

#### Group
The Group component contains all the information for groups. This includes the group name, the logged in user, the available channels to the user and a log out button. 

Group admins will have an input form to add new channels and buttons to remove channels. Note, default channel _general_ cannot be removed (however an admin can remove a group in the Dashboard component).

Group admins can also add users to the group and remove users from the group. Adding a non-existent user simply creates the user and adds them to the group. Adding a user to the group automatically adds them to the default channel _general_. 

#### Login
The Login component allows a user to log in. Any user can type any username and log in. User data will persist after they log out. If a username does not exist in the system, the server will seamlessly create the user in the background. 

### Services
#### Image
The image service handles the upload of images to the server. It contains a function that performs a POST request to the server. 

#### Socket
The socket service handles the web socket communications in real-time. The sockets contain three rooms:
* join
* leave
* new-message

Join notifies the server that the user has joined the channel. Leave notifies the server that the user has left the channel. New-message is used for new messages, which may be text or images. 

The server responds in the message room, broadcasting only to the room which it originally received from. 

#### Users
The users service contains the requests for all dashboard, groups and channel data manipulation to and from the server. 
