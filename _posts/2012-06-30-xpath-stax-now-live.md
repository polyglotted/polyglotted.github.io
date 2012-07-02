---
layout: post
title: XPath-Stax parser is now live in Maven Central Repository
---

{{ page.title }}
================

<p class="meta">30 Jun 2012 - London</p>

[Polyglotted.org](http://www.polyglotted.org) is dedicated to solving big data issues
and one of the recent concerns we faced was to process thousands of large XML
files processed by different batch jobs. 

Since the data was processed by support personnel, we had to allow 
[XPath](http://www.w3.org/TR/xpath/) expressions for building easier jobs. Naturally 
the concern was to efficiently parse the large files (typically 3-5 GB) in size.
Stackoverflow search led us to this blog post on [Conveniently processing large xml
files](http://andreas.haufler.info/2012/01/conveniently-processing-large-xml-files.html) 
and we liked the approach and decided to use the source.
 
Our jobs had specific performance expectations as to run within 30 minutes of time 
and in a constrained environment with only 4GB of RAM available. The servers
were beefy machines with 24 cores, so we could easily parallelize our application.
Given the default behavior of SAX parsing model to be not safe for multiple thread 
access, we had to resolve to STAX parsing. However when we processed our files, 
we started running out of memory and the application could not cope up. 

The main issue with the above source is that it still creates a lot of DOM objects 
which are really heavy weight when processing multiple thousands of them. We had to
write our own implementation, which is light weight and uses little to no memory
for processing. Next came the requirement from a different sources to be map our
returned data into simple POJOs and we decided to map them to existing 
[JAXB](http://www.oracle.com/technetwork/articles/javase/index-140168.html) bindings. 

Both the base parser and the bindings are limited in scope, as they do not have 
access to the entire document in memory. However the code is usable and so we decided
to release them to the open source.

Documentation for xpath-stax can be found at [Polyglotted.org](http://www.polyglotted.org/xpath-stax)

xpath-stax-1.0.0 is now live at [maven repository](http://search.maven.org/#browse%7C-1206644886)

You can find the source code for the library at [github](https://github.com/polyglotted/xpath-stax)

Please feel free to comment on the library and contribute changes


