# KiteXProjectOverview
General KiteX Project description


#Learnings

## Video Tracking - Open CV, GPUImage
Initially I tried to install and run Open CV on my iPhone. After trying for hours I began seeking other options. I found a post/article by the creator of GPUImage showing GPU accelerated image/color tracking - and though it was perfect. I initially implemented the current solution with the original GPUImage, but later realized that a swift version GPUImage2 had been made.
The API had changed slightly so I ended up rewriting most of it, with the logic mostly staying the same. GPUImage2 is really easy to work with and very powerful! Great job. 

## HTTP vs Websocket
I always start out with the simplest solution that I expect to work. 
In order to control the stepper motor I would send HTTP requests from my iPhone directly to the ESP8266, that which were acting as a accespoint.
However when getting close to 10-20 request per seconds the ESP would eventually crash. Further the latency were typical around 100 ms.
Eventually I decided to change to using websocket. It were suprisingly simple to setup and it has a incredible performance.
I were able to achive a roundtrip latency of around 5 ms and it's rock stable. 


## WebsocketServer on Laptop or the ESP
Initially I tried to run the WebSocketServer on the ESP, but I ended up moving the server to the MacBook. 
This means I don't have to worry about the WebSocketServer performance. You can do faster iterations and easier debugging.
The server could be written in a high level programming language.
Since all data passes through my laptop it's easy to log it to a file and should be easy to implement the auto guidence system.
It seems like the MB Air has better wifi performance as a router than the ESP8266, meaning longer range for other systems.
Ofcause it adds and extra step between the camera and motor controller, but it seems to be worth it.

