# Transcribe-AI

This is a serverless project for automatic transcription and summarization using AWS services like Cognito, API Gateway, Lambda, S3, and DynamoDB.

Is made to serve long videos, and in particular non-english speakers content.

![Alt text](<transcribe-ai aws architecure.png>)

## Table of Contents 

- [About the Project](#about-the-project)
- [Getting Started](#getting-started)
- [How it Works](#how-it-works)
- [Usage](#usage)
- [Acknowledgements](#acknowledgements)

## About the Project

This AWS-based serverless architecture provides a user-friendly platform for uploading files that get automatically transcribed and summarized large videos. S3 presign URLs make sure the files are securely uploaded directly to S3. All the file processing is done in the backend using AWS Lambda functions.

## Getting Started

Before you can use this project, you need to setup an AWS account and configure your local environment with AWS CLI. Check [AWS CLI Configuration](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html) for more information.

## How it Works

1. Users login with Cognito and upload a large file (defined size max 200 MB): When user send the video, a resta API is called to get a presign s3 upload URL with a lambda. This URL returns to the frontend and then another call is made to the presign S3 URL to upload the video.
2. When the video is uploaded triggers a lambda, and from here a state machine is triggered which is a pipeline of Lambda functions to process the file, call Whisper API Model for transcription, summarize the results using Open AI model, and save the data in DynamoDB.
3. Amazon SES is used to email the user once their file has been processed. Thus, user receive transcription and summary of the video.

## Usage

This project can be used for any application where automated transcription and summarization services are needed. It's built on serverless architecture, which makes it highly scalable and cost-efficient.

To use this service, you need to login with your Cognito credentials, upload your file, and wait for an email with your transcriptions and summaries.

See the `usage.md` for more information on how to interact with the service.

## Acknowledgements

This project uses [whispert APIs](https://openai.com/research/whisper) for transcription  and [OpenAi models] (https://platform.openai.com/docs/models) for summarization, and service and uses [mjml.io](https://mjml.io/try-it-live/H3c6xeeanK) to create HTML templates for emails


