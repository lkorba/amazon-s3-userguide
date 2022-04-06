# Delete an empty Amazon S3 bucket using an AWS SDK<a name="example_s3_DeleteBucket_section"></a>

The following code examples show how to delete an empty Amazon S3 bucket\.

**Note**  
The source code for these examples is in the [AWS Code Examples GitHub repository](https://github.com/awsdocs/aws-doc-sdk-examples)\. Have feedback on a code example? [Create an Issue](https://github.com/awsdocs/aws-doc-sdk-examples/issues/new/choose) in the code examples repo\. 

------
#### [ \.NET ]

**AWS SDK for \.NET**  
  

```
        /// <summary>
        /// Shows how to delete an Amazon S3 bucket.
        /// </summary>
        /// <param name="client">An initialized Amazon S3 client object.</param>
        /// <param name="bucketName">The name of the Amazon S3 bucket to delete.</param>
        /// <returns>A boolean value that represents the success or failure of
        /// the delete operation.</returns>
        public static async Task<bool> DeleteBucketAsync(IAmazonS3 client, string bucketName)
        {
            var request = new DeleteBucketRequest
            {
                BucketName = bucketName,
            };

            var response = await client.DeleteBucketAsync(request);
            return response.HttpStatusCode == System.Net.HttpStatusCode.OK;
        }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/dotnetv3/S3#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/DotNetSDKV3/s3-2006-03-01/DeleteBucket) in *AWS SDK for \.NET API Reference*\. 

------
#### [ C\+\+ ]

**SDK for C\+\+**  
  

```
using namespace Aws;
int main()
{
    //TODO: Change bucket_name to the name of a bucket in your account.
    //If the bucket is not in your account, you will get one of two errors:
    Aws::String bucketName = "<Bucket Name>";
    //TODO:  Set to the AWS Region of the bucket bucket_name.
    Aws::String region = "us-east-1";

    Aws::SDKOptions options;
    Aws::InitAPI(options);
    {
       
        Aws::Client::ClientConfiguration clientConfig;
        if (!region.empty())
            clientConfig.region = region;

        S3::S3Client client(clientConfig);

        Aws::S3::Model::DeleteBucketRequest request;
        request.SetBucket(bucketName);

        Aws::S3::Model::DeleteBucketOutcome outcome =
            client.DeleteBucket(request);

        if (!outcome.IsSuccess())
        {
            auto err = outcome.GetError();
            std::cout << "Error: DeleteBucket: " <<
                err.GetExceptionName() << ": " << err.GetMessage() << std::endl;
        }
        else
        {
            std::cout << "The bucket was deleted" << std::endl;
        }
    }
    ShutdownAPI(options);
    
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/cpp/example_code/s3#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/SdkForCpp/s3-2006-03-01/DeleteBucket) in *AWS SDK for C\+\+ API Reference*\. 

------
#### [ Go ]

**SDK for Go V2**  
  

```
	fmt.Println("Delete a bucket")
	// Delete the bucket.

	_, err = client.DeleteBucket(context.TODO(), &s3.DeleteBucketInput{
		Bucket: aws.String(name),
	})
	if err != nil {
		panic("Couldn't delete bucket: " + err.Error())
	}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/gov2/s3#code-examples)\. 
+  For API details, see [DeleteBucket](https://pkg.go.dev/github.com/aws/aws-sdk-go-v2/service/s3#Client.DeleteBucket) in *AWS SDK for Go API Reference*\. 

------
#### [ Java ]

**SDK for Java 2\.x**  
  

```
        DeleteBucketRequest deleteBucketRequest = DeleteBucketRequest.builder().bucket(bucket).build();
        s3.deleteBucket(deleteBucketRequest);
        s3.close();
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javav2/example_code/s3#readme)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/SdkForJavaV2/s3-2006-03-01/DeleteBucket) in *AWS SDK for Java 2\.x API Reference*\. 

------
#### [ JavaScript ]

**SDK for JavaScript V3**  
Create the client\.  

```
// Create service client module using ES6 syntax.
import { S3Client } from "@aws-sdk/client-s3";
// Set the AWS Region.
const REGION = "REGION"; //e.g. "us-east-1"
// Create an Amazon S3 service client object.
const s3Client = new S3Client({ region: REGION });
export { s3Client };
```
Delete the bucket\.  

```
// Import required AWS SDK clients and commands for Node.js.
import { DeleteBucketCommand } from "@aws-sdk/client-s3";
import { s3Client } from "./libs/s3Client.js"; // Helper function that creates an Amazon S3 service client module.

// Set the bucket parameters
export const bucketParams = { Bucket: "BUCKET_NAME" };

export const run = async () => {
  try {
    const data = await s3Client.send(new DeleteBucketCommand(bucketParams));
    return data; // For unit tests.
    console.log("Success - bucket deleted");
  } catch (err) {
    console.log("Error", err);
  }
};
// Invoke run() so these examples run out of the box.
run();
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javascriptv3/example_code/s3#code-examples)\. 
+  For more information, see [AWS SDK for JavaScript Developer Guide](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/s3-example-creating-buckets.html#s3-example-deleting-buckets)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-s3/classes/deletebucketcommand.html) in *AWS SDK for JavaScript API Reference*\. 

------
#### [ PHP ]

**SDK for PHP**  
Delete an empty bucket\.  

```
$s3client = new Aws\S3\S3Client(['region' => 'us-west-2', 'version' => 'latest']);

try {
    $s3client->deleteBucket([
        'Bucket' => $bucket_name,
    ]);
    echo "Deleted bucket $bucket_name.\n";
} catch (Exception $exception) {
    echo "Failed to delete $bucket_name with error: " . $exception->getMessage();
    exit("Please fix error with bucket deletion before continuing.");
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/php/example_code/s3/s3_basics#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/SdkForPHPV3/s3-2006-03-01/DeleteBucket) in *AWS SDK for PHP API Reference*\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
class BucketWrapper:
    def __init__(self, bucket):
        self.bucket = bucket
        self.name = bucket.name

    def delete(self):
        """
        Delete the bucket. The bucket must be empty or an error is raised.
        """
        try:
            self.bucket.delete()
            self.bucket.wait_until_not_exists()
            logger.info("Bucket %s successfully deleted.", self.bucket.name)
        except ClientError:
            logger.exception("Couldn't delete bucket %s.", self.bucket.name)
            raise
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/s3/s3_basics#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/boto3/s3-2006-03-01/DeleteBucket) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------
#### [ Ruby ]

**SDK for Ruby**  
  

```
  # Deletes the objects in an Amazon S3 bucket and deletes the bucket.
  #
  # @param bucket [Aws::S3::Bucket] The bucket to empty and delete.
  def delete_bucket(bucket)
    puts("\nDo you want to delete all of the objects as well as the bucket (y/n)? ")
    answer = gets.chomp.downcase
    if answer == "y"
      bucket.objects.batch_delete!
      bucket.delete
      puts("Emptied and deleted bucket #{bucket.name}.\n")
    end
  rescue Aws::Errors::ServiceError => e
    puts("Couldn't empty and delete bucket #{bucket.name}.")
    puts("\t#{e.code}: #{e.message}")
    raise
  end
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/ruby/example_code/s3#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.aws.amazon.com/goto/SdkForRubyV3/s3-2006-03-01/DeleteBucket) in *AWS SDK for Ruby API Reference*\. 

------
#### [ Rust ]

**SDK for Rust**  
This documentation is for an SDK in preview release\. The SDK is subject to change and should not be used in production\.
  

```
pub async fn delete_bucket(client: &Client, bucket_name: &str) -> Result<(), Error> {
    client.delete_bucket().bucket(bucket_name).send().await?;
    println!("bucket deleted");
    Ok(())
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/rust_dev_preview/s3#code-examples)\. 
+  For API details, see [DeleteBucket](https://docs.rs/releases/search?query=aws-sdk) in *AWS SDK for Rust API reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, see [Using this service with an AWS SDK](UsingAWSSDK.md#sdk-general-information-section)\. This topic also includes information about getting started and details about previous SDK versions\.