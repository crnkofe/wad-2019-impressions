# WeAreDevelopers'19 impressions

## Day 1 Talks

### Rapid Prototyping - how to start a successful IoT project (Robert Jänisch)

- there are still not enough good business cases for IOT adoption
- I recall the infamous exponential growth IOT curve being shown however I have my doubts thats how this is going to play out
- likely candidates for next mass IOT adoption are industry and business
- start with UX first (user stories) - after all, user interface is everything user sees

### Monitor your data like if it was your code (Tom Baeyens)

This talk emphasized data monitoring in the context of machine learning. ML algorithms in practice are the minority of the total stack.
ML still needs the entire provisioning/monitoring backend similar to how ordinary application code supporting stack is structured today.
Some tasks off the top of my head that are important:
- GDPR and data anonymization
- data cleaning (most data engineers spend majority of their time cleaning data)
- drift (detecting drift, rebuilding data models)
- errors (errors in ML predictions due to data changes, missing data, etc.)

Other notices:
- data does not throw exceptions - it just gets corrupted - or in short GIGO - garbage in garbage out
- iirc this article was mentioned from Mr. Fowler https://martinfowler.com/articles/break-monolith-into-microservices.html
- for ML https://blog.acolyer.org/ was mentioned as a good resource
- SodaData is going to open source Soda which is a tool for monitoring data https://events.wearedevelopers.com/world-congress/program/

### 1.2 or 1,2? -- The Challenges of Becoming a Data-Driven Company (Manuel Eugster)

*Data Democratization* is the idea that access should just be given to anyone who wants to deal with it regardless of experience.
This idea was a bit foreign to me as ML is such a complicated topic but there are many tools today that help deal with various
	intricacies of data (drift, anonymization, conversions, etc.). Anyone includes the customer so they can check their own data.

TODO: Read Creating a Data-Driven Organization by Carl Anderson

Important steps during transformation to data-driven company:
- set golden rules/book of data formatting (commas versus dots)
- decouple domains so they are easier to understand and manage
- send everyone to business analytics class on Harward so they could speak the same language
- ICE scoring for prioritizing business goals
- meetings should be centered around data rather than around opinions - no data no meetings
- product owner is responsible for data lake

### Modern React: Things You Didn't Know Where Possible (Roy Derks)

This was a nice coding talk demoing latest React features:
- React has lately gotten fancy lazy loading
- use fragments to return multiple results (previously it was done by composing multiple results)
- use state with hooks to avoid writing as much boilerplate as before (sample was for increment)
- context can be exposed through hooks (effectively making a global state context)
- TODO: Read about Redux pattern

### How to architect your application infrastructure for effective API delivery (Kevin Jones)

This talk was about some basics of how to architect and combine reverse-proxies together with API's.
Three architectures were presented(with an overly heavy emphasis on nginx but I find nginx cool):
- edge gateway 
	- have a single reverse-proxy gateway or similar between external clients and your services
	- services connect to each other directly
	- edge gateway handles auth, load balancing etc.
	- the problem is that services still handle gateway provided functionalities internally
- two tier gateway (not sure if this is the right name)
	- have an external reverse-proxy gateway and a common internal gateway
	- all internal services use the internal proxy (which may eventually become the bottleneck)
	- internal gateway in this case can take less responsibility since it operates inside internal network
- microgateway
	- this is a two-tier arch where the main gateway handles some responsibilities
	- internally services are grouped and each group has a gateway
	- services inside internal gateway still communicate directly
- sidecar gateway
	- if I understood this correctly each service comes packaged with a micro-gateway
	- gateways are managed by service teams
	- this is standard practice according to the speaker today
	- I imagine one way of doing this is with a nicely crafted Docker

Service mesh was briefly mentioned as an attempt to modernize these architectures for micro-service but the differentiation is not there yet.

### Ephemeral onions (Silvia Puglisi)

This talk was about the Tor project and how to use what it provides. Essentialy tor is a network of trust where connections are encrypted.
Tor is a P2P protocol and some interesting ideas for development were showcased/mentioned by speaker:
- services can be deployed on the network and ran as p2p with no central service host
- identity provider could be easily setup
- temporary file sharing was showcased
- check https://github.com/hiromipaw for samples

Somehow tor reminds me of blockchain but the tech details are completely different.

### Serverless security: defence against the dark arts (Yan Cui)

This was a really cool talk. Some takeaways:
- OWASP top 10 vulnerabilities are not really changing that much over the years (we're still commiting the same security bs as we did)
- the weakest link in the chain is where the hackers will strike
- nodejs was roasted for its lack of security handling 
	- as a demo the speaker showed how he used a transitive dependency to send AWS credentials to his home address
- platforms are being targeted as attackers - best defense today is (beside upgrading to nodejs 5.x+) to use dependency checkers
- on Cloud make sure to use server side encryption which is standard today
- Denial of Wallet sounded like a catchphrase at first but
	- with serverless you pay for what you use - which means a prolonged ddos due to autoscaling can soon become very very costly (think 1000xN lambdas)
- options to defend agains DoW is to use throttling per IP and avoid unnecessary timeouts
	- with timeouts its possible to start a lot of services in a very short time
- a good preventive measure is to put alerts on unused regions to prevent machines suddenly popping up where there should be none
- apply the least privilege principle - a client should have access to at most what they need (RBAC, IAM on AWS)

## Day 2 Talks

### Developing augmented reality apps: going beyond ARCore and ARKit (Andreas Schacherbauer)

I'm pretty new to AR. Two things stuck beside the epic Terminator reference:
- augmented reality should make use of context - if aug. reality app doesn't take into account its surroundings then what's the point
- there's a lot of blind spots in the frameworks (iirc motion blur and similar functionality that people notice is not yet provided by existing frameworks)

### ModelOps - Lifecycle Management for Reliable and Trusted AI (Waldemar Hummer)

ModelOps is an extension of ML into Operations. I find it interesting how DevOps is now becoming the new black. I've header 
DevSecOps at I think last year's WAD. But combining all of that knowledge we devs might as well aspire to be superhuman.

Takeaways:
- 75% of ML models never reach production
- ML code is just the tip of the iceberg - a new term was mentioned - hidden tech debt 
- TODO: read https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems
- lots of tools for making AI modelling easier were shown, which in turn is paving the way for AI democratization
- use YAML to define your ML pipeline, rather than do everything by hand
- only trust your AI model if it is trackable, controllable and monitorable

### Your tech skills are not enough (Karla Schönicke)

This talk was about how we devs need to put some more work into soft skills. 

Some takeaways:
- new fancy acronym to scare people with [VUCA](https://en.wikipedia.org/wiki/Volatility,_uncertainty,_complexity_and_ambiguity)
- focus should be on value delivery (no point in hitting a deadline with no value being delivered)
- [bus factor](https://en.wikipedia.org/wiki/Bus_factor)
- it's important to spend around 2 hours per week giving constructive feedback(compliments as well as critiques)
	- people feel more appreciated with someone actually spending time with thinking about how to help them
- sprint retrospective is about team growth - seems obvious but from my experience that rarely happens
- having team buildings is important for morale
- 3 key things to takeaway
	- provide feedback (check [FBI](https://developerhood.com/blog/feeling-behaviour-impact-fbi-feedback-formula/) ) 
	- be open-minded about things
	- learn regularly (maybe even write a tech blog about learning)

### Audi's journey to an hybrid enterprise big data platform (Matthias Graunitz)

For some reason I don't recall much about this talk:
- notably a plus for using a cloud was that data was collected closer to the customer
- they used Kerberos and LDAP extensively and I need to check both of them out
- also Terraform was mentioned as provisioning tool

### Robofacturing - About the human role in the future of robotic manufacturing (Giuseppe Montano)

This was a really cool talk from a speaker that works on rovers that will be sent to nearby planets.

Takeaways:
- the biggest UX issues is how to provide good feedback given the ever increasing autonomy of machines
- two scales for autonomy were shown (SAE and human factors)
- theres a difference between autonomy and authority
	- each AI scale at some point takes away authority from the human and that is where the Frankenstein leaves the lab
- cognitive mismatch was mentioned which seems to be similar to semantic gap in IT but from a design standpoint
	- difference between what operator thinks is going on and what is actually happening
- there are 3 sources of risk:
	- misunderstanding the interface
	- incomplete information
	- similar alternatives
- *framing effect* - given two alternative options take the least risky
- *robofactoring* was defined by the speaker as software defined manufacturing

### Same, same but different - Upscaling the Open Source startup (Jutta Horstmann)

Some takeaways:
- culture always wins - having agile or bureaucracy might be cool but in the end it will be trumped by culture
- speakers company practices speed dating - matching random people from the company that haven't met yet
- the company was remote from the start with all pluses and minuses that brings
- servant leadership was mentioned which is what basically enables empowered teams
- when the company was growing benevolent dictator style started to become problematic

### Riding the Storm: Scaling the early Team (Andre Vella)

Similar to the previous talk the speaker was afraid of loosing the traits of a small company during growth and
made an effort to keep the special culture the had even when growing up.

They wanted to keep:
- ownership and accountability
- good communication
- fast pace (move fast and break things)

Some takeaways:
- conway was mentioned. Software built reflects company communication.
- teams built were crossfunctional (product owner, analytics, devs, business person)
- Tuckmann theory was shown as a reference on how teams grow
- interesting page was mentioned on how to do and not do devops https://web.devopstopologies.com/
- TODO: check Management 3.0
- use Voight-Kampf test for selection of engineering managers
- create a culture manifesto as a common doc
- set clear expectations and responsibilities
- TODO: reread 5 dysfunctions of a team

### Coding for Humanoid Robots

This talk highlighted what today a robot(think Pepper) needs to be able to do in order for it to be useful:
- since robots are pretty new it needs to be able to explain what it does to the user
- the robot has a tablet mounted on it - avoid using the tablet to input data, use voice chat which is essentially the natural way to interact with it
- when a crowd is before the user there needs to be some criteria in place with who it is talking\
- when fetching data from the cloud for exampe the robot needs to do something like huming or waving hands
	- otherwise it looks really awkward
- the robot needs to deliver some value at the end (use closed questions for guiding the user)
- always test with people who've never seen the robot before
- note that people will challenge the robot - just another thing to keep in mind
- provide nice fallbacks in case the robot does not understand the user

The robot is pretty expensive but an enterprise could afford it. Inside it is basically an Android with a 
nice looking SDK. It is responsive and can deliver some result within 200ms and behaves similar to an actual Android app.

### Other talks

Day 2 ended with a really cool talk on the future of AI. I really like the phrase "design is hope made real".
Ripple CTO came and made a stand on how InterLedger will revolutionize international payments. It sounds like a really cool tech.
I'm not that convinced about that revolution though. Interledger is a kind of a base for communication in Internet of Value where
packets also contain value rather than just data.

TODO: Tableaux was mentioned several times. Yet another tech I need to check. It would be really nice for some people to have a nice page,
where you just type some python code and data is magically concatenated, processed, modelled etc.


