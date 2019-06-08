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
