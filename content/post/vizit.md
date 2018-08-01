+++
title = "MDS Capstone Project: Visualizing Massive Open Online Courses"
date = 2018-01-01T10:18:54-07:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "/post/vizit/how_long_video.png"
caption = ""
preview = true

+++
After eight months of coursework, the [UBC Master of Data Science](https://masterdatascience.science.ubc.ca/) (MDS) concludes with a 2-month [Capstone project](https://ubc-mds.github.io/capstone/about/).
 Our group's project focused on analyzing data from UBC's
[massive open online courses](https://en.wikipedia.org/wiki/Massive_open_online_course) (MOOCs). UBC offers dozens of MOOCs to thousands of students through the [edX platform](https://www.edx.org/school/ubcx). Unlike in-person classes, in a MOOC the instructor cannot observe student engagement directly. Instead, they must infer student engagement from recorded events. An example of course event would be a user pausing a video. A single course can record millions of events in its lifetime. [Ido Roll](http://ctlt.ubc.ca/people/ido-roll/) from UBC's [Centre for Teaching, Learning, and Technology (CTLT)](https://ctlt.ubc.ca/) mentored our project. Our task was to help MOOC instructors understand their students through a dashboard.

## Goals

The purpose of this project was to help answer five questions about the UBC MOOCs:

1. Who are my students?
2. How do students watch/use course videos?
3. What are students talking about in the discussion forums?
4. How well are my students doing on problems and assignments?
5. What supplementary material are my students using?

We built quick prototypes for course instructors to provide feedback. This feedback helped us decide which directions to take the dashboards in. 

## A Tour of the Dashboards

Below I describe four of the visualizations included in our project. You can find more information [here](https://andrewlim1990.github.io/edx_dashboard_documentation.github.io/index.html).

### Demographics

![Education Bar Plot](/img/post/vizit/level_of_education.png)

A common question that instructors asked was, "Who are my students?" One can filter this visualization by gender, engagement time, and if a user paid for the course. We chose the bar plot for many of our visualizations. Bar plots provide instructors with an easy way to interpret the distribution of data. This bar plot shows the number of users at each education level in a course.

### Video Watch Rates

![Video Length](/img/post/vizit/how_long_video.png)

We received feedback that our more complicated video plots were difficult to interpret. Our solution was to provide this simple bar plot to anchor the instructor. This plot shows where the video appears in the course (the start of the course is at the top) and how long the videos were. We found that if we included the names of the videos on the plot, it looked too busy. To remedy this, we use a mouseover to display the name and more detailed information. 

### Detecting High and Low Watch Rates

![Video Expectation](/img/post/vizit/high_low_video_rates.png)

In all the courses we observed, users watched the first video more than any other. We also found that users watched the first 30 seconds of a video more than any other segment. Thus, showing video watch rates would echo these trends. This plot attempts to highlight the video segments that deviate from this expectation. We create a linear regression model to find the expected watch rate for each video segment in each video. We then display the deviation of the actual watch rate from the expected one. 

### Forums Word Cloud and Bar Plot

![Forum Dashboard](/img/post/vizit/forum.png)

No existing edX dashboard shows the topics that forum users are discussing. To remedy this, we created a linked bar plot and word cloud. The bar plot shows where student activity occurs. The word cloud shows the most prominent topics that they discuss. The instructor can drill down into a section by clicking a bar, which will update the word cloud.

## Future Plans

These dashboards are available for all UBC MOOCs. If you would like them integrated into your course, please contact a member of the CTLT. In the future, we want to build dashboards for in-person classes as well.

If you would like to contribute to the project, you can look through our code [here](https://github.com/AndrewLim1990/mooc_capstone_public).

## Lessons Learned

The amount of data in these courses made this project was challenging. One of the most valuable things I learned on this project was how to build data pipelines. We had learned about cloud computing and Docker in class, but deploying a massive project can be tricky. Another difficulty of the project was that no two courses were the same. This data diversity encouraged us to make plots that would be as robust to variations as possible. 

I also learned the importance of getting rapid feedback. Our original plots only made sense to us after we had explained them in person. Each iteration made our visualizations more intuitive. The goal of data visualization is not to make the most complicated plots, but the most intuitive ones. 

## Acknowledgments

I would like to thank Ido Roll and Sarah Perez from UBC CTLT, and the users who provided feedback during the development of these dashboards. I would also like to thank my fellow team members [David Laing](https://laingdk.github.io/), [Andrew Lim](https://andrewlim1990.github.io/) and [Subi Zhang](http://subizhang.com/), as well as our Teaching Fellow mentor [Giulio Dalla Riva](http://gvdallariva.net/). 
