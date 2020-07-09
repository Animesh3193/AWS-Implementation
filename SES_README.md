# AWS-Implementation
![alt text](/AWS_SES/images/SES_Logo.png "Simple Email Service Logo")

  Amazon SES is an email platform that provides an easy, cost-effective way for you to send and receive email using your own email addresses and server emails and domains

### Use Cases
  1. Implementing Subscribe and Un-Subscribe system
  2. Transactional or Conformation or marketing emails from a company to customers.
  3. Correspondence emails as such that of yammer group in Tek.
  4. Alerts mail or Support ticket emails internal to the application etc.
    
    *For inventory management we have use it as an alert system and to deliver reports*


### Something to know about
  1. AWS SES email can be sent through two ways i.e. SMTP details generated or through api call through SDK *We use boto3 for python*.
  2. Daily limit of sending mail from SES through the default SandBox is only 200 from external source through either of the above steps mentioned.
  3. As for the default SandBox specified SES Mail can only be sent to people that are subscribed to the sandbox, else to be able to send to any body, request need to be raised to support center with a new case.
  4. From inside an ec2 instance if the application is configured to send email through SES the daily limit changes to 62000 mails per day.
  5. Even the SES email sent or recieved can be stored in S3 storage.
  6. Api calls to SES can be logged using AWS Cloud Trail and SES email sending or recieving can be configured as an event in AWS CloudWatch to trigger different event.

    *We might not use the functionality of point 5 and 6, can be taken up as an enhancement*

#### Initializing
We can create a SES api with provided Boto SDK Tool with Python. Documentation can be found [here](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ses.html)

```python
        import boto3

        def create_ses_client():
            client = boto3.client(
                'ses',
                region_name=settings.AWS_SES_REGION,
                aws_access_key_id=settings.AWS_ACCESS_KEY,
                aws_secret_access_key=settings.AWS_SECRET_KEY
            )
            return client
            
```

#### Adding Email to SES
As this is a default sandbox environment we cannot send mail to any one we wish, until they are added to the AWS email address identity.

We can do by directly requesting in the email verification console of AWS else we can call AWS SES Api *We use Boto SDK here too*

> This is an API Method below
```python
        ses_client = create_ses_client()

        # To use above api to send mail

        sns_client.verify_email_identity(
        EmailAddress='some_valid_email@teksystems.com',
        )

        [Output]: {'ResponseMetadata': {'RequestId': '644eceae-a790-4739-9a88-e7867784398d',
          'HTTPStatusCode': 200,
          'HTTPHeaders': {'x-amzn-requestid': '644eceae-a790-4739-9a88-e7867784398d',
           'content-type': 'text/xml',
           'content-length': '215',
           'date': 'Fri, 03 Jul 2020 03:16:16 GMT'},
          'RetryAttempts': 0}}
```

>This is an AWS Console Method. It can be directly accessed from the [link](https://us-east-2.console.aws.amazon.com/ses/home?region=us-east-2#verified-senders-email:)
**Prerequisites** :- AWS Credential with IAM Permission for SES Should be provided.
AWS Verify Console : 
![alt text](/AWS_SES/images/register_mail.PNG "Registering Email")



#### After adding the email
After the emails are verified , a system generated email is sent which contains a link which is sent to email and when clicked registers the email.
See the following image below for refernce.
Emails Registered : 
![alt text](/AWS_SES/images/verify_email.PNG "List of email")

