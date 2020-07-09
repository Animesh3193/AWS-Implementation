# AWS-Implementation
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

