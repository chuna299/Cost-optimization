# AWS Cloud Cost Optimization - Identifying Stale Resources

## Identifying Stale EBS Snapshots

In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

### Description:

The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.


**challenges faced:**
1. Task timed out after 3.01 seconds
  Sol: We need to change the timeout value to 10 seconds in the General configurations.
2. "errorMessage": "An error occurred (UnauthorizedOperation) when calling the DescribeSnapshots operation: You are not authorized to perform this operation
   Sol: We need to provide the policy of full EC2 access and snapshots for the role to describe the snapshots and delete the snapshots. Role is present in the under the policies.
