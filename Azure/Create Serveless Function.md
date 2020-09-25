
>Important
>This is using Windows to host the Azure Functions

## Create Serveless Function that is trigger by HTTP Call

[Create Serverless Function with API Gateway](http://jamesgriff.in/index.php/2018/03/04/creating-serverless-api-azure-functions-monetising-api-management/)

>NOTE
>Need to create an Azure Blog storage and updload image to the Blog storage.  
>Each time you make change to Azure Functions click on the URL on the Azure Functions Overview page to warm up the Function(s) before you test the function to see if it works.

## Create Serveless Function that is trigger by HTTP Call with setting up a Pub/Sub using Azure Service Bus

[Create Serverless Function to Publish](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-output?tabs=csharp)

>NOTE
>Need to create an Azure Service Bus (a basic one works) then create a queue to publish a message too.  

Do not use the HTTP Trigger method parameter in the above microsoft doc. Use the HTTP Trigger method parameter setup seen below

```C#
        [FunctionName("FunctionPublisher")]
        [return: ServiceBus("imagequeue", Connection = "AzureSBConnection")]
         public static string FunctionPublisher([HttpTrigger(AuthorizationLevel.Function, "post", Route = "{Publish}")] HttpRequestMessage request, ILogger log)
       
        {
            log.LogInformation($"C# Publish Message");
            string jsonContent = request.Content.ReadAsStringAsync().Result;
            log.LogInformation($"This input {jsonContent}");
            
            return jsonContent;

        }
```
When sending a request, make sure if has a "body" field in the request.

```json
{
  "body":"Testing Publish"
}
```

Get the Service Bus connection from the SharePolicy section in the Azure Service Bus you create earlier. Once you have the connection, go to the Function Overview page 
then the Configuration section and add a new configation. Name the Key = "AzureSBConnection" and Vaule = *the Service Bus connection you got from the SharePolicy section*

Now you should be able to publish a message.

## Create Serveless Function that is trigger by Service Bus Message

Within the same solution as the Message Publisher that was created in the previous section, create a new function. You use the code below.

```C#
        [ServiceBusAccount("AzureSBConnection")]
        [FunctionName("SubscribeToMessage")]
        public static void Run([ServiceBusTrigger("imagequeue")] string myQueueItem, ILogger log)
        {
            log.LogInformation($"C# ServiceBus queue trigger function processed message: {myQueueItem}");

        }
```

Once you publish the Subscriber function to Azure, go to the Functions section and select the Subscribe function. Go to the Code and Test section and 
expand the Log section at the bottom of the screen. 

Try publishing a message using the HTTP Function and you should see in the Logs window the message you Published with the HTTP Function that publishes messages.

