# TERN
TURTLEDOVE Enhancements with Reduced Networking

----------------

## Table of Contents

- [Introduction](https://github.com/SemanticSugar/TERN#introduction)
- [Authors](https://github.com/SemanticSugar/TERN#authors)
- [Stakeholder Feedback / Opposition](https://github.com/SemanticSugar/TERN#stakeholder-feedback--opposition)
- [0. Before Advertising Begins](https://github.com/SemanticSugar/TERN#0-before-advertising-begins)
- [1. On the Advertiser's Site](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site)
  - [a. Faster delivery of ads](https://github.com/SemanticSugar/TERN#a-faster-delivery-of-ads)
  - [b. Elimination of minimum interest group sizes](https://github.com/SemanticSugar/TERN#b-elimination-of-minimum-interest-group-sizes)
  - [c. Reduced networking](https://github.com/SemanticSugar/TERN#c-reduced-networking)
  - [d. Writing multiple interest groups](https://github.com/SemanticSugar/TERN#d-writing-multiple-interest-groups)
  - [e. Multiple ad formats](https://github.com/SemanticSugar/TERN#e-multiple-ad-formats)
  - [f. Ad categories](https://github.com/SemanticSugar/TERN#f-ad-categories)
  - [g. SSP tokens](https://github.com/SemanticSugar/TERN#g-ssp-tokens)
    - [i. Pre-approval](https://github.com/SemanticSugar/TERN#i-pre-approval)
    - [ii. Delayed-approval](https://github.com/SemanticSugar/TERN#ii-delayed-approval)
  - [h. Products](https://github.com/SemanticSugar/TERN#h-products)
  - [i. More refined bidding signals and reporting signals](https://github.com/SemanticSugar/TERN#i-more-refined-bidding-signals-and-reporting-signals)
  - [j. DSPs control bidding](https://github.com/SemanticSugar/TERN#j-dsps-control-bidding)
  - [k. Preserving third-party tag functionality](https://github.com/SemanticSugar/TERN#k-preserving-third-party-tag-functionality)
- [2. In the Background](https://github.com/SemanticSugar/TERN#2-in-the-background)
  - [a. Validate ads](https://github.com/SemanticSugar/TERN#a-validate-ads)
  - [b. Download ad web bundles](https://github.com/SemanticSugar/TERN#b-download-ad-web-bundles)
  - [c. Fetch ads request](https://github.com/SemanticSugar/TERN#c-fetch-ads-request)
- [3. Publisher Data](https://github.com/SemanticSugar/TERN#3-publisher-data)
  - [a. The publisher/contextual request](https://github.com/SemanticSugar/TERN#a-the-publishercontextual-request)
  - [b. The SSP](https://github.com/SemanticSugar/TERN#b-the-ssp)
- [4. Browser Signals](https://github.com/SemanticSugar/TERN#4-browser-signals)
  - [a. Recency](https://github.com/SemanticSugar/TERN#a-recency)
  - [b. Frequencies](https://github.com/SemanticSugar/TERN#b-frequencies)
  - [c. Impression Recencies](https://github.com/SemanticSugar/TERN#c-impression-recencies)
- [5. Generating Bids](https://github.com/SemanticSugar/TERN#5-generating-bids)
- [6. The Auction](https://github.com/SemanticSugar/TERN#6-the-auction)
- [7. Rendering the Ad](https://github.com/SemanticSugar/TERN#7-rendering-the-ad)
- [Considered Alternatives](https://github.com/SemanticSugar/TERN#considered-alternatives)
  - [a. TURTLEDOVE](https://github.com/SemanticSugar/TERN#a-turtledove)
  - [b. Product-level Turtledove](https://github.com/SemanticSugar/TERN#b-product-level-turtledove)
  - [c. Outcome-based Turtledove](https://github.com/SemanticSugar/TERN#c-outcome-based-turtledove)
  - [d. SPARROW](https://github.com/SemanticSugar/TERN#d-sparrow)
- [FAQ](https://github.com/SemanticSugar/TERN#faq)
  - [a. Where does machine learning fit in?](https://github.com/SemanticSugar/TERN#a-where-does-machine-learning-fit-in)
  - [b. How do I stop a campaign from spending?](https://github.com/SemanticSugar/TERN#b-how-do-i-stop-a-campaign-from-spending)
  - [c. How do I apply frequency caps or optimization?](https://github.com/SemanticSugar/TERN#c-how-do-i-apply-frequency-caps-or-optimization)

----------------

## Introduction

The purpose of this document is to capture a variety of GitHub issues and repos that seek to alter
the main [TURTLEDOVE](https://github.com/WICG/turtledove) proposal. By collating industry experience
and feedback into a single document containing a more complete specification, we believe that more
productive discussion will ensue, and that these consensus-based enhancements will more easily be
applied to the original proposal.

We intend to enhance TURTLEDOVE in the following privacy-preserving ways:

- Clarifying the necessary inputs to participate in an auction
- Clarifying how to deal with multiple ad formats
- Reducing networking overhead by streamlining the data which flows through SSPs
- Eliminating the need for thresholds on interest group sizes
- Reducing the time to potentially deliver an impression
- Better supporting dynamic creative and product recommendation use cases
- Supporting some functionality of third-party tags
- Further specifying auditability of delivered ad creatives
- Adding a `privateData` object that can never escape the browser, but improve bidding signals (among potential other use cases)
- Specifying the auction dynamic to avoid game-theoretic complications
- Specifying frequency capping and optimization
- A monosyllabic acronym that is still thematically avian

These ideas are drawn from many authors. Inspiration is taken from discussions in:

- [TURTLEDOVE](https://github.com/WICG/turtledove/)
- [TURTLEDOVE Issue #5 - Ad Signals in the auction and group membership](https://github.com/WICG/turtledove/issues/5)
- [TURTLEDOVE Issue #36 - Dynamic Creative Use Case](https://github.com/WICG/turtledove/issues/36)
- [TURTLEDOVE Issue #37 - Clarification on Entities](https://github.com/WICG/turtledove/issues/37)
- [TURTLEDOVE Issue #38 - Contextual Bid](https://github.com/WICG/turtledove/issues/38)
- [TURTLEDOVE Issue #46 - Limit on Number of Interest Groups / Web Bundles](https://github.com/WICG/turtledove/issues/46)
- [Product-level Turtledove](https://github.com/jonasz/product_level_turtledove)
- [Outcome-based Turtledove](https://github.com/jonasz/outcome_based_turtledove)
- [Frequency Capping and Optimization](https://github.com/W3C/web-advertising/blob/master/frequency-capping-and-optimization.md)

Reading through the original TURTLEDOVE proposal is a necessary prerequisite to understanding this document.

----------------

## Authors

- [Andrew Pascoe](https://github.com/appascoe)
- [Valentino Volonghi](https://github.com/dialtone)

If you would like to contribute, please feel free to open a PR. Our preference is to make
this a dynamic document to build consensus.

----------------

## Stakeholder Feedback / Opposition

This section summarizes stakeholder sentiment and any feedback; link each to most recent discussion
or outcome.

| Stakeholder | Sentiment | Discussion      |
| ----------- | --------- | --------------- |
| NextRoll    | In favor  | (this document) |

----------------

## 0. Before Advertising Begins

[Outcome-based Turtledove](https://github.com/jonasz/outcome_based_turtledove) suggests a mechanism
for SSPs to audit ads before they are delivered. While a bit more complex than described here, it
essentially boils down to the proposal that an ad must _attempt_ to reach a sufficient number of users
before it can be shown. Unfortunately, this will have drastically deleterious effects for smaller
advertisers and merchants.

Consider, for example, a local pizza shop attempting to advertise through a platform like Yelp. This
is a situation where advertising may be very effective to drive a user to conversion, particularly
if there are discounts on the table. However, being a local business, it is unlikely to reach a
particularly large audience. If there are time-sensitive offers or products available, the shop may
not even be able to reach the threshold before the offer has expired.

In lieu of this, we propose an auditing mechanism that is more in line with how creative review
operates today. An SSP can offer an endpoint:

```
https://ssp.example/ad-review
```

where a DSP can provide a JSON object of the sort:

```
{
  'advertiser': 'https://advertiser.example',
  'dsp': 'https://dsp.example',
  'name': 'ad-123456789',
  'ad-cbor-url': 'https://dsp.example/ads/ad-123456789.wbn',
  'categories': ['cat1', 'cat2', 'cat3'],
  'formats': ['1024x768', '512x384']
}
```

This gives the SSP an opportunity to review the content of the ad, confirm that it belongs to
the declared advertiser, and adheres to its delcared categories (for brand safety), etc.
Once review is completed, the DSP can query:

```
https://ssp.example/check-review
```

with

```
{
  'name': 'ad-123456789'
}
```

and receive back

```
{
  'request-id': 'ad-123456789',
  'review-token': 'review-token-123879'
}
```

This review token will be used later by the DSP, and can be used later by the browser. If a DSP
has a good relationship with an SSP (for example, by having its own creative review process that
is robust enough to the SSP's standards), the SSP could also immediately provide a review token
on the first request without a need for the DSP to follow up on the `/check-review` endpoint. This
trusted pre-approval is how creative review processes tend to function today.

Perhaps the review token could be computed as something like (we'll talk more about this later):

```
hash(hash(ssp_secret_key, ad-content), hash(dsp, ad-cbor-url, categories))
```

By including the `ad-content` here, we ensure that the DSP cannot change the images in the creative
to something else after approval. The SSP would be responsible for storing a map of:

```
hash(dsp, ad-cbor-url, categories) -> hash(ssp_secret_key, ad-content)
```

for quick lookup during the browser validation phase.

We believe this is a better proposal that will ensure bad actors are audited and removed from the
online ad ecosystem while also keeping the wheels oiled for trustworthy players.

----------------

## 1. On the Advertiser's Site

When a browser lands on advertiser's site, the advertiser's pixel fires. The browser exposes an API:

```.writeAdvertisementData(input)```

The pixel produces a JSON object for the `input` of the form:

```
{
  'advertiser': 'https://advertiser.example',
  'dsp': 'https://dsp.example',
  'ssps': ['https://ssp-1.example',
           'https://ssp-2.example'],
  'groups': { 'interest-group-1': { 'timestamp': ts,
                                    'ttl': duration },
              'interest-group-2': { 'timestamp': ts,
                                    'ttl': duration } }
  'third-parties': {'https://third-party-1.example': 'https://third-party-1.example/js/metrics.js',
                    'https://third-party-2.example': 'https://third-party-2.example/js/metrics.js'},
  'decision-logic-url': 'https://dsp.example/js/bidding.js',
  'ads': [{'name': 'ad-123456789',
           'formats': [{ 'aspect_ratio': '16:9',
                         'min_height': 400,
                         'max_height': 800 }],
           'ad-cbor-url': 'https://dsp.example/ads/ad-123456789.wbn',
           'ssp-tokens': {'https://ssp-1.example': {'token': 'review-token-12345',
                                                    'isPreApproved': true },
                          'https://ssp-2.example': {'isPreApproved': false }},
           'categories': ['cat1', 'cat2', 'cat3'],
           'cache-lifetime-secs': 21600,
           'max-times-per-minute': 1,
           'max-times-per-hour': 6,
           'products': {'product-id-1': 'https://dsp.example/products/product-id-1.wbn',
                        'product-id-2': 'https://dsp.example/products/product-id-2.wbn'},
           'privateData': { ... } },
          {'name': 'ad-987654321',
           'formats': ['1024x768', '512x384'],
           'ad-cbor-url': 'https://dsp.example/ads/ad-987654321.wbn',
           'ssp-tokens': {'https://ssp-1.example': {'token': 'review-token-54321',
                                                    'isPreApproved': true },
                          'https://ssp-2.example': {'token': 'review-token-09876',
                                                    'isPreApproved': true}},
           'categories': ['cat4', 'cat5'],
           'cache-lifetime-secs': 86400,
           'max-times-per-minute': 1,
           'max-times-per-hour': 12,
           'products': {'product-id-3': 'https://dsp.example/products/product-id-3.wbn',
                        'product-id-4': 'https://dsp.example/products/product-id-4.wbn'},
           'privateData': { ... } }]
}
```

This JSON object is significantly more complex than what is required in the `.joinInterestGroup()` call
in TURTLEDOVE, but it is not without cause. We list the reasons for each object below. However,
after receiving the JSON object, the browser proceeds to act as largely described in TURTLEDOVE: it adds
the browser to all of the interest groups in the object (for auditing by the user and the potential follow-up
[interest group requests](https://github.com/SemanticSugar/TERN#c-fetch-ads-request) later),
caches what it needs to from the ad and product web bundles, and so on.

We propose that these objects be namespaced by the value in the `'dsp'` field. Browsers are going to have
natural limits on the amount of storage the user is willing to tolerate. An unscrupulous actor on the
market could perform an attack by loading many such objects into the browser, forcing storage evictions
of the JSON objects written by other DSPs. These issues are discussed in [TURTLEDOVE Issue #46 - Limit on Number of Interest Groups / Web Bundles](https://github.com/WICG/turtledove/issues/46).
With these objects namespaced, the malevolent actor would only be able to evict its own objects. In the
event of reaching some global limit in the browser, the browser itself can measure the most aggressive
writers to storage, and prioritize the eviction of their items in deference to more responsible DSPs.

While it may have been intended in TURTLEDOVE, we make explicit here that _the `'advertiser'` field value
does not need to match the current site_. Advertisers will enter into co-ops that permit them to target
each other's users. For example, a pet _food_ store may wish to cross-target with a pet _toy_ store.
Knowing that a user is browsing cat food implies that they may be interested in cat toys, and vice versa.
Note that this is not a violation of privacy: the identity of the user isn't disclosed to a third party.
It only provides an opportunity for the third party to have a more effective upper funnel campaign than
may be available through contextual targeting alone.

### a. Faster delivery of ads

We combine writing interest groups along with the web bundles for ads. This means that, in principle,
ads can be delivered nearly immediately after browsing away from the site.

Recency is an important factor in the efficacy of ads. At NextRoll, we see that ad requests that come
ten minutes after the browser has been on the site produce bids that are ~40% lower than requests that
come one minute after the browser has visited the site. TURTLEDOVE suggests a later interest group request
as much as four hours after being added to an interest group. We expect that this would dangerously decrease
publisher revenues.

### b. Elimination of minimum interest group sizes

Also by combining interest groups with ad web bundles, we no longer need to worry about minimum
sizes for interest groups at this stage. Since the browser is on the advertiser's site, its set of
interest groups already can be known in full to the advertiser through first-party cookies, and
thus there is no reduction in privacy.

This is a critical feature for small advertisers and merchants, and also for advertisers that
wish to perform product recommendation for rare or highly specific products. Refer to [section 0](https://github.com/SemanticSugar/TERN#0-before-advertising-begins)
for a descriptive example of such an advertiser. A discussion is covered in [TURTLEDOVE Issue #36](https://github.com/WICG/turtledove/issues/36).

### c. Reduced networking

There's no particular need for the browser to make follow-up calls when it's already
on the advertiser's site. This should reduce the amount of background network calls the
browser will need to make. (However, we will still maintain some interest group request, as
described below, but this can be optional and much less frequent.)

### d. Writing multiple interest groups

Rather than writing one interest group at a time, we can write multiple. Accordingly, each needs
to have its own TTL specified. We also include the timestamp at which the browser was added to an
interest group for signals described later in this document.

TURTLEDOVE appears to allow multiple interest groups to be added to the browser, but it seems to
require multiple calls to `.joinInterestGroup()`. This is unnecessary.

### e. Multiple ad formats

Similarly, we also write multiple ad web bundles at a time and allow specifying the sizes (and/or
aspect ratios) at which an ad bundle knows how to render itself. This is necessary because the
browser does not know the size of ad slots that will later be up for auction on a publisher's
site. When it comes time to perform the on-device auction, the browser can eliminate the evaluation
of ads that are not compatibly sized.

The number of allowed formats could be limited and chosen from a set of well-known values (e.g., IAB
standard ad units) to prevent use as a tracking vector.

We also note here that the `ads` object can be an empty list `[]`. It is possible that a campaign
or set of ads have not yet been created in order to target a set of interest groups. Ads can be
provided later during the fetch ads request [described below](https://github.com/SemanticSugar/TERN#2-in-the-background).

This may be supported by the TURTLEDOVE specification, but we make it explicit here to remove any
doubt.  One of the main benefits of this ability is the increase in size of targeted groups which
will thus increase the privacy of its members.

### f. Ad categories

As part of the validation process described in [section 0](https://github.com/SemanticSugar/TERN#0-before-advertising-begins),
ads need to declare their categories so publishers can decide whether they would
want such an ad on their site. However, we need to trust that the declared categories
are not a lie. This is the purpose of the SSP review tokens.

### g. SSP tokens

During [section 0](https://github.com/SemanticSugar/TERN#0-before-advertising-begins),
we described a mechanism through which SSPs can perform a validation process for
creatives. As the market functions today, there are two ways of doing this: with a pre-approval
process, and approving some time after the first bid is made (delayed-approval). We consider both
options here:

#### i. Pre-approval

We stated earlier that the SSP provides a token to the DSP of the sort:

```
review-token = hash(hash(ssp_secret_key, ad-content), hash(dsp, ad-cbor-url, categories))
```

Here, the browser itself can compute `ad-hash = hash(dsp, ad-cbor-url, categories)` and query:

```
https://ssp.example/validation
```

with

```
{
  'ad-hash': hash(dsp, ad-cbor-url, categories),
  'isPreApproved': true
}
```
and the SSP, using the `ad-hash` as a key, does a lookup in its map and replies with

```
{
  'review-token': 'review-token-12345',
  'isPreApproved': true
}
```

for the browser to compare with the declared SSP review token.

Note that in this scheme, only the SSP has to download the content before this validation check
(this is why the `ad-content` is part of the hash on the SSP's side). The SSP is free to re-check
the `ad-content` automatically during the validation request, or re-check periodically based on a
TTL to ensure nothing has changed under the hood. If a DSP has proven itself trustworthy, these
re-checks may occur infrequently, and the SSP can just return the review token directly. In the end,
the SSP can set its own review policy.

(Alternatively, the SSP could return to the browser

```
hash(ssp_secret_key, ad-content)
```

during the lookup, and the browser itself could be responsible for computing

```
hash(hash(ssp_secret_key, ad-content), hash(dsp, ad-cbor-url, categories))
```

Either scheme is effective.)

If the returned review token  matches, we can say that all the declared information about the ad
is valid, and then any brand safety filtering can be applied with confidence. If the validation
fails, naturally, the ad is rejected for display.

Note that this doesn't have to happen at impression time, and so no user browsing privacy is
violated.

#### ii. Delayed-approval

In a delayed-approval situation, the DSP has a relationship with the SSP that allows their ads to
be run without an initial creative review before display. In this case, the browser needs to
confirm that the SSP and DSP know about each other.

Say that the DSP shares a secret key with the SSP, `dsp_shared_secret`. Similarly, the SSP shares a
secret with the DSP, `ssp_shared_secret`. The browser now needs only confirm that the SSP and DSP
have indeed shared their secrets. The browser generates a random string, `seed`, and sends a query

```
{
  'ssp': 'https://ssp.example',
  'dsp': 'https://dsp.example',
  'seed': '3498h3gjksakdfjkasfd'
}
```

to both

```
https://ssp.example/delayed-approval
https://dsp.example/delayed-approval
```

where both the DSP and SSP compute

```
{
  'ssp-token': hash(seed, ssp_shared_secret),
  'dsp-token': hash(seed, dsp_shared_secret)
}
```

Now the browser compares the responses from both the SSP and DSP and confirms that they match.
This demonstrates that the SSP and DSP have this relationship. From here, the browser can store
internally that when `'isPreApproved': false` occurs under a particular SSP/DSP combination, it's
safe to display the ad.

The browser itself may want to set a TTL before it checks to see when the ad is eventually reviewed.
It can query the validation endpoint as in [section 1.g.i](https://github.com/SemanticSugar/TERN#i-pre-approval).
If it receives an error response, it can reconfirm the relationship, continue to trust the ad for a while longer,
or expire the ad. This is up to the browser's policy. However, assuming that the SSP/DSP relationship
is still trusted, the response

```
{
  'review-token': 'review-token-12345',
  'isPreApproved': true
}
```

can be used to update the advertisement data JSON object

```
'https://ssp.example': { 'isPreApproved': false } ---> 'https://ssp.example': {'token': 'review-token-12345',
                                                                               'isPreApproved': true }
```

so the browser knows to trust the ad with a longer TTL. When the DSP attempts to use the same ad in
the future, it can supply the review token when writing the advertisement data JSON object, so the
browser can validate normally.

### h. Products

We incorporate a set of product IDs with their associated web bundles a la [Product-level Turtledove](https://github.com/jonasz/product_level_turtledove).
These are at the ad level because different creatives may want to incorporate different product sets.
This element of the JSON object is optional if delivering a static ad.

TURTLEDOVE doesn't appear to support dynamic creative out of the box, and this addition either
actually provides a mechanism, or makes it explicit.

### i. More refined bidding signals and reporting signals

We also incorporate a `privateData` object a la [Outcome-based Turtledove](https://github.com/jonasz/outcome_based_turtledove).
Note that Outcome-based Turtledove calls this object `userSignals`. We think this element can be used
for a variety of signals that we wouldn't want to escape from the browser that can be used in the
bidding function, perhaps not even necessarily related to the user. Examples include metadata about the campaign,
advertiser, or the ad itself. This is also a good place to add additional metadata not just for the
bidding function, but to feed into the [Aggregate Reporting API](https://github.com/csharrison/aggregate-reporting-api).
The `privateData` object can also contain information to remove the ad from contention if an
interest group expires due to its TTL.

An explicit example of a `privateData` field could be `bucketed-probability`, which, through the
Aggregate Reporting API, could help make sure enough users are added to the bucket and provide
a feedback signal to DSPs that their models are well-calibrated for advertising in the wild, rather
than just relying on holdout test datasets.

### j. DSPs control bidding

A clearer distinction between SSP and DSP, which TURTLEDOVE lacks. This will be important later
for reducing networking, but as seen here, the `bidding.js` file is provided by the DSP. Many DSPs prefer
to control their own bidding logic; if necessary, an SSP that also sometimes functions as a DSP can simply
repeat the SSP's URLs in the DSP fields.

For sophisticated DSPs, the primary benefit of SSPs is the management of publisher networks, not collecting user signals
or providing bidding algorithms. A discussion on this topic occurs in [TURTLEDOVE Issue #37 - Clarification on Entities](https://github.com/WICG/turtledove/issues/37).

### k. Preserving third-party tag functionality

TURTLEDOVE does not have a mechanism for third-party tags, such as impression beacons, to be attached
to ads. Of course, granular impression beacons are off the table in order to maintain privacy, but we
should find some way of preserving aggregate data for third parties; it's important for auditing and
providing some choice on the market for advertisers who may want to use analytics tools that are
separate from the SSP and DSP responsible for showing impressions.

We suggest that the reporting metrics specified by a third-party script can be used in the Aggregate
Reporting API (ARAPI), but in a separate storage than what the DSP or SSP may want to track. ARAPI
would then function as usual, just with these new third-party entities as additional consumers of reports.
This is really nothing more than an additional namespace.

This is more apropos to ARAPI, but we include it here for convenience and completeness. ARAPI currently
specifies as an example:

```
const entryHandle = window.writeOnlyReport.get('campaign-123');
entryHandle.set('country', 'usa');
entryHandle.append(“visits”, “1”);
entryHandle.reportAfter(2 * kMsecPerDay);
entryHandle.expireAfter(7 * kMsecPerDay);
```

which would then later generate a report like:

```
{
  'entryName': 'campaign-123',
  'country': 'usa',
  'visits': '1'
}
```

ARAPI does not clearly specify to whom this report would be sent, but we presume it would be sent
to the DSP and SSP in an encrypted format, to be aggregated and decrypted by a helper service, as
discussed in the [Multi-Browser Aggregation Service Explainer](https://github.com/WICG/conversion-measurement-api/blob/master/SERVICE.md).
We suggest a minor change to ARAPI that declares who's performing the in-browser aggregation and
will receive the report:

```
const dspHandle = window.writeOnlyReport.get('https://dsp.example', 'campaign-123');
const thirdPartyHandle = window.writeOnlyReport.get('https://third-party.example', 'campaign-123');
```

These URLs effectively define separate namespaces where reports can have different keys or methods
of computing metrics. For example:

```
dspHandle.set('country', 'usa');
dspHandle.append(“visits”, “1”);
dspHandle.reportAfter(2 * kMsecPerDay);
dspHandle.expireAfter(7 * kMsecPerDay);

thirdPartyHandle.set('region-type', 'suburban');
thirdPartyHandle.append(“news-domain-visits”, “1”);
thirdPartyHandle.reportAfter(1 * kMsecPerDay);
thirdPartyHandle.expireAfter(3 * kMsecPerDay);
```

From here, the browser would generate two reports:

```
{
  'entryName': 'campaign-123',
  'country': 'usa',
  'visits': '1'
}

{
  'entryName': 'campaign-123',
  'region-type': 'suburban',
  'news-domain-visits': '1'
}
```

The first would be sent to the DSP and the second to the third party. The two reports cannot be
mixed, and are encrypted separately to be sent to different servers. We believe this maintains
privacy while still keeping third-party tags in the ecosystem.

----------------

## 2. In the Background

The browser has a variety of functions to perform in the background. Here's what we see as valuable:

### a. Validate ads

This is already described in [section 0](https://github.com/SemanticSugar/TERN#0-before-advertising-begins)
and in [section 1g](https://github.com/SemanticSugar/TERN#g-ssp-tokens).

### b. Download ad web bundles

Each potential ad (or product) to be shown has a URL for the ad web bundle to be downloaded. Given the number of
advertising entities on the web, and also given the number of potential ad sizes a browser would
have to cache for delivery, storage in the browser could be a significant issue.

We suggest that web bundles can _also_ be downloaded at win time in the eventual internal auction.
At first blush, this may seem like a violation of privacy, but if the browser is consistently
making requests to download ad web bundles, such requests at win time would be indistinguishable
from a background request.

### c. Fetch ads request

This largely functions the same as in the TURTLEDOVE proposal. We keep the same nomenclature as in
TURTLEDOVE with an endpoint `/fetch-ads`, but the response just contains URLs to ad web bundles. The
actual downloading of the bundles is described above in [section 2b](https://github.com/SemanticSugar/TERN#b-download-ad-web-bundles).
Here, the browser queries

```
https://dsp.example/.well-known/fetch-ads
```

with

```
{
  'advertiser': 'https://advertiser.example',
  'groups': { 'interest-group-1': { 'timestamp': ts,
                                    'ttl': duration },
              'interest-group-2': { 'timestamp': ts,
                                    'ttl': duration } }
}
```

Note that the set of groups in this request, in contrast to the set written in
[section 1](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site) would be subject
to privacy guidelines such as k-anonymity and/or differential privacy as discussed in the
original TURTLEDOVE proposal. Since the browser is off the advertiser's site, first-party data
is no longer available, and we should not reveal too much about the user.

The DSP responds with the same object as described in [section 1](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site).
This may seem redundant, but we include it for a couple of reasons.

One, the DSP may have a desire to update the JSON object that was supplied on the advertiser's site.
This could be because certain ads or campaigns have been paused, creatives could have been refreshed,
or there may be a new offer or sale that would interest the user.

Two, it's possible that the DSP has added the browser to interest groups that do not have creatives
available at the time on the advertiser's site. They may be in the process of being validated by an
SSP, or an advertiser is waiting to launch a sale, etc.

The browser can set policies here on how often this fetch request needs to be made. If no ads have been provided, it my
call more frequently, versus following the web bundle guidelines on expiration.

Another difference from TURTLEDOVE is that this call explicitly goes to the DSP. This was part of
a discussion in [TURTLEDOVE Issue #37 - Clarification on Entities](https://github.com/WICG/turtledove/issues/37).
Given that these signals are all produced by the DSP, and the DSP has no desire to reveal its
interest group to SSPs, there is no reason to pass through an SSP first. Any concerns about creative
validation are covered by [section 2a](https://github.com/SemanticSugar/TERN#a-validate-ads). This should
significantly reduce network traffic on the internet so requests don't have to go to an SSP only to be
forwarded to a DSP, and will also reduce computational resources if the DSP chooses to encrypt its data
as it passes through the SSP.

----------------

## 3. Publisher Data

This section discusses what calls are made to produce publisher data for bidding signals.

### a. The publisher/contextual request

When the browser lands on a publisher page, an SSP script is run that queries the SSP with
a `publisherRequest` object, an example of such request is below and we include mostly the main fields we believe to be
important:

```
{
  'url': 'https://publisher.example/path/to/page',
  'ad-slot-id': '1234',
  'ad-sizes': ['320x480', '1024x768', '1920x1080'],
  'restricted-categories': ['cat1', 'cat2'],
  'floor-price': 0.75,
  'metadata': {'page-categories': ['cats', 'dogs'],
               'above-the-fold': true,
               ...
               'published-date': '2020-09-19'}
}
```

The required fields are strictly what's necessary to determine which ads would even be
valid for the slot. The floor price lets the publisher declare how much it's willing to
let the slot go for. Finally, metadata is a catch-all object where the publisher can
declare whatever it desires about the page to SSPs; the fields present above are just
potential examples.

### b. The SSP

The SSP, on its own and/or by forwarding the publisher request to its integrated
DSPs is responsible for sending back to the browser a `publisherResponse` object:

```
{ 'dsps': { 'https://dsp-1.example': { 'ads': [ { 'advertiser': 'https://advertiser-1.example',
                                                  'third-parties': {'https://third-party-1.example': 'https://third-party-1.example/js/metrics.js',
                                                                    'https://third-party-2.example': 'https://third-party-2.example/js/metrics.js'},
                                                  'decision-logic-url': 'https://dsp-1.example/js/bidding.js',
                                                  'name': 'ad-123456789',
                                                  'formats': [{ 'aspect_ratio': '16:9',
                                                                'min_height': 400,
                                                                'max_height': 800 }],
                                                  'ad-cbor-url': 'https://dsp-1.example/ads/ad-123456789.wbn',
                                                  'ssp-token': {'token': 'review-token-12345',
                                                                'isPreApproved': true },
                                                  'categories': ['cat1', 'cat2', 'cat3'],
                                                  'cache-lifetime-secs': 21600,
                                                  'max-times-per-minute': 1,
                                                  'max-times-per-hour': 6,
                                                  'products': {'product-id-1': 'https://dsp-1.example/products/product-id-1.wbn',
                                                  'product-id-2': 'https://dsp-1.example/products/product-id-2.wbn'},
                                                  'privateData': { ... }
                                                }
                                              ],
                                       'publisherSignals': { ... } },
            'https://dsp-2.example': { 'ads': [ { 'advertiser': 'https://advertiser-2.example',
                                                  'third-parties': {'https://third-party-3.example': 'https://third-party-3.example/js/metrics.js'},
                                                  'decision-logic-url': 'https://dsp-2.example/js/bidding.js',
                                                  'name': 'ad-987654321',
                                                  'formats': ['1024x768', '512x384'],
                                                  'ad-cbor-url': 'https://dsp-2.example/ads/ad-987654321.wbn',
                                                  'ssp-token': {'isPreApproved': false},
                                                  'categories': ['cat4'],
                                                  'cache-lifetime-secs': 86400,
                                                  'max-times-per-minute': 3,
                                                  'max-times-per-hour': 30,
                                                  'products': {'product-id-3': 'https://dsp-2.example/products/product-id-3.wbn'},
                                                  'privateData': { ... }
                                                }
                                              ],
                                       'publisherSignals': { ... } }
          }
}
```

Clearly, a good chunk of these data come from integrated DSPs (recall that an SSP can function
like a DSP, if it so chooses).

This response is a modified version of what we saw in [section 1](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site).
The SSP is already known and therefore there's no need for a set of SSP trust tokens within each ad.
Interest groups are no longer required.

However, given that during the publisher request, there is no access to the interest groups or
ads already in the browser, it is unknown to the SSP, or its integrated DSPs, whether the
browser is primed to bid on any ads already. This means that 1) the SSP must communicate with
all of its DSPs for every publisher request, and 2) DSPs will want to respond to every such
publisher request _even if they don't have a contextual ad to show_. That means the `ad` field
in each DSP object is optional.

Each `ad` has a `privateData` object that can provide signals about the ad, campaign, etc. as before.
However, in addition, even if an ad is not present in the DSP's object, there is a higher level
`publisherSignals` object where the DSP can provide signals that will be passed into its `bidding.js`
function. This object can contain signals from the `publisherRequest` object or additional signals
that the SSP chooses to provide the DSP when querying them. The point is to provide additional
flexiblity to SSPs and DSPs when it comes time to bid. In particular, the publisher's `floor-price`
value is a very important field for the `bidding.js` function. Of course, `publisherSignals` can
be an empty object.

To the point that `publisherSignals` can be an empty object, we suggest that it be acceptable that
a `publisherResponse` is _not_ required (though probably recommended) to
[generate a bid](https://github.com/SemanticSugar/TERN#5-generating-bids). This could cut down on
overall network traffic if a DSP is not required to respond, but as stated, it's unlikely that the
`publisherSignals` will not be very valuable.

Note also that because the SSP does not necessarily have access to each DSP's `bidding.js` function,
it is unable to perform any internal auction to select a winner. All potential ads must be sent
back to the browser for evaluation.

Another distinction from TURTLEDOVE is that this response does not contain any computed bids.
While the TURTLEDOVE proposal on the surface seems reasonable in supplying an actual bid back,
this really isn't particularly feasible, because the price of ads depends highly on how often
the user has already seen a particular ad, or ads from the same advertiser. We'll address how
those signals can be provided later, but the point is, pricing is very dynamic. For this reason,
every ad returned here links to a `bidding.js` function, and the `ads` object from each DSP is
a list.

Many of these issues are discussed in [TURTLEDOVE Issue #38 - Contextual Bid](https://github.com/WICG/turtledove/issues/38)
and [TURTLEDOVE Issue #37 - Clarification on Entities](https://github.com/WICG/turtledove/issues/37).

----------------

## 4. Browser Signals

In the current advertising market, many important signals are computable by DSPs that have
profound effects on ad prices. These will no longer be available in the original TURTLEDOVE
proposal. Here, we suggest that the browser itself compute some of these signals itself to
maintain both flexible pricing that props up publisher revenues while maintaining user
privacy. These ideas are discussed in [TURTLEDOVE Issue #5 - Ad Signals in the auction and group membership](https://github.com/WICG/turtledove/issues/5)
and [Frequency Capping and Optimization](https://github.com/W3C/web-advertising/blob/master/frequency-capping-and-optimization.md).

This is not an exhaustive list of signals that could be provided by the browser, but they
are some particularly critical ones that certainly require some resolution that is not
provided by the TURTLEDOVE proposal.

These can be provided in a `browserSignals` object like:

```
{
  'interest-group-1-recency': time-since-joining-interest-group-1,
  'interest-group-2-recency': time-since-joining-interest-group-2,
  'ad-total-frequency': total-times-ad-has-been-displayed,
  'ad-day-frequency': times-ad-has-been-shown-last-24-hours,
  'advertiser-total-frequency': total-times-user-has-seen-ad-from-advertiser,
  'advertiser-day-frequency': times-user-has-seen-ad-from-advertiser-last-24-hours
}
```

### a. Recency

Recall that when adding the browser to an interest group, we had an object:

```
'groups': { 'interest-group-1': { 'timestamp': ts,
                                  'ttl': duration },
            'interest-group-2': { 'timestamp': ts,
                                  'ttl': duration } }
```

At bid time, the browser looks at the current timestamp `T` and computes `T - ts` for each interest group and adds it to the
`browserSignals` object for the particular ad `bidding.js` calculation. There should also be a mechanism for binning
these recencies to report back in the Aggregate Reporting API for data analysis and improved bidding. Within the browser,
there's no concern about passing these fields as they are. For reporting, suitable noise (for differential privacy) or
attaining a threshold for k-anonymity can be applied to the timestamp to avoid identification of the user, while
maintaining the signal.

Alternatively, the [`generate_bids()`](https://github.com/SemanticSugar/TERN#5-generating-bids) function
itself could compute this (assuming it will have access to the browser's UTC epoch time), but we include
this as a simple concrete example.

### b. Frequencies

Each ad object contains both a `name` for the ad and the `advertiser` field. The
browser can keep incremental counts under both of these keys, for both total
frequency and daily frequency. Similarly to recency, the browser can add these
to the `browserSignals` object to be passed into the particular ad `bidding.js`
calculation and provide a mechanism for binning for reporting and data analysis.

To address the concern about frequency capping (halting displaying an ad because
it's been shown too many times already), a DSP can include the frequency cap in
the `privateData` object, which will also be passed into `bidding.js`. By comparing
the frequency cap to the passed in value from `browserSignals`, the `bidding.js`
function can choose to return a bid of `0`, effectively preventing the ad from
being shown.

### c. Impression Recencies

Another potential addition to `browserSignals` is how recently a particular ad has
been shown to the user, or even a list of the N most recent timestamps an ad has
been shown:

```
{
  'ad-impression-recencies': [ts1, ts4, ts7, ts10],
  'advertiser-impression-recencies': [ts2, ts3, ts5, ts6, ts8, ts9, ts11],
}
```

In addition to being useful as a predictive signal for machine learning models,
these timestamps can also be used more granularly inside the browser by the
[`generate_bids()`](https://github.com/SemanticSugar/TERN#5-generating-bids) function
to obviate the need for the `'max-times-per-minute'` and `'max-times-per-hour'`
fields in the [advertisement data](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site)
JSON object. This smoother control will allow for more dynamic pricing a less
clumped approach to ad delivery. For example, parameters like

```
{
  'max-times-per-minute': 1,
  'max-times-per-hour': 5
}
```

could just lead to five ads being shown in the first five minutes of an hour.
A sophisticated `generate_bids()` function can ensure this is distributed more
evenly (or less!) as dictated by an optimization algorithm.
  

----------------

## 5. Generating Bids

From here, each ad that is in the browser (interest-based and contextual) needs to
be evaluated for pricing before being passed into the auction. This is largely similar
to the TURTLEDOVE proposal. A DSP's `bidding.js` has a signature of:

```
generate_bid(adSignals, publisherSignals, browserSignals) {
  ... // all sorts of logic
}
```

The `adSignals` object is the exact same object from [section 1](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site)
that is the input for `.writeAdvertisementData(input)`. This ensure that the `generate_bid()`
function has as many signals about the ad as possible, including the crucial `privateData`
object that can contain probability estimates, frequency caps, blocklists of interest groups
for negative targeting (for example, that a user has already converted). Note that the `groups`
object is also passed in, which allows for this "negative targeting."

The `publisherSignals` object is extracted from the [`publisherResponse`](https://github.com/SemanticSugar/TERN#b-the-ssp)
object that comes from the DSP key matching this `generate_bid()` call. This is an opportunity to apply bid
modifications on whether the ad is above the fold, or if an advertiser has brand safety concerns,
and doesn't want their ads shown on pages about particular topics (this blocklist for the
advertiser would be in the `adSignals`' `privateData` object. If there was no `publisherResponse`
object, the `publisherSignals` object here would be `{}`.

Finally, there's the [`browserSignals`](https://github.com/SemanticSugar/TERN#4-browser-signals) object
that supplies data for other critical bid modifiers, including frequency capping.

We believe at this point, DSPs will be well-equipped to produce bid prices that maintain as much
advertising efficacy, publisher revenues, and user privacy as possible.

----------------

## 6. The Auction

Finally, there's the matter of the auction. This may be contentious, but we propose that the
internal auction in the browser be a second price auction. This used to be the standard in the
industry until header bidding precipitated a shift to first price auctions.

Unfortunately, first price auctions are subject to significant game theoretic distortions. When
determining the price of a bid, the concern of the advertiser is to extract as much economic
utility as possible. As with any exchange of money, there is some point at which the purchaser
would neither gain nor lose any utility. We call this the "true value." It's not an acceptable
price to bid in a first price auction, because the purchaser gains nothing from the purchase.

Therefore, a bid in a first price auction must be less than this true value. However, it must not
be so low as to be below the price of the market, otherwise the purchaser will not win the auction.
Ergo, the goal of bidding is to bid as little above the going rate on the market as possible, while
being below the true value.

TURTLEDOVE (and TERN) do not provide any mechanism for buyers to get an insight into the going
rates of the market. They are not notified of any losses, and in a first-price scenario, what
they pay is solely a function of their own bids.

Second price auctions avoid this quandary, by having the highest bid paying the second-highest
bid in the auction. When auctioning off a single item, second price auctions are mathematically
proven to have a winning strategy of bidding the true value. Given the lack of insight into the market,
and also the increased complexity of the `bidding.js` function in a first price auction due to game-theoretic
modifications, we strongly recommend moving back to second price auctions as the standard in the
industry.

The concern of publishers, of course, is that second price auctions can reduce win prices,
particularly if purchasers are in collusion. This is why in the [`publisherRequest`](https://github.com/SemanticSugar/TERN#a-the-publisher-request)
object, we specify that the `floor-price` set by the publisher is a required field to be
sent to the SSP, and consequently, all DSPs. This effectively makes a publisher a bidder
in its own auction, guaranteeing a minimum second price. Note that this does not alter the
dominant strategy of other partipants from bidding their true value.

Second price auctions are a superior mechanism for keeping participants honest, ensuring entities
with deeper knowledge of market prices don't have significant advantages in the auctions,
and reducing the amount of computation that will have to occur on users' machines.

A further benefit of second price auctions is that it removes any incentive to use win price as a vector of entropy to
try and identify users. If the winner never receives back the bid price they used, but the price of second bidder
instead, it only becomes possible to inject information if all bidders collude.

----------------

## 7. Rendering the Ad

Once the auction is run and the winning ad is selected, it needs to be rendered. We believe
it makes sense for these ads to be rendered in a [fenced frame](https://github.com/shivanigithub/fenced-frame/blob/master/README.md).
However, some other proposals, such as [Product-level Turtledove](https://github.com/jonasz/product_level_turtledove),
suggest that the browser itself should be responsible for the logic of assembling dynamic
creatives.

We're not in favor of this. We believe it will limit the flexibility that dynamic creatives
offer to the ecosystem. Rather, we suggest that the rendering logic be provided by:

```
'ad-cbor-url': 'https://dsp.example/ads/ad-123456789.wbn'
```

and that this web bundle be given access by the browser to the other objects necessary to
render the ad, such as:

```
'products': {'product-id-1': 'https://dsp.example/products/product-id-1.wbn',
             'product-id-2': 'https://dsp.example/products/product-id-2.wbn'}
```

This will enable such logic as tying the category of the product(s) to the category
of the page, providing a better user experience and greater ad efficacy. This is just
an example; there are likely to be more reasons that the ad web bundle itself should
have these data available for it to be rendered as the DSP sees fit.

----------------

## Considered Alternatives

### a. [TURTLEDOVE](https://github.com/WICG/turtledove/)

TURTLEDOVE is the basis of this proposal, but we feel it is not fleshed out enough, and
also required some extensions to support some heavily-used aspects of the adtech ecosystem,
including product recommendations, third-party tags, creative review process, and limitations
on interest group sizes that are too severe for meaningful optimization.

We believe that TERN addresses all these concerns while still maintaining the same level of
privacy that TURTLEDOVE accomplishes.

### b. [Product-level Turtledove](https://github.com/jonasz/product_level_turtledove)

We adopted the core approach of Product-level Turtledove in TERN. The main departures are
the creative review process, and eliminating the scrambling of ordered product recommendations
in the creatives themselves. Ranking is extremely important for optimization, and the main
concern addressed by the scrambling is to prevent "creepy" ads from being assembled ad hoc while
avoiding review. To us, this appears to be a very minor concern given the impact of removing
effective ranking.

A creative review process is provided in TERN, but functions more similarly to what we see
today. We think the approach here is plenty robust and will enable the removal of bad actors
from the market.

### c. [Outcome-based Turtledove](https://github.com/jonasz/outcome_based_turtledove)

We also adopted the core approach from Outcome-based Turtledove for providing more granular
bidding signals within the browser. Really, the main difference is that we just renamed the
object from `userSignals` to `privateData` to 1) recognize that more than just user signals
can be provided (e.g. campaign frequency caps, category blocklists, etc.), and 2) that the
name explicitly describes that these data are not to leave the browser.

The other major proposal in Outcome-based Turtledove is the ask that ads have a number of
attempted deliveries on a sufficiently sized set of users before they can actually be
displayed. We're not supportive of such a mechanism due to its strong, negative implications
for small advertisers and the platforms they run on. There are many such advertisers on the
market today, generally represented by marketplaces such as Amazon, Rakuten, and Yelp. These
small merchants deserve an opportunity to advertise to their potential customers on the
internet, where these users have likely discovered them. These marketplaces deserve an
opportunity to offer their merchants a digital advertising product on the web. This is an
instance where both small and large players can be substantially impacted for the same
underlying cause.

### d. [SPARROW](https://github.com/WICG/sparrow)

We have also considered SPARROW. In principle, we're supportive of what SPARROW aims to
accomplish. Our main issue with the proposal is the trusted, third-party servers that are
responsible for executing machine learning models.

Upon our consideration, we were left with a bunch of unresolved questions:

- Who would be responsible for these servers? Running real-time bidding systems is expensive
and requires years of knowledge to fully develop.
- How would payment be structured for DSPs running on these servers? Traffic seems like one
way, but some models are larger and more computationally complex. Presumably, since there's
now a third party, costs for RTB would increase.
- We regularly ship large models (in the tens of gigabytes) multiple times daily. Across all
players in the market, would we expect this third party to be able to scale well?
- Given the broad array of types, complexities, and sizes of models throughout the market,
how would this third party guarantee suitable instances for all players? Would there be
shared tenancy? How would resource contention be resolved?
- How would a DSP have any introspection into the live performance of their models? Sometimes
software with bugs gets shipped and requires a quick rollback. This seems like a very real,
significant risk.
- Given all of the above, how will such a service be live within the stated timeline for
the deprecation of third-party cookies?

Without clear resolutions to these questions, we're much more supportive of a TURTLEDOVE-like
approach, of which TERN is an example.

----------------

## FAQ

### a. Where does machine learning fit in?

Before writing the advertisement data JSON as described in [section 1](https://github.com/SemanticSugar/TERN#1-on-the-advertisers-site),
a model can be applied server-side to generate predictions which can be packed into the
`privateData` object. For example:

```
privateData = { 'ad-ctr': 0.0134,
                'conversion-value': 12.50 }
```

Then, in the [`publisherResponse`](https://github.com/SemanticSugar/TERN#b-the-ssp), the
`publisherSignals` object can be used to pass signals related to the page or ad slot:

```
publisherSignals = { 'ad-slot-ctr': 0.00597,
                     'page-categories': ['news', 'sports'] }
```

Both of these objects will be passed into the [`generate_bid()`](https://github.com/SemanticSugar/TERN#5-generating-bids)
function, where arbitrary logic can be used to combine these signals into a final bid price.

### b. How do I stop a campaign from spending?

You can use the `publisherSignals` object in the [`publisherResponse`](https://github.com/SemanticSugar/TERN#b-the-ssp)
object to define a blocklist of campaigns:

```
publisherSignals = { 'stopped_campaigns': ['campaign123', 'campaign456'] }
```

The [`privateData`](https://github.com/SemanticSugar/TERN#i-more-refined-bidding-signals-and-reporting-signals)
object can contain the campaign ID attached to the particular ad:

```
privateData = { 'campaign_id': 'campaign456' }
```

Then, the [`generate_bid()`](https://github.com/SemanticSugar/TERN#5-generating-bids) function can contain
logic like:

```
if adSignals.privateData.campaign_id in publisherSignals.stopped_campaigns:
  return 0;
```

### c. How do I apply frequency caps or optimization?

Inside the [`privateData`](https://github.com/SemanticSugar/TERN#i-more-refined-bidding-signals-and-reporting-signals)
object, you can specify frequency parameters and/or a frequency cap:

```
privateData = { 'frequency_optimization': { 0: 1.0,
                                            1: 0.9,
					    2: 0.6,
					    3: 0.4,
					    4: 0.1 },
		'frequency_cap': 4 }
```

The browser supplies the frequency for the ad in [`browserSignals`](https://github.com/SemanticSugar/TERN#4-browser-signals),
in the `ad-day-frequency` field:

```
browserSignals = { 'ad-day-frequency': 4 }
```

Then, the [`generate_bid()`](https://github.com/SemanticSugar/TERN#5-generating-bids) function can contain
logic like:

```
if browserSignals['ad-day-frequency'] >= privateData.frequency_cap:
  return 0
else
  bid *= privateData.frequency_optimization[browserSignals['ad-day-frequency']]
  return bid
```
