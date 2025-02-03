---
title: "How to Install Forticlient on Kali Linux"
categories: [Cybersecurity, Linux]
tags: [Linux]
date: 2024-08-03 18:00:00 -0500
math: false
mermaid: true
pin: true
media_subpath: /assets/img/how-to-install-forticlient/
image: logo-forti.png
---
---

Hello everyone! Recently, I faced several challenges while trying to correctly install FortiClient on various Linux systems, particularly those based on Debian, such as Kali Linux. Since I use this tool daily, I thought it would be helpful to write this blog post to assist anyone who might be experiencing similar issues. So Let's do it!! 😁

---

The version of Kali Linux I am using is 2024.2 However, I found that compatibility issues also arise in earlier versions, particularly with the libappindicator1 library, which is one of the dependencies of the FortiClient package.

As a first step, it is necessary to add the repositories from the official sources, as shown in the Fortinet documentation. In this case, we will use the repositories indicated for Debian-based OS and make a small modification to the process. At the time of writing this article, version 7.4 of FortiClient was not available, so we will use version 7.2, as demonstrated below. For more information, you can access the following link : https://docs.fortinet.com/document/forticlient/7.4.0/linux-release-notes/213138/install-forticlient-linux-from-repo-fortinet-com.

To begin the process you need to install the GPG key to ensure the package authenticity and security. You can do this by running the following command in your terminal:

```bash
wget -O - https://repo.fortinet.com/repo/forticlient/7.2/debian/DEB-GPG-KEY | gpg --dearmor | sudo tee /usr/share/keyrings/repo.fortinet.com.gpg
```

Next, you need to create a new file in the `/etc/apt/sources.list.d/` directory to add the Fortinet repository. Create a file named `repo.fortinet.com.list` with the following content:
```bash
deb [arch=amd64 signed-by=/usr/share/keyrings/repo.fortinet.com.gpg] https://repo.fortinet.com/repo/forticlient/7.2/debian/ stable non-free
```
After adding the repository, update your package lists to ensure that you have the latest information from all repositories:

```bash
sudo apt-get update
```
Once the package lists are updated, you can proceed to install FortiClient by running:

```bash
sudo apt install forticlient
```

However, there is the first issue during the installation 😥, you might encounter errors such as:

>forticlient depends on libappindicator1, which is not installable.
{: .prompt-danger }

This error occurs because the libappindicator1 library is not available in the current repository or has been deprecated. To resolve this issue, we need to manually install the missing library or find an alternative solution, such as using a compatible version of the library or installing it from a different source like the official debian sources as follow.

First, download the libappindicator binary using the following command:

```bash
wget http://http.us.debian.org/debian/pool/main/liba/libappindicator/libappindicator1_0.4.92-7_amd64.deb
```

Then, install it using dpkg with the command:

```bash
sudo dpkg -i libappindicator1_0.4.92-7_amd64.deb
```

As expected, when installing libappindicator, a new issue crops up because this package depends on libdbusmenu-gtk4. This dependency hurdle might feel like déjà vu, presenting an error similar to the previous one. But don't worry, we'll tackle it head-on! 😎.

First, you'll need to download the libdbusmenu-gtk4 binary to resolve this dependency issue. You can do this by running the following command:

```bash
wget http://http.us.debian.org/debian/pool/main/libd/libdbusmenu/libdbusmenu-gtk4_18.10.20180917~bzr490+repack1-1_amd64.deb
```
Next, you'll need to install it using dpkg. Run the following command:

```bash
sudo dpkg -i libdbusmenu-gtk4_18.10.20180917~bzr490+repack1-1_amd64.deb
```

Great! Once libdbusmenu-gtk4 is installed, you'll be able to install libappindicator correctly without any more dependency issues. This paves the way for a smooth installation of FortiClient.

Simply rerun the command to install libappindicator:

```bash
sudo dpkg -i libappindicator1_0.4.92-7_amd64.deb
```

Finally, to install FortiClient, you'll need to use the following command:

```bash
sudo apt-get satisfy forticlient
```
This command ensures that all dependencies are met and installs FortiClient smoothly on your system.With these steps completed, you should now have FortiClient up and running, ready to enhance your Linux experience. If you encounter any issues or have any questions, feel free to reach out for help. Happy computing!

---

Additionally, you can verify that there are no broken packages on your system by using the following command:

```bash
sudo dpkg --configure -a
```

This command will attempt to fix any broken package installations, ensuring that everything is in working order. By completing this step, you can be confident that your system is stable and FortiClient is ready to use without any issues.
Thanks for read!! 🤓.