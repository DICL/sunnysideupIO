---
layout: post
title:  "What is SunnySideUP"
date:   2016-05-29 17:07:08 +0900
categories: jekyll update
---

# Ourselves
SunnySideUp is a big data start-up located in UNIST, South Korea. 
Our mission as an entreprise is to provide a cutting-edge solutions for Big Data processing.

# Our organization
SunnySideUp was founded in DICL Lab (UNIST) as an organization which monetize 
research projects related to big data. 

# Our products
Among the several projects being develop in DICL lab, few of them aim to become a possible 
comercial product. At this moment, we are developing a big data framework formed by two main products:
EclipseMR for data processing, EclipseDFS for data storage, and EclipseSQL for fast distributed database querying.

Important mention for EclipseMR as being the most advance product in our lab. Our benchmarks (published in research papers) 
shows that EclipseMR is 10x faster than standard _MapReduce_ current solutions in the market.

EclipseMR is an MapReduce framework written in C++ using a novel spatial caching and scheduling technique.

Here is a snippet of a simple _MapReduce_ application to count the lines in a large file.

{% highlight c++%}

int main () {
  DataSet& A = DataSet::open("FileA");
  DataSet& B = A.map([](string line){ 
   return {"Total", to_string(line.length())};
  });

  B.reduce([](string a, string b){ 
    int total = atoi(a.c_str()) + atoi(b.c_str());
    return to_string(total);
  });
}

{% endhighlight %}

# Our business model
Being computer scientists we love open source, all of the backbone components of our framework is
released under Apache License 2.0. 

Our revenues comes from documentation, support, and mostly fine tailored solutions for specific problems (finance, medical solutions)

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
