---
layout: post
title: 'Provenir - A semantic web application for art provenance'
---

TL;DR - [Provenir](http://provenir.herokuapp.com)

One of the courses I am enrolled with, this semester at USC, deals with principles involved in information integration on the web and concepts of semantic web. Semantic Web aims to inter link and organize all of the information on the World Wide Web in a structured manner. It is built on specifications such as the Resource Description Framework (RDF), Web Ontology Language (OWL), etc.

As a part of the class project for the course, we were suggested to do a project which had art as it's central theme. Me and my partner [Gladon](http://linkedin.com/in/gladon) came up with an idea to build a website, by extracting and integrating data from multiple sources, where a user can search for an art work and get it's provenance information as a timeline. We got in touch with folks at the Getty Research Institute to check if we could get access to their Provenance Index database. We are still waiting to hear back from them. However, we discovered that querying on their website allowed us to download up to about 10,000 provenance records. So, to begin with we decided to query the databases for every alphabet. And we had sizeable data to work with. Since the project involved integration of data across sources, we were looking for other sources where we could get provenance information of art works. We discoverd the National Gallery of Art (NGA) website had provenance information of most of the art works they possess. We decided on NGA as our other data source and scraped most of what we could, off of their site. The art records from NGA were structured compared to the ones from Getty. NGA even had every artist and art work represented by a unique URL. The ones from Getty were text documents.

Typically, an information integration project involves the following phases (to the best of our knowledge), in processing the data:

* Cleaning
* Reconciliation
* Entity recognition
* Merging

Cleaning:

Cleaning of the data involves making sure the data, in whatever format they are in, actually are what they claim to be. Like for example, you may have a comma separated value (CSV) file which has 5 fields : Artist Name, Nationality, Era, Birth date, Death Date. Cleaning such a CSV involves making sure what is in the artist name field is in fact just the artist name, nothing more, nothing less. We had many records from they Getty data source that had "British painter (19th century)" as the artist name. Cleaning also involves making sure all of the information fits a certain format so that our further processing becomes easier. Dates are a typical example where the same data is often represented in different formats.

We resolved these challenges by using a tool called Open Refine - formerly called Google Refine. Open Refine lets you apply regular expressions on data in a iterative and interactive manner. It helps you clean data quickly. We also developed a bunch of our own scripts to massage the data into the format we needed for our further processing.

Reconciliation:

One of the principles of semantic web is to inter-link data. What this means is, suppose my name is represented as Varun S L on a certain site, and Varun S Lingaraju on another site, there needs to be a way to inter-link these two documents representing the same entity, me. This is realised in semantic web using the specifications Resource Description Framework (RDF) and Web Ontology Language (OWL) through the process of reconciliation. Wikipedia, as we all know is huge source of information, and has pages on a wide array of topics. What most of us did not know is, DBpedia. DBpedia is a project, that has all of the information in Wikipedia, in a structured and linked manner.

Now that we had so much of cleaned data, in order to collate the information from both the source, we needed a way to tell that if there were certain entities (in our case, artists and art works) that were present in both the sources. So, we reconciled our data with DBpedia. Now we had a good chunk of, all of the data we started out with, associated(linked) with the actual wikipedia entries for the artist. Using this we managed to reconcile a small portion of the art works.

Entity recognition:

Another aspect of our project, apart form presenting the provenance of art works as a timeline, was to interlink the art works in our database across facets like the era to which the art belonged to, the art dealer through which it moved during it's course, or the artist who created it. In order to do this, we had to categorize all the art works in our database based on these facets. We already had the artist name for the art work, and we also had the era information from the DBpedia reconciliation. What we did not have was the organization, art dealer, current owner and museum information. These information were present in the sale records of these art works. However, we needed a way to recognize these entities from plain text of sale records. We used a service called Open Calais. As Wikipedia puts it, Calais is a service by Thomson Reuters that automatically extracts semantic information from web pages in a format that can be used on the semantic web. So you feed the Calais API your input and it spits out any entitites it recognizes. We fed the Open Calais API the sale records we had from our data sources and we associated the entities Calais recognized with the corresponding art work. So we now had categorized all our data across the three facets.

Merging :

This is where merging the sale records comes into the picture. Of all the sale records we obtained from both the sources, our majoe effort was spent in cleaning the sale records and associating a date to every sale. This was much more challenging than we anticipated. For, the dates were not in the same format (obviously!). Some had terms like after 1936, while some were too specific like 19/6/1954. Again Open Refine and home brewed scripts to the rescue. For every art work, we sorted the dates of the sale on both the sources and then merged them based on dates.

What we discovered was brilliant. Some of the art works now had information that gave a more complete information of an art works provenance than what either of the two sources (Getty and NGA) provided. This is what we had envisioned our project to be and we are happy the project actually achieves that. Of course, the produt is far from being perfect. But we have a prototype that works.

We created a website based on the cleaned, reconciled data that we had and we have hosted it at [Provenir](http://provenir.herokuapp.com). Hope you enjoy using the site as much as we enjoyed creating it. :)
