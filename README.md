# FEED: Chines Financial Event Extraction Dataset Benchmark

## Abstract

We release a large-scale Chinese financial event extraction dataset FEED, consisting of 31,748 documents on five financial event types derived from the Chinese financial portals, which considers the case of event arguments scattered in multiple sentences and one document containing multiple events. In order to construct FEED dataset, we first extract candidate events from financial announcements by Fonduer. Then we build an event knowledge base using weakly supervised classification, and finally label events via distant supervision. We also verify the usability  of FEED and the distinguishability between baseline models. Empirical results show that FEED is challenging for existing event extraction methods, which indicates that Chinese financial event extraction remains an open problem and requires further efforts.

## Introduction

In order to efficiently build a large-scale Chinese financial EE dataset from massive financial announcements, we propose an approach based on distant supervision. The overview of this approach is illustrated bellow. We first extract candidate events from preprocessed data by Fonduer. Second, an event knowledge base is built using weakly supervised classification method. Finally, we label the events via distant supervision to obtain the FEED dataset.

![Dataset Construction](https://user-images.githubusercontent.com/83271325/136687323-24478485-bb82-45bd-86b5-5e3e8acff150.png)

## Event Knowledge Base
We select the five types of announcements with the most reference value to build our event ontology, namely EquityRepurchase (ER), EquityFreeze (EF), EquityUnderweight (EU), EquityOverweight (EO) and EquityPledge (EP). Each event type defines the event roles including key roles and non-key roles that needed to form a structured event. The key role is the indispensable information to form a legal structured event, while any non-key role could be missing in an event. The event ontology for five types of announcements is shown bellow. 
![Event Ontology](https://user-images.githubusercontent.com/83271325/136688228-0dfe0323-8a16-40f0-b183-d2c00cc02385.png)

And the number of structured events in knowledge base construction for each event type is illustrated as follows:
|Event Type|# Event|# Document|
|:--:|:--:|:--:|
|ER|4,531|3,667|
|EF|1,900|1,168|
|EU|7,343|5,593|
|EO|8,449|5,787|
|EP|24,737|15,533|

## Statistics of FEED
The raw data are company announcements from 2008 to 2018 crawled from the Chinese financial portal East Money (http://data.eastmoney.com/notices/hsa.html) and 31,748 documents containing 46,960 events are obtained. We also manually labeled 900 documents as testing set used for weakly supervision classification and measuring the construction performance of knowledge base. Finally, the 31,748 documents are divide into training set, validation set and testing set randomly according to the ratio of 8:1:1 considering the balance of the number of each event type. The statistics of FEED are shown bellow.
|Event Type|# Document|Training|Validation|Testing|
|:--:|:--:|:--:|:--:|:--:|
|ER|3,667|2,942|360|365|
|EF|1,168|938|120|110|
|EU|5,593|4,453|560|580|
|EO|5,787|4,622|580|585|
|EP|15,533|12,443|1,555|1,535|
|Total|31,748|2,5398|3,175|3,175|

## Examples in FEED
This figure shows an example of extracting multiple events from a document. Different paragraphs in the document correspond to two different events, both of which belong to EP.
![example](https://user-images.githubusercontent.com/83271325/136688391-fdc044b0-28f9-47c6-8dfb-8af587f25f7d.jpg)

