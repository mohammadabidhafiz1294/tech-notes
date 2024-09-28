[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a09462d-3f5b-43a9-badf-6f5786d8d7aa_1218x646.png)
In order to level up massively and work towards senior software engineering positions, You need to grow beyond “I can build a basic app.”

What we usually mean by that is, I can:

- Write some CRUD APIs
    
- Spin up a database + server
    

Awesome as a junior/mid-level. Won’t cut it for a senior engineer and beyond.

I’ve seen so many awesome engineers struggle during practical data modeling, coding, or white-boarding rounds because they don’t have good experience and understanding in these 6 key areas.

You’ll need to develop expertise and experience in them if you want to grow into senior+ software engineering positions.

## **1. Data Modeling**

Learning how to model data well is an underrated skill in our industry. 

Senior engineers are usually tasked with leading larger new projects that might not be a solved problem, or require new data models and solutions. You’ll be tasked to come up with a data model / architecture that:

- solves your unique problem
    
- fits with your existing systems
    
- can be easily extended
    
- is performant
    

A lot of data modeling is going to be in databases – whether relational, or document-based, so you’ll want to get good at both of these – not just Mongo.

The core of data modeling comes down to **Entities, Attributes, and Relationships.**

Here’s a really helpful summary [from this article](https://medium.com/@seckindinc/data-modeling-fundamentals-dba245b7dc9f) by Seckin Dinc, Head of Data and Product at FreeNow:

**Entity**

An **entity** is a real-world object or concept that can be uniquely identified and described, such as a person, place, thing, event, or concept. An entity is typically represented by a table in a relational database, and each instance of the entity is represented by a row in the table.

**Attribute**

An **attribute** is a characteristic or property of an entity, such as a name, age, address, or color. Attributes are represented by columns in the table that represents the entity.

**Relationship**

A **relationship** is a connection or association between two or more entities. Relationships describe how entities interact or relate to each other, and are represented by lines or connectors between the entities in a data model.

Relationships can be one-to-one, one-to-many, or many-to-many.

This just scratches the surface of data modeling, at some point you’ll want to deep dive into a book on data modeling like:

- [Designing Data Intensive Applications](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321/ref=as_li_ss_tl?dchild=1&keywords=data+modeling&qid=1600368182&s=books&sr=1-8&linkCode=sl1&tag=solutionsre04-20&linkId=3900919f0391be393a0445fbaf9bd559&language=en_US)
    
- [The Data Warehouse Toolkit](https://www.amazon.com/Data-Warehouse-Toolkit-Definitive-Dimensional/dp/1118530802/ref=as_li_ss_tl?dchild=1&keywords=data+modeling&qid=1600368182&s=books&sr=1-3&linkCode=sl1&tag=solutionsre04-20&linkId=ec23dad0c8d3a724368434177b545537&language=en_US)
    
- [Learning SQL](https://www.amazon.com/Learning-SQL-Generate-Manipulate-Retrieve/dp/1492057614/ref=asc_df_1492057614/?tag=hyprod-20&linkCode=df0&hvadid=416926729608&hvpos=&hvnetw=g&hvrand=16197514364379769505&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9012333&hvtargid=pla-896777802699&psc=1&tag=&ref=&adgrpid=94182731736&hvpone=&hvptwo=&hvadid=416926729608&hvpos=&hvnetw=g&hvrand=16197514364379769505&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9012333&hvtargid=pla-896777802699)

## **2. Events, Message Queues, and Workers**

A lot of companies today are building / working in distributed systems that process work in real-time (APIs), but also asynchronously (queues + workers).

An asynchronous or event driven system is really a different mental model to become familiar and confident in, so it’s worth spending time learning it.

One of the key pieces of an asynchronous system is message queues. Message queues are really useful when working with micro services. You can use them to:

- Rate limit processing of events
    
- Communicate between micro services
    
- Shard the load of specific types of events to be processed at different rates
    
- Batch process a bunch of events
    

Here’s an example:

Let’s say your app needs to send out an email campaign to millions of customers. Rather than spinning up one mega server to handle and send out all the emails.

- throw those emails on a queue
    
- have worker pods scale and pick them up
    
- send out the emails asynchronously
    

Message queues can also be used for interservice communication.

If an action / event:

- Doesn’t need instant feedback
    
- Spans several domains
    
- Is used by multiple consumers
    

It’s a great candidate for events + message queues.

eg. customer orders, uses coupon, needs receipt email

## **3. Autoscaling infrastructure**

Autoscaling… ahh… the fancy buzzword that we all like to throw around.

But really, it’s super important when you are working on systems that have spiky load, or need to scale without human resources.

For monoliths, learn how to setup autoscaling ec2 instances. When traffic/usage gets over a certain threshold, you can spin up multiple servers to handle your traffic.

For micro services you can implement horizontal pod autoscaling in kubernetes. 

Whenever the cpu, or memory usage spikes for a K8s pod, you can spin up a new batch of “pods” to handle the load.

This works for both API pods and “worker” pods. Combined with point 2 above, worker pods can really help you crush through a ton of asynchronous load requests.

For databases use something like Amazon Aurora which will spins up new replicas based on increased load, and spin them down when the heavy load is processed.

## **4. Cloud technologies**

I know DHH had a rant post last month where he talked about moving away from the cloud… but seriously, most modern companies run their apps/servers in the cloud and gaining huge advantages from it.

You can’t really avoid learning about AWS / Azure / Google Cloud.

And one thing I’ve been hearing from companies is that certifications can be helpful yes – but you also need to have real-world experience beyond just your certification.

They want someone who can work with cloud systems, and use cloud tools to solve business scaling problems.

Here is a list of the most popular AWS tools I’ve used over the last 5 yrs:

- SNS, SQS = event-driven architecture / message queues 
    
- S3 = unlimited storage/scale for static pages, images, assets 
    
- RDS = cloud databases 
    
- K8s =  for micro services running in containers
    
- EC2 = for monoliths running on servers
    
- Kafka, Kinesis = event streaming
    

There are 100s more services / tools that the various cloud providers offer, but that should get you started with some of the commonly used ones.

## **5. Caching**

When your system reaches more scale and has moments of sporadic traffic, one tool that works really nicely is caching.

Caching allows your systems to handle more load, and respond quicker to your users’ requests without scaling up your servers.

Here’s something I’ve seen – we all know about caching, and we all talk about it, but we may not have much real-world experience with it.

So many times in technical interviews when I’ve asked about caching, an engineer will say “oh, I’d probably just throw Redis at it”… or “We should add a cache there.”

But when I ask more questions, it’s clear they don’t understand the fundamentals of where / when to apply caching, or have experience doing it in systems of scale.

One of the ways you can learn about implementing caching and what types of problems / scenarios it’s useful for is by reading engineering blogs, and systems design books.

Here is a quick overview of the various types of caching you could implement in your app:

- **Site cache** – serves content quickly to return website visitors
    
- **Application/Output caching** – server level HTML caching
    
- **Distributed Data caching** – redis, memcached, GemFire, Ehcache
    
- **File caching** – CDN for static files, images, multimedia
    

## 6. Concurrency / Idempotency

For me this has been one of the hardest problems to solve in computer science – concurrency and idempotency in distributed systems.

The last 3 yrs I’ve worked in a distributed systems of microservices, queues, workers, autoscaling, and events-driven system of eventually consistency. In that environment, all this became much more important and much more complex.

Let’s walk through an example to wrap our heads around what this might look like. Let’s say that a guest wants to place a restaurant order on a website:

- They fill out the form and then click submit
    
- Nothing happens, no loader, no success message…
    
- They click it again after 30 seconds… and again…
    
- Finally, they refresh the page and try it again
    
- Yay it finally worked
    

Here’s what happened in the background:

- The first request went through – the UI just had a bug where the button was never disabled during the request, and no success message was shown
    
- requests 2 and 3 went through as well
    
- after page reload, request 4 also went through with all the same form details
    

The guest goes to their email and sees orders for 4 meals 😩 This sucks from a guest experience perspective – especially since we were processing payment for the order.

This problem is only compounded with concurrency in distrubuted systems – where you have a bunch of parallel processes happening at the same time.

One way to solve this issue is with creating idempotency in your systems.

> Quick def on idempotency if you aren’t super familiar: 
> 
> The ability to execute the same operation multiple times without changing the result beyond the initial application.

In our case having an idempotent system would allow a guest to submit the same order multiple times ensuring that only one is made.

One way to implement this would be sending in an idempotency key via the api requests to make the order.

That idempotency key could would be a hashed key of the forms data.

- That hash of form data ensures that even across page reloads, no duplicate orders are created
    
- We’d take that key and save it in the orders db table, with a unique constraint
    
- Future requests to make the same order with the same email/phone are rejected, or provide an alert to the guest to confirm if they want the duplicate order

Problem solved 😅

Here are a few helpful deep-dive articles on idempotency if you want to keep reading up on how other companies have implemented it in their systems:

- [https://stripe.com/blog/idempotency](https://stripe.com/blog/idempotency)
    
- [https://brandur.org/idempotency-keys](https://brandur.org/idempotency-keys)