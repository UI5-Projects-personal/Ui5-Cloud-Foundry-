# Ui5-Cloud-Foundry-
Cloud foundry learning UI5 Deployment

# UI5 App Router local testing & deployment:

## 1) Types of App routers
    A) Managed App router
    B) Standalone App router
 
 ## Managed App router
 1)It is configured as a part of CAP project. No special configuration is needed
 cds watch would run the managed app router
 2)To test an application with a destination locally just change the URL at the correponding object and run the app.

## Standalone App router
1) It is not configured as a part of CAP Project. 
2) It is an npm application.
3) Create a folder with the name App router.
4) Add package.json. 

{
    "name": "approuter",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "devDependencies": {},
    "engines": {
        "node": "^12.0.0"
    },
    "scripts": {
        "start": "node node_modules/@sap/approuter/approuter.js"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "dependencies": {
        "@sap/approuter": "^8.5.4"
    }
}

5) Add xs-app json with the destinations.
{
    "welcomeFile": "/app/esmanage/index.html",
    "authenticationMethod": "route",
    "sessionTimeout": 30,
    "logout": {
        "logoutEndpoint": "/do/logout",
        "logoutPage": "/"
    },
    "routes": [
        {
            "source": "^/resources/(.*)$",
            "target": "/resources/$1",
            "authenticationType": "none",
            "destination": "ui5"
        },
        {
            "source": "^/test-resources/(.*)$",
            "target": "/test-resources/$1",
            "authenticationType": "none",
            "destination": "ui5"
        },
        {
            "source": "^/app/esmanage/(.*)$",
            "target": "$1",
            "localDir": "../app/esmanage/webapp",    ---- Points to index.html
            "authenticationType": "none"
        }

    ]
}
6) Configure the resources for the destination.


## To Run Locally
1) In the app router folder.
2) Configure default-env.json inside approuter 
{
    "destinations": [
        {
            "name": "ui5",
            "url": "https://sapui5.hana.ondemand.com/"
        }
    ]
}
2) npm run start.
3) This will start the approuter server with the application configured.


