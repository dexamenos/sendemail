Erik:

folgende apt-Pakete sind für Perl erforderlich

`apt install libio-socket-inet6-perl libio-socket-ssl-perl`

----

# sendEmail
SendEmail is a lightweight, command line SMTP email client. If you have the need to send email from a command line, this free program is perfect: simple to use and feature rich. It was designed to be used in bash scripts, batch files, Perl programs and web sites, but is quite adaptable and will likely meet your requirements. SendEmail is written in Perl and is unique in that it requires NO MODULES. It has an intuitive and flexible set of command-line options, making it very easy to learn and use. SendEmail is licensed under the GNU GPL, either version 2 of the License or (at your option) any later version.
[Supported Platforms: Linux, BSD, OS X, Windows 98, Windows NT, Windows 2000, &amp; Windows XP]

sendEmail - Send email from a console near you!
Written by: Brandon Zehm <caspian@dotconf.net>



------------------
Installation
------------------

SendEmail is a perl script/program, and only needs to be copied to a directory
in your path to make it accessible.  Most likely the following steps will
be sufficient:

1) Extract the package
    tar -zxvf sendEmail-v1.XX.tar.gz

2) Copy the sendEmail.pl script (and it's symlink sendEmail) to /usr/local/bin
    cp -a sendEmail-v1.XX/sendEmail.pl /usr/local/bin

3) Make sure its executable
    chmod +x /usr/local/bin/sendEmail.pl

4) Run it
    `sendEmail.pl`
      or
    `/usr/local/bin/sendEmail.pl`
      or if it's symlinked to "sendEmail" and in your path, just run:
    `sendEmail`

NOTES:

* Running sendEmail without any arguments will display a helpful usage summary.
* SendEmail is written in Perl, so no compilation is needed.
* On a Unix/Linux OS if your perl binary is not installed at /usr/bin/perl
you may need to edit the first line of the script accordingly.






---------------
Usage Overview
---------------

sendEmail-1.56 by Brandon Zehm <caspian@dotconf.net>

Synopsis:  sendEmail -f ADDRESS [options]

  Required:
    -f ADDRESS                from (sender) email address
    * At least one recipient required via -t, -cc, or -bcc
    * Message body required via -m, STDIN, or -o message-file=FILE

  Common:
    -t ADDRESS [ADDR ...]     to email address(es)
    -u SUBJECT                message subject
    -m MESSAGE                message body
    -s SERVER[:PORT]          smtp mail relay, default is localhost:25

  Optional:
    -a   FILE [FILE ...]      file attachment(s)
    -cc  ADDRESS [ADDR ...]   cc  email address(es)
    -bcc ADDRESS [ADDR ...]   bcc email address(es)
    -xu  USERNAME             username for SMTP authentication
    -xp  PASSWORD             password for SMTP authentication

  Paranormal:
    -b BINDADDR[:PORT]        local host bind address
    -l LOGFILE                log to the specified file
    -v                        verbosity, use multiple times for greater effect
    -q                        be quiet (i.e. no STDOUT output)
    -o NAME=VALUE             advanced options, for details try: --help misc
        -o message-content-type=<auto|text|html|other>
        -o message-file=FILE         -o message-format=raw
        -o message-header=HEADER     -o message-charset=CHARSET
        -o reply-to=ADDRESS          -o timeout=SECONDS
        -o username=USERNAME         -o password=PASSWORD
        -o tls=<auto|yes|no>         -o fqdn=FQDN

  Help:
    --help                    the helpful overview you're reading now
    --help addressing         explain addressing and related options
    --help message            explain message body input and related options
    --help networking         explain -s, -b, etc
    --help output             explain logging and other output options
    --help misc               explain -o options, TLS, SMTP auth, and more



---------------
Examples
---------------

Send a simple email:

```
    sendEmail -f me@gmail.com      \
            -t friend@yahoo.com    \
            -s smtp.gmail.com:587  \
            -xu me@gmail.com       \
            -xp MY-PASSWORD        \
            -u "Test email"        \
            -m "Hi buddy, this is a test email."
```

Sending to mutiple people:

```
    sendEmail -f myaddress@isp.net \
            -t "Scott Thomas <scott@isp.net>" jason@isp.net renee@isp.net \
            -s relay.isp.net     \
            -u "Test email"      \
            -m "Hi guys, this is a test email."
```

Sending to multiple people using cc and bcc recipients:
(notice the different way I specified multiple To recipients, you can do this for cc and bcc as well)

```
  sendEmail -f myaddress@isp.net \
            -t scott@isp.net;jason@isp.net;renee@isp.net \
            -cc jennifer@isp.net paul@isp.net jeremiah@isp.net \
            -bcc troy@isp.net miranda@isp.net jay@isp.net \
            -s relay.isp.net \
            -u "Test email with cc and bcc recipients" \
            -m "Hi guys, this is a test email."
```


Sending to multiple people with multiple attachments:

```
  sendEmail -f myaddress@isp.net \
            -t jason@isp.net \
            -cc jennifer@isp.net paul@isp.net jeremiah@isp.net \
            -s relay.isp.net \
            -u "Test email with cc and bcc recipients" \
            -m "Hi guys, this is a test email." \
            -a /mnt/storage/document.sxw "/root/My Documents/Work Schedule.kwd"
```

Sending an email with the contents of a file as the message body:

```
  cat /tmp/file.txt | sendEmail -f myaddress@isp.net \
                                -t jason@isp.net \
                                -s relay.isp.net \
                                -u "Test email with contents of file"
```

Sending an email with the contents of a file as the message body (method 2):

```
  sendEmail -f myaddress@isp.net \
            -t jason@isp.net \
            -s relay.isp.net \
            -o message-file=/tmp/file.txt \
            -u "Test email with contents of file"
```

Sending an html email:  (make sure your html file has <html> at the beginning)

```
  cat /tmp/file.html | sendEmail -f myaddress@isp.net \
                                 -t jason@isp.net \
                                 -s relay.isp.net \
                                 -u "Test email with html content"
```








------------
Contributors
------------

Many thanks go to the people who have submitted ideas and patches.
I know I've forgotten to mention everyone who's helped with sendEmail,
but here is a small list.  Please let me know if you feel your name
should be here!

  v1.56
   - Several people submitted fixes for the authentication bug.
     Thanks to all of you for nagging me to get this release out!

  Simon Matter (v1.55)
   - Local bind address patch

  CBL Team <http://cbl.abuseat.org/> and Chris Peay (v1.55)
   - Bug reports about sendEmail causing people get blacklisted.

  Jared Cheney (v1.42)
   - More bare LF bug fixes and bare period encoding.
   - Mime encoding patch

  Buddy Nahay (v1.41)
   - Bare LF bug report

  John Rouillard (v1.41)
   - html detection bug report

  Reidar Johansen (v1.40)
   - Added support for HTML email
   - Created a function called tz_offset that determines the local timezone
   - Many other fixes and suggestions

  Paul Kreiner (v1.40)
   - Submitted a patch that forces the timestamp string to always follow
     the HH:MM:SS convention required by the RFCs.

  Al Danial
   - Found and reported a logging/typo/attachment issue in v1.32

  Svante Gerhard
   - Found and reported the file attachment/padding issue in v1.31

  Charles Leeds
   - Put together all the original file attachment code and got me
     on the path to v1.3x
   - Provided the compiled Windows executable version of sendEmail
     for a LONG time.  I really appreciate your help!

  Nick Pasich
   - Passing the email message via STDIN
   - Multiple <to> recpients
   - Log file option
   - Quiet option
   - Cc option
   - Lots of other suggestions and code

  Richard Duim
   - For mime/content-type/attachment suggestions

  Ulisses Montenegro
   - First one to report problems with bare LF's on qmail servers

  Michael Santy
   - Reported problems with various SMTP servers and helped me fix a few
     fairly serious problems.

  Many other people have submitted bug reports and helped to make sendEmail
  what it is today, and my best regards go out to all those .. complainers ;-)


