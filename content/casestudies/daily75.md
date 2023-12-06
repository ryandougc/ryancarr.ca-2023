# Daily 75 Case Study

## Project Description

A daily email newsletter that guides you through the Blind 75 algorithms

What are the Blind 75 algorithms? It’s is a set of 75 algorithms that are common to find in software engineering technical interviews. 

After signing up for the newsletter, each morning you receive an email at 7am with the daily algorithm from the Blind 75 set. The algorithms start in order from easiest to most difficult, and come in an order that takes advantage of spaced repetition for the best learning outcome as possible. 

At 7pm each evening, you receive an email with the solution to the days algorithm.

<aside>
📌 **Read the blog!**

The Daily 75 blog is a written guide on how to think about each of the blind 75 algorithms in order to come up with the solution.

[Daily 75 Blog](https://www.notion.so/Daily-75-Blog-521064067ce64736ba47440890d128f7?pvs=21)

</aside>

## Skills Used

- Node.js Express RESTful API written in TypeScript
- NoSQL Database (MongoDB)
- Web Scraping (puppeteer and cheerio)
- External API Consumption (SendGrid email marketing)

<aside>
<img src="https://cdn-icons-png.flaticon.com/512/5968/5968292.png" alt="https://cdn-icons-png.flaticon.com/512/5968/5968292.png" width="40px" /> **JavaScript**

</aside>

<aside>
<img src="https://cdn-icons-png.flaticon.com/512/919/919825.png" alt="https://cdn-icons-png.flaticon.com/512/919/919825.png" width="40px" /> **Node.js**

</aside>

<aside>
<img src="https://cdn.icon-icons.com/icons2/2699/PNG/512/expressjs_logo_icon_169185.png" alt="https://cdn.icon-icons.com/icons2/2699/PNG/512/expressjs_logo_icon_169185.png" width="40px" /> **Express**

</aside>

<aside>
<img src="https://www.opc-router.com/wp-content/uploads/2020/04/icon_rest_webservice_600x400px.png" alt="https://www.opc-router.com/wp-content/uploads/2020/04/icon_rest_webservice_600x400px.png" width="40px" /> **REST API**

</aside>

<aside>
<img src="https://cdn.iconscout.com/icon/free/png-256/free-typescript-1174965.png?f=webp" alt="https://cdn.iconscout.com/icon/free/png-256/free-typescript-1174965.png?f=webp" width="40px" /> **TypeScript**

</aside>

<aside>
<img src="https://icons.iconarchive.com/icons/cornmanthe3rd/plex/256/Other-html-5-icon.png" alt="https://icons.iconarchive.com/icons/cornmanthe3rd/plex/256/Other-html-5-icon.png" width="40px" /> **HTML5 & CSS3**

</aside>

<aside>
<img src="https://static-00.iconduck.com/assets.00/mongodb-icon-2048x2048-cezvpn3f.png" alt="https://static-00.iconduck.com/assets.00/mongodb-icon-2048x2048-cezvpn3f.png" width="40px" /> **MongoDB**

</aside>

## What I Learned From This Project

### **SOA VS OOP**

This project was my second project using Service Oriented Architecture (SOA). It was insightful as I really started to find the places where SOA excels and where Object Oriented Programming (OOP) comes into play. 

What I found was that SOA is great for interacting with APIs and outside sources. Bringing in data to my application and sending data out for certain use-cases was quick, easy and made perfect sense for how to use this.

I eventually ran into a problem where I created a service that would iterate over files in a local directory, push their names into a dictionary, and retrieve the file contents by referring to the dictionary. I realized that this service was executing each time I called it and iterating over the files each time I used it. I didn’t want to have to iterate over all 75 files each time I used the service.

The easiest solution for me to implement was using OOP to create a class for the local file dictionary and add methods onto it for retrieving specific files. This means the program iterates through the files only once, compiling a dictionary of the files. Now we can easily call methods to retrieve only 1 file at a time.

## Project Outcomes

This project is currently in the beta testing phase. I am going through the algorithms myself, compiling all of the most efficient solutions, writing blog posts explaining each algorithm, and taking notes on any improvements I would like to make. Since these algorithms are protected under copyrights from Leetcode I will not be able to really make this a mainstream application, but I am finding its a very useful tool so far that could really help some people. I will need to do some research on copyright laws to see if there’s a way to allow people to use this tool for their own education. Worst case scenario I will need to write my own algorithms for people to solve.