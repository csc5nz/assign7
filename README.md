# Project 7 - WordPress Pentesting

Time spent: **23** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. WordPress 4.2 - Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: Attacker is able to inject code through the comments of a post which will be activated when admin hover mouse over comment.
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: 
  ![](https://i.imgur.com/GjoJS3H.gifv) or <img src="https://i.imgur.com/GjoJS3H.gifv" width="800">
  [https://i.imgur.com/GjoJS3H.gifv](https://i.imgur.com/GjoJS3H.gifv)

  - [ ] Steps to recreate: Attacker as a regular user must post a comment with a script. The comment must be truncated by the database for the exploit to work. Once the comment is posted, the victim as an admin user must check comments and hover the mouse over the malicious comment and the script will run. I try using the recommended comment from the exploits page: <a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>. I added enough text to make the database truncate the comment. But the exploit didn't work. I tried multiple changes such as types of quotations, placement of brackets, differnt scripts, different triggers, etc. I noticed that if I cliked on edit comment as admin, the comment was not getting truncated. I tried making a longer comment but this didn't work either. It seems that this version of sql is not truncating the comment and thus the exploit is not working since the exploit was tested on MySQL versions 5.1.53 and 5.5.41.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/trunk/src/wp-admin/comment.php)


1. WordPress 2.5.0-4.7.4 - Filesystem Credentials Dialog CSRF
  - [ ] Summary: Attacker is able to change the hostname and password.
    - Vulnerability types: CSRF
    - Tested in version: 2.5.0-4.7.4
    - Fixed in version: 4.2.15
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: The WordPress installation must not be able to write to the wp_content folder. The attacker is able to make admin change the hostname and password by creating a page which sends a post comand with a new hostname and password. Some social engineering is required since the admin must click the submit button in this from. I created a html page with a form whose action is the wpdestilleries plugins.php: "http://wpdistillery.vm/wp-admin/plugins.php". It contains hiddent input tags with my chosen username and password as default values. It also contains a submit button which the admin must be tricked into cliking while he/she is loged in as admin on wp. I tested the code and the malicious page runs and redirects to the wp admin's plug in page. I'm unable to check if the hostname and password were changed. I did extensive research to see how to find this out but was unable to find it.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
3. WordPress 3.6.0-4.7.2 - Authenticated Cross-Site Scripting (XSS) via Media
  - [ ] Summary: Add a mp3 file with a script in its mettadata mettadata 
    - Vulnerability types: xss
    - Tested in version: 4.2
    - Fixed in version: 4.2.13
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: Upload mp3 file with script in its mettadata. Create media playlist. Post playlist on page. This must be done as admin.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)

## Assets

xss.mp3

## Resources

- [https://www.exploit-db.com/exploits/36844/](https://www.exploit-db.com/exploits/36844/)
- [https://packetstormsecurity.com/files/131644/](https://packetstormsecurity.com/files/131644/)
- [https://sumofpwn.nl/advisory/2016/cross_site_request_forgery_in_wordpress_connection_information.html](https://sumofpwn.nl/advisory/2016/cross_site_request_forgery_in_wordpress_connection_information.html)



## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
