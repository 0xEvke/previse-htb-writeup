# previse htb writeup

-----------------------------------------------------------------------------------------------------------------------------

Frist i scan ports with nmap

![Uploading nmapscan.PNG…]()

This are the results:

kinda basic

-----------------------------------------------------------------------------------------------------------------------------

so lets put previse.htb in /etc/hosts/

![addingprevise htb](https://user-images.githubusercontent.com/83223136/133935470-4b128797-3bdb-4334-b467-53e63c7743c0.jpg)

-----------------------------------------------------------------------------------------------------------------------------


after all we can rn look at the website:

![lookingatwebsite](https://user-images.githubusercontent.com/83223136/133935495-ce874a64-7085-44d2-a8e8-e78ae22d5bcb.PNG)

I tried basic logins just in case:

![tryingadminadmin](https://user-images.githubusercontent.com/83223136/133935505-dd7b58bb-334a-4a98-9040-cfc558061dd2.PNG)

but nothing

-----------------------------------------------------------------------------------------------------------------------------

lets try gobuster

![lookingforpages](https://user-images.githubusercontent.com/83223136/133935540-19c90cef-153a-4bbf-bb01-20e8e21a8f9f.PNG)

gobuster find out for previse.htb/nav.php

-----------------------------------------------------------------------------------------------------------------------------

lets look at the nav.php

![findingnavphp](https://user-images.githubusercontent.com/83223136/133935693-8ecff7b4-c04b-46d7-ac14-0da169c6d2a8.jpg)

i tried to click on any button but it gets me back to the login page

-----------------------------------------------------------------------------------------------------------------------------

lets add burp suite into this

i did bypass login like this

![bypassing1](https://user-images.githubusercontent.com/83223136/133935880-61160c74-e978-4c49-bacf-54f1355b7678.jpg)

![bypassing2](https://user-images.githubusercontent.com/83223136/133935894-79b05472-8239-4977-ac81-dde41f37ef38.jpg)

![bypassing3](https://user-images.githubusercontent.com/83223136/133935897-c494c324-02b1-40ce-a5de-2b26546f58c5.jpg)

and we successfully bypass login page

-----------------------------------------------------------------------------------------------------------------------------

we are on register page right now

![wegothere](https://user-images.githubusercontent.com/83223136/133935937-52f36766-0337-4942-b498-83997e906b61.jpg)

just make account.

![justlogin](https://user-images.githubusercontent.com/83223136/133935955-85571e69-1875-4725-8849-a359a36a8c5d.jpg)

and here just login

-----------------------------------------------------------------------------------------------------------------------------

after quick looking at the navbar I found page where is website

![filepage](https://user-images.githubusercontent.com/83223136/133936035-dc717538-0e07-4428-b29a-23fc04401875.jpg)

after downloading it I found config.php

![filepack](https://user-images.githubusercontent.com/83223136/133936071-cb8ae5d6-8229-45cc-96ff-711e4cb1d22c.jpg)

I looked at it and I found db informations

![dbinformation](https://user-images.githubusercontent.com/83223136/133936114-ab911453-716e-4e41-a9b2-b9830a978c24.PNG)

-----------------------------------------------------------------------------------------------------------------------------

If you wonder how to get revshell

![tryingtogetrevshell](https://user-images.githubusercontent.com/83223136/133936381-8b438d3c-3c8f-4dcd-8583-e446d8d064b9.jpg)

I'll try to put payload here

![dothispayloadandsetreadylisteners](https://user-images.githubusercontent.com/83223136/133936389-1550e105-30ad-4d10-8b25-9025b68079c8.jpg)

and it worked

![wegotrevshell](https://user-images.githubusercontent.com/83223136/133936421-94b59b93-ccd5-48d8-b0d6-e332a6969b53.jpg)

write python3 -c 'import pty;pty.spawn("/bin/bash")'

-----------------------------------------------------------------------------------------------------------------------------

Because we got db informations lets look at the database

![wegotthis](https://user-images.githubusercontent.com/83223136/133936516-652469b5-637d-42cb-8e44-e19a62b80c7c.jpg)

and we got this

so we need to hash it, we're using hashcat

![thisshoulddecrypt](https://user-images.githubusercontent.com/83223136/133936522-5b0543f0-d207-4edf-85de-51810db98155.PNG)

and password is: ilovecody112235!

![wegotuser](https://user-images.githubusercontent.com/83223136/133936544-b0c695d9-5bed-4d9a-b943-fc0288f6412f.PNG)

and we got user
-----------------------------------------------------------------------------------------------------------------------------

# privilege escalation

![privlegeesc](https://user-images.githubusercontent.com/83223136/133936592-666b8ef8-047e-437e-b5e9-91f79373b289.PNG)

after looking at file, file looks like this

![unknown](https://user-images.githubusercontent.com/83223136/133936730-35075648-d684-486e-aae6-5460bd52998f.jpg)

I figured out that this needs to be something with gzip
So i located it and i found in tmp and bin

So lets try to import revshell

![tryprivesc](https://user-images.githubusercontent.com/83223136/133936780-d9d5c613-3f76-4c01-bba1-3e54fefb15f0.PNG)

and lets run 

![running](https://user-images.githubusercontent.com/83223136/133936838-20ffadc2-1747-4c95-a12e-6b65fc6ea0bf.PNG)

and lets look at the listners

![pwned](https://user-images.githubusercontent.com/83223136/133936874-b821e0b6-5fc6-4ef9-97e2-31e4155ce6c8.PNG)

and it worked.
