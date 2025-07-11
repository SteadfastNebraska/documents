![](assets/20250711_143634_steadfastlogo.png)

The SteadFast project was created in an attempt to passivly monitor off-school network connection quality to identify student connection issues and simplify federal digital equity reporting requirements. Emphsis is placed on protecting student PII and privacy. The project intentionally avoids using 3rd party services to minimize ongoing expense.

Please note that these repos are a public copy of our internal repos. We will only update this repo when bugs are fixed or new features are added. We do not work in this repo, it is a sanitized copy of our working repos for you to use to create your own version of the tool. Many required data points are hard coded in the source. Things like the IP address ranges of your school network segments must be edited into the source and you will need to deploy your own private copy of the service worker.

The system 'can' collect geo location data when the student approves but does not collect geo location data normally simply because it is not available without user permission. Speed tests are only executed when the device is not connected to a configured school network. Collected data is stored on the local device until the device connects to the private school network, only when connected to a school network is the collected data transported over the network to the API. Collected data is never exposed to the public network to maximize data privacy.

The data can only be coorilated to a specific student by the students school administrators. The Steadfast system does not maintain any student information. The device ID is used to index the collected data. This ID allows the school to identify the device and who it is assigned to.

Steadfast system is designed to collect connection quality indicators when school devices are off the schools network to help identify students that may need help getting a quality connection when not at school. The system is completly closed and does not use any external services. No collected data is presented to a public network. The system consists of a data store, two web applications, a GraphQL API, and a Chrome extension. The web applications and API can reside on the same web server. The web application is split into a speed test service and an administration tool. Only the speed test service needs to be publicly available. The other services should reside behind your schools firewall.

Data Store
We choose MongoDb for the backend data store. No particular reason for this choice other than ease of use for this application. A SQL database can easily replace the document based data store if you prefer working with SQL. The project currently uses MongoDb version 4. The MongoDb server is a standard docker deploy of MongoDB.

Web Servers
GraphQLYoga is used for the API endpoint. The API provides functions to read/write test results and control access. Speed tests are performed against this server as well using image file transfers and web sockets. Edge devices need to pass on all request headers. We offload https at the edge and run all servers http only.

A second web server is used to house the administrative interface. This interface provides functions to add schools and achool admins to the system to control data access. This is the final piece of the system and is currently under development.

Chrome Extension
This is the workhorse of this system. Most of our schools use chromebooks or laptops with chrome browser installed. MDM and Google school accounts making this the best choice for our environment. The extension gets the users email address and specific settings from google/MDM when the user logs into the device/browser. The extension and extension operational settings are configured in the google management tools or your MDM system, default settings and network information are hard coded so you will need to modify the code and build/deploy your own specific version of the extension.

What Now

if you wish to deploy this tool for your school, please refer to the readme within each repo for specific deployment information.
