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

