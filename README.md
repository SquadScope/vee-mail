# vee-mail
Simple Script to get Mails from Free Veeam Agent for Linux

vee-mail uses the sqlite database which get's filled from Veeam Agent for Linux Free in /var/lib/veeam/veeam_db.sqlite.
The Linux version from Veeam Agent does not send notification e-mails like the windows version.
So this script reads the data from the sqlite database and fills it into the template file which get's sent per mail to you.

# Dependencies

veeam
sqlite3
bc
curl (only for vee-mail update check)
sendmail
nullmailer

# Install

git clone https://github.com/SquadScope/vee-mail
move the directory "vee-mail" to /opt or any other directory you would like to install it into
change vee-mail.confg file to your needs.
chmod +x vee-mail.sh

install nullmailer

sudo nano /etc/nullmailer/remotes
  mail.example.com smtp --user=tiffany.test@example.tld --pass=<Password> --port=587 --starttls
  
sudo nano /etc/mailname
    example.tld
    
sudo nano /etc/nullmailer/defaultdomain
    example.tld
    
sudo nano /etc/nullmailer/adminaddr
    admin@example.tld


sudo export NULLMAILER_HOST=example.tld

sudo export NULLMAILER_USER=tiffany.test

The vee-mail.sh script is prepared to send a mail using CC to a second person. To make use of it just uncomment "echo "Cc: $friendname $ltlt$EMAILCCTO$gtgt" >> $EMAILFILE" at the end of vee-mail.sh and enter an email address in "EMAILCCTO=" in vee-mail.config


# Use

You can use the vee-mail script as a post-backup script directly in veeam (Configure - select Job, Advanced/Scripts/Post-Job) or start it manualy after the veeam backup has run:

/opt/vee-mail/vee-mail.sh


# Release notes

## Version 0.5.10
First release on Github with new name "vee-mail"

# Related Works
Special thanks to @grufocom for his amazing vee-mail script.
@Steve Litt on  http://www.troubleshooters.com/linux/nullmailer/ for his nullmailer example script.
