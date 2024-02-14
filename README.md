# WiresharkAnalysis
<h4>In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.</h4>
<h2 dir="auto" tabindex="-1">Environments and Technologies Used</h2>
<ul dir="auto">
 	<li>Microsoft Azure (Virtual Machines)</li>
 	<li>Remote Desktop</li>
 	<li>Various Command-Line Tools</li>
 	<li>Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)</li>
 	<li>Wireshark (Protocol Analyzer)</li>
</ul>
<h2 dir="auto" tabindex="-1">Operating Systems Used</h2>
<ul dir="auto">
 	<li>Windows 10 (21H2)</li>
 	<li>Ubuntu Server 20.04</li>
</ul>
<h2 dir="auto" tabindex="-1">High-Level Overview</h2>
<ul dir="auto">
 	<li>Create Resources</li>
 	<li>Observe ICMP Traffic</li>
 	<li>Observe SSH Traffic</li>
 	<li>Observe DHCP Traffic</li>
 	<li>Observe DNS Traffic</li>
 	<li>Observe RDP Traffic</li>
</ul>
<h2 dir="auto" tabindex="-1">Actions and Steps</h2>
<div class="group w-full text-gray-800 dark:text-gray-100 border-b border-black/10 dark:border-gray-900/50 bg-gray-50 dark:bg-[#444654]">
<div class="text-base gap-4 md:gap-6 md:max-w-2xl lg:max-w-xl xl:max-w-3xl p-4 md:py-6 flex lg:px-0 m-auto">
<div class="relative flex w-[calc(100%-50px)] flex-col gap-1 md:gap-3 lg:w-[calc(100%-115px)]">
<div class="flex flex-grow flex-col gap-3">
<div class="min-h-[20px] flex flex-col items-start gap-4 whitespace-pre-wrap">
<div class="markdown prose w-full break-words dark:prose-invert light">
<ul>
 	<li>In this tutorial about Network Security Groups and Inspecting Network Protocols, you'll start by creating two VMs on Azure - one Linux and one Windows 10 machine, both with two CPUs and on the same VNET. Then, on the Windows machine, you'll need to download Wireshark (a network protocol analyzer), which can be found at the link provided. After installing Wireshark, you'll filter it to only capture ICMP traffic, which is a protocol used to relay messages about network connection issues and is also used by ping to test connectivity between hosts. By filtering Wireshark to capture only ICMP packets and pinging the private IP address of the Linux machine, you'll be able to visualize the packets in Wireshark.</li>
 	<li>After that we will retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:</li>
</ul>
<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/68747470733a2f2f692e696d6775722e636f6d2f7959474b7541792e706e67.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/68747470733a2f2f692e696d6775722e636f6d2f7959474b7541792e706e67.png" alt="" />
</a>

<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/2-1.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/2-1.png" alt="" />
</a><ul>
 	<li>Attempt to ping google.com and see results</li>
</ul>
<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/3-2.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/3-2.png" alt="" />
</a><ul>
 	<li>Now we initiated perpetual ping from Windows VM to Ubuntu VM</li>
</ul>
<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/4-2.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/4-2.png" alt="" />
</a><div class="group w-full text-gray-800 dark:text-gray-100 border-b border-black/10 dark:border-gray-900/50 bg-gray-50 dark:bg-[#444654]">
<div class="text-base gap-4 md:gap-6 md:max-w-2xl lg:max-w-xl xl:max-w-3xl p-4 md:py-6 flex lg:px-0 m-auto">
<div class="relative flex w-[calc(100%-50px)] flex-col gap-1 md:gap-3 lg:w-[calc(100%-115px)]">
<div class="flex flex-grow flex-col gap-3">
<div class="min-h-[20px] flex flex-col items-start gap-4 whitespace-pre-wrap">
<div class="markdown prose w-full break-words dark:prose-invert light">
<ul>
 	<li>After disabling inbound ICMP traffic, we will no longer receive echo replies from the Linux machine. To block ICMP traffic, we will create a new Network Security Group on the Linux machine and set it to block ICMP. If we want to allow the traffic, we can enable ICMP on the Linux Network Security Groups page in Azure.</li>
</ul>
<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/5-3.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/5-3.png" alt="" />
</a>
<a href="https://vikaspatel.tech/wp-content/uploads/2023/04/6-2.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/6-2.png" alt="" />
</a><div class="group w-full text-gray-800 dark:text-gray-100 border-b border-black/10 dark:border-gray-900/50 bg-gray-50 dark:bg-[#444654]">
<div class="text-base gap-4 md:gap-6 md:max-w-2xl lg:max-w-xl xl:max-w-3xl p-4 md:py-6 flex lg:px-0 m-auto">
<div class="relative flex w-[calc(100%-50px)] flex-col gap-1 md:gap-3 lg:w-[calc(100%-115px)]">
<div class="flex flex-grow flex-col gap-3">
<div class="min-h-[20px] flex flex-col items-start gap-4 whitespace-pre-wrap">
<div class="markdown prose w-full break-words dark:prose-invert light">

&nbsp;
<h3 dir="auto" tabindex="-1" align="center">SSH traffic</h3>
</div>
<ul>
 	<li dir="auto">Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.</li>
 	<li dir="auto">Exit the SSH connection by typing ‘exit’ and pressing [return]:</li>
</ul>
<p dir="auto"><a href="https://vikaspatel.tech/wp-content/uploads/2023/04/8-2.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/8-2.png" alt="" />
</a></p>

<h3 dir="auto" tabindex="-1" align="center">DHCP Traffic</h3>
<ul>
 	<li dir="auto">Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)</li>
</ul>
<p dir="auto"><a href="https://vikaspatel.tech/wp-content/uploads/2023/04/9-2.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/9-2.png" alt="" />
</a></p>

<h3 dir="auto" tabindex="-1" align="center">DNS traffic</h3>
<ul>
 	<li dir="auto">From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:</li>
</ul>
<p dir="auto"><a href="https://vikaspatel.tech/wp-content/uploads/2023/04/10.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/10.png" alt="" />
</a></p>

<h3 dir="auto" tabindex="-1" align="center">RDP traffic</h3>
<ul>
 	<li>To filter for RDP traffic only  use command (tcp.port == 3389)</li>
</ul>
<p dir="auto"><a href="https://vikaspatel.tech/wp-content/uploads/2023/04/11-1.png">
  <img class="alignnone size-full wp-image-180" src="https://vikaspatel.tech/wp-content/uploads/2023/04/11-1.png" alt="" />
</a></p>

<h5 dir="auto">Finally, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT so that you don't incur unnecessary charges. Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.</h5>
<div class="Layout-sidebar" data-view-component="true">
<div class="BorderGrid BorderGrid--spacious" data-pjax="">
<div class="BorderGrid-row hide-sm hide-md">
<div class="BorderGrid-cell"></div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
