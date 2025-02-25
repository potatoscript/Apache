# 🖥️ Apache Server Setup 🚀

In this tutorial, we'll set up an **Apache server** on your Windows computer. By the end, you'll have a fully working web server that can serve **PHP** websites. We’ll take it slow, so even someone who's never done this before will understand.

---

### 🚀 STEP 1: Download and Install Apache Web Server

1. **Download Apache 2.4** from the official site:
   - Go to [Apache Lounge](http://www.apachelounge.com/download/) and download the latest version of Apache 2.4 (choose the one named `httpd-2.4.29-win32-VC15`).
   
2. **Extract the Apache Files**:
   - After downloading, you'll get a ZIP file. Extract that ZIP file to your `C:` drive. The folder should be named `Apache24`:
     ```
     C:\Apache24
     ```
   
---

### 🚀 STEP 2: Install Microsoft Visual C++ 2015 Runtime

Apache needs a **C++ runtime** to run on your computer. Don’t worry—this is simple.

1. Download and install **Microsoft Visual C++ 2015 Runtime** from [Microsoft’s website](https://www.microsoft.com/en-us/download/details.aspx?id=48145).
   
2. This will allow Apache to run properly on your system, so don't skip this step!

---

### 🚀 STEP 3: Download PHP

1. **Download PHP 5** from the official PHP website:
   - Go to [PHP Downloads](http://windows.php.net/download/) and choose **PHP 5**. It is recommended to download the **Thread Safe** version.

---

### 🚀 STEP 4: Configure Apache to Work with PHP

We need to tell Apache how to use PHP. Here's how:

1. **Open Apache’s configuration file**:
   - Go to the folder `C:\Apache24\conf` and find the file named `httpd.conf`. Open it with a text editor (like Notepad).

2. **Add the PHP configuration** at the bottom of the file. Copy and paste the following lines:
   ```
   LoadModule php5_module "c:/php/php5apache2_4.dll"
   AddHandler application/x-httpd-php  .php
   PHPIniDir "c:/php"
   LoadFile "c:/php/libpq.dll"
   ```

   - These lines tell Apache where to find PHP, how to handle `.php` files, and where to load the necessary files for PHP to work.

3. **Set the Server Name**:
   - Find the line that starts with `#ServerName` and change it to:
   ```
   ServerName http://localhost:80
   ```

4. **Set the Index File**:
   - Apache uses an "index" file to load your website. To make PHP files load first, find the `DirectoryIndex` line and change it like this:
   ```
   <IfModule dir_module>
       DirectoryIndex index.php index.html
   </IfModule>
   ```
   This makes Apache look for an `index.php` file when you open your website.

---

### 🚀 STEP 5: Update the System PATH Variable

We need to make sure that your computer knows where Apache and PHP are installed. This is done by updating the **PATH** environment variable.

1. Open the **Command Prompt** (you can search for `cmd` in the Start menu).
2. Enter this command:
   ```
   setx PATH "%PATH%;c:\php;c:\apache24;c:\apache24\bin"
   ```

3. **Reboot** your computer to make sure all the settings are applied.

---

### 🚀 STEP 6: Register Apache as a Service

Now we need to tell Windows to start Apache automatically when your computer starts.

1. **Open Command Prompt** again (as Administrator if needed).
2. Register Apache as a service by typing:
   ```
   c:\apache24\bin\httpd -k install
   ```

3. **If you don't want Apache to start automatically when your computer restarts**, use this command to make it start only when you want it:
   ```
   c:\> sc config Apache2.4 start=demand
   ```

4. **Check if Apache is running**:
   - Type the following to test:
   ```
   c:\Apache24\bin\httpd -s
   ```

   If everything’s set up correctly, you’ll see a message that shows no errors.

---

### 🚀 STEP 7: Configure PHP Settings

We now need to set up PHP properly:

1. **Rename the PHP configuration file**:
   - In the folder `C:\php`, there should be a file named `php.ini-development`. Rename it to `php.ini`.

2. **Set the `extension_dir`**:
   - Open the `php.ini` file with a text editor and find the line:
     ```
     ;extension_dir = "ext"
     ```
     Remove the `;` at the beginning so it looks like this:
     ```
     extension_dir = "ext"
     ```

3. **Enable PHP extensions**:
   - To enable PostgreSQL support (optional), find the lines:
     ```
     ;extension = php_pdo_pgsql.dll
     ;extension = php_pgsql.dll
     ```
     and remove the `;` to enable these extensions:
     ```
     extension = php_pdo_pgsql.dll
     extension = php_pgsql.dll
     ```

4. **Check the PHP modules**:
   - To see if PHP is working and what modules are loaded, open the command prompt and type:
     ```
     c:\> php -m
     ```

   This will display a list of all active PHP extensions and modules.

---

### 🚀 STEP 8: Allow Access Through Firewall

Finally, make sure your **Windows Firewall** is configured to allow Apache to serve web pages.

1. Open the **Windows Firewall** settings.
2. Ensure that the ports used by Apache (typically **port 80** for HTTP) are open to incoming traffic.

---

### 🎉 Congratulations! You Have Successfully Installed Apache and PHP!

If you’ve followed all the steps, your Apache server should now be up and running with PHP support.

- You can now start creating websites using PHP and host them on your **local server** by placing your website files in `C:\Apache24\htdocs`.

### What to do Next?
1. **Test Apache**:
   - Open your browser and go to `http://localhost`. If you see a page that says "It works!", then Apache is running perfectly.
   
2. **Test PHP**:
   - Create a new file in the `C:\Apache24\htdocs` folder, name it `index.php`, and put the following code inside:
     ```php
     <?php
     phpinfo();
     ?>
     ```
   - Then go to `http://localhost/index.php` in your browser. You should see a detailed PHP info page that shows all the settings and modules loaded by PHP.


---

### STEP 1 :
- Download Apache 2.4 Install : (http-2.4.29-win32-VC15) from http://www.apachelounge.com/download/
- Extract the zip Apache24 to the root of c:\  -> c:\Apache24

### STEP 2 :
- Install a framework called microsoft Visual C++ 2015 Runtime
- 
- This is required for Apache to run.

### STEP 3 :
- Download PHP 5 from http://windows.php.net/download/

### STEP 4 :
- Edit Apache's config file `c:\Apache24\conf\httpd.conf
- Add the following lines to the bottom of the file
```
   LoadModule php5_module "c:/php/php5apache2_4.dll"
   AddHandler application/x-httpd-php  .php
   #configure the path to php.ini
   PHPIniDir "c:/php"
   LoadFile "c:/php/libpq.dll"
```
- Set the ServerName `http://yourserverName:80`

- Find Directory index and add index.php as below
- So we can load hte index.php at the initial load of our localhost server
```
<IfModule dir_module>
    DirectoryIndex index.php index.html
	
</IfModule>
```

### STEP 5 :
- Register the path where the application reside.
  This is done by editing the PATH variable 
  We can set this from the command prompt:
  ```
     setx PATH "%PATH%;c:\php;c:\apache24;c:\apache24\bin"
  ```
- Save and reboot the system. (restart your device)

### STEP 6 :
- Register Apache Service by Open a command prompt and type
```
   c:\apache24\bin\httpd -k install
```
- If do not want Apache starting automatically at start-up/reboot:
```
   c:\> sc config Apache2.4 start = demand
```
- Now let check Apache setting by issuing the command below
```
   c:\Apache24\bin\httpd -s
```

### STEP 7 :
- PHP setting
- Rename the file `c:\php\php.ini-development` to `c:\php\php.ini`
- Uncomment extension directory as below
```
   ;extension_dir = "ext"  -> extension_dir = "ext"
```

- if error occur: Call to undefined function then you need to set it explicitly.
```
  extension_dir = "C:\php\ext"
```

- Uncomment pgsql modules as below
```
   ;extension = php_pdo_pgsql.dll  -> extension = php_pdo_pgsql.dll
   ;extension = php_pgsql.dll      -> extension = php_pgsql.dll
```
- Check to make sure it shows loaded modules with the command below
```
   c:\> php -m
```

### STEP 8 :
- Finally check your firewall to allow remote access

Congratulations you have your apache server installed !

