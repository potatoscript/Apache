### STEP 1 :
- Download Apache 2.4 Install : (http-2.4.29-win32-VC15) from http://www.apachelounge.com/download/
- Extract the zip Apache24 to the root of c:\  -> c:\Apache24

### STEP 2 :
- Install microsoft Visual C++ 2015 Runtime
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
```
  DirectoryIndex  index.html  index.php
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

