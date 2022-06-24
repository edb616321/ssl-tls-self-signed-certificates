 <!-- Author: Edward Brookman -->


<!-- ABOUT THE PROJECT -->


##SSL-TLS Self-Signed Certificates for `[SMB/Labs]`

## About The Project
Ever run into a **"Your connection is not private"** or **"Secure connection failed"** error when setting up a server in a lab or small business. It can be embarrassing and frustrating. 

This repository is dedicated to providing easy to understand, step-by-step instruction and cheat sheets to help us eliminate this pesky technical problem. 

I will start with the proxmox server instructions as this is one of my personal favorites. I use proxmox VE for many of my internal virtualization projects. It is a fantastic product [https://www.proxmox.com/en/]. 

I plan to add similar instructions for all major servers. I will also be adding bash, Ansible and Terraform scripts when possible.  

`Before you start:`


* It is assumed that you have a working knowledge of the linux server environment and bash shell. 
* It is also assumed that you have proxmox VE installed and configured (if relevant).
* I strongly recommend that you install and configure an on-premise DNS server. Technitium is my favorite but there are many to choose from - [https://technitium.com/dns/].
* Once your DNS server is installed, add the proper A record mapping your internal domain name to your IP address. 
* Make sure that you can manage your SSH connections properly. I use MobaXterm [https://mobaxterm.mobatek.net/].


<p align="right">(<a href="#top">back to top</a>)</p>



### Choose your poison

Sample list of instructional, 'Markdown' files available.

* Proxmox ([[ssl-tls-self-signed-certificates/Proxmox-tls-self-signed-cert-process.md]])
* [Apache]
* [Tomcat]
* [Wordpress]
* More to come.....

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- CONTRIBUTING -->
### Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>











