# dicered
There are two approaches for this solution:

Approach 1:

Step 1: Setup S3 bucket at AWS for a static website (dice.red).  Setup with versioning enabled.  Setup with 90 days (i.e. for 3 months) deletion policy for previous version files.  S3 has auto-scaling so load balancing is not an issue.  It is cost-effective than using EC2 for static web pages. (URL: https://s3.amazonaws.com/dice.red/index.html)
Step 2: Registered domain dice.red at Route 53 with two SSL certificates for each www.dice.red and dice.red.
Step 3:  Setup up CloudFront to redirect http to https for both CNAME: dice.red and www.dice.red
Step 4:  Installed and setup Jenkins server at AWS in one EC2 node.  http://35.182.227.60:8080/
Step 5:  Assigned IAM Role with S3 full access to EC2.
Step 6:  In Jenkins is set FreeStyle build with S3 publisher plug-in  and Git plug-in installed.
Step 7: https://github.com/criticalisland/dicered is connected for the build and GitHub hook trigger for GITScm polling is selected.   
Step 8:  Run the build Artifact-copy to test.

Approach 2:

Steps 1-3 from above.
Step 4: Instead of Jenkins, I used https://gitlab.com/dicedotred/snappaytest for repo and pipeline.  Set up for CICD is in it.
Environment variables for S3 are stored in settings to secure.
