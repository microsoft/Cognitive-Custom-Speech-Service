
# Cognitive Speech Service samples

Here you can find a set of audio data and language data for testing the [Microsoft Cognitive Services Custom Speech service](http://cris.ai).

## How it works?

The samples are a collection of data, both acoustic and language, which you can use to try out the Custom Speech service. The audio files (.wav) and transcript files should help you to get started with the service.

Simply clone this repository with 
```
git clone https://github.com/Microsoft/Cognitive-Custom-Speech-Service.git
```
on the comandline.

Then go to the folder of the sample you like
```
cd <sample_folder>
```
If you have Powershell 5.0 installed you can use in Powershell the *Compress-Archive* cmdlet
```
Compress-Archive -Path '<sample_folder>\Test Data\Test Acoustic Data\*.wav' -DestinationPath data.zip
```

This will create a zip file containing all wav files without additional folder information as a flat list.

If you do not have Powershell installed you can use a zip tool of your choice but you have to zip the files as a flat list without path information.

Now, you have everthing prepared to get started with [Custom Speech service](http://cris.ai).

There is a [help page](http://cris.ai/help) describing how to use the service or you can find some help [here](https://www.microsoft.com/cognitive-services/en-us/Custom-Speech-Service/documentation/Home).

## Biology Sample

### Introduction

The biology sample is a great example of how powerful a custom language model can be for your application. 

### Data

The sample consist of approximately 150 statements about organisms that lived primarily in Triassic and Jurassic period. The names are in scientific form which rarely appear in everyday language. The facts are described in the ‘Language Data.txt’ file.
In addition, the sample contains approximately 50 audio utterances (50 .wav files) which can be used to test the above model using the offline testing feature during deployment. There is a transcriptions.tsv file associated with those audio files that captures the transcriptions of each one of them. If you open the file you will see that it contains key value pairs where the name of the file is the key and the transcription the actual value. You can .zip those audio files and import them along with the associated transcription file using the ‘Import Acoustic Data’ menu option.

### Modelling

You can use the ‘Language Data.txt’ file to create a language model on Custom Speech Service and deploy it along with an acoustic baseline model of the two available. Simply upload the file using the ‘Import Language Data’ and create a new Language model via the ‘Create Language Model’ menu option.
Once you have created a language model you can deploy it via the ‘Deployments’ menu option.
During deployment of your custom model you can tick the ‘Offline Test’ option. Point to the acoustic data you uploaded in the previous step. The model deployment process will start and once deployed the audio utterances will be tested against the newly deployed endpoint. The audio utterances will be send for transcription and the results will be displayed. 

### Results

As part of the results page you will see a set of numbers along with a list of transcriptions (as many as the audio files you uploaded). Read the transcriptions to get a feel of the quality of the results. The numbers serve as a comparison between the baseline model and the custom model that you created. They demonstrate transcription accuracy both from the baseline and the custom model. Remember that the transcriptions.tsv contains the correct transcriptions of all the audio files, so internally our system compares those against both the baseline and the custom models. The improvement over baseline for this sample is typically around 70% and the overall accuracy of the custom is close to 90%. Needless to say that with a richer language model accuracy can potentially go up.
