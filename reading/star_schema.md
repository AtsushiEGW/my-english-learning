# Star Schema The Complete Reference

## Introduction

> Dimensional design is a pillar of every modern-day data warehouse architecture.

- ディメンショナルデザインは、すべての今日のデータウェアハウス構造を支える柱である。
- ディメンショナルデザインは、あらゆる現代のデータウェアハウス構造を支える柱の一つである。
- a pillar は不定冠詞なので、「の一つ」の意味合いになる

> Based on a disarmingly simple approach to process measurement, dimensional design enables extraordinarily powerful analytics.

- disarmingly: disarm(武装解除する) --> disarming(武装解除するような->人の心を和ませるような) 難しいものだと身構えていたがその必要はないと思うほど --> 拍子抜けするほど

- process measurement は「ビジネスプロセスの計測」(データウェアハウス・ディメンショナルモデリングの世界では、「ビジネスプロセス」（sales, orders, inventory など企業の業務活動）を数値として記録・計測することが設計の出発点になります。たとえば「何個売れたか」「いくら売上があったか」がまさに process measurement です。)

> The products of dimensional design — the star schema, the snowflake, and the cube — can be found in virtually every data warehouse implementation.

- スタースキーマ、スノーフレーク、キューブといった、ディメンショナルデザインの産物(products)は、事実上あらゆるDWH実装・導入例(implementation)においてみられる.
- データに於いて
  - processing: データを計算・変換する動作のことをいう
  - implementation: システムやアーキテクチャを実際に構築・導入すること

> Despite this popularity, relatively little is written about dimensional design.

- これほど普及しているにも関わらず、ディメンショナルデザインについて書かれているものは比較的少ない
- little などは副詞で修飾できる
  - relatively little: 比較的少ない量
  - surprisingly few: 驚くほど少ない数
  - comparatively much: 比較的多い量

> Although some outstanding works are available, most assume a particular architecture or philosophy— my own prior work included.

- outstanding: 際立った
- assume: 前提とする、所与のものとして扱う
  - This analysis assumes a linear relationship. この分析は線形関係を前提としている

> Additionally, these treatments are organized around vertical industries or major business functions, making them difficult to refer to when faced with a specific design challenge.

Additionally, /
these treatments / are organized /
    around vertical industries or major business functions/ , 
{
    making them difficult /
    to refer to when faced with a specific design challenge.
}






This book is a complete reference to dimensional design—the first intended for any
reader. The best practices presented in this volume cut across all architectures, including
those espoused by W.H. Inmon and Ralph Kimball. Organized around the key concepts of
dimensional design, this book provides full, in-depth treatment of each topic, sequenced in
a logical progression from fundamentals through advanced techniques.
This book is designed for both beginners and experts in dimensional design. If you are a
beginner, it is the ideal place to start. Each chapter provides you with best practices and their
underlying rationale, detailed examples, and the criteria you need to make design decisions.
If you are an expert, you will be able to use this guide as a reference. Whenever you face a
particular design challenge, you will find a chapter or section dedicated to the topic.
Dimensional design enables profoundly powerful business analysis. A solid understanding
of the underlying principles is essential, whether you are directly involved in design activities,
work with dimensional data structures, manage projects, or fund implementations. Mastery of
the techniques and best practices in this book will help you unleash the full potential of your
data warehouse, regardless of architecture, implementation scope, or software tools.







### About This Book

This book has been designed as a complete, in-depth reference for anyone who works with
dimensional data—the star, the snowflake, or the cube.

- The content is organized into chapters and sections dedicated to the core concepts
of dimensional design so you can find everything you need to know about a particular topic in one place.
- Each topic is treated comprehensively. Full explanations for best practices allow you to make informed design decisions based on operational realities.
- No assumptions are made about your data warehouse environment. The best practices here apply in all architectures, including those espoused by W.H. Inmon and Ralph Kimball.
- Specific software products are not referenced, but the ways in which your tools may influence design decisions are fully explored.

The result is a treatment that is comprehensive and useful, regardless of your level of
experience, data warehouse architecture, or available tools.

### Organized Around Core Concepts

This book is organized around the core concepts of dimensional modeling, rather than a
series of business scenarios by vertical industry. Focusing on these concepts allows a complete
treatment of each topic, without forcing you to flip back and forth between various business
cases. Each topic is explored in depth, rather than spread across multiple chapters.
This comprehensive treatment of each concept allows Star Schema: The Complete Reference
to serve as a useful resource. Experienced modelers will find what they need with a quick
scan through the Table of Contents. Need to brush up on the implications of a snapshot
design? Everything you need can be found in Chapter 11. Thinking about implementing a
bridge table? It’s all there in Chapter 9. Need to implement a hybrid slow change? A
complete discussion can be found in Chapter 8. Each chapter concludes with references to
external treatments of the topic, should you wish to search for more examples.
For those new to dimensional design, the material has been sequenced so the book can
be read cover to cover. The first three chapters explore fundamentals, and subsequent
sections delve deeply into various aspects of dimensional design. Help on choosing where to
start is provided at the end of this introduction.

### Comprehensive and Practical, Not Dogmatic

While this book highlights a series of best practices, the underlying motivation is always
fully explored. You will learn the reasons for these guidelines, and develop the ability to
make informed decisions on how to apply them. The result is a practical approach to data
warehouse design—one that is responsive to organizational and operational context, rather
than independent of it.
Dimensional designers, for example, are often trained to record information at the
lowest level of detail possible. The reasons for this guideline are fully explained in Chapter 3,
along with situations where these reasons might not apply. Similarly, designers are always
taught that different business processes deserve their own models, or stars. Chapter 4
explains why this is the case, and fully explores what happens when this guideline is relaxed.
Even when you stick to the best practices, there is no single “right way” to model a
particular business process. You will learn how each design option strikes a balance among
business value, the required effort to construct reports, the complexity of the load process,
and cost. Flattening a recursive hierarchy, for example, simplifies reporting and reduces
development cost, but limits the power of the final solution; the alternatives are fully
explored in Chapter 10. Derived schemas can make reporting easier and improve performance, but provide significant additional work to load data into the data warehouse, as described in Chapter 14.

### Architecture-Neutral

This book makes no assumptions about your data warehouse architecture. The best practices
outlined in these pages apply whether you follow W.H. Inmon’s Corporate Information
Factory approach or Ralph Kimball’s dimensional data warehouse “bus” approach, or simply
build subject-area data marts. In each of these paradigms, there is a place for dimensional
data. No matter how you put dimensional design to work, this book will allow you to make
the most of it.
If you don’t know anything about these thought leaders or their recommended
architectures, you will learn something about them in Chapter 2. There, you will find a
high-level overview of various approaches, and information on how dimensional design fits into
each. What you won’t find is an argument in favor of one approach over another. This book’s
coverage of dimensional design is disentangled from such considerations. Anyone can use it.

#### Common Vocabulary

This book is designed to service any data warehouse architecture, but it is necessary
to establish a common vocabulary. When it comes to dimensional design, that
vocabulary comes from Ralph Kimball. By providing a way to talk about dimensional
design, he has made a valuable contribution to the world of data warehousing, giving
us terms like grain, conformance, and slowly changing dimensions. These and other terms
can be found in his seminal work on dimensional design: The Data Warehouse Toolkit,
Second Edition, by Ralph Kimball and Margy Ross (Wiley, 2002).
Wherever possible, this book makes use of terminology established by Kimball
and Ross. Each term will be fully explained. However, it is not presumed that the
reader adheres to Kimball’s approach to data warehousing. His approach is one of
several architectures that make use of dimensional design. These architectures are
discussed in Chapter 2; the principles in this book can be employed in any of these
situations.

### Product-Independent

This book makes no assumptions about specific hardware or software products in your data
warehouse architecture. The dimensional techniques described are largely universal, and
can be implemented using tools and technologies from a variety of vendors.
This is not to say that the software products used by your organization will not influence
your dimensional design. To the contrary, they can, will, and should bear such influence.
Although specific software products will not be discussed, the influence of various kinds of
tools will be explored. These include database management systems (DBMSs), reporting or
business intelligence (BI) software, and data integration or extract transform load (ETL)
tools.
The capabilities of your RDBMS and reporting tools, for example, may drive the decision
to produce a “snowflake” design, rather than a star, as you will learn in Chapter 7. The
capabilities of a business intelligence tool, or the sophistication of its users, may shape your
approach to schema design issues outlined in Chapter 16. Development of the ETL process
is complex, and may benefit from some design considerations discussed in Chapter 17.

### Snowflakes and Cubes

Most of the examples in this book feature the star schema. The principles of dimensional
modeling can also be used to design snowflakes and cubes. The best practices are largely
the same, with a few exceptions that are highlighted and explored. The snowflake is
featured in Chapter 7; the influence of business intelligence tools on this design option are
discussed in Chapter 16. The cube is introduced in Chapter 3; many useful ways to pair
stars with cubes are explored in Chapters 14, 15, and 16.


### Who Should Read This Book

This book is written for you, the data warehouse practitioner. If your work in any way involves
stars, snowflakes, or cubes, then this is your guide to all things dimensional. No assumptions
are made regarding your skill level, role, or preferred architecture.
You may design dimensional models, work with dimensional data, manage activities, or
pay the bills. Your role may fall into a variety of categories, including:

- Business Analysis
- Data Architecture / Star Schema Design
- Business Intelligence and Reporting
- Data Integration or ETL
- Database Administration
- Quality Assurance
- Data Administration
- Project Management
- Executive Leadership / IT Management
- Power User

It will be assumed that you have a basic familiarity with relational database concepts like
tables, columns, and joins. There will be occasional examples of SQL code; these will be
fully explained for the benefit of novice readers.
No assumptions are made about your level of experience. If you are new to dimensional
design, you will probably want to read this book from cover to cover. Experienced practitioners
may prefer to skip directly to areas of particular interest. The next section provides advice on
how to proceed.







Analytics that cross process boundaries are extremely powerful. This holds true within a
subject area and across the enterprise. As the previous chapter showed, process-focused
analytics require separate fact tables, and cross-process analytics require bringing this
information together. This is accomplished by drilling across, and its success or failure hinges
on dimensions.
This chapter focuses on insuring cross-process capability through conformed dimensions.
With the right dimension design and content, it is possible to compare facts from different
fact tables, both within a subject area and across the enterprise. Many powerful metrics can
only be provided in this manner. Incompatible dimensions, on the other hand, prevent
drilling across. The resulting stovepipes can be frustrating.
The requirements for conformed dimensions are spelled out as a series of rules. It is
possible to memorize these rules and follow them blindly, but students of dimensional
design are better off understanding why they are important. Before enumerating the
conditions for conformance, this chapter takes a closer look at how dimensions make or
break a successful drill-across.
Conformance, it turns out, can take many forms. This chapter will look at several ways
that dimensions can conform and offer practical advice to keep your designs out of trouble.
Conformed dimensions can do more than enable drilling across. They can serve as the
focus for planning enterprise analytic capability. This chapter closes with practical
considerations surrounding conformance in each of the major data warehouse
architectures—the Corporate Information Factory, the dimensional data warehouse “bus”
architecture, and the stand-alone data mart.

## The Synergy of Multiple Stars

Dimensional designs are usually implemented in parts. Regardless of architecture style, it is
impractical to organize a single project that will encompass the entire enterprise. Realistic
project scope is achieved by subdividing the enterprise into subject areas and subject areas
into projects.
Over time, as each new star is brought online, the organization receives two kinds of
analytic benefits. First, and most obviously, it becomes possible to analyze the business
process measured by the star. The value of this benefit alone is usually significant. People
gain valuable insight into business activity, whether they are directly involved in the process,
responsible for it, or simply interested parties. Some processes, such as sales, may gain
attention from all levels of the enterprise.
With each new star comes a second kind of benefit, often expected but sometimes
unanticipated. Not only does the star afford insight into a new business process, but it also
allows the process to be studied in conjunction with others. Again, this kind of analysis may
be of interest to people who are involved in a particular process area, but it is equally likely
to interest higher levels of corporate management.
A powerful example of cross-process analysis appeared in Chapter 4, “A Fact Table for
Each Process.” The report in Figure 4-13 compared information from numerous processes:
sales call activity, delivery of sales proposals, orders, and shipments. Looking across these
processes to form a consolidated picture of business activity is highly useful for sales
management, company executives, directors, and investors.
The report in Figure 4-13 also contained a measurement called yield, which represented the
ratio of sales calls made to orders taken. This single metric may be one of the most important
indicators tracked by interested parties, and it can only be constructed by crossing process
boundaries. As Chapter 4 advised, schema designers need to be alert to the existence of
business measurements that cross process boundaries. Because these measurements do not
exist as a column in a table somewhere, they may be easily lost in the shuffle if not documented
and targeted for delivery.
Every business has chains of linked processes, often beginning with product development
or acquisition, extending through customer acquisition, and culminating in the collection of
revenues. These chains can be found at micro- and macro-levels. Within a subject area such as
sales, for example, there may be a series of linked processes like those in Figure 4-13. Sales are
also a participant in a macro-level chain, connecting product manufacturing, sales, marketing,
customer support, and finance.
The stars that represent each process connect to one another through common dimensions.
This can be envisioned graphically, as depicted in Figure 5-1. Orders, shipments, and a variety of
other stars relate to one another through a set of dimensions. These dimensions, which appear
in the center column of the diagram, serve as a framework, across which process comparisons are
supported. Any two fact tables that link to the same dimension can theoretically be compared
using the drill-across technique described in Chapter 4.
At a logical level, when a series of stars share a set of common dimensions, the dimensions
are referred to as conformed dimensions. As suggested in the previous chapter, two fact tables do
not have to share the same physical dimension table to support comparison. If the separate
dimension tables conform, it will be possible to drill across them.
When dimensions do not conform, short-term victories give way to long-term defeat.
Orders and shipments stars, for example, might be implemented one at a time. As each is
brought online, new insights are afforded to various groups of interested parties. In this
respect, each successful implementation reflects well on the data warehouse team that
brought it to fruition. If these individual stars do not share a common view of what a
customer is, or what a product is, that goodwill may eventually give way to indifference or
disdain. While it is possible to study orders or shipments, it is not possible to compare them.
At best, the response is frustration over a missed opportunity. At worst, a general distrust of
the analytic infrastructure develops.
As you will see later in this chapter, dimensions can conform in a variety of ways. While
conformance may be conveyed by a diagram like the one in Figure 5-1, such pictures
quickly become difficult to lay out and understand. The crucial concept of conformance is
often better depicted through alternate means.
As the key to long-term success, conforming dimensions are crucial in any data
warehouse architecture that includes a dimensional component. Before spelling out the
requirements for conformance and their implications, let’s take a closer look at how they
support, or fail to support, drilling across. Understanding how and why this process breaks
down sheds important light on the concept of dimensional conformance.

## Dimensions and Drilling Across

Dimensions are the key enablers of the drill-across activity that brings together information
from different processes. Drill-across failure occurs when dimensions differ in their structure
or content, extinguishing the possibility of cross-process synergy. Dimension tables need not
be identical to support drilling across. When the attributes of one are a subset of another,
drilling across may also be possible.

## What Causes Failure?

Dimensions and their content are central to the process of comparing fact tables. In the
first phase of drilling across, dimensions are used to define a common level of aggregation
for the facts from each fact table queried. In the second phase, their values are used to
merge results of these queries. Dimensional incompatibilities can disrupt this process. The
stars in Figure 5-2 are rife with examples.
The stars in Figure 5-2 describe two processes: orders and returns. Each has been
implemented by a separate department and resides in a separate database. Individually,
these stars permit valuable analysis of the processes they represent. Both include dimension
tables representing day, customer, and product. Given these commonalities, it is reasonable
to expect these stars should permit comparison of these processes. For example, one might
ask to see returns as a percentage of orders by product during a particular period. The two
drill-across phases, as introduced in Chapter 4, would unfold as follows:
1. A query is issued for each fact table, aggregating the respective facts (quantity
ordered and quantity returned) by product.
2. These intermediate result sets are merged based on the common product names,
and the ratio of quantity ordered to the quantity returned is computed.
A similar process might be followed to drill across various other dimension attributes
such as product type or category, or across dimension attributes from the day, customer, or
salesperson tables.
Unfortunately, several factors prevent these stars from supporting this activity, at least
when it comes to products. The problems lie in the respective product tables. Differences
in their structure and content get in the way of comparing orders and returns.

## Differences in Dimension Structure

The two product dimension tables have many differences, any one of which can foil an
attempt to drill across. First, consider differences in the structure of the dimension tables.
•
•
The product dimension table in the orders star contains a type dimension; the one
in the returns star does not. It may be difficult or impossible to compare orders to
returns based on product type depending on other characteristics of the tables.
Columns that appear to be the same thing are named differently in the two stars.
For example, the column that contains the name of the product is called product in
the orders star, and prod_name in the returns star. A similar situation exists for the
columns that contain category descriptions. These differences may stand in the way
of drill-across operations as well.
It can be tempting to dismiss these differences since a skilled developer might be able
to work around them. Although product type is not present in the orders star, a developer
might be able to match each product from the orders star to a product type in the returns
star. The SKU, which is the natural key, might be used to support this lookup process. After
these equivalences are identified, orders could be aggregated by type and compared to
returns.
Similarly, a developer could work around the differences in column names to compare
orders and returns by category. Applying his or her knowledge of column equivalencies, the
developer groups orders by category, and groups returns by prod_cat. When joining these
intermediate result sets, the developer would match the category from the orders query
with prod_cat from the returns query.
These workarounds are further examples of what Chapter 4 referred to as “boiling the
frog.” They range from simple to complex, but each compensates for design-level
shortcomings by complicating the reporting process. These kinds of workarounds have
many drawbacks:
•
•
•
•
Specific knowledge is required to drill across.
It may not be possible for anyone but the most skilled developers to use
workarounds to compare the processes.
Workarounds risk inconsistent and inaccurate results when applied incorrectly.
Workarounds stand in the way of the automated generation of drill-across reports
for ad hoc reporting tools.
Not every structural incompatibility can be overcome by a workaround. If the two stars
have different definitions of a product, there may be deeper difficulties. This might occur if
one star takes into account packaging differences, while the other does not. Timing may
also get in the way. If one star collects data on a monthly basis, while the other does so on
a weekly basis, there would be virtually no way to compare this data. Weeks and months
cannot be rolled up to any common level of summarization.
Last, reliance on these workarounds depends on some consistency in the content of the
two versions of the dimension. If there are also content differences, it may become impossible
to overcome structural differences.

## Differences in Dimension Content

In the case of the stars in Figure 5-2, further difficulties are evident when you examine the
content of the product dimension tables:
•
Product names and categories are formatted differently. The orders star uses mixed
case and punctuation; the returns star formats data in all caps without punctuation.
These differences will get in the way during the merge phase of drilling across since
these values are the basis of the merge.
Names are not consistent. SKU 3333-01 is called “9
• × 12 bubble mailer” in the
orders star, and “STANDARD MAILER” in the returns star. It may be that a change
in product name was handled as a type 1 change for orders and was ignored for
returns. The inconsistent names will impede the merging of intermediate result
sets for queries that involve the product name.
•
The product with the natural key 4444-22 has one row in the orders star but two
rows in the returns star. It appears that this product underwent a change in
category that was treated as a type 1 change in the orders star, and a type 2 change
in the returns star. It is possible to compare orders and returns by category, but the
orders will skew toward the more recent value.
•
The product with SKU 6666-22 is present in the orders star but not in the returns
star. This will not impede drilling across, but is an indicator that inconsistencies
exist between the tables.
•
The product with SKU 5555-22 is assigned different surrogate key values in the two
stars. Care must be taken when joining tables.
Again, it may be possible to work around some of these limitations, but the impact on
the reporting process would be severe, and not all the issues can be overcome. For
example, developers might try to address the first limitation by converting all text to
uppercase and stripping punctuation before joining two intermediate result sets together.
This will have a negative impact on query performance, since the product name for each
granular fact must be adjusted and sorted prior to aggregation. This will not help in
situations where product names are recorded differently, as is the case with product
3333-01.
Some of the limitations might be dealt with by only referring to SKUs when querying
each star, then using a single dimension table to determine the associated dimension
values. The facts from each star could then be aggregated before merging intermediate
result sets. Again, this additional processing will severely hamper performance. It will
require that each report be constructed by a skilled developer and thus eliminate any
chance that a business intelligence tool could generate a drill-across report. Furthermore, it
will not work in situations where one table omits a particular product, or where a product
has multiple rows in one of the dimension tables.
None of these considerations takes into account the confusion that users may experience
when trying to interpret the results. How does one compare orders and returns for a product
if each star specifies the product differently? Which product name should be placed on the
report? What if this report is compared to one that uses the other name? The last two
incompatibilities on the list may not directly hamper a drill-across operation but can lead to
situations where analysts working with data sets from the two stars produce erroneous results
by linking a dimension table to a fact table from the other star.

## Preliminary Requirements for Conformance

To support successful drill-across comparisons, designers must avoid incompatibilities like
those in Figure 5-2. The issues that rendered the two product dimension tables incompatible
can be addressed by requiring that the two tables be the same. As noted in Chapter 4, there
are two crucial parts to this sameness: the tables must be the same in structure and in content.
Same Structure Structurally, the tables should have the same set of dimension columns.
This avoids the need to piece together missing information such as the product_type
column. Corresponding dimension columns should have the same names so there is no
ambiguity in where their equivalencies lie. They should also have the same data type
definitions since their content will be identical.
These structural equivalences support the first phase of a drill-across operation. The
dimension columns can be relied upon to define a consistent scope of aggregation for each
fact table. In the first phase of drilling across, each fact table can be queried using the same
dimensional groupings, without the need for a special processing workaround. Additionally,
the structural compatibility supports a successful merge in the second phase, although
content will also play a crucial role.
Same Content In terms of content, the values found in dimension columns must be
expressed identically. If the name of product 3333-01 is “9 × 12 bubble mailer” in the orders
star, it should be “9 × 12 bubble mailer” in the returns star. This common value will allow
intermediate results from each star to be joined during the second phase of a drill-across
operation. Use of consistent value instances avoids the need to clean up or convert
corresponding column values so that they match, and guarantees that values will support
the merge of intermediate results.
Corresponding dimension tables should provide consistent results when substituted for
one another. In terms of content, this requires that they contain the same set of rows, that
corresponding rows share the same surrogate key values, and that slow change processing
rules have been applied consistently. These requirements, however, do not apply in cases
where the corresponding dimension tables describe different levels of summarization.