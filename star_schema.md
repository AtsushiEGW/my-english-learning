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
