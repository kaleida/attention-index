# Change and Issues Log

This file describes the changes to the dataset, and any known
issues with the quality of the data.

## General Limitations

The data for following publishers only includes articles that were promoted
on their front or on their Facebook page, likely a small proportion 
of everything they published:

- thetimes.co.uk
- reuters.com
- foxnews.com
- breitbart.com
- ft.com


## June 2017

- **25 June 2017** Started tracking the New Statesman and Mirror Online.
- **17 June 2017** Correctly deal with the blogspot domain redirection
madness that impacted Another Angry Voice. The net effect is that
Facebook promotion data for AAV may be inaccurate before this date.
- **13 June 2017** Facebook [improved accuracy of engagement data](https://medium.com/kaleida/facebook-engagement-data-gets-more-accurate-and-bigger-d25647589fe8). We 
observed that enagagements reported increased by between
75% and 1000% as a result.

## May 2017

- **31 May 2017** BBC now has an operational Google News Sitemap.
Before this date, only BBC articles that featured on their front or
on Facebook were included. 
- **31 May 2017** Fixed lead article tracking for Skwawkbox. Lead promotion data
may be invalid before this date.
- **16 May 2017** Started tracking Lib Dem Voice, Evolve Politics, Your News Wire, RT and Brexit Central. 
As much data as possible was backfilled, but promotion data may be inaccurate
before this date. 
- **15 May 2017** Started tracking indy100, Skwawkbox, Guido Fawkes, Westmonster. 
As much data as possible was backfilled, but promotion data may be inaccurate
before this date. In addition, indy100's lack of historical links
means that many articles for them will be missing before this date too.
- **12 May 2017** Switched to using Facebook's [v2.9 Graph API](https://developers.facebook.com/docs/apps/changelog#v2_9).
This splits out reactions, comments and shares separately from the engagement
number. Data before this date may only have fb_engagements populated.
- **9 May 2017** Started tracking Another Angry Voice and The Canary. As much
data as possible was backfilled, but promotion data may be inaccurate
before this date.


