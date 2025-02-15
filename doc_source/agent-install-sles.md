# Manually install SSM Agent on SUSE Linux Enterprise Server instances<a name="agent-install-sles"></a>

Connect to your SLES instance and perform the following steps to install the AWS Systems Manager Agent \(SSM Agent\)\. Perform these steps on each instance that will run commands using Systems Manager\. You can perform the installation using either a `zypper` command or an `rpm` command\.

**To install SSM Agent on SUSE Linux Enterprise Server**

1. **Option 1**: Use a `zypper` command:
   + Run the following command:

     ```
     sudo zypper install amazon-ssm-agent
     ```
   + Enter `y` in response to the prompt\.

   **Option 2**: Use an `rpm` command\.
   + Create a temporary directory on the instance\.

     ```
     mkdir /tmp/ssm
     ```
   + Change to the temporary directory\.

     ```
     cd /tmp/ssm
     ```
   + Run the following commands one at a time to download and run the SSM Agent installer\. 

     *region* represents the identifier for an AWS Region supported by AWS Systems Manager, such as `us-east-2` for the US East \(Ohio\) Region\. For a list of supported *region* values, see the **Region** column in [Systems Manager service endpoints](https://docs.aws.amazon.com/general/latest/gr/ssm.html#ssm_region) in the *Amazon Web Services General Reference*\.

     Intel 64\-bit \(x86\_64\) instances:

     ```
     wget https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_amd64/amazon-ssm-agent.rpm
     ```

     ARM 64\-bit \(arm64\) instances:

     ```
     wget https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_arm64/amazon-ssm-agent.rpm
     ```

1. Run the following command to determine if SSM Agent is running\. The command should return the message amazon\-ssm\-agent is running\.

   ```
   sudo systemctl status amazon-ssm-agent
   ```

1. Run the following commands if the previous command returns the message amazon\-ssm\-agent is stopped\.

   1. Start the service\.

      ```
      sudo systemctl enable amazon-ssm-agent
      ```

      ```
      sudo systemctl start amazon-ssm-agent
      ```

   1. Check the status of the agent\.

      ```
      sudo systemctl status amazon-ssm-agent
      ```

**Note**  
If you're unable to download the agent from the AWS Region you specify, use one of the following global URLs\. Even though the following URLs show 'ec2\-downloads\-windows', these are the correct URLs for Linux operating systems\.  
Intel 64\-bit \(x86\_64\)  

  ```
  https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm
  ```
ARM 64\-bit \(arm64\)  

  ```
  https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_arm64/amazon-ssm-agent.rpm
  ```

**Important**  
An updated version of SSM Agent is released whenever new capabilities are added to Systems Manager or updates are made to existing capabilities\. If an older version of the agent is running on a managed node, some SSM Agent processes can fail\. For that reason, we recommend that you automate the process of keeping SSM Agent up\-to\-date on your machines\. For information, see [Automating updates to SSM Agent](ssm-agent-automatic-updates.md)\. Subscribe to the [SSM Agent Release Notes](https://github.com/aws/amazon-ssm-agent/blob/mainline/RELEASENOTES.md) page on GitHub to get notifications about SSM Agent updates\.