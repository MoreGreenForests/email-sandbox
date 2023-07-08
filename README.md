# Test Bed and Best Practices for Email

Great history of email protocols, some protocol basics, and some new tools to handle common issues:
https://www.youtube.com/watch?v=mrGfahzt-4Q

## SMTP (Simple Mail Transfer Protocol)

### Use nslookup
nslookup is a network administration command-line tool for querying the Domain Name System to obtain the mapping between domain name and IP address, or other DNS records. 

```bat
C:> nslookip

```

### MX or Mail Exchange Records

```bat
> set type=mx
>funwith.email

```
In a one liner
```bat
> nslookup -type=mx zh.funwith.email
```

### Example of manual smtp

```bat
> telnet smtp1.funwith.email 25
220 smtp1.funwith.email SMTP. Nice to see you.
HELO dylanbeattie.net
250 smt1.funwith.email
MAIL FROM: <dylan@dylanbeattie.net>
250 OK
RCPT TO <hellow@funwith.email>
250 OK
DATA
354 End data with <CR><LF>.<CR><CF>
Hello!
.
250 Queued as E9E550BE9R6
QUIT 
221 BYE
```

Can check if relaying is disallowed for the recipiant doing this manually.

CAN-SPAM Act 2003

## ESMTP (Extended Simple Mail Transfer Protocol)

SMTP uses HELO and ESMTP uses EHLO

Checking allowed methods.

```bat
telnet smtp1.funwith.email 25
220 smtp1funwith.email SMTP. Nice to see you
EHLO dylanbeattie.net
250-smtp1funwith.email Hello dylanbeattie.net
250-AUTH PLAIN LOGIN CRAM-MD5
250-STARTTLS
250-ENHANCEDSTATUSCODES

STARTTLS
220 Start TLS
EHLO dylanbeattie.net
250-smtp1funwith.email Hello dylanbeattie.net
AUTH PLAIN ZnVud210aDplbWFpbA==
235 Authentication successful
```

Most corporate and other email servers and exchanges use spam blacklists. If someone reports you you need to request to be whitelisted again. Some have validation but others do not.

Some common ones are:
BACKSCATTERER
BARRACUDA
NIXSPAM
LASHBACK
PSBL
SPAMCOP
and 

You can check if your domain is listed at these services


## SMTP vs MIME (Multipurpose Internet Mail Extensions)

7 bit ascii for any simple email

Anything more we need to use mixed format or MIM

MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="a239rfanwoefho9"

You need to set the types in a multipart message so by type:

text/plain
text/html
image/png

Or Adding an attachment
Content-Type: image/png: name=test.png
Content-Transfer-Encoding: base64
Content-Disposition: attachment: filename=test.png

## Can try MJML
https://www.mailjet.com/resources/email-tools/mjml/

Can create in MJML and compile so it works with various devices and platforms

## Mailtrap
https://mailtrap.io/
Gives HTML looks and what platforms will work and not work. Spam analysis and more.
