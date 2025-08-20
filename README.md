# Agartha
###### Payload Injection (LFI, RCE, SQLi, with optional BCheck), Auth Issues (Access Matrix, HTTP 403), HTTP-to-JavaScript, and Bambdas
<hr/>

Agartha, specializes in advance payload generation and access control assessment. It adeptly identifies vulnerabilities related to injection attacks, and authentication/authorization issues. The dynamic payload generator crafts extensive wordlists for various injection vectors, including SQL Injection, Local File Inclusion (LFI), and Remote Code Execution(RCE). Furthermore, the extension constructs a comprehensive user access matrix, revealing potential access violations and privilege escalation paths. It also assists in performing HTTP 403 bypass checks, shedding light on auth misconfigurations. Additionally, it can convert HTTP requests to JavaScript code to help digging up XSS issues more.

In summary:

- **Payload Generator**: It dynamically constructs comprehensive wordlists for injection attacks, incorporating various encoding and escaping characters to enhance the effectiveness of security testing. These wordlists cover critical vulnerability classes like SQL Injection (SQLi), Local File Inclusion (LFI), Remote Code Execution (RCE), and now also support BCheck syntax for seamless integration with Burp's BCheck framework.
	- **Local File Inclusion, Path Traversal:** It helps identifying vulnerabilities that allow attackers to access files on the server's filesystem.
	- **Remote Code Execution, Command Injection:** It aims to detects potential command injection points, enabling robust testing for code execution vulnerabilities.
	- **SQL Injection:** It assists to uncover SQL Injection vulnerabilities, including Stacked Queries, Boolean-Based, Union-Based, and Time-Based.
- **Auth Matrix**: By constructing a comprehensive access matrix, the tool reveals potential access violations and privilege escalation paths. This feature enhances security posture by addressing authentication and authorization issues. 
	- You can use the web **'Spider'** feature to generate a sitemap/URL list, and it will crawl visible links from the user's session automatically.
- **403 Bypass**: It aims to tackle common access restrictions, such as HTTP 403 Forbidden responses. It utilizes techniques like URL manipulation and request header modification to bypass implemented limitations.
- **Copy as JavaScript**: It converts Http requests to JavaScript code for further XSS exploitation and more.
- **Bambdas Script Generator**: The feature supports automatic generation of Bambdas-compatible scripts based on user input. It eliminates the need for manual coding, enabling faster creation of custom scripts and streamlining integration with the Bambdas engine.<br/><br/>

Here is a small tutorial how to use.

## Installation
You should download 'Jython' file and set your environment first:
- Burp Menu > Extender > Options > Python Environment > Locate Jython standalone jar file.

You can install Agartha through official store: 
- Burp Menu > Extender > BApp Store > Agartha

Or for manual installation:
- Burp Menu > Extender > Extensions > Add > Extension Type: Python > Extension file(.py): Select 'Agartha.py' file

After all, you will see 'Agartha' tab in the main window and it will be also registered the right click, under: 
- 'Extensions > Agartha - LFI, RCE, SQLi, Auth, HTTP to JS', with three sub-menus:
	- **'Auth Matrix'**
 	- **'403 Bypass'**
	- **'Copy as JavaScript'**<br/><br/>


## Local File Inclusion / Path Traversal
It supports both Unix and Windows file syntaxes, enabling dynamic wordlist generation for any desired path. Additionally, it can attempt to bypass Web Application Firewall (WAF) implementations, with various encodings and other techniques.
- **'Depth'** specifies the extent of directory traversal for wordlist generation. You can create wordlists that reach up to or equal to this specified level. The default value is 5.
- **'Waf Bypass'** inquires whether you want to enable all bypass features, such as the use of null bytes, various encoding techniques, and other methods to circumvent web application firewalls.

<img width="1000" alt="Directory Traversal/Local File Inclusion wordlist" src="https://github.com/volkandindar/agartha/assets/50321735/b457e6c2-0829-4959-84aa-9116886b99f7"><br/><br/>

## Remote Code Execution / Command Injection
It generates dynamic wordlists for command execution based on the supplied command. It combines various separators and terminators for both Unix and Windows environments.
- **'URL Encoding'** encodes the output.

<img width="1000" alt="Remote Code Execution wordlist" src="https://github.com/volkandindar/agartha/assets/50321735/d28c12c9-c6fb-4509-9299-888f3f048c12"><br/><br/>

## SQL Injection
It generates payloads for various types of SQL injection attacks, including Stacked Queries, Boolean-Based, Union-Based, and Time-Based. It doesn’t require any user inputs; you simply select the desired SQL attack types and databases, and it generates a wordlist with different combinations.
- **'URL Encoding'** encodes the output.
- **'Waf Bypass'** inquires whether you want to enable all bypass features, such as the use of null bytes, various encoding techniques, and other methods to circumvent web application firewalls.
- **'Union-Based'** requires the specified depth for payload generation. You can create wordlists that reach up to the given value. The default value is 5.
- The remaining aspects pertain to database types and various attack vectors.

<img width="1000" alt="SQL Injection wordlist" src="https://github.com/volkandindar/agartha/assets/50321735/51a010b6-4d9a-4dc9-a634-b353f6b30b95"><br/><br/>

## BCheck Code Generator
BCheck is Burp Suite's framework for creating and importing custom scan checks. These user-defined checks run alongside Burp Scanner’s built-in routines, allowing you to tailor scans to specific vulnerabilities or testing needs. By using BChecks, you can extend Burp’s scanning capabilities and streamline your workflow for more targeted and efficient assessments.
Now you can generate the code automatically:

<img width="1000" alt="BCheck Code Generator" src="https://github.com/user-attachments/assets/2da25e94-b8d6-441a-baef-1b829f877051">

- You can click the “**Generate the Payloads**” button in the blue box above to create a classic wordlist, which can be used manually in Burp's Intruder or Repeater.
- Now, you also have the option to click the “**Generate payloads for BCheck**” button in the red box to generate the same payloads formatted in BCheck syntax, ready to be used in automated scans.

<img width="1000" alt="BCheck Code Generator" src="https://github.com/user-attachments/assets/c38b5816-2a24-4f13-b3f3-a7c62b3ca236">

After clicking the "Generate payloads for BCheck" button, the BCheck code will be automatically copied to your clipboard.

Next, go to 'Extensions > BChecks > New > Blank' from the Burp Suite menu, and simply paste the generated code.

Your payloads are now integrated into a BCheck. You can either manually send or scan HTTP requests, or initiate a Burp scan that incorporates BCheck controls to automatically test the injection payloads generated by the tool.
- **Manual scanning**: Right-click an HTTP request and select "Send to BChecks Editor". Then click the generated BCheck item and select "Run test".
- **Automatic scanning**: Right-click an HTTP request, choose 'Open Scan Launcher', then go to 'Scan configuration > Select from library > Audit checks – BChecks only'. Close the dialog, and your scan will now run exclusively with the BChecks you have defined.

<img width="1000" alt="BCheck Code Generator" src="https://github.com/user-attachments/assets/0ff1ecf5-1a84-444b-bc6e-7e2d7153dc5d">

**Fine-tuning advises**: The generated code serves as a template and may require some adjustments, as behavior can vary between different applications and servers.

Refining filters—such as specifying HTTP response codes or keywords within responses—can help reduce false positives and make the results more precise and less noisy.<br/><br/>

## Authorization Matrix / User Access Table
This part focuses on analyzing user session and URL relationships to identify access violations. The tool systematically visits all URLs associated with pre-defined user sessions and populates a table with HTTP responses. Essentially, it creates an access matrix, which aids in identifying authentication and authorization issues. Ultimately, this process reveals which users can access specific page contents.
- You can right-click on any request and navigate to 'Extensions > Agartha > Auth Matrix' to define **user sessions**.
- Next, you need to provide the **URL addresses** that the user (HTTP header/session owner) can access. You can utilize the web 'Spider' feature for automated crawling or supply a manually curated list of URLs.
- Afterward, you can use the **'Add User'** button to include the user sessions.
- Now, it's ready for execution. Simply click the **'Run'** button, and the table will be populated accordingly.

<img width="1000" alt="Authorization Matrix" src="https://github.com/volkandindar/agartha/assets/50321735/6f89e22c-e29c-413d-96d8-c2a8d7ac39d4">

A little bit more details:
1. This is the field where you enter the username for the session you provide. You can add up to four different users, with each user being assigned a unique color to enhance readability.
 	- The 'Add User' button allows you to include user sessions in the matrix.
 	- You can change the HTTP request method to 'GET', 'POST', or 'Dynamic', the latter of which is based on proxy history.
 	- The 'Reset' button clears all contents.
 	- The 'Run' button executes the task, displaying the results in the user access matrix.
 	- The 'Warnings' section highlights potential issues using different colors for easy identification.
 	- The 'Spider (SiteMap)' button automatically generates a URL list based on the user's header/session. The visible URLs will be populated in the next textbox, where you can still make modifications as needed.
 	- 'Crawl Depth' defines the maximum number of sub-links that the 'Spider' should crawl to detect links.
2. The field is for specifying request headers, and all URLs will be accessed using the session defined here.
3. Specify the URL addresses that users can visit. You can create this list manually or utilize the **'Spider'** crawler feature. Make sure to provide a visitable URL list for each user.
4. All provided URLs will be listed here and attempted to access using the corresponding user sessions.
5. The first column represents a scenario with no authentication attempt. All cookies, tokens, and potential session parameters will be removed from the HTTP calls.
6. The remaining columns correspond to the users previously generated, each marked with a unique color to indicate the respective URL owners. 
7. The cell titles display the HTTP response 'codes:lengths' for each user session, providing a clear overview of the response details for each access attempt.
8. Just click on the cell you want to examine, and the HTTP details will be displayed at the bottom.

Please note that potential session terminators (such as logoff, sign-out, etc.) and specific file types (such as CSS, images, JavaScript, etc.) will be filtered out from both the 'Spider' and the user's URL list.

<img width="1000" alt="User Access Table Details" src="https://github.com/user-attachments/assets/addabcc7-7dab-482b-91aa-4856b9e16126">

After clicking 'RUN', the tool will populate the user and URL matrix with different colors. In addition to user-specific colors, you will see red, orange, and yellow cells indicating possible access issues.
- **Red** highlights a critical access violation, indicated by the response returning 'HTTP 200' with the same content length.
- **Orange** signifies a moderate issue that needs attention, marked by the response returning 'HTTP 200' but with a different content length.
- **Yellow** indicates that the response returns an 'HTTP 302' status, signifying a redirection.

The task at hand involves a bulk process, and it is worth to mention which HTTP request methods will be used. The tool provides three different options for performing HTTP calls:
- **GET**, All requests are sent using the GET method.
- **POST**, All requests are sent using the POST method.
- **Dynamic**, The request method is determined by the proxy history. If no information is available, the base header method will be used by default.<br/><br/>

## 403 Bypass
HTTP 403 Forbidden status code indicates that the server understands the request but refuses to authorize it. Essentially, it means, ‘I recognize who you are, but you lack permission to access this resource.’ This status often points to issues like ‘insufficient permissions’, ‘authentication required’, ‘IP restrictions’, etc.

The tool addresses the common access forbidden error by employing various techniques, such as URL manipulation and request header modification. These strategies aim to bypass access restrictions and retrieve the desired content.

It is worth to mention two different usage cases:
1. In scenarios related to **Authentication Issues**, it is essential to consider removing all session identifiers. After doing so, test whether any sources become publicly accessible. This approach helps identify unauthenticated accesses and ensures that sensitive information remains protected. 
2. For **Privilege Escalation and Authorization** testing, retain session identifiers but limit their use to specific user roles. For instance, you can utilize a regular user’s session while substituting an administrative URL. This focused approach allows for more precise and efficient testing, ensuring that privileged sources are not accessible without the appropriate roles. 

There are 2 ways you can send HTTP requests to the tool.
1. You can load requests from proxy history by clicking the ‘Load Requests’ button. Doing so will automatically remove all session identifiers, making it suitable for attack **Case 1**. Any potential session terminators (such as logoff, sign-out, etc.) and specific file types (such as CSS, images, JavaScript, etc.) will be also filtered out. Please note that this will be a bulk process and may take longer as it involves revisiting each HTTP request from the history. However, this comprehensive verification of all endpoints is essential for ensuring the security of the authentication mechanisms
2. You can send individual requests by right-clicking. Session identifiers will be retained/untouched, making this approach suitable for attack **Case 2**. This controlled approach allows you to assess whether privileged sources are accessible without proper roles. It will be more specific and faster, as users will select which URLs to test rather than copying everything from history.

<img width="1000" alt="Sending individual requests" src="https://github.com/volkandindar/agartha/assets/50321735/54b567a0-6b69-43f4-b727-f01709f4cc79">

The page we aim to access belongs to a privileged user group, and we retain our session identifiers to verify if Privilege Escalation is feasible.
<br/><br/>
Simply clicking the 'RUN' button will execute the task.

The figure below illustrates that a URL may have an access issue, with the ‘Red’ color indicating a warning.

<img width="1000" alt="Attempt details" src="https://github.com/user-attachments/assets/37fd6e3f-2348-48ce-a323-d7294a7a424b">

1. Load requests from the proxy history by selecting the target hostname and clicking the ‘Load Requests’ button.
 	- **Enable Filters**: Since processing all URLs in the HTTP history is a bulk task, this section provides options to apply matching criteria.
 	 	- The Enable URL grouping feature (experimental) aims to eliminate similar endpoints that differ only by unique IDs, counting them as a single entry.
 	 	- You can choose to load only URLs from the past n days.
 	 	- You can also specify certain keywords to control which URLs are loaded.
2. URL and Header details
3. Request attempts and results
4. HTTP requests and responses

Please note that the number of attempts is contingent upon the specific target URL.
<br/><br/>

## Copy as JavaScript
The feature enables the conversion of HTTP requests into JavaScript code, which can be particularly useful for going beyond XSS vulnerabilities and bypassing header restrictions.

To use this feature, simply right-click on any HTTP request and select 'Extensions > Agartha > Copy as JavaScript'.

<img width="1000" alt="Copy as JavaScript" src="https://github.com/volkandindar/agartha/assets/50321735/c0149adb-d0ab-4aa3-98a1-34b86bd68d3f">

It will automatically save to your clipboard, including some additional remarks for your reference. For example:
```
Http request with minimum header paramaters in JavaScript:
	<script>
		var xhr=new XMLHttpRequest();
		xhr.open('GET','http://dvwa.local/vulnerabilities/xss_r/?name=XSS');
		xhr.withCredentials=true;
		xhr.send();
	</script>

Http request with all header paramaters (except cookies, tokens, etc) in JavaScript, you may need to remove unnecessary fields:
	<script>
		var xhr=new XMLHttpRequest();
		xhr.open('GET','http://dvwa.local/vulnerabilities/xss_r/?name=XSS');
		xhr.withCredentials=true;
		xhr.setRequestHeader('Host','dvwa.local');
		xhr.setRequestHeader('User-Agent','Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0) Gecko/20100101 Firefox/127.0');
		xhr.setRequestHeader('Accept','text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8');
		xhr.setRequestHeader('Accept-Language','en-US,en;q=0.5');
		xhr.setRequestHeader('Accept-Encoding','gzip, deflate, br');
		xhr.setRequestHeader('DNT','1');
		xhr.setRequestHeader('Sec-GPC','1');
		xhr.setRequestHeader('Connection','keep-alive');
		xhr.setRequestHeader('Referer','http://dvwa.local/vulnerabilities/xss_r/');
		xhr.setRequestHeader('Upgrade-Insecure-Requests','1');
		xhr.setRequestHeader('Priority','u=1');
		xhr.send();
	</script>

For redirection, please also add this code before '</script>' tag:
	xhr.onreadystatechange=function(){if (this.status===302){var location=this.getResponseHeader('Location');return ajax.call(this,location);}};
```
Please note that the JavaScript code will execute within the original user session, with many header fields automatically populated by the browser. However, in some cases, the server may require specific mandatory header fields. For example, certain requests might fail if the 'Content-Type' is incorrect. Therefore, you may need to adjust the code to ensure compatibility with the server's requirements.
<br/><br/>

## Bambdas Code Generator
Bambdas are lightweight scripts that run directly within Burp Suite, allowing users to quickly customize and automate various tasks. They can be used to define custom match-and-replace rules, add dynamic table columns, apply filters, and tailor the interface to better suit specific testing workflows. 

<img width="1000" alt="Bambdas Code Generator" src="https://github.com/user-attachments/assets/a2681d9b-4c05-4876-98bb-5a4252bb4aff">

Explanations, A little bit more details:
1. Regarding script creation GUI, you can select general settings here. For example:
 	- Processing only in-scope addresses or all domain addresses.
 	- Hiding specific file extensions or not.
 	- Colors for URLs defined in the scope section, located in the first part of Group 3.
   	- Colors for URLs that have already been tested, located in the second part of Group 3.
   	- Colors for filters defined mostly in Group 2.
   	- Number of past days to display.
 	- Number of past days to be processed by the script.
2. The options in the second section are mainly related to processing HTTP requests and responses:
 	- Provides options to specify whether the search criteria should be applied to the URL, the request, or the response. Selecting any of these will activate the corresponding options below. For example, if you want to search for 'Vulnerable JavaScript Functions', this will only be possible in HTTP responses.
 	- Option to hide specific HTTP methods.
 	- "Search HTML comments", "Downloadable file extensions", and "Vulnerable JS Functions" are generally searched within HTTP responses.
 	- "Valuable keywords" searches can be applied to URLs, requests, and responses.
   	- "SQLi-suspect identifiers, XSS-suspect identifiers, LFI-suspect identifiers, SSRF-suspect identifiers, Open Redirect-suspect identifiers, and RCE-suspect identifiers" can be searched in URLs or requests. Unlike "Valuable keywords", which searches free-text, these options detect parameters specifically.
3. The options in the third section are mainly for defining scope, already tested URLs, and URLs you want to hide.
 	- You can define the URLs to be tested in the "Definition of testing scope" section. If you enter /, the entire application will be considered in scope; if you add a specific path like /users, only that directory and its contents will be in scope. The "Color for testing scope" option applies to this section.
   	- The "Already Tested URLs" section contains the list of URLs that have already been tested. The "Color for tested items" option applies here.
 	- The "Black-Listed URLs" section contains URLs you wish to hide from the proxy history.

    **Examples of definitions**: 
    - /
 	    - Root path — includes everything.
    - /portal/users
 	    - Includes specifically this path and its subpaths, for example:
 	 	    - /portal/users?id=1
 	 	    - /portal/users/?id=1
 	 	    - /portal/users/dashboard
    - /admin/\*/users/\*/class
     	- The asterisk (*) acts as a placeholder for IDs, UUIDs, etc., and the rest of the path will be included.
    - /health-check
 	    - Includes specifically this path and its subpaths, for example:
 	 	    - /health-check
 	 	    - /health-check/Monitor
 	 	    - /health-check/?Level=Info
4. Finally, the fourth section is where the script generated by clicking the "Run" button is displayed, and the script is now ready for use. In general, this script can be added in two different ways:
 	- Temporary (project-based): From the application menu, go to Proxy > HTTP History > Bambda Mode > Apply & Close.
   	- Permanent (application-wide): From the application menu, go to Extensions > Bambda Library > New > Blank > View filter + HTTP history > Save & Close.
 	

**Please note**: Enabling all options, especially for large projects, can result in significant system resource usage and increased processing time. If the script you have created does not complete within a reasonable time, it may be beneficial to revise it.

<img width="1000" alt="Bambdas Code Generator" src="https://github.com/user-attachments/assets/2e13f4e2-46ea-4970-b403-95bc03aeb8b1">

**Option precedence**: The highest priority is 'Color for tested items', followed by 'Color for testing scope', and finally 'Color for parameters/keywords'.

The figure above illustrates the following:
- **Pink** indicates the testing scope (the first part of group 3).
- **Yellow** represents the tested scope (the second part of group 3).
- **Cyan** highlights matches for the search criteria (Group 2). In addition, you can see which criterion matched in the 'Notes' section of each HTTP call.

If you later update or modify a script that has already been created, there are a few important points to keep in mind:
- If you set your script as Permanent (application-wide), you will need to reload it by following these steps:

		Bambda Script mode > Load

  <img width="800" alt="Bambdas Code Generator" src="https://github.com/user-attachments/assets/819a2a11-e0b3-450c-95bc-391615b7bcc3">

- If you use your script as Temporary (project-based), you generally have two options:
 	1. If you want the modified script to be active from that point onward, no additional steps are required—simply click Apply.
 	2. If you want the modified script to process the entire proxy history, you must either re-enable Bambda Mode, or toggle the boolean resetScreen parameter inside the script:
		```
		// 'true' clears colors/notes
		// 'false' executes the script  
		boolean resetScreen = false; // or true
		
		```
		<img width="800" alt="Bambdas Code Generator" src="https://github.com/user-attachments/assets/ebb64ddb-9720-4ccd-9a27-988110cfaaa6">

<br/><br/>
[Another tutorial link](https://www.linkedin.com/pulse/agartha-lfi-rce-auth-sqli-http-js-volkan-dindar)

