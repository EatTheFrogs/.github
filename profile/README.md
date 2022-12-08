# Eat The Frog ([EatTheFrog.app](https://eatthefrog.app))

#### "If it's your job to eat a frog, it's best to do it first thing in the morning... And If it's your job to eat two frogs, it's best to eat the biggest one first." - Mark Twain

## “Eat The Frog” Meaning
'Eat the frog' is a philosophy centered around achieving one's goals in an efficient manner. To eat the frog is to take a task that you know should be completed and simply get it done, without procrastination, no matter how difficult or unpleasant the task may be. The term originated from the Mark Twain quote shown above and was further popularized by Brian Tracy's book *Eat That Frog!* which expands upon the wisdom taken from Twain's proverb.

## Functionality
Simply put, EatTheFrog.app was built with the intention of helping users eat their frogs and effectively achieve their goals. The app allows users to enter goals of any type and log progress events whenever they make any leaps. It offers specialized event templates to make the process of logging completed events smooth and easy. Checkout the Home page of the website using the link at the top of the README for more details!

## Tech Specs

### Frontend
The frontend is contained in the [EatTheFrog.app repo](https://github.com/EatTheFrogs/EatTheFrog.app). It is a single-page application built using component-based ReactJS and is secured with Okta OIDC. It is hosted using static build files behind an NGINX proxy server on an Ubuntu VPS.

### Backend
The backend is composed of 6 Java Spring Boot microservice applications. It mainly consists of REST APIs and uses MongoDB for persistence and RabbitMQ for asynchronous messaging. The services include:
- [APIGateway](https://github.com/EatTheFrogs/APIGateway): Routes external request to appropriate microservice
- [UserProvisioningService](https://github.com/EatTheFrogs/UserProvisioningService): Listens for Okta user updates with event hooks and drops update message on a queue
- [UserService](https://github.com/EatTheFrogs/UserService): Proxy to User database. Listens to queue for new user messages and creates / deletes users
- [GoalService](https://github.com/EatTheFrogs/GoalService): Proxy to Goal database
- [EventService](https://github.com/EatTheFrogs/EventService): Proxy to Event database
- [EventTemplateService](https://github.com/EatTheFrogs/EventTemplateService): Proxy to EventTemplate database

### CI/CD
This project is equipped with a lightweight CI/CD pipeline powered by Jenkins. The Jenkins server uses GitHub event hooks to automate builds and deploy actions as defined in the Jenkinsfile within each repo. The backend services are deployed using Docker containers and docker-compose. Originally the plan was to use Kubernetes for deployments... This plan was foiled when I learned that my VPS isn’t capable of running K8s due to OpenVZ --- only found this out after spending a week setting up a working Kubernetes system on my local.


## Takeaways
Coming from a professional background of strictly backend engineering and only having limited experience with frontend technologies, this project served as an excellent head-to-toe dive into full stack development. I was aware I had some “blindspots” as to what goes into keeping a platform fully and efficiently functioning (outside of the backend) so this was fun to finally dedicate the time to build out a full platform and get to be hands-on at all levels. 
