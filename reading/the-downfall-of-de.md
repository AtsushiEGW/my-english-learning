

# The Rise of the Date Engineer

I joined Facebook in 2011 as a business intelligence engineer. By the time I left in 2013, I was a data engineer.

I wasn’t promoted or assigned to this new role. Instead, Facebook came to realize that the work we were doing transcended classic business intelligence. The role we’d created for ourselves was a new discipline entirely.

My team was at forefront of this transformation. We were developing new skills, new ways of doing things, new tools, and — more often than not — turning our backs to traditional methods.

We were pioneers. We were data engineers!

## Data Engineering?

Data science as a discipline was going through its adolescence of self-affirming and defining itself. At the same time, data engineering was the slightly younger sibling, but it was going through something similar. The data engineering discipline took cues from its sibling, while also defining itself in opposition, and finding its own identity.

Like data scientists, data engineers write code. They’re highly analytical, and are interested in data visualization.

Unlike data scientists — and inspired by our more mature parent, software engineering — data engineers build tools, infrastructure, frameworks, and services. In fact, it’s arguable that data engineering is much closer to software engineering than it is to a data science.

In relation to previously existing roles, the data engineering field could be thought of as a superset of business intelligence and data warehousing that brings more elements from software engineering. This discipline also integrates specialization around the operation of so called “big data” distributed systems, along with concepts around the extended Hadoop ecosystem, stream processing, and in computation at scale.

In smaller companies — where no data infrastructure team has yet been formalized — the data engineering role may also cover the workload around setting up and operating the organization’s data infrastructure. This includes tasks like setting up and operating platforms like Hadoop/Hive/HBase, Spark, and the like.

In smaller environments people tend to use hosted services offered by Amazon or Databricks, or get support from companies like Cloudera or Hortonworks — which essentially subcontracts the data engineering role to other companies.

In larger environments, there tends to be specialization and the creation of a formal role to manage this workload, as the need for a data infrastructure team grows. In those organizations, the role of automating some of the data engineering processes falls under the hand of both the data engineering and data infrastructure teams, and it’s common for these teams to collaborate to solve higher level problems.

While the engineering aspect of the role is growing in scope, other aspects of the original business engineering role are becoming secondary. Areas like crafting and maintaining portfolios of reports and dashboards are not a data engineer’s primary focus.

We now have better self-service tooling where analysts, data scientist and the general “information worker” is becoming more data-savvy and can take care of data consumption autonomously.

### ETL is changing

We’ve also observed a general shift away from drag-and-drop ETL (Extract Transform and Load) tools towards a more programmatic approach. Product know-how on platforms like Informatica, IBM Datastage, Cognos, AbInitio or Microsoft SSIS isn’t common amongst modern data engineers, and being replaced by more generic software engineering skills along with understanding of programmatic or configuration driven platforms like Airflow, Oozie, Azkabhan or Luigi. It’s also fairly common for engineers to develop and manage their own job orchestrator/scheduler.

There’s a multitude of reasons why complex pieces of software are not developed using drag and drop tools: it’s that ultimately code is the best abstraction there is for software. While it’s beyond the scope of this article to argue on this topic, it’s easy to infer that these same reasons apply to writing ETL as it applies to any other software. Code allows for arbitrary levels of abstractions, allows for all logical operation in a familiar way, integrates well with source control, is easy to version and to collaborate on. The fact that ETL tools evolved to expose graphical interfaces seems like a detour in the history of data processing, and would certainly make for an interesting blog post of its own.

Let’s highlight the fact that the abstractions exposed by traditional ETL tools are off-target. Sure, there’s a need to abstract the complexity of data processing, computation and storage. But I would argue that the solution is not to expose ETL primitives (like source/target, aggregations, filtering) into a drag-and-drop fashion. The abstractions needed are of a higher level.

For example, an example of a needed abstraction in a modern data environment is the configuration for the experiments in an A/B testing framework: what are all the experiment? what are the related treatments? what percentage of users should be exposed? what are the metrics that each experiment expects to affect? when is the experiment taking effect? In this example, we have a framework that receives precise, high level input, performs complex statistical computation and delivers computed results. We expect that adding an entry for a new experiment will result in extra computation and results being delivered. What is important to note in this example is that the input parameters of this abstraction are not the one offered by a traditional ETL tool, and that a building such an abstraction in a drag and drop interface would not be manageable.

To a modern data engineer, traditional ETL tools are largely obsolete because logic cannot be expressed using code. As a result, the abstractions needed cannot be expressed intuitively in those tools. Now knowing that the data engineer’s role consist largely of defining ETL, and knowing that a completely new set of tools and methodology is needed, one can argue that this forces the discipline to rebuild itself from the ground up. New stack, new tools, a new set of constraints, and in many cases, a new generation of individuals.

### Data modeling is changing

Typical data modeling techniques — like the star schema — which defined our approach to data modeling for the analytics workloads typically associated with data warehouses, are less relevant than they once were. The traditional best practices of data warehousing are loosing ground on a shifting stack. Storage and compute is cheaper than ever, and with the advent of distributed databases that scale out linearly, the scarcer resource is engineering time.

Here are some changes observed in data modeling techniques:

- further denormalization: maintaining surrogate keys in dimensions can be tricky, and it makes fact tables less readable. The use of natural, human readable keys and dimension attributes in fact tables is becoming more common, reducing the need for costly joins that can be heavy on distributed databases. Also note that support for encoding and compression in serialization formats like Parquet or ORC, or in database engines like Vertica, address most of the performance loss that would normally be associated with denormalization. Those systems have been taught to normalize the data for storage on their own.
- blobs: modern databases have a growing support for blobs through native types and functions. This opens new moves in the data modeler’s playbook, and can allow for fact tables to store multiple grains at once when needed
- dynamic schemas: since the advent of map reduce, with the growing popularity of document stores and with support for blobs in databases, it’s becoming easier to evolve database schemas without executing DML. This makes it easier to have an iterative approach to warehousing, and removes the need to get full consensus and buy-in prior to development.
- systematically snapshoting dimensions (storing a full copy of the dimension for each ETL schedule cycle, usually in distinct table partitions) as a generic way to handle slowly changing dimension (SCD) is a simple generic approach that requires little engineering effort, and that unlike the classical approach, is easy to grasp when writing ETL and queries alike. It’s also easy and relatively cheap to denormalize the dimension’s attribute into the fact table to keep track of its value at the moment of the transaction. In retrospect, complex SCD modeling techniques are not intuitive and reduce accessibility.
- conformance, as in conformed dimensions and metrics is still extremely important in modern data environment, but with the need for data warehouses to move fast, and with more team and roles invited to contribute to this effort, it’s less imperative and more of a tradeoff. Consensus and convergence can happen as a background process in the areas where the pain point of divergence become out-of-hand.

Also, more generally, it’s arguable to say that with the commoditization of compute cycles and with more people being data-savvy then before, there’s less need to precompute and store results in the warehouse. For instance you can have complex Spark job that can compute complex analysis on-demand only, and not be scheduled to be part of the warehouse.

## Roles & responsibilities

### The data warehouse

A data warehouse is a copy of transaction data specifically structured for query and analysis. — Ralph Kimball

A data warehouse is a subject-oriented, integrated, time-variant and non-volatile collection of data in support of management’s decision making process. — Bill Inmon

The data warehouse is just as relevant as it ever was, and data engineers are in charge of many aspects of its construction and operation. The data engineer’s focal point is the data warehouse and gravitates around it.

The modern data warehouse is a more public institution than it was historically, welcoming data scientists, analysts, and software engineers to partake in its construction and operation. Data is simply too centric to the company’s activity to have limitation around what roles can manage its flow. While this allows scaling to match the organization’s data needs, it often results in a much more chaotic, shape-shifting, imperfect piece of infrastructure.

The data engineering team will often own pockets of certified, high quality areas in the data warehouse. At Airbnb for instance, there’s a set of “core” schemas that are managed by the data engineering team, where service level agreement (SLAs) are clearly defined and measured, naming conventions are strictly followed, business metadata and documentation is of the highest quality, and the related pipeline code follows a set of well defined best practices.

It also becomes the role of the data engineering team to be a “center of excellence” through the definitions of standards, best practices and certification processes for data objects. The team can evolve to partake or lead an education program sharing its core competencies to help other teams become better citizens of the data warehouse. For instance, Facebook has a “data camp” education program and Airbnb is developing a similar “Data University” program where data engineers lead session that teach people how to be proficient with data.

Data engineers are also the “librarians” of the data warehouse, cataloging and organizing metadata, defining the processes by which one files or extract data from the warehouse. In a fast growing, rapidly evolving, slightly chaotic data ecosystem, metadata management and tooling become a vital component of a modern data platform.

### Performance tuning and optimization

With data becoming more strategic than ever, companies are growing impressive budgets for their data infrastructure. This makes it increasingly rational for data engineers to spend cycles on performance tuning and optimization of data processing and storage. Since the budgets are rarely shrinking in this area, optimization is often coming from the perspective of achieving more with the same amount of resources or trying to linearize exponential growth in resource utilization and costs.

Knowing that the complexity of the data engineering stack is exploding we can assume that the complexity of optimizing such stack and processes can be just as challenging. Where it can be easy to get huge wins with little effort, diminishing returns laws typically apply.

It’s definitely in the interest of the data engineer to build [on] infrastructure that scales with the company, and to be resource conscious at all times.

### Data Integration

Data integration, the practice behind integrating businesses and systems
through the exchange of data, is as important and as challenging as its ever
been. As Software as a Service (SaaS) becomes the new standard way for companies to operate, the need to synchronize referential data across these systems becomes increasingly critical. Not only SaaS needs up-to-date data to function, we often want to bring the data generated on their side into our data warehouse so that it can be analyzed along the rest of our data. Sure SaaS often have their own analytics offering, but are systematically lacking the perspective that the rest of you company’s data offer, so more often than not it’s necessary to pull some of this data back.

Letting these SaaS offering redefine referential data without integrating and sharing a common primary key is a disaster that should be avoided at all costs. No one wants to manually maintain two employee or customer lists in 2 different systems, and worst: having to do fuzzy matching when bringing their HR data back into their warehouse.

Worst, company executive often sign deal with SaaS providers without really
considering the data integration challenges. The integration workload is systematically downplayed by vendors to facilitate their sales, and leaves data engineers stuck doing unaccounted, under appreciated work to do. Let alone the fact that typical SaaS APIs are often poorly designed, unclearly documented and “agile”: meaning that you can expect them to change without notice.

### Services
Data engineers are operating at a higher level of abstraction and in some cases that means providing services and tooling to automate the type of work that data engineers, data scientists or analysts may do manually.

Here are a few examples of services that data engineers and data infrastructure engineer may build and operate.

data ingestion: services and tooling around “scraping” databases, loading logs, fetching data from external stores or APIs, …
metric computation: frameworks to compute and summarize engagement, growth or segmentation related metrics
anomaly detection: automating data consumption to alert people anomalous events occur or when trends are changing significantly
metadata management: tooling around allowing generation and consumption of metadata, making it easy to find information in and around the data warehouse
experimentation: A/B testing and experimentation frameworks is often a critical piece of company’s analytics with a significant data engineering component to it
instrumentation: analytics starts with logging events and attributes related to those events, data engineers have vested interests in making sure that high quality data is captured upstream
sessionization: pipelines that are specialized in understand series of actions in time, allowing analysts to understand user behaviors
Just like software engineers, data engineers should be constantly looking to automate their workloads and building abstraction that allow them to climb the complexity ladder. While the nature of the workflows that can be automated differs depending on the environment, the need to automate them is common across the board.

## Required Skills

SQL mastery: if english is the language of business, SQL is the language of
data. How successful of a business man can you be if you don’t speak good english? While generations of technologies age and fade, SQL is still standing strong as the lingua franca of data. A data engineer should be able to express any degree of complexity in SQL using techniques like “correlated subqueries” and window functions. SQL/DML/DDL primitives are simple enough that it should hold no secrets to a data engineer. Beyond the declarative nature of SQL, she/he should be able to read and
understand database execution plans, and have an understanding of what
all the steps are, how indices work, the different join algorithm and the
distributed dimension within the plan.

Data modeling techniques: for a data engineer, entity-relationship modeling should be a cognitive reflex, along with a clear understanding of normalization, and have a sharp intuition around denormalization tradeoffs. The data engineer should be familiar with dimensional modeling and the related concepts and lexical field.

ETL design: writing efficient, resilient and “evolvable” ETL is key. I’m
planning on expanding on this topic on an upcoming blog post.

Architectural projections: like any professional in any given field of expertise, the data engineer needs to have a high level understanding of most of the tools, platforms, libraries and other resources at its disposal. The properties, use-cases and subtleties behind the different flavors of databases, computation engines, stream processors, message queues, workflow orchestrators, serialization formats and other related technologies. When designing solutions, she/he should be able to make good choices as to which technologies to use and have a vision as to how to make them work together.

## All in all
Over the past 5 years working in Silicon Valley at Airbnb, Facebook and Yahoo!, and having interacted profusely with data teams of all kinds working for companies like Google, Netflix, Amazon, Uber, Lyft and dozens of companies of all sizes, I’m observing a growing consensus on what “data engineering” is evolving into, and felt a need to share some of my findings.

I’m hoping that this article can serve as some sort of manifesto for data engineering, and I’m hoping to spark reactions from the community operating in the related fields!


# The Downfall of the Data Engineer

This post follows up on The Rise of the Data Engineer, a recent post that was an attempt at defining data engineering and described how this new role relates to historical and modern roles in the data space.

In this post, I want to expose the challenges and risks that cripple data engineers and enumerates the forces that work against this discipline as it goes through its adolescence.

While the title of this post is sensationalistic and the content quite pessimistic, keep in mind that I strongly believe in data engineering — I needed a strong title that contrasts with my previous article. Understanding and exposing the adversity that the role is facing is a first step towards finding solutions.

Also note that the views expressed here are my own, and are based on observations made while talking to people from dozens of data teams across Silicon Valley. These views are not the views of my employer, or directly related to my current position.

## Boredom & context switching

Watching paint dry is exciting in comparison to writing and maintaining Extract Transform and Load (ETL) logic. Most ETL jobs take a long time to execute and errors or issues tend to happen at runtime or are post-runtime assertions. Since the development time to execution time ratio is typically low, being productive means juggling with multiple pipelines at once and inherently doing a lot of context switching. By the time one of your 5 running “big data jobs” has finished, you have to get back in the mind space you were in many hours ago and craft your next iteration. Depending on how caffeinated you are, how long it’s been since the last iteration, and how systematic you are, you may fail at restoring the full context in your short term memory. This leads to systemic, stupid errors that waste hours.

When the idle time between iteration cycles is counted in hours, it becomes tempting to work around the clock to keep your “plates spinning”. When 5–10 minutes of work at 11:30pm can save you 2–4 hours the next day, it tends to lead to unhealthy work-life balance.

## Consensus seeking
Whether you think that old-school data warehousing concepts are fading or not, the quest to achieve conformed dimensions and conformed metrics is as relevant as it ever was. Most of us still hear people saying “single source of truth” every other day. The data warehouse needs to reflect the business, and the business should have clarity on how it thinks about analytics. Conflicting nomenclature and inconsistent data across different namespaces, or “data marts” are problematic. If you want to build trust in a way that supports decision-making, you need a minimum of consistency and alignment. In modern large organizations, where hundred of people are involved in the data generation side of the analytical process, consensus seeking is challenging, when not outright impossible in a timely fashion.

Historically, people used the pejorative term “data silo” to designate issues related to heterogenous analytics that would be scattered across platforms or use incompatible referential. Silos naturally spawn into existence as projects get started, teams drift and inevitably as acquisitions occur. It’s the task of the business intelligence (now data engineering) teams to solve these issues with methodologies that enforces consensus, like Master Data Management (MDM), data integration, and an ambitious data warehousing program. Nowadays, at modern fast pace companies, the silo problem quickly grows out of proportion, where you could use the term “dark matter” to qualify the result of the expansion of chaos that is taking place. With an army of not-so-qualified people pitching in, the resulting network of pipelines can quickly become chaotic, inconsistent and wasteful. If the data engineer is the “librarian of the data warehouse”, they might feel like their mission is akin to classifying publications in a gigantic recycling plant.

In a world where the dashboard lifecycles are counted in weeks, consensus becomes a background process that can hardly keep up with the rate of change and shifting focus of the business. Traditionalists would suggest starting a data stewardship and ownership program, but at a certain scale and pace, these efforts are a weak force that are no match for the expansion taking place.

## Change Management

Given that useful datasets become widely used and derived in ways that results in large and complex directed acyclic graphs (DAGs) of dependencies, altering logic or source data tends to break and/or invalidate downstream constructs. Downstream nodes like derived datasets, reports, dashboards, services and machine learning models may then need to be altered and/or re-computed to reflect upstream changes. Typically, the metadata around data lineage is usually incomplete or is buried in code that only a select few will have the capacity and patience to read. Upstream changes will inevitably break and invalidate downstream entities in intricate ways. Depending on how your organization values stability over accuracy, change can be scary and that can lead to pipeline constipation. If the data engineer’s incentives are geared towards stability, they will learn quickly that best way to not break anything is to not change anything.

Since pipelines are typically large and expensive, adequate unit or integration testing can be expected to be somewhat proportional. The point being: there’s only so much you can validate with sampled data and dry-runs. And if you thought a single environment was more chaos than you could handle, try to stay sane while throwing a dev and staging environment that use intricately different code and data! In my experience, it’s rare to find any sort of decent dev or test environments in the big data world. In many cases, the best you’ll find are some namespaced “sandboxes” that people use to support whatever undocumented process they see fit.

Data engineering has missed the boat on the “devops movement” and rarely benefit from the sanity and peace-of-mind it provides to modern engineers. They didn’t miss the boat because they didn’t show up, they missed the boat because the ticket was too expensive for their cargo.

## The worst seat at the table

Modern teams move fast, and whether your organization is engineering-driven, PM-driven or design-driven, and whether it wants to think of itself as data-driven, the data engineer won’t be driving much. You have to think of it as an infrastructure role, something that people take for granted and bring their attention to when it’s broken or falling short on its promises.

If there’s a data engineer that is part of the conversation at all, it’s probably to help the data scientists and analysts gathering the data they need. If the data of interest isn’t already available in the structured part of the data warehouse, chances are that the analyst will proceed with a short term solution querying raw data, while the data engineer may help in properly logging and eventually carrying that data into the warehouse. Most likely an answer is required in a timely fashion, and by the time the new dimensions and metrics are backfilled into the warehouse, it’s already old news and everyone has moved on. The analyst will get the glory for the insight, and everyone else may question the need for the slow background process of consolidating this new piece of information in the warehouse.

While “impact” — which implies velocity and disruption — is the most sought after word in employees’ performance review, data engineering is condemned to being a slow background process with little short term impact. Data engineers are many degrees removed from those who are “moving the needle”.

## Operational creep

Operational creep is a hard reality for professions that involve supporting the systems that they build. Q/A teams have largely been replaced by the “you support what you build” motto and most people in the field rally around this idea. This approach is regarded as the proper way to make engineer conscious and responsible for the technical debt accumulating.

Since data engineering typically comes with a fairly high maintenance burden, operational creep comes fast and disarms engineers faster than you can hire them. Yes, modern tooling help people be more productive, but arguably that’s only machinery that allows pipeline builders to keep more plates spinning at once.

Moreover, operational creep can lead to high employee turnover, which ultimately lead to low quality, inconsistent, unmaintainable messes.

## Real software engineers?

People in the field have heard arguments as to whether data engineers were “real software engineers” or some different class of engineers. In some organization the role is different and may have different [lower] salary bands. Casual observation may suggest that the rate of data engineers with a computer science degree may be significantly lower than across software engineering as a whole.

The role, for the reasons depicted in this article, can suffer from a bad reputation that spins that viscous circle.

## But wait — there’s still hope!

Don’t quit just yet! There’s still a huge consensus around data being a key competitive advantage, and companies are investing more than ever in analytics. “Data maturity” follows a predictable growth curve that ultimately leads to the realization that data engineering is extremely important. As you read these words, hundreds of companies are doubling down on their long-term data strategy and investing in data engineering. The role is alive, growing and well.

With numerous companies plateauing on their data ROI and feeling the frustration of “data operational peak”, it’s inevitable that upcoming innovation will address the pain points described here, and eventually create a new era in data engineering.

One could argue that a possible path forward is de-specialization. If the proper tooling is made available, perhaps simple tasks can be deferred to information workers. Perhaps more complex workloads can become a dimension of common software engineering work, much like what happened to Q/A and release engineers while continuous delivery technologies and methodologies emerged.

In any case, proper tooling and methodology will define the path forward for the role, and I’m hopeful that it is possible to address most of the roots causes leading to the concerns expressed in this post.

I’m planning an upcoming blog post titled “Next generation, data-aware ETL” where I’ll be proposing a design for a new framework that has accessibility and maintainability at its very core. This yet-to-be-built framework would have a set of hard constraints, but in return will provide strong guarantees while enforcing best practices. Stay tuned!