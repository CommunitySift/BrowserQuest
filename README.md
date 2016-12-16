# How to use BrowserQuest to test a Community Sift implementation

## Introduction 
To show you how to integrate Community Sift with your existing social game, we created this fork of [BrowserQuest](https://github.com/mozilla/BrowserQuest), the experimental HTML5/JavaScript multiplayer game created by Little Workshop. 

To see a preview of BrowserQuest with the Community Sift filter enabled, go to [browserquest.communitysift.com](http://browserquest.communitysift.com)

## What is Community Sift?
A configurable API service to automatically filter out trolls’ toxic content, such as:

* profanity (things you wouldn’t say to grandma)
* hate speech
* harassment
* grooming
* aggressive language (hostility towards other people, often associated with cyberbullying)
* sexually explicit language (sexual acts, body parts, and other sexual content)

——

# Running BrowserQuest with Community Sift integration
To test your own local instance of Browser Quest that includes a Community Sift integration, do the following:

## Install Node.js
* Visit Nodejs.org: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
* Install LTS version

## Install Required Modules
* Open a terminal to the folder where you checked out BrowserQuest.
* Type `npm install`
    *    If the Community Sift node.js module is not available in NPM (e.g. still private), then install it locally first
    *    Check out the node.js module to a separate directory from the BrowserQuest code
    *    [https://github.com/2hat/sdk-node.js](https://github.com/2hat/sdk-node.js)
    *    In the BrowserQuest directory, edit the file `package.json`
    *    Under dependencies, change the value for the `community-sift` key to be `file:<dir>` (where `<dir>` is the directory you install the Community Sift module)
    *    e.g. if you checked out the module to a folder at the same level as the BrowserQuest folder, you can change the value to `file:../CommunitySift`
    *    type `npm install` again to get the rest of the dependencies

## Configure Community Sift

*   Edit `config/default.json`
    *   Edit the keys in the `community_sift` section to match where you will be calling the Community Sift server

## Starting the BrowserQuest server

*   Edit `server/config.json` if desired
*   Open a terminal to the BrowserQuest source
*   type `node server/js/main.js`

## Serving the client files

*   Copy directory “shared” under “client”
    *    i.e. so there is now a “client/shared” directory
*   In client/config, copy config_local.json-dist as config_local.json
*   Edit config_local.json
*   Change the value of “host” key to be “localhost”
    *   This assumes you are running the client on the same machine as your BrowserQuest server.  If it is on a different machine, then use that address and port
*   Copy config_local.json as config_build.json
*   This step is not necessary to run locally, and you would do it a little differently if deploying, but it saves a little pain if only running locally
*   Chrome does not allow a file uri `file:///…` to load resources, so we need to serve `index.html` using a server too (not sure about other browsers, might just be able to load index.html directly):
*   In a console, go to the `source` directory
*   `cd client`
*   `npm install -g http-server` (only needed the first time, after that just go on to next step)
*   `http-server -p <port>` with port being the port you wish to use to serve the files
*   Now you can go to [http://localhost:8080/](http://localhost:8080/) to see the game

——

## About BrowserQuest

### Documentation
Documentation is located in client and server directories.

### BrowserQuest Code License
Code is licensed under MPL 2.0. Content is licensed under CC-BY-SA 3.0. See the LICENSE file for details.

### BrowserQuest Credits

BrowserQuest was created by Little Workshop:
	•	Franck Lecollinet - @whatthefranck
	•	Guillaume Lecollinet - @glecollinet
