---
published: true
title: So, we love Jupyter & SAS...
layout: post
---
### Contents
* ##### [Some Background and Motivations](#backstory)
* ##### [What's in it for you](#tasks)
* ##### [Before you actually start](#note)
* ##### [Python and Google Trends](#pygoogletrends)
* ##### [Forecasting using SAS within Jupyter](#sasforecasting)
* ##### [Tying it all together with visualization](#visuals)
* ##### [Document workflow with Jupyter and share results](#convert)
* ##### [Concluding Thoughts](#thoughts)

##### <a name="backstory">Thoughts and Motivations</a>
Read on if you do or even if you don't. Chances are you'll love what you see.

People enjoy doing certain things as a part of their jobs. One such thing for an analytics professional is to be able to work with the
best in class tools to deliver top-notch decision support solutions while tapping
into their scientific training. We are simple beings, looking to deliver complex
things as simple stories. After all, I struggle to remember even one data point if it has to be explained
in more than a 3 dimensional co-ordinate plane. In fact, most people that we know have similar problems. The reason is, as humans our ability to process complexity is limited. But we still solve extremely complex problems. We do all this by breaking them down in smaller pieces and solving it one piece at a time.


In general, most people enjoy, relish and look forward to opportunities where they can work with tools that best allow them to express their creativity without limiting their problem solving capabilities. Something that encourages a fluent thought-to-execution paradigm. In fact, this expectation is true for most practitioners - the need to minimize <u> thought-to-execution friction</u> is probably the single biggest productivity requirement in corporate America.

 In most mature analytically advanced organizations this need makes data science professionals to constantly look for solutions that best allow them to express themselves swiftly,
efficiently and with the least amount of friction (learning curve) while making sure they make no compromises on the end product. This becomes imperative as the scope of your data science team widens and the impact you make in the organization
increases. In fact, we all know that learning from data quickly and efficiently
gives your organization not just the competitive advantage but sometimes, the best chance of survival.
This is especially true as most organizations don't have the luxury of time for
data science teams to go on a "learn while you do" fun ride.

What all of this means is that as a data scientist / advanced analytics professional, the best that you can do is to focus your energies on
learning just the best in class tech and marrying such tech all along your delivery pipeline/ workflow.

And so, when I heard about the SAS kernel and extensions for Jupyter, I was thrilled.
This now meant that the most well researched/ tested and documented analytics procedures on the planet from the
top advanced analytics vendor (SAS) can be easily integrated into my favorite open source tool (the Jupyter Notebook).
I could now use my python scripts along with SAS procedures & JS charts to do what we all love to do - delight our
users.

##### <a name="tasks">So, WIIFM /What will I get out of this?</a>
*************
*<font color="black"> <b> If you're thinking what's in it for me, read the Q&A below to get a sense of what the rest of the post tries to accomplish</b></font>*

1. How can I write something that might be custom to my org and execute that from a notebook?
  * In most cases, typical data prep involves writing transformations to massage the data in the context that best makes sense for your analysis step. But for this post, we'll work with web data. Specifically, we'll use one of my python modules that extracts data from google trends programmatically.

2. How do I integrate the results with my favorite SAS procedures?
  * We'll see how to use PROC ARIMA that ships with SAS ETS to build forecasts using ARIMA models on the data we collect from *Step1* above. In
  general, this can be any SAS procedure that you have access to across Machine Learning, Forecasting, ETL and Data Mining depending on the nature of the problem you're trying to solve.

3. How can I export the results so we can visualize the data using a JS charting library?
  * We'll see how you can leverage the Highcharts API for your visualization needs.I use this as I find that it's simple to prep web ready time series visuals. But essentially, your options are plenty here. SAS comes with a powerful set of visualization tools with strong statistical analysis capabilities. Similarly, there are a plenty of great open source visualization packages. You can go as fancy as you like but the point here is to demonstrate extensibility and the power of the Jupyter+SAS+Python combo while _highlighting_ how you can quickly go from thought to execution while delivering a top-notch work product!

Finally we'll touch a bit on nbconvert and the basics of nbconvert to show how to export all your good work and serve it up in other formats.

********************

##### <a name="note">Before you start :</a>
>If you are a commercial SAS user who is interested in doing any of this (or to simply follow along),
make sure you have the SAS kernel and extensions for Jupyter installed (only available for Linux at the time of this post). If you just want the link to get this done - [here](https://github.com/sassoftware/sas_kernel).
If you'd like a bit more information on SAS and Jupyter and why - [check out this cool piece!](http://blogs.sas.com/content/sasdummy/2016/04/24/how-to-run-sas-programs-in-jupyter-notebook/)



##### <a name="pygoogletrends">Python and Google Trends</a>

First things first, we need to get some data. Maybe some dummy data that can still be useful. Useful enough to get our imaginations flying.

What ever your area of work is or the nature of your business is, insights from Google searches can tell profound stories. In the past, people I've worked with have asked - wouldn't it be cool if we could somehow tap into Google Trends Data ? So, to make things interesting, let's do just that. Get google trends data programmatically (no point in getting manual dumps of data on a csv file - it's no fun if you have to do this once a week for example) and cook-up some dummy data based on the trends.

We'll use the gtrends python module. You can pick it up from my github repo [here](https://github.com/datasciencemonkey/gtrends) or even simpler, download a copy of the .py [script](https://github.com/datasciencemonkey/gtrends/blob/master/gtrends/gt_parser/gTrendsParser.py). Make sure you read the README file on the repo to understand how to apply this to whatever you might be interested in querying.

**Note:** If the set up stuff bothers you, worry not! Simply download the [sample notebook](https://github.com/datasciencemonkey/sas_n_python/blob/master/Load_SAS_from_Python.ipynb) that covers all of this with SAS models in Jupyter.

Methods that matter on the gtrends module that give you the data set you need, once you've imported the script into your workspace.

```python
import pandas as pd
from gt_parser import gTrends_Parser
google_terms = 'amazon, ebay' # Example Terms
myParserObject = gTrends_Parser(google_terms)
myParserObject.get_raw_data_blobs()  # Sends a get request and collects the data
myParserObject.full_blob_dict  # has the entire data blob as a raw un-processed object
myParserObject.table_data_dict  # has just the raw data
myParserObject.get_column_names()  # parses and displays the column names
myParserObject.get_row_values()  # parses and displays row values
myParserObject.get_data_frame_raw()  # reads and converts data into a raw data frame - Dates still need to be processed
final_frame = myParserObject.get_data_frame_processed()
```
Our data frame now looks like this. Clearly, some amount of post processing is needed - so, that is what we'll do

<img src="https://datasciencemonkey.github.io/images/final_frame.png" style='width:100%;' border="0" alt="Null">

*The image above talks a bit about visualization but let's park that part for just a bit (We'll come back to it soon).*

But from a data stand point, this results in a pandas data frame that has the data we need to generate the dummy time series data.

From here, our **dummy visitation data** can be generated easily like this:

```python

final_frame['amazon_visits']=0
final_frame['ebay_visits']=0
def dummy_data_builder(frame,scalar=1000000):
    for i in range(len(frame)):
        frame['amazon_visits'][i] = frame['amazon'][i] *(scalar + random.randint(1,10000))
        frame['ebay_visits'][i] = frame['ebay'][i] *(scalar + random.randint(1,10000))
    return frame
# to see if we get the dummy data
sas_frame = dummy_data_builder(final_frame)  
```

The sas_frame has the data that we need to forecast the dummy visitation data using time series modeling techniques.

Next, we move this data into a SAS library after converting the pandas data frame into a csv file. This process is extremely simple, so let's move on to the juicy part - utilizing SAS procs inside jupyter.


##### <a name="sasforecasting">SAS Forecasting in Jupyter</a>
If you are a seasoned analytics pro, you know by now SAS produces a phenomenal array of forecasting products like SAS Forecast Server for High Performance Forecasting, SAS ETS for Econometrics and Time Series Analysis & Forecasting etc. These products coupled with SAS Studio/ Enterprise Guide/Forecast Server Studio greatly simplify the forecasting process by providing easy to use "canned tasks" or walk through GUIs that generate the SAS code for you. So, if you are lazy like me, use these code generating tools to your advantage. Pick up the code and stick it right into your Jupyter notebook! From there, if you want to tweak this to your heart's content - sure, you always have the official user guide and the procedure documentation to fall back to.

For this particular post, we'll simply use PROC ARIMA here to demonstrate the use of *<u>SAS within Jupyter</u>* capability - but if you want to delve deep into Time Series Modeling topics (which is a huge topic in itself & beyond the scope of this post), check out other SAS reference materials. Notice that %%SAS is used to invoke the SAS Jupyter cell magic.

```sql
%%SAS
/*Import the data file that we just created*/
proc import datafile="dummy_data.csv"
     out= sashelp.dummy_fsct_data
     dbms=csv
     replace;
run;
/*Print to see the data we imported*/
proc print data = sashelp.dummy_fsct_data (obs=4) ;
run;

/*Run ARIMA & generate forecasts */
proc arima data=sashelp.dummy_fsct_data plots
    (only)=(forecast(forecast ))
        out=sashelp.amz_dummy_visits_fcst;
    identify var=amazon_visits(12);
    estimate p=(1) (12) q= (12) method=ML;
    forecast lead=12 back=2 alpha=0.05 id=cal_date interval=month;
    outlier;
run;

proc arima data=sashelp.dummy_fsct_data plots
    (only)=(forecast(forecast ))
        out=sashelp.ebay_dummy_visits_fcst;
    identify var=ebay_visits(1);
    estimate p=(1)(12) q= (12) method=ML;
    forecast lead=12 back=2 alpha=0.05 id=cal_date interval=month;
    outlier;
run;
```
Again, this could have been any SAS procedure that you have access to & is relevant to your problem. I just happened to pick a time series example for this post because of my liking for the SAS forecasting tools & the "quick bang for the buck" nature of these tools. While I use only SAS ETS here (as a glimpse into what's possible), by using SAS High Performance forecasting one can automate the entire forecasting process very easily. You can do things like model selection bake-offs based on an optimizing metric from a slew of possible models, include dependent variables (i.e. add potential causals), define & automate transformations, include events for all types of effects, set up automatic outlier detection etc.

Finally we combine the forecasts we just generated and prep them up for visualization.

```sql
%%SAS
proc sql;
create table sashelp.dummy_visits_fcst  as
select a.cal_date, a.ebay_visits, a.forecast as ebay_forecasts,
b.amazon_visits,b.forecast as amazon_forecasts
from sashelp.ebay_dummy_visits_fcst a inner join
sashelp.amz_dummy_visits_fcst b
on a.cal_date = b.cal_date;
run;
quit;
```

##### <a name="visuals">OK, Let's get the results and visualize them</a>
Now that we've obtained the forecasts, let's make a web ready,interactive, time series visualization from the results.

We use the highcharts api for this and a little python module (pandas-highcharts) to help us accomplish this easily. Your choice could be plotly/matplotlib/gplot or ggvis or even D3 depending on your preference, but once again - following the theme of the post, we'll keep things simple and elegant.

<img src="https://datasciencemonkey.github.io/images/forecasting_animation.gif" style='width:100%;' border="0" alt="Null">


Now, that is not just simple but it is pleasing to the eye & interactive! All inside the Jupyter Notebook!

I did skip the part of moving the SAS results into the pandas dataframe, but you can see that in the [notebook here](https://github.com/datasciencemonkey/sas_n_python/blob/master/Load_SAS_from_Python.ipynb).

##### <a name="convert">Great! Time to share our story!</a>
As a bonus, let's see how to share your glittering analysis in a variety of formats, thanks to a little Jupyter extension - **nbconvert!**
Nb convert allows you to convert your analysis to html/latex/pdf or even [revealjs slides](http://lab.hakim.se/reveal-js/#/).

The basic idea is simple. Install nbconvert and then install reveal-js locally and then run the following command to convert the jupyter notebook into slides from the directory where you have your notebook.

```bash
jupyter nbconvert <my_notebook.ipynb> --to slides
```
This will produce a .slides.html file on the same folder. You can then simply serve this up during your presentation to get produce these type of [results](http://lab.hakim.se/reveal-js/#/). You can also easily change the themes and transitions. Beyond this, you can automate the whole process quite easily. Maybe I'll show that in another post.