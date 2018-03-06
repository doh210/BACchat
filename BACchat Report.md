Samuel Lee, David Oh, Elisabeth Pillsbury | March 5th, 2018
##COSC 89 Final Project: BACchat
######Overview:

Given an audio sample, our application uses Machine Learning and Watson’s Speech to Text and Tone Analyzer services to determine whether or not an individual is inebriated. There are two ways to analyze speech: you may either upload a pre-recorded sample or record yourself live. 

While we transcribe the audio, we analyze it in real time for various emotional, lingual, and social parameters. It analyzes an audio clip sentence by sentence so it takes a little while for the data to show up on our plot here. When the clip finishes, we run it through our classifier and display the conclusion. 

######Business model & motivation:

BACchat is a web application that uses cognitive computing to deduce whether a person is drunk or sober by their speech. While breathalyzers already exist, they are not as readily available and nearly as fun to use as detecting drunkenness by speech alone. This is where BACchat comes in. We plan on making BACchat a free service that is readily available to anyone from bartenders to undergraduate college students.

######Knowledge sources:

* ML (@sam)
Because of the large number of machine learning tutorials and support avaliable in python, we decided to do our machine learning in python3 using scikit learn. 
We followed the tutorial at `https://www.digitalocean.com/community/tutorials/how-to-build-a-machine-learning-classifier-in-python-with-scikit-learn` to get us started. Using this tutorial we were able to structure our data in a similar way. 

A problem that we ran into getting our python machine learning code to interact with our javascript. Using flask, we set up a simple python api that would gather our data. We heavily used stackoverflow for trouble shooting and help to set up this api.

* We adapted BACchat from an open source demo on Github called Real Time Tone Analyzer which was developed by IBM. We made further modifications to integrate our machine learning module, display the results, and upload a pre-recorded audio sample for analysis.

######Tools & techniques:

* watson tone analyzer
* watson speech-to-text
* gaussian naive bayes algorithm
	* In order to train our own classifier, we used the Gaussian Naive Bayes machine learning algorithm on 60 training audio samples gathered from YouTube and a corpus of sober speech recordings from UCSB ranging in length from 20 to 60 seconds -- 30 sample recordings were of sober individuals, and 30 were drunk.

######Organization (how you planned the effort):

* sam did the ml api
* elisabeth did a bit of front end styling
* david and elisabeth collected and analyzed training data
* david and elisabeth created the video


######Difficulties encountered:

* Creating a classifier 

* Integrating JS and Python
We knew that the machine learning almost had to take place in python. We looked into a couple of options such as spawning a child process from the Javascript. However, we found that setting up a simple api would be the most straightforward and correct way of integrating the two parts of our application.

* Sending data from Javascript to Python 
We dealt with significant difficulty when we tried to grab the tone analyzer data and word confidence data and send it the python machine learning api. We wanted the overall tone analysis of the audio clip but the application was configured such that the tone analyzer would request analysis from Watson after every sentence or so. However, after reading through the code, we found that the aggregate of the emotions of the current audio clip could be found. This aggregate was constantly getting updated. Further, there was no indication of when the aggregate was finished getting updated. 
To work around this, we would send this aggregate to the python api as we recieved it from the tone analyzer. This is written to a file 'data.json'. While we never recieved an end signal from when the aggregate was finished updating, we did recieve an end signal from when the websocket that is used for the speech-to-text closed. On the websocket closure, we send a GET request to the api to read in the most recent aggregate data in the data.json and run the ML on it. 

We also wanted to incorporate the word confidence score from the text-to-speech. This data also came in every sentence or so. We wanted to incorporate the overall confidence score for the entire audio clip. We did something similar where we send off the data as we get it and the api stores this data in a text file. However, because the Javascript aplication does not aggregate this data we must aggregate it on the api-side.

* gathering emotion data for entire doc
* running app locally (lots of deprecated packages)
* in using speech-to-text, we lose the tone of the speaker and don't get the best transcription

######Fair assessment of the result:

* 66% accuracy score
* for a proof of concept, def impressive!

######Improvements and further work:

* larger training set
* display confidence rating rather than a binary
* real test subjects (rather than youtube recordings)
* introduce "training mode" to add to ml
* better classification (closer sentence by sentence analysis)
* could include content analysis in our training data
* While BACchat is still in its early stages, we hope that it can be improved by adding training data, displaying a spectrum of drunkenness, and including a training mode so that it may even be used one day as a viable substitute for breathalyzers.
