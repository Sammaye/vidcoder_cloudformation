Cloudformation Video Encoder Example (aws_worker)
=======================

This is a Cloudformation template example for video encoding to be used in conjunction with the aws_worker repository made by @Sammaye [here](https://github.com/Sammaye/aws_worker).

There are a few things you need to know in order to use this template.

## S3 Bucket Policy

It does not include the bucket policy for S3. I could not seem to get it to work even with the tutorials and examples so you will have to add it yourself each time you produce a new cluster.

This means you only need to set the policy every time you delete and remake a cluster, not every time you update one (unless you use a differently defined user then you do).

Here is an example policy you can use:

	{
		"Version": "2008-10-17",
		"Id": "UploadWorker",
		"Statement": [
			{
				"Sid": "Stmt1295042087538",
				"Effect": "Allow",
				"Principal": {
					"AWS": "arn:aws:iam::663341881510:user/VideoEncoder-WorkerUser-3498584dd" // You can get this easily by looking at the permissions on your SQS queues and copying the user mentioned there
				},
				"Action": "s3:*",
				"Resource": "arn:aws:s3:::videos.x.co.uk/*" // This is your bucket. Replace videos.x.co.uk with your bucket name
			}
		]
	}

## Template holders to be replaced

There are some template holders to be replaced with your own content:

- your_input_queue_name_here

This is your actual input queue name, i.e. my-videos

- your_input_queue_url_here

This is the URL of your input queue, i.e. https://us-west-2.queue.amazonaws.com/6/my-videos

- your_output_queue_url_here

This is the URL of your output queue, same as above but for your output queue.

There; everything else is for your tweaking pleasure. Have fun!