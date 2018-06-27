---
title: Speech To Text Tutorial | Microsoft Docs
description: Tutorial to use Speech to Text
services: cognitive-services
author: PanosPeriorellis
manager: onano

ms.service: cognitive-services
ms.technology: Speech to Text
ms.topic: article
ms.date: 04/16/2018
ms.author: panosper
---

# Getting Started with Speech to Text Customization

In this tutorial, you will create one acoustic model and one language model that we will evaluate and test using the Congitive Service Speech SDK. 

#Preparation

The data for this tutorial are on [GitHub](https://github.com/Microsoft/Cognitive-Custom-Speech-Service/tree/master/Samples/Sample1%20-%20Biology). Please download this data to your local desktop and let's start the tutorial.

# Step 1: Upload the Data

In this step you will prepare the data to be uploaded on the Speech to Text portal. Follow these instructions:

1. Go to https://cris.ai and login using your MSA
2. From the menu named 'Custom Speech' click and select 'Adaptation Data'
3. In the Adaptation Data View click 'Upload' button

    ![The Upload View](../../../../tree/master/media/Datasets.jpg)

4. Type a frieldly name for your data set in the box 'Name'
5. Optionally provide a description
6. Choose the locale. It is important to note here that once the data is uploaded the locale cannot change
7. Click the 'Browse' button associated with the transcritions file (.txt) and select the transcritpion file named "adaptation_transcriptions.txt" from the data you earlier downloaded
8. Click the 'Browse' button associated with the Audio files (zip) and select the .zip file named "adaptation_acoustic_data" .
9. Click the Import button located next to the Acoustic Datasets  

The view will change back to the main "Datasets" view and the progress of the upload will be shown. Monitor the Status label. When it changes to completed the data can be used.

![Dataset Uploaded View](media/DatasetUploaded.jpg)

Now let's do the same for the language data.

Again Under the section 'Language Datasets' Click the Import Button. The view will change again to that of the Language Import.

1. Enter an alias name for your language data
2. Enter an description (this steo is optional)
3. Carefully select the locate
4. Click on Browse, locate and click on the dataset named 'LanguageAdaptationData.txt'
5. Click Create and observe the new view featuring the progress of the langauge dataset upload.
6. When the status changes to complete the data can be used

>[!NOTE]
You can edit some of the details of the uploaded data such as Name and Description. Locale cannot be changed. If this is the case then you need to upload the data again following the aforementieond process. 

Now that the data is uploaded let us adapt some models.

# Step 2: Adaptation

In this step we will first create an a custom acoustic model followed by a language model using the data we uploded. At the end of this step we will be ready to evaluate our newly created models. 

Adaptation is carried out for acoustic and language models in separate distinct steps. One can adapt only an acoustic or a language model or both. In this tutorial we adapt both. Let us start.

1. From the menu named 'Custom Speech' click and select 'Acoustic Model'
2. In the Acoustic Model View click 'Create' button

    ![Acoustic Model Creation View](media/AcousticModelCreationView.jpg)

3. Provide a frieldy name to the model in the Name text box
4. Optionally Provide a description 
5. Pick the locale
6. Pick the baseline model you want to adapt
7. Click Create

>[!NOTE]
Pronunciation does not require a separate adaptation. The language data along with the pronunciation file are part of the language adaptation process.

# Step 3: Evaluation

We have adapted 2 models and now we are ready to evaluate them. We will evaluate them separetely and we will evaluate both together. We will carry out a total of 3 evaluations. This is generally useful to understand where the biggest impact over baseline is gained. Let us start. First we need to upload our acoustic data.

Following the process we described for Data Import please upload the data set entitled 'Acoustic Test Data'. Once this is completed carry out the following instructions:

1. From the menu named 'Custom Speech' click and select 'Accuracy Tests'
2. In the Accuracy Tests View click 'Create' button

    ![Accuracy Test Creation View](media/AccuracyTestCreationView.jpg)

3. Provide a frieldy name to the model in the Name text box
4. Optionally Provide a description 
5. Pick the locale
6. Pick the baseline model you want to adapt. Note here that you will immediately see all the models that have been adapted using that baseline
7. Pick the Acoustic Model we created
8. Pick the baseline language model 
9. Click Create

Observe that the view changes and the status of the evaluation is indicted by the Status label. When completed the following screen shows that Word Error Rate (WER) achieved using that model against our acoustic data. 

>[!NOTE]
WER is an industry standard for measuring accuracy rates. It is percieved as strict.

# Step 4: Deployment

We have 2 models and we have also identified which combination of those is the best for our production system. Let us now deploy the model.

1. From the menu named 'Custom Speech' click and select 'Deployments'
2. Click 'Create' button.
3. Observe the view presented. Select the locale
4. Type a friednly name for your deployment
5. Optionally provide a description
6. Select your subscription under which you want to deployment your model

>[!NOTE]
It is important to note here that a free subscription only provides quotas for testing rather than putting a model into production

7. Leave content log in as default. This will create a deployment through which all content send to the model as well as transcriptions will be logged
8. Select the base model 'Microsoft Conversational Model'
9. Select both the acoustic and the language model we adapted.
10. Accept the terms and click 'Create'

![Deployment Creation View](media/DeploymentCreationView.jpg)

In the screen presented you see a table with all your deployments. You can observe the locale, name, description, the date it was created, its status and a list of actions represented by 4 links. 'Delete' enables you to delete the deployment at any time. You do not lose the models or any of the work we did earlier. 'Delete' basically decommissions the deployment and stops incurring charges. In addition you can 'Edit' the name and description fields. 'Details' show the endpoint details and finally -since we let the logging option to default- you can see an option to delete the log data. These are the audio uploaded to the endpoint as well as the transcriptions.

Now let us have a closer look on the 'Details' link.

![Deployment Details View](media/DeploymentDetails.jpg)

You can view here table with the endpoint details for websocket and HTTP Rest access. At the top of the table you can view also the Subscrition Key which is used to authenticate access to that endpoint.

Let us look at the endpoints in turn.

There are 2 HTTP REST APIs one for interactive mode and one for dictation which provides punctuations. These endpoints provide final results only.

There are 2 WebSocket with the .NET/Android/iOS client library endpoints which allow us to upload audio up to 15 seconds or up to 2 minutes while both supporting dictation mode

There are additionally 2 WebSocket with the .NET service library endpoints supporting either short or up to 10mins of audio while both supporting dictation mode

and finally there are 3 WebSocket with the Speech Protocol/JavaScript WebSocket API endpoints that support the aforementioned features.

To authenticate and use the Web Socket endpoints have a look at our [Client SDK library](https://github.com/Microsoft/Cognitive-Custom-Speech-Service/tree/master/Samples/Sample1%20-%20Biology

>[!NOTE]
If you do not want any logs to be traced you can select the appropriate option during the 'Deployment Creation' phase. If a deployment has been created with the default option to log and your requirements change then you would need to delete that deployment and create a new one with the required option selected.

# Calling the Endpoint
Now that you have the endpoint you cna use the Speech Services SDK to download

# Step 5: Further samples
Now that we have the endpoint deployed let us use the SDK we downloaded in the initial step and upload some audio.

The SDK is fairly straight forward to use. In the code below we instantiate our recognizer and set up our call back methods.

`SpeechRecognizer recognizer = this.factory.CreateSpeechRecognizer(file);`
`recognizer.IntermediateResultReceived += this.OnCarbonPartialResponseReceivedHandler;`
`recognizer.FinalResultReceived += this.OnCarbonFinalResponse;`
`recognizer.SynthesisResultReceived += this.OnCarbonSynthesis;`

For a richer set of samples check out the ![Speech Services SDK()]

# Conclusions
* [Get Started](cognitive-services-custom-speech-get-started.md)
* [FAQ](cognitive-services-custom-speech-faq.md)
* [Glossary](cognitive-services-custom-speech-glossary.md)

