# Data

Data is your business. Data-informed, not data-driven.

> Don't draw the wrong conclusion even if you have data.

How data can improve performance. What performance? Please find out from your domain.

To mine data, you need to store metrics, telemetry data. Tiny events that happen in your business processes.

Keywords: Data collection, monitoring, measurement, telemetry, data points, frequency, volumes, data-driven decision

Features:

* Drill-down
* Slices
* Aggregate
* Window function

Self-analyze and self-correct.

Currently, the KPI in Jobline are mostly about counters. Displaying the "how many" of things. Like "how many CV has been profile on this day", "how fast is the processing time", etc. We need to figure what kind of interesting behavior we want to analyze.

First, we need to know what performance problem do we see (from recruiters as well as from client). Poor engagement with client when sending resume? Slow approval from client?

Not a lot of "predictive patterns" to gain ☹️.

> Predict what's going to happen, instead of waiting for it to happen (requires lots of data!)

Too many businesses regard data analytics as pertaining mainly to realizing value from some existing data.

## Data Collection - Gather the right data

> What success metric to measure?

Consciously map how you use data in each phase of the product lifecycle.

Mostly from FileMaker and into other databases. Running schedule scripts to import data at regular interval. How frequent the interval determine the final resolution.

We do have a stream of "structured data". The schema is well-known.

Looking at the right data is the only way to understand your world.

"Idle job/application" has some bad data that can make it easy to draw the wrong conclusions.

## Log Analysis

**Root-cause analysis** - Imagine candidate submit or upload Timesheet, but FM is logging different timestamp. How come we definitively know when such action occurs. What POSTed request can we inspect to pin-point "when" the action exactly take place.

`navigator.sendBeacon`

Fire off beacon to learn your user's behavior!

## Predictive Model

Predictive model abstracts away the complexity of the world, focusing in on a particular set of indicators that correlate in some way with a quantity of interest (who will churn, or who will purchase).

## Case Studies

* [Training and serving NLP models using Spark MLlib](https://www.oreilly.com/ideas/training-and-serving-nlp-models-using-spark-mllib)
* [Scaling Knowledge at Airbnb](https://medium.com/airbnb-engineering/scaling-knowledge-at-airbnb-875d73eff091#.bglfxzsj1)

## Tools

* [RMarkdown](http://rmarkdown.rstudio.com/)
* [Jupyter](http://jupyter.org/)
* [IPython Notebook](http://ipython.org/notebook.html)
* [IRuby??](https://github.com/SciRuby/iruby)

## Questions

* Who are the top 10 customers/clients?
* What customer postal code has the most orders?
* How do sales vary between customers with and without accounts?
* Are orders affected by holidays?
* Are they any unpopular items?
* What percentage of sales comes from xxx?
* What are the most frequent combinations of xxx?
* How do vendor requisitions vary by time and location?
* Volumes of purchases from vendors?
* Seasonal pattern?
* Backorder?
* What is our total exposure? Are our premiums high enough?
* How does this recruiter compare to the other recruiter in terms of sales rate? Processing time? Number of CV sent?
* Churn rate for our client. Which clients has the most staffs turnover rate and thus we need to be careful doing business with them.
* What is our recruiters' habits?