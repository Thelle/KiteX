# KiteXProjectOverview
## Why are Kite mills interesting?
Traditional wind mills is often the preferred solutions when creating new power plants due low price per watt and environmental impact. Using kites as a mean of capturing wind energy has potential to significantly reduce the cost of energy.

The energy that you can extract from the wind is largely related with the swept area of the wind turbine. With a kite it would be possible to sweep a given area with a much smaller system than a traditional wind turbine. A tether to the ground can replace most of the supports structure, the inner parts of the wings, the tower and the foundations. Makani estimates that their kite system can deliver approximately 10 times the energy per weight of a traditional wind turbine.

Two further advantages of the kite system is that they can more easily capture the wind at a higher altitude where winds are more consistent, delivering their rated output a higher degree of the time, which is an important advantage when a large portion of the locally generated energy is from unreliable sources. Since the bending moment on the foundation of a kite mill is small to non-existent it will be much easier to setup these kite system in offshore conditions.

From a technical perspective it would have been possible to make such a kite ever since the invention of the computer, but right now we are getting to a point in time where both advanced enough materials and computer technology is readily available (cheap enough).

## What is the purpose of KiteX
I would like to promote the development of kite technology in order to create a future where energy is cheaper and renewable. I think cheaper would help the natural progression towards a society where people are freed from duty of work and can pursue more interesting exercises. I find the reflections in these answers quite interesting: https://www.quora.com/If-energy-was-free-and-renewable-how-would-the-economy-be-fundamentally-different-from-what-it-is-now

For now KiteX will be a project and company with the goal of creating these wind mills of the future. We will make sure to share all learnings we can that would not compromise the future of the company.


## Who are We?

### Andreas Bruun Okholm
I have a mixed design, mechanical and aerospace degree from the Technical University of Denmark. While and after my degree I started a project to create a smartphone based wind measuring tool, which was intended to be a better wind meter, but also allow kite-surfers to share wind information. I worked on this project for 3 years varying between hardware and software development. We managed to create the most sold smartphone wind meter and the first one to measure wind direction in the world. It's with these competences I venture into the Kite energy arena, a reasonable understanding of mechanics, aerodynamics, programming and how startups work. The fact that I have always loved kites and been kitesurfing for the past 10+ years has nothing to do with my excitement for this new technology.

### Want to join?
Do you share the same vision for a the kite future? contact us! :)

# What are the steps?
Given my background the most obvious route towards a kite mill is to (always go for the most difficult problems first, yet achievable)
1. Create an autonomous flying kite (DONE)
2. Create a tethered drone that can take off and land autonomously
3. Combine 1 and 2 into a completely autonomous kite
4. Add energy generation
5. Make it big



# Step 1 - Autonomously flying kite
On September the 13th, 2016 I managed to carry out a the first successful autonomous flight (and record it at the same time. Check it out at: https://youtu.be/O_YaRTxpii8.

### Autonomous Kite 002
Overall the system consists of a kite, a motorized kite steering system, a laptop for control and a smartphone for video tracking.
![Image of AK002 Setup](http://aokholm.github.io/KiteX/images/AK002Setup.jpg)

![Image of the AK002 dataflow](http://aokholm.github.io/KiteX/img/AK002DataFlow.jpg)







##Learnings
Apologies, but these are somewhat random and unorganized at least for now.

### Video Tracking - Open CV, GPUImage
Initially I tried to install and run Open CV on my iPhone. After trying for hours I began seeking other options. I found a post/article by the creator of GPUImage showing GPU accelerated image/color tracking - and though it was perfect. I initially implemented the current solution with the original GPUImage, but later realized that a swift version GPUImage2 had been made.
The API had changed slightly so I ended up rewriting most of it, with the logic mostly staying the same. GPUImage2 is really easy to work with and very powerful! Great job.

### HTTP vs Websocket
I always start out with the simplest solution that I expect to work.
In order to control the stepper motor I would send HTTP requests from my iPhone directly to the ESP8266, that which were acting as a accespoint.
However when getting close to 10-20 request per seconds the ESP would eventually crash. Further the latency were typical around 100 ms.
Eventually I decided to change to using websocket. It were suprisingly simple to setup and it has a incredible performance.
I were able to achive a roundtrip latency of around 5 ms and it's rock stable.


### WebsocketServer on Laptop or the ESP
Initially I tried to run the WebSocketServer on the ESP, but I ended up moving the server to the MacBook.
This means I don't have to worry about the WebSocketServer performance. You can do faster iterations and easier debugging.
The server could be written in a high level programming language.
Since all data passes through my laptop it's easy to log it to a file and should be easy to implement the auto guidence system.
It seems like the MB Air has better wifi performance as a router than the ESP8266, meaning longer range for other systems.
Ofcause it adds and extra step between the camera and motor controller, but it seems to be worth it.

### Artificial Intilligence - Python vs Node
Being a newbie to the field of Machine learnign I can highly recommend these two series on machinelearnig:
- Machine Learning Course - CS 156 by Caltech: https://www.youtube.com/watch?v=mbyG85GZ0PI&list=PLD63A284B7615313A,
- Networks Demystified by Welch Labs: https://www.youtube.com/watch?v=bxe2T-V8XRs&list=PLK1aXp7PZ2tMrm1h_JDBcJDhIpbQZPOr1

I used at least a day trying to figure out how to run any deep neural network code in python and never actually managed to run anything if I also wanted to be able to directly plot the results with Matplotlib. I think I tried: scikit-learn, PyBrain and scikit-neuralnetwork in all combinations with System (Python 2.7 installation), PyEnv (3.4, 3.5) and Anaconda. And in every instance there were something wrong. Just wanting to get something running I ended up using Synaptic:  http://synaptic.juancazala.com/, which can be run on Node or in your browser - plotting solved! And it worked out of the box! ah. It's sad that Python version and package management can be such a pain.


## Cool Articles about Airborne wind energy
* M.L. LOYD.  "Crosswind kite power (for large-scale wind power production)" Journal of Energy, Vol. 4, No. 3 (1980), pp. 106-111.
http://edge.rit.edu/content/R15901/public/Matt%20Kennedy/homes.esat.kuleuven.be_~highwind_wp-content_uploads_2011_07_Loyd1980.pdf
*
