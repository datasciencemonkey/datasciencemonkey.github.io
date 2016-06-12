---
published: true
title:  For the love of Jupyter and SAS!
layout: post
---
## For the love of Jupyter and SAS!

### Contents
* ##### [Some Background and Motivations](#backstory)
* ##### [What's in it for you](#tasks)
* ##### [Before you actually start](#note)
* ##### [Python and Google Trends](#pygoogletrends)
* ##### [SAS and Forecasting](#sasforecasting)
* ##### [Tying it all together with visualization](#visuals)
* ##### [Document workflow with Jupyter and share results](#nbconvert)
* ##### [Concluding Thoughts](#thoughts)

<a name="backstory"></a>
People enjoy doing certain things as a part of their daily jobs. One such thing for an analytics professional is to be able to work with the
best in class tools to deliver top-notch decision support solutions while tapping
into their scientific training. We are simple beings, looking to deliver complex
things as simple stories. After all, I struggle to remember anything more a point if it has to be explained
in anything more than a 3 dimensional co-ordinate plane. The point is - we all solve problems breaking them down.


I enjoy, relish and look forward to opportunities where I can work with tools that best allow me to express my creativity while not limiting my problem
solving capabilities. This means, that  I am always looking to add tools to my arsenal that allow me to do what I do best - solve problems by
breaking them down into smaller pieces & yet provide the right platform where I can tap into the best of breed tools custom built for a purpose. Something that encourages a quick thought to execution paradigm.In fact this expectation is true with most people.

In most mature analytically advanced organizations, data science professionals are constantly looking for solutions that best allow to express themselves swiftly,
efficiently and with the least amount of friction (learning curve) while making sure they make no compromises on the end product. This becomes imperative as the scope of your data science team widens and the impact you make in the organization
increases. In fact, we all know learning from data quickly and efficiently
gives your organization not just the competitive advantage but sometimes, the best chance of survival.
This is especially true as most organizations don't have the luxury of time for
data science teams to go on a "learn while you do" fun ride.

What all of this means is that as a data scientist / advanced analytics professional, the best that you can do is to focus your energies in
learning just the best in class tech and marrying such tech all along your delivery pipeline/ workflow.

And so, when I heard about the SAS kernel and extensions for Jupyter, I was thrilled.
This now meant that the most well researched/ tested and documented analytics procedures on the planet from the
top advanced analytics vendor (SAS) can be easily integrated into my favorite open source tool (the Jupyter Notebook).
I could now use my python scripts along with SAS procedures & JS charts to do what we all love to do - delight our
users.

So with that intent, my goal for the rest of this post is to show how this can be made possible.

<a name="tasks"></a>

*************
*<font color="red"> If you're thinking what's in it for me, read the Q&A below -</font>*

1. How you could write something that might be custom to your org and execute that from a notebook?
  * I am going to show you a python module that I wrote to work with google trends data programmatically
2. Integrate the results with SAS Analytics. This could your Machine Learning, Econometric or Time Series Forecasting
or Data Mining or Optimization Procedures.
  * I am going to show you how to use simple ARIMA models from SAS ETS to build forecasts
3. Visualize and circulate results in a format that makes sense for you
  * I am going to show how you could leverage the highcharts api for your visualization needs. But essentially your options are
    plenty here. For format conversions - we'll touch a bit on nbconvert and the basics of nbconvert.

********************

<a name="note"></a>

#### **Note**:
---------
>Before we proceed any further, if you are a commercial SAS user who is interested in doing any of this (or to simply follow along),
make sure you have the SAS kernel and extensions for Jupyter installed. If you just want the link to get this done - [here](https://github.com/sassoftware/sas_kernel).
If you'd like a bit more information on SAS and Jupyter and why - [check out this cool piece!](http://blogs.sas.com/content/sasdummy/2016/04/24/how-to-run-sas-programs-in-jupyter-notebook/)

-------------------