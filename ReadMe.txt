The purpose of the project is to stream our desktop to web application



For user authentication we are using google auth2
ref: https://developers.google.com/identity/protocols/oauth2/scopes -- the url regularly changed so just search google auth2 scopes
For setup we can add script tag in index.html in public directory as: <script src = "https://apis.google.com/js/api.js"></script>



There are 3 folders in this project

1. Client -- its a frontend of our application
2. api -- its act like backend of our application(but not actual backend)
3. rtmpserver -- it is used to stream video of our desktop


Client:
Packages Required:
	"axios": "^0.20.0", -- used to fetch data from api
	"flv.js": "^1.5.0", -- used to download live stream and play video on our html element
	"lodash": "^4.17.20", -- helper library
	"react": "^16.13.1", -- built in package
	"react-dom": "^16.13.1", -- built in package
	"react-redux": "^7.2.1", -- it is used to provide better communication between react and redux
	"react-router-dom": "^5.2.0", -- it is used to route different pages
	"react-scripts": "3.4.3", -- built in package
	"redux": "^4.0.5", -- it is a state management system
	"redux-form": "^8.3.6", -- it is used to make redux automatically manage our forms
	"redux-thunk": "^2.3.0" -- it is a middleware to make api requests in redux
for clarity on flv: https://www.npmjs.com/package/flv




api:
Packages Required:
	"json-server": "^0.16.2" -- it is used to start api server
For clarity on json-server refer: https://www.npmjs.com/package/json-server
Steps for creating:
 1. Create db.json file where we can store required data of streams
 2. Modify package.json with 
		"start": "json-server -p 3001 -w db.json"  -- It continously watch db.json file for any changes
	unser scripts section
 3. Start the server by npm start 
 4. The api server is started in 3001 port





rtmpserver:

Packages Required:
	"node-media-server": "^2.2.4" -- it is a server to stream the video

for clarity on node media server: https://github.com/illuspas/Node-Media-Server, https://www.npmjs.com/package/node-media-server

Steps:
	1. create index.js file and copy the code
					const NodeMediaServer = require('node-media-server');

					const config = {
					  rtmp: {
						port: 1935,
						chunk_size: 60000,
						gop_cache: true,
						ping: 30,
						ping_timeout: 60
					  },
					  http: {
						port: 8000,
						allow_origin: '*'
					  }
					};

					var nms = new NodeMediaServer(config)
					nms.run();
	2. Modify the package.json file under scripts section
				"start": "node index.js"
	3. start the server with npm start
	4. Server started at 8000 port


Seting OBS:

obs is used to broadcast our video to online
Install the obs to local machine 

Share our stream:
	1. click on any stream in client application
	2. in the url we can see the id of the stream at the end
	3. Open settings in obs
	4. GoTo stream tab
	5. select custom in drop down list
	6. In server or url feild copy this: rtmp://localhost/live
	7. In stream key, enter the id we got in step 2
	8. click on apply and ok
	9. click on start stream
	10. now we can see our stream in our application
	

For our project to be run we should start client application, api, rtmpserver









