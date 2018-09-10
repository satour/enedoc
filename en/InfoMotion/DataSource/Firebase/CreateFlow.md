---
lastUpdated: 2018-08-09
---

###Create Flow 

Now with firebase ready lets create a flow to push data. 
In an enebular project go to flows and click on the add button at the bottom right side of the screen. 

![CreateFlow-flowList](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-flowList.png)


Enter a name and decription then click continue. 

![CreateFlow-createFlow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-createFlow.png)


Click on `Edit Flow` to open the flow editor. 

![CreateFlow-editFlow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-editFlow.png)


(If firebase is not installed please install `node-red-contrib-firebase`.)

Create the following flow. 
inject -> function -> firebase modify -> debug 
![CreateFlow-flow](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-flow.png)


Double click the inject node and set the interval to 10 seconds. 
Click done when finished. 

![CreateFlow-injectNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-injectNode.png)


Double click the function node and set the function as below. 

![CreateFlow-functionNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-functionNode.png)


```javascript
var data = {
        timestamp: Date.now(),
        value:{
            country:['JP','CN','USA'][Math.floor(Math.random()*3)],
            value: Math.floor(Math.random()*10),
            created:Date.now()
        }
      }
      
msg.payload = data;
return msg;
```

Double click the firebase node and set the inputs as follows. 

Click on the pencil to edit the firebase url and auth type then update. 
Firebase:
	firebase: `YOUR FIREBASE PROJECT ID`
	auth type: `none` 

![CreateFlow-firebaseConfigNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseConfigNode.png)


Child path : `test`
Method : `Push`
value : `msg.payload`
name : (any name you want)

![CreateFlow-firebaseNode](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseNode.png)


Now with all nodes set you can now click deploy. 
Check your debug log tab to see if data is being pushed correctly. 

![CreateFlow-debugLog](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-debugLog.png)


You can also check your firebase project database to see the data being saved.

![CreateFlow-firebaseProjectDatabase-en](./../../../../img/InfoMotion/DataSource/firebase/CreateFlow-firebaseProjectDatabase-en.png)