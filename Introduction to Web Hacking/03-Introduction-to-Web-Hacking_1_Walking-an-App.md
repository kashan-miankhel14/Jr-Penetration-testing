# walking an application

## Walking An Application

In this room you will learn how to manually review a web application for security issues using only the in-built tools in your browser. More often than not, automated security tools and scripts will miss many potential vulnerabilities and useful information.

Here is a short breakdown of the in-built browser tools you will use throughout this room:

- **View Source** — Use your browser to view the human-readable source code of a website.
- **Inspector** — Learn how to inspect page elements and make changes to view usually blocked content.
- **Debugger** — Inspect and control the flow of a page’s JavaScript
- **Network** — See all the network requests a page makes.

_No answer needed_

## Exploring the Website

_No answer needed_

## Viewing the Page Source

**What is the flag from the HTML comment?**

To obtain that information look in the source code and see the comment, when you open the /new-home-beta, the flag will be displayed


**What is the flag from the secret link?**

Look into the details of the source code. You will see the /secret-page. Go there and the flag will be displayed


**What is the directory listing flag?**

Go to the /assets and check the source code, you will get access to the whole directory with file flag.txt as well. Open the file and you will get your answer.


**What is the framework flag?**

Check the last comment in the main page source code. When visiting the site, look there is a Change Log entry with information that /tmp.zip should be the file we are looking for. Open the page /tmp.zip and you can download and extract the file. Within that file there is flag.txt


## Developer Tools — Inspector

**What is the flag behind the paywall?**

Go to the /news section and open the article behind the paywall. Click on inspect the element and you will see the Inspector menu, look for “premium-customer-blocker” and click on that. On the right side you will see the settings of that blocker, try to change the display to “none” instead of blocked. Boom! It is done, now you can see the flag.


## Developer Tools — Debugger

**What is the flag in the red box?**

To check it go to the /contact page and open Debugger (click on the Inspect Element and then move to Debugger). In the Debugger menu look for the flash.mini.js in the assets. There select the Preety Print view and scroll down to line 108. Click on the line number, this will create a breakpoint and stop executing the flash. Refresh the page and you will see the red banner being displayed.


## Developer Tools — Network

**What is the flag shown on the contact-msg network request?**

With the network tab open, try filling in the contact form and pressing the **Send Message** button. You’ll notice an event in the network tab, and this is the form being submitted in the background using a method called AJAX. AJAX is a method for sending and receiving network data in a web application background without interfering by changing the current web page.

When you have sent the message, refresh the page once again and check the contact-msg element. Go to Response to get the Response flag.

