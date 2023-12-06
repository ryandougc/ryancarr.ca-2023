# K9DetectionSports Case Study

### My Role

- Planning and Research
- Design
- Development
- Testing
- DevOps
- Maintenance

As the sole developer, I was responsible for the entire process of creating this web platform. I worked with the client from the requirements gathering stage, all the way through planning, design, development, testing, launching and now maintenance.

### About K9DetectionSports.ca

K9DetectionSports is a local dog training business that teaches dog owners the sport of scent work. Think of a recreational and fun version of police dog sniffing for drugs or bombs. This sport is an incredible bonding experience for dogs and their owners. 

### The Process

To begin, I wanted to see the full picture of the existing system that was allowing the business to run, at the time. Going over what they already had setup let me understand the bare minimum that a new system would need to do. It also shows the opportunities for automation to improve the business’ workflow and improve efficiency. It was easy to see that their previous system was wasting hundreds of hours each year from manual data transfers and updates over the different platforms and technologies being used. 

My solution to this data transfer issue was to build a single relational database that contains all the business’ client data. It will also be where the data for the classes they host will be held.

The next problem would be to build an interface to interact with this data. Previously, the business was using Excel as a sort of database, piping in data from google forms and using a lot of paper records for class data, which would be manually entered onto their website for advertising. One major feature to keep in mind is that the client wanted to be able to access this interface from anywhere and any device. They also needed a way to easily email each of the clients when they join a class.
My solution was to build a web dashboard that would act as a Customer Relationship Management platform. This web dashboard would give the client access from any device (with an internet connection) and can be securely accessed by implementing an authentication and authorization service. This dashboard would need tools to automate emails, manage existing users, and upload data about new classes.

Lastly, the client would need a way to advertise new classes that they are hosting, and give their customers a place to register for those classes. This would mean a new website. Since all of their data will now be in a database, we want to be able to access that data from the website. Their existing website was built using a drag-and-drop website builder, and would require some funky workarounds to access the data in the database.
We decided that a fully custom website was the best way to go here. This gave us the opportunity to build a base of a web interface that could be built upon as the business scales. It would also allow us to sync the dashboard and website. This allowed us to build some Content Management System functionality into the dashboard, allowing the client to have a single location to update their website and manage their customer data.

After going through the process to discover exactly what the ideal management platform would look like for K9DetectionSports, I built out a system to automate as many processes as possible. We were able to work closely together throughout the development process and iterate as we went. Because of this iterative approach, we were able to come up with great new ideas for automating different aspects of the business workflow.

As a result of building this system, we were able to increase administration efficiency by over 300%. Now, maintaining and updating the business only takes a couple hours for each session. We were even able to save the business over $300 per year by consolidating all of their website resources into one custom server.

### Objective

- Build a custom CMS system to manage the public facing class registration website.
- Build a custom CRM dashboard to manage students and classes.
- Automate introduction emails when a user is admitted into a class and facilitate group emails on a class-by-class basis.

### Technical Specs

The entire project was custom coded and is currently running on a Linux Server.

- Node.js
- JavaScript
- REST API
- HTML5 + CSS3
- PostgreSQL
- Ubuntu Server
- Nginx

![user-registration.png](/images/casestudies/k9detectionsports/user-registration.png)

Screenshot ********************************of the class registration page for user’s to see the available classes********************************

![class-manager.png](/images/casestudies/k9detectionsports/class-manager.png)

*Screenshot of the class manager page where the trainer would manage a class*

### Project Outcome

This web app is still in place today, and has been for nearly 6 years now. After implementing the system, administration efficiency improved by over 300%.

Previously they were using systems mashed together using Google forms, spreadsheets, paper receipts and manual emailing.
