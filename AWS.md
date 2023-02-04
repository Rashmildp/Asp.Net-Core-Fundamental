# AWS

## AWS Lambda
AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you.

Run your codes without worying or managing servers.


## serverless architecture

A serverless architecture is a way to build and run applications and services without having to manage infrastructure

## AWS Cognito

Onboarding platforms which utlizes the AWS cognito and lambda to help Onboarding of any application easier. On other word, this process utlizes the users signing and signup.

## User pools.

Like a database that saves all the user credentials such as user name , email address like that.

 **Create endpoint in user management to genetate access token/refresh token based on user's username and password for authentication.**

 ```bash
export.put = async(event,context,callback)=>{
    try{
     const {email,password}=JSON.parse(event.body);
     var params = {
     AuthFlow = '',
     AuthParameters :{
     USERNAME : email,
     PASSWORD : password,
     },
     ClinentId : process.env.USER_POOL_CLIENTID,
     UserPoolId: process.env.USER_POOL_ID,
     };
     const response = await cognitoidentityserviceprovider
                      .adminInitiateAuth(params),
                      .promise();
    callback(null, {
      statusCode :200,
      headers:{
      'Access-Control-Allow-Origin':'*',
      },
      body:JSON.stringyfy(response.AuthenticationResult),
    }
    );

      }catch(error){
      console.error(error);
      }
}

 ```

## Amazon EC2

Amazon Elastic Computer Cloud (Amazon EC2) provides scalable computing capcity in the amazon web services.

Features. 

1. Virtual computing environment , known as **instances**.

2. Storage volumes for temporary data that's **deleted** when you stop hibernate, or **terminate** your instance, known as instance store volumes.




![Screenshot 2023-02-04 192341](https://user-images.githubusercontent.com/64850016/216772035-18435bf9-ca01-446a-a559-8dd2caa215e1.png)

### instances

An instance is a virtual server in the cloud. 

Its configuration at launch is a copy of the AMI that specified when launched the instance.

Can launch different types of instances from a signle AMI.

Each instance type offers different compute and memory capabilities.

### AWS Credentails validation.

```bash
async function valiadateCreds(body){
var sts = new AWS.STS({apiversion:'2011-06-05',
accessKeyId : accessKeyId,
secretAccessKey: body.secretAccessKey
});
try{

const k = await sts.getCallerIdentity({}).promise()
return k;
}catch (e){
console.log(e);
throw e;
}
}



```



     






















