# Wildfire Prevention with Satellite Image Analysis

Washington State experiences thousands of wildfires every year. My goal for this project is to plant the seed for a product or service that can scan through satellite data in order to identify areas at risk for wildfires. While I start this project with a focus on Washington State, it can easily be expanded to data from the entire world. The users of this product would likely be state governments interested in being able to prevent wildfires in their state.

This repository contains data collection, exploratory data analysis, and several convolutional neural network models used to predict whether or not a location is susceptible to wildfires. There is also a notebook previewing implementation of the neural network for real world applications. The data for this exploration consists of roughly 20,000 labeled satellite images. 10,000 of the images are locations which have experienced wildfires, while the other 10,000 have never seen a wildfire before.

The structure of this repository is as follows:
- Posing the Question: First I needed to understand exactly how I wanted to pose the question of how to address wildfires
- Data Collection and Cleaning: I could not find adequate off-the-shelf data sets on areas that have had wildfires, so I needed to collect these images myself and clean other related data.
- Exploratory Data Analysis: It's always important to visualize the data you're working with in order to understand it.
- Initiating a Baseline Model: My first model used a simple artificial neural network at just over 50% accuracy. This needed improvement.
- Building a More Sophisticated Model: My second and final model is a convolutional neural network. I believe this model is about as good as can be expected with the data I'm using.  I acheived 69% test accuracy with this model. 
- Model Evaluation: It's important to also find information like recall and accuracy when it comes to the model's efficacy of identifying wildfire prone areas. I used confusion matrices for this as they are the most effective visualization for the job.
- Deployment: I built a simple method of testing the model through a Jupyter Notebook file.  The user inputs latitude and longitude, and the system runs it through the API call and neural network to tell you wildfire risk.
- Conclusions and Finding Areas for Improvement: 69% accuracy is great for messy real world data, but there is room for improvement. I hope to come back to this model with more questions, better satellite imagery, a stronger neural network, and a more effective deployment system soon!


For this project, I used the Google Static Maps API to collect satellite imagery for roughly 12,000 locations that have seen wildfires in the past 12 years. For each latitude and longitude set (sourced from the Washington State DNR [here](https://data-wadnr.opendata.arcgis.com/datasets/dnr-fire-statistics-2008-present-1/data)), I plugged the location data into the Maps API to pull and download each image. For the non-wildfire images, I simply used a randomly generated set of 10,000 longitude and latitude pairs existing in Washington. This is how I sourced my labeled data for this project. Examples below:

__Areas with wildfires:__

![text](example_images/wf1.jpg)

![text](example_images/wf2.jpg)

![text](example_images/wf3.jpg)

__Areas without wildfires:__

![text](example_images/nwf1.jpg)

![text](example_images/nwf2.jpg)

![text](example_images/nwf3.jpg)

While I was unable to collect satellite imagery of the site a few days before the fire, I believe this will suffice as a proof of concept, especially since areas that experience wildfires often experience them again. Essentially, I will be training the neural network to recognize areas that are prone to wildfires. There's room for improvement here in terms of finding images to label as 'wildfire prone', but I believe this is a good start, especially since the data can be replaced later. I'm currently waiting on API access to some more advanced satellite image services, and when access is granted, I will re-download with more accurate imagery.

# Exploratory Data Analysis

Before diving into the neural network, here's a glimpse at the state of wildfires in Washington. This first map shows a sample of wildfires by size. Yellow points to smaller wildfires, orange means medium sized, and red circles are the largest wildfires.

![Imgur](https://i.imgur.com/FnWfVNk.png)

As you can see, many of the largest wildfires take place in central Washington, while the smaller and medium sized wildfires are scattered around the state more evenly.

This next map shows wildfires by cause. Yellow means lightening, blue means debris, and red means arson.

![Imgur](https://i.imgur.com/jRITn47.png)

It's interesting to see where the clusters of arson are. This is another insight police and fire departments can use to prevent fires in their areas.

# Neural Network

For this project, I chose to use a convolutional neural network. It's the industry standard for image recognition as it is able to pick up patterns and distinguish different images from each other. A convolutional neural network works by using filters that scan through images. At first, these filters are randomly weighted, but as the model learns and is refined, the filters begin to pick up patterns like edges, lines, shapes, or even color intensity (in the case of RGB images). I tried several versions of the convolutional neural network, and by the end, I had one that I was satisfied with. 

The model turned out to be 77% accurate on the training set and 69% accurate on the test set.  While this is not stellar, I think it is reasonably accurate given how much of Washington is covered in relatively dry, flammable forest.  As you can see in the confusion matrix, much of the loss in accuracy is driven by the high false positive rate.  While this is not ideal, it's understandable given how many images in the non-wildfire category are still at moderate risk of wildfire.

Below is the chart showing training and testing accuracy and loss, as well as the confusion matrices for the training and test sets:

![Imgur](https://i.imgur.com/19Mb4YI.png)

![Imgur](https://i.imgur.com/5BQCV55.png)

![Imgur](https://i.imgur.com/fnKzt76.png)

At the end of training, my model was able to accurately predict wildfire risk of new locations as fed into the system. For example, I fed in the longitude and latitude of a location of a wildfire in California (the model has not seen any images from California so I thought it would be an interesting test), and it correctly identified the area as high risk.

![Imgur](https://i.imgur.com/iqeEwGF.png)

# Further Work

In the future, there are several things I would like to try:
- Satellite imagery of wildfire locations a day before the fire started. This would make my training data quite a bit more accurate, as it would train the model to recognize locations right before they went up in flames.
- A web app or service that scans through satellite databases in real time to warn fire departments of risky areas. With my current resources, this is not quite feasible in terms of API costs or computational power.

# Conclusion

There's a ways to go before this project is fully deployable on a national or international level, but I believe it's a great start for a different take on wildfire prevention. Hopefully in the future, this project can be fully deployed and used by fire deparments around the world. As I gain more expertise in handling image recognition tasks and collecting satellite imagery from more complex and thorough sources (e.g. NASA), I can't wait to come back to this project and develop the neural network to make it more and more accurate!

Thanks for reading, and please let me know if you have any questions or comments!

-Thomas Brown
