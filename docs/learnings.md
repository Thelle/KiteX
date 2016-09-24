# Learnings

A bit of unorganized learnings leading up to the AK002 prototype.

### Accces Point
Hack your mac to be an access point even without an internet connection to share. I successful followed this [tutorial](http://www.laszlopusztai.net/2016/02/14/creating-a-wi-fi-access-point-on-os-x/) and have been able to make a AP easily every time. Would of cause be nicer it it could be turned on and off from the command line so I could easily do it in a startup script in node

### Video Tracking - Open CV, GPUImage
Initially I tried to install and run Open CV on my iPhone. After trying for hours I began seeking other options. I found a [post/article])http://www.sunsetlakesoftware.com/2010/10/22/gpu-accelerated-video-processing-mac-and-ios) by the creator of GPUImage showing GPU accelerated image/color tracking - and though it was perfect. I initially implemented the current solution with the original [GPUImage](https://github.com/BradLarson/GPUImage), but later realized that a swift version [GPUImage2](https://github.com/BradLarson/GPUImage2) had been made.
The API had changed slightly so I ended up rewriting most of it, with the logic mostly staying the same. GPUImage2 is really easy to work with and very powerful! Great job.

### HTTP vs Websocket
I always start out with the simplest solution that I expect to work. In order to control the stepper motor I would send HTTP requests from my iPhone directly to the ESP8266, which also were functioning as an accesspoint. However when getting close to 10-20 request per seconds the ESP would eventually crash. Further the latency were rather high, typical around 100 ms. Eventually I decided to use a websocket instead. It was surprisingly simple to setup and it has been performing great. I were able to achieve a roundtrip latency of around 5 ms and it's rock stable. Digging a little deeper it seems that it would be benificial to have a UDP datalink for the low latency information compared to a TCP which is the underlying protocol of the websocket. However TCP seems good enough for now.

### WebsocketServer on Laptop or the ESP
Initially I tried to run the WebSocketServer on the ESP, but I ended up moving the server to the MacBook.
This means I don't have to worry about the WebSocketServer performance. You can do faster iterations and easier debugging.
The server could be written in a high level programming language.
Since all data passes through my laptop it's easy to log it to a file and should be easy to implement the auto guidence system.
It seems like the MB Air has better wifi performance as a router than the ESP8266, meaning longer range for other systems.
Of cause it adds and extra step between the camera and motor controller, but it seems to be worth it.

### Artificial Intilligence - Python vs Node
Being a newbie to the field of Machine learning I can highly recommend these two series on machinelearnig:

* Machine Learning Course - CS 156 by Caltech: https://www.youtube.com/watch?v=mbyG85GZ0PI&list=PLD63A284B7615313A,
* Networks Demystified by Welch Labs: https://www.youtube.com/watch?v=bxe2T-V8XRs&list=PLK1aXp7PZ2tMrm1h_JDBcJDhIpbQZPOr1

I used at least a day trying to figure out how to run any deep neural network code in python and never actually managed to run anything if I also wanted to be able to directly plot the results with Matplotlib. I think I tried: scikit-learn, PyBrain and scikit-neuralnetwork in all combinations with System (Python 2.7 installation), PyEnv (3.4, 3.5) and Anaconda. And in every instance there were something wrong. Just wanting to get something running I ended up using Synaptic:  http://synaptic.juancazala.com/, which can be run on Node or in your browser - plotting solved! And it worked out of the box! ah. It's sad that Python version and package management can be such a pain.
