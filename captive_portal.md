# Captive Portal

## What is a captive portal?

When a client connects to a WiFi Pineapple or any access point that has a captive portal present, the client will automatically be redirected to a special web page. This special web page is known as a landing page, and typically requires clients to perform an action before they can use the internet as intended.

## Who uses captive portals and why?

Captive portals have many applications but are most commonly used to authenticate clients. Public Wi-Fi hotspot providers, such as Starbucks and McDonald's, typically use a captive portal to redirect clients to a web page containing a user agreement or terms of use. In this scenario, clients must agree to the terms of use before they are authenticated and permitted to use the internet freely. Some businesses provide public Wi-Fi hotspots solely because the implementation of a captive portal enables them to advertise products and services, solicit subscriptions, sell internet service, and satisfy other business-related agendas.

Although captive portals have many legitimate uses, like those described above, it's important to note that they also have the potential of being used maliciously by criminal hackers. By providing clients with a well-designed captive portal that is professional in appearance, criminal hackers are able to deceive unsuspecting clients and provide them with a sense of legitimacy. This misled sense of legitimacy, as a result, increases the client's susceptibility to malicious attacks. For example, it's a known fact that criminal hackers have successfully used captive portals to distribute malware and gather sensitive user data, including login credentials, email addresses, and financial information.

## Guide

In this guide, you will learn how to set up a captive portal on your WiFi Pineapple using the Evil Portal infusion. To improve the quality of your user experience, you will also be provided with a package containing custom splash page images and HTML code. If you prefer, you can watch the [video tutorial here](http://youtu.be/nw4bo4rXGgQ) instead.

  1. Connect to your WiFi Pineapple via Wi-Fi or ethernet cable
  2. Open a web browser and Log into your WiFi Pineapple's web interface
     http://172.16.42.1:1471
     Before proceeding to the next step, make sure your Pineapple is connected to the internet. The easiest way to connect your Pineapple to the internet is to use the client mode feature in the network tile.
  3. Open the **"Pineapple Bar"** tile
  4. Select the **"Pineapple Bar: Available Infusions"** tab
  5. Find **"Evil Portal"** in the list of infusions and click **"Install"**
  6. When prompted, click **"Install to internal storage"**
  7. Find the Evil Portal small tile, and click **"Install Dependencies"**
     If the Evil Portal small tile does not refresh automatically after installing the dependencies, simply refresh your web browser.
  8. Open the **"Evil Portal"** tile
  9. Select the **"Configure UHTTP Daemon"** tab
  10. Find the `config uhttp main` section and locate the following line
      ```
      list listen_http 0.0.0.0:80
      ```
      Then **replace** it with:
      ```
      list listen_http 0.0.0.0:8080
      ```
  11. Click **"Save Changes"**
  12. Select the **"Configure NoDogSplash"** tab
  13. Find the **"FirewallRuleSet users-to-router"** section and add the following firewall rules at the bottom of the section
      ```
      FirewallRule allow tcp port 1471
      FirewallRule allow tcp port 8080
      ```
  WARNING! Failure to add the above firewall rules will result in the inability to bypass the captive portal and access the Pineapple's web interface.

  14. Click **"Save Changes"**
  15. Click **"Restart UHTTP Daemon"**
  16. Open a new tab in your web browser and navigate to: http://sunstudiophoto.com/pineapple

  WARNING! Use vigilance when downloading files from third-party sources. If you choose to download files from a source other than http://wifipineapple.com, you do so at your own risk.

  17. Download the **"portal.zip"** package and save it to your desktop
  18. **Unzip** the portal.zip package to your desktop
      ```
      cd Desktop
      unzip portal.zip
      ```
     You should now have a folder titled "portal" on your desktop. The portal folder contains the custom splash page images and HTML code that we'll be using to give our captive portal a custom look. It also includes a PSD folder with the splash page's Photoshop project files, which, optionally, can be further customized to suit your needs.
  19. **SCP** the three .png image files from the portal folder to your Pineapple's `/etc/nodogsplash/htdocs/images/` directory
      ```
      scp '/root/Desktop/portal/button1.png' root@172.16.42.1:/etc/nodogsplash/htdocs/images/
      scp '/root/Desktop/portal/button2.png' root@172.16.42.1:/etc/nodogsplash/htdocs/images/
      scp '/root/Desktop/portal/background.png' root@172.16.42.1:/etc/nodogsplash/htdocs/images/
      ```
  20. Open the **splash.html** file with a text editor and **copy** the HTML code
  21. Move back to the Evil Portal tile in your web browser, and select the **"Edit Splash"** tab
  22. **Replace** the existing HTML code with the HTML code that you copied from the splash.html file
  23. Click **"Save Changes"**
  24. Click **"Start NoDogSplash"**
  25. When prompted, click **"Start Once"**
  26. Open a new tab in your web browser and **navigate to** any web page

That's it! If all went as planned, you should be redirected to your captive portal's landing page. Go ahead and click the "Accept" button to see how it works.