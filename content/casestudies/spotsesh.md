# SpotSesh Case Study

## Project Description

SpotSesh is a web application that leverages the Spotify API to connect users in sessions. Each session has a host, the person who created the session, and everyone else joins their session. When ready, the host can start the listening session. The app shuffles the top 5 songs of all the members in the session and starts playing them on the hosts device. 

## Skills Used

- Node.js Express RESTful API written in TypeScript
- Real-time sessions with WebSockets
- Vue.js single page application
- Consuming a third party API (Spotify API)
- Responsive Design with HTML5 and CSS3

<aside>
<img src="https://cdn-icons-png.flaticon.com/512/5968/5968292.png" alt="https://cdn-icons-png.flaticon.com/512/5968/5968292.png" width="40px" /> **JavaScript**

</aside>

<aside>
<img src="https://cdn-icons-png.flaticon.com/512/919/919825.png" alt="https://cdn-icons-png.flaticon.com/512/919/919825.png" width="40px" /> **Node.js**

</aside>

<aside>
<img src="https://socket.io/images/logo.svg" alt="https://socket.io/images/logo.svg" width="40px" /> **Socket.io**

</aside>

<aside>
<img src="https://icons.iconarchive.com/icons/cornmanthe3rd/plex/256/Other-html-5-icon.png" alt="https://icons.iconarchive.com/icons/cornmanthe3rd/plex/256/Other-html-5-icon.png" width="40px" /> **HTML5 & CSS3**

</aside>

<aside>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/2367px-Vue.js_Logo_2.svg.png" alt="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/2367px-Vue.js_Logo_2.svg.png" width="40px" /> **Vue.js**

</aside>

<aside>
<img src="https://pinia.vuejs.org/logo.svg" alt="https://pinia.vuejs.org/logo.svg" width="40px" /> **Pinia**

</aside>

<aside>
<img src="https://cdn.iconscout.com/icon/free/png-256/free-nginx-3628948-3030173.png?f=webp" alt="https://cdn.iconscout.com/icon/free/png-256/free-nginx-3628948-3030173.png?f=webp" width="40px" /> **Nginx**

</aside>

## Lessons Learned

### Handling web-socket traffic through a reverse proxy

This application uses web sockets as the architecture that supports the sessions users can join. While I have used web-sockets for a project in the past, I didn’t dive deep into how web-sockets can be made available on a server, particularly through an Nginx reverse proxy. 

When running a server with an Nginx reverse proxy, all traffic is navigated using a typical URL over the HTTP protocol. The reverse proxy then directs the traffic to the correct resource according to its configuration files. The problem with sending HTTP traffic to a web-socket is that web sockets are a separate protocol from HTTP. Web-sockets, luckily, are made to be easily upgraded to be compatible with HTTP. In-fact, the Socket.io

## Project Outcome

This project has been launched on [my website](http://spotsesh.ryancarr.ca). Currently, it is in alpha mode and is still undergoing a thorough testing process. After alpha testing, I can get some friends to test this app out and hopefully launch as a service that many other people can use and enjoy as well.

## Room for Improvement

There are many areas for improving this application, most of which are related to ease of use and user experience. This initial alpha launch is an MVP. Many small features, improvements and bug fixes will be done over the next few weeks to get the app ready for beta testing.