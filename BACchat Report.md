Samuel Lee, David Oh, Elisabeth Pillsbury | March 5th, 2018
##COSC 89 Final Project: BACchat
######Overview:

Given an audio sample, our application uses Machine Learning and Watson’s Speech to Text and Tone Analyzer services to determine whether or not an individual is inebriated. There are two ways to analyze speech: you may either upload a pre-recorded sample or record yourself live. 

While we transcribe the audio, we analyze it in real time for various emotional, lingual, and social parameters. It analyzes an audio clip sentence by sentence so it takes a little while for the data to show up on our plot here. When the clip finishes, we run it through our classifier and display the conclusion. 

######Business model & motivation:

BACchat is a web application that uses cognitive computing to deduce whether a person is drunk or sober by their speech. While breathalyzers already exist, they are not as readily available and nearly as fun to use as detecting drunkenness by speech alone. This is where BACchat comes in. We plan on making BACchat a free service that is readily available to anyone from bartenders to undergraduate college students.

######Knowledge sources:

* ml stuff (@sam)
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

* creating own classifier with v little ml knowledge
* integrating js and python
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