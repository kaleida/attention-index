# DOCUMENTATION #

## SUMMARY ##

<img src="https://raw.githubusercontent.com/kaleida/attention-index/master/kaleida-attention-index-venn-diagram.png" width="300" align="right" hspace="10">**Kaleida's Attention Index** is a measure of observed interest in subjects. The index is derived using publicly available data from global news media and social platforms.

Publisher data and social data are combined to arrive at an overall Attention Score. We obtain this data using a range of tools to process the data including our own homegrown applications and 3rd party data processing services as described below.

<img src="https://raw.githubusercontent.com/kaleida/attention-index/master/kaleida-attention-index-data-factors-chart.png">

We've published our work in a python notebook. That document goes step-by-step through our data explorations detailing how we arrived at these results. It includes the exploratory analysis, charts, data tables, statistics and the resulting formulas.

<img src="https://raw.githubusercontent.com/kaleida/attention-index/master/kaleida-attention-index-facebook-engagements-formula.png">
<img src="https://raw.githubusercontent.com/kaleida/attention-index/master/kaleida-attention-index-lognormal-engagements.png">

The **Attention Index** data is made available by Kaleida Networks Ltd. to the public under a Creative Commons license ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode)) including permission for commercial use. You are explicitly encouraged to use and share the data. We just ask that you give us attribution. And feel free to [contact us](matt@kaleida.com) if you have any questions about the data or usage.

## METHODOLOGY ##

You are encouraged to apply our approach to developing the Attention Index. The following methodology provides detail about what the data means, how it was collected and what we're doing with it.

The process begins by collecting published content. For each publisher in our list our crawlers scan publisher home pages, Google sitemaps and Facebook brand pages to identify URLs. We look at URL patterns for each publisher to identify content types, excluding offsite links, links to index pages or other stuff we don't care about.

The scanning process is performed on a regular basis in order to identify 1) when new articles exist, 2) when promotion of an article begins, 3) when promotion of an article ends, 4) changes in placement of an article on publisher properties including whether or not an article is the lead article on the web site home page.

When a new URL is discovered our tools extract data about the page including data from any meta tags.

Then we process the article. First we identify the body text and pass it to a natural language processor to extract the terms mentioned in the text. We differentiate between a thing that is mentioned vs what the article is about by separating out the terms which are in the headline, standfirst and first paragraph from the other mentioned terms. We also run the body text through sentiment analysis tools.

Processing is handled by tools developed inhouse, [Google's NLP services](https://cloud.google.com/natural-language/), and a service called [Aylien](http://aylien.com/).

Next we track performance. We look at engagement on Facebook while simultaneously updating promotion data with each publisher scan. We use Facebook's graph API to collect social activity for each URL. Facebook returns the number of shares, number of comments and number of reactions. We collect this data on a regular basis until the sharing activity appears to stop.

All this data is stored using [Elasticsearch](https://www.elastic.co/) and hosted via [Amazon Web Services](https://aws.amazon.com/).

The stats for each article then get rolled up into buckets, as needed. For example, we can query aggregate totals for shares of all articles by a given publisher for any given time period. Data can be sorted and filtered by total engagements, engagements per minute, publisher, subject, list of subjects, promotion time, promotion placement, etc.

More details about the fields available, descriptions of the data, and sample output are described in the definitions below.

## DEFINITIONS ##

| Field        | Description |
| ------------- |-------------|
| id | an automatically generated Kaleida-defined id representing a single article. |
| url | the canonical URL of a single article. does not change after discovery.|
| headline | the headline of the article by the publisher. does not change after discovery currently.|
| discovered | the date/time the url was first discovered by Kaleida's tools. ISO 8601 format.|
| published | the date/time of publication of the article according to rules developed inhouse. ISO 8601 format. published date/time may be before discovered date/time.|
| fb_engagements | total number of engagements according to Facebook's API as of the last recorded scan. engagements equals comments + reactions + shares.|
| fb_max_engagements_per_min | the maximum number of engagements per minute observed.|
| fb_comments | number of comments for this url according to Facebook's API. subset of engagements.|
| fb_reactions |  number of reactions including likes for this url according to Facebook's API. subset of engagements.|
| fb_shares |  number of shares of this url in Facebook posts according to Facebook's API. subset of engagements.|
| publisher_name | name of the publisher of this article.|
| publisher_id | unique identifier of the publisher of this article.|
| mins_as_lead | number of minutes this article appeared on the publisher's featured position on the web site home page. |
| mins_on_front | number of minutes this article appeared anywhere on the publisher's web site home page |
| num_articles_on_front | if `mins_on_front` > 0, average number of articles that appeared on the publisher's web site home page while this article was present there. |
| fb_brand_page | this article was promoted by the publisher on the publisher's Facebook brand page. *true/false* |
| fb_brand_page_likes | if `fb_brand_page` is true, number of likes to the publisher's Facebook brand page at the time of posting. |
| alexa_rank | Alexa global rank for this publisher. |
| **response_score** | Facebook engagements scored on a log normal scale. *max = 50* |
| lead_score | score of value to publisher using `mins_as_lead` and weighted by `alexa_rank`.  *max = 20* |
| front_score | score of value to publisher using `mins_on_front` and weighted by `alexa_rank`.  *max = 15* |
| facebook_promotion_score | score of value of promotion on Facebook using `fb_brand_page` and weighted by `fb_brand_page_likes`.  *max = 15* |
| **promotion_score** | score of all the publisher promotion activities for this article = `lead_score` + `front_score` + `facebook_promotion_score`. *max = 50* |
| **attention_index** | Total attention score for this article = `response_score` + `promotion_score`. *max = 100* |
