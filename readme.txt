IoTCloud
Saturday, November 18, 2017
2:22 PM
 
AWSIoT:
	1.	Aws create login
	2.	AWSIoT -> Get started
	3.	Create a thing – Thing name
	4.	Security Tab - Create a certificate 
	a.	Download certificate files and rt ca(naming convention)
	 
	5.	Security Tab – Select certificate – Actions – Activate
	6.	Security Tab – Policies – Create a policy
	a.	Actions - iot:*
	b.	Resources - *
	7.	Security Tab – Select certificate – Actions – Attach policy created in prev step
	8.	Test tab – Subscribe to a Topic – Enter Topic name – Topic_1
	9.	Act Tab – Create Rule 
	a.	Attribute - *
	b.	Topic – Topic_1
	c.	Condition – Na, since we need all data
	10.	Click on 'Add Rule' and choose Amazon Kinesis Firehose streams
 
 
Amazon Kinesis:
	Firehose:
		1.	Create a Kinesis Firehose
		2.	Source – Direct put mtd(aws iot)
		3.	Destination – Create a new s3 bucket
		4.	Create a new IAM role
	Analytics:
		1.	Create an application 
		2.	Choose an existing stream (it will show the firehose created in previous step)
		3.	Data generate many times
		4.	Identify schema
		5.	Run Sql editor
		CREATE OR REPLACE STREAM "DESTINATION_SQL_STREAM" ("lotNo" integer, "availability" integer, "availableLot" integer, "COL_timestamp" integer, "arrtime" timestamp);
		-- Create pump to insert into output 
		CREATE OR REPLACE PUMP "STREAM_PUMP" AS INSERT INTO "DESTINATION_SQL_STREAM"
		-- Select all columns from source stream
		SELECT STREAM * 
		FROM "SOURCE_SQL_STREAM_001"
		-- LIKE compares a string to a string pattern (_ matches all char, % matches substring)
		-- SIMILAR TO compares string to a regex, may use ESCAPE
		WHERE "availability" =1;
		6.	Create new delivery stream - (from analytics to dashboard)
	Firehose:
		a.	Create a Kinesis Firehose
		b.	Source – Direct put mtd
		c.	Destination – Re-use the s3 bucket
		d.	Use the same IAM role
	Analytics:
		a.	Connect to destination -> select a stream
		b.	Destination source – Destination_stream
		c.	Use existing IAM role
	Quicksight
		a.	QuickSight Signup account name – sinanal
		b.	QuickSight capacity region - US West (Oregon)
		c.	Amazon S3 (1 bucket) - chose parkinglot bucket
	 
 
 
 
Bluemix:
1.	Create new flow/Import flow
2.	Mqtt:
	Mqtt – Topic_1 – Edit
	a.	Enter Topic name
	b.	Enter server name – From aws iot – manage – thing – Interact - Https
 
