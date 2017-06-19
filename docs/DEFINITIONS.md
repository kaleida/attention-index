
## DEFINITIONS ##

If you [download the data](../data) you'll find several fields in each CSV. Many of them are self-explanatory. Some are specific to the **Attention Index**. Below are the field names and descriptions that should clarify what the values mean. You can also read more about the [methodology](METHODOLOGY.md) and how the figures are calculated

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
