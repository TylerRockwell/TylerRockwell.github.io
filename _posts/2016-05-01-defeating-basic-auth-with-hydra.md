---
layout: post
title: Defeating HTTP Basic Auth with Hydra
description: "An intro to cracking passwords with Hydra"
tags: [netsec, pentesting, hydra]
---

[HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) is a known weak authentication system and isn't often used in web apps anymore. However it is used quite frequently in our home network devices like routers and webcams. To complicate matters, these devices don't have any lockout mechanisms in place to prevent password guessing attacks like dictionary or brute-force attacks.

I'm going to demonstrate just how easy it is to break into such a device by running an attack on my home webcam using Hydra.

### Step 1 - Gather Tools

#### THC-Hydra - Our dictionary attack tool of choice

* Comes preinstalled with security distros of Linux (e.g. Kali)
* OSX Install via Homebrew - `brew install hydra`. I had to use the `--with-libssh` option
* Debian - `sudo apt-get install hydra hydra-gtk`

#### Wordlist - A list of passwords to test

I've created wordlists using data from [passwordrandom.com](http://www.passwordrandom.com/most-popular-passwords)

* [100 most common passwords](https://gist.github.com/TylerRockwell/1f24a4b237627811b449db9f90804e84)
* [1,000 most common passwords](https://gist.github.com/TylerRockwell/e66bb76374aba34ed430dab2617e9d4a)
* [10,000 most common passwords](https://gist.github.com/TylerRockwell/ab97b16045c3993edf528f8012b8fffa)

_Disclaimer: People commonly use passwords with NSFW language. Expect it in these lists._

There are more conclusive lists out there (hint google 'rockyou wordlist'), but these should be enough to get you started.

#### Optional Username List - A list of usernames to test

For this demo, I'm not using a username list and am just going by the commonly used default username `admin`

If you have username list you'd like to use, then go for it.

### Step 2 - Scanning the Target

![Today's Target]({{ site.url }}/images/hydra-basic-auth/main-page.png){: .center-image}

If you've ever used an IP camera or similar networked device, the above image is probably rather familiar.
A basic form and buttons that look like they came straight from geocities, what more could we want from hardware
manufacturers? If I click on the Server Push mode Login button, I am presented with a basic auth login form.


![Basic Auth]({{ site.url }}/images/hydra-basic-auth/login-form.png){: .center-image}

Sure, basic auth should be totally fine to protect this remotely controllable window into my home.

To execute the attack,
I need the following information:

* IP Address of device
* Listening port
* Where to submit guesses (e.g. /login.html)
* Request type used to submit

Since this is on my network, I already know the IP address of this device. If I didn't know it offhand, it could
be found rather easily by scanning the network with a tool such as `nmap`.

So, I've got its local ip address `192.168.1.4` and the port it's listening on is `8090`

I still need to know where to point the attack, though. Perhaps the Chrome dev tools can give me some insight.

![Dev tools ftw!]({{ site.url }}/images/hydra-basic-auth/form-submission.png){: .center-image}

Submitting garbage data to the form and checking out the network panel gives me a pretty clear indication
of where the data is going. `get_camera_params.cgi` is the only request with a status of `401`. Turns out I'm not very good at guessing
passwords by flapping my hand across the keyboard. By clicking on the request, I can see that it was submitted
with a `GET` request. With that, I have enough information to craft an attack.

### Step 3 - Crafting the Attack

Typing `hydra` or `hydra -h` at the command line prints basic usage info to the screen.

A basic attack will look as follows

`hydra -l username -P password_file.txt -s port -f ip_address request_method /path`

The `-f` flag tells hydra to stop on the first valid password it finds.
You can use `-L username_list.txt` if you'd like to use a list of usernames.

Filling in the information I gathered in step 2, I get the following:

`hydra -l admin -P 1000_common_passwords.txt -s 8090 -f 192.168.1.4 http-get /get_camera_params.cgi`

And about 10 seconds later, I have the password:

![Rekt]({{ site.url }}/images/hydra-basic-auth/pwn3d.png){: .center-image}

Remember kids, don't use weak or common passwords!
