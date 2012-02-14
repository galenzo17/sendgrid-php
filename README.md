# sendgrid-php #
This library allows you to quickly and easily send emails through SendGrid using PHP.

## License ##
Licensed under the MIT License.

## Install ##
```
git clone git@github.com:sendgrid/sendgrid-php.git
```

## SendGrid APIs ##
SendGrid provides two methods of sending email: the Web API, and SMTP API.  SendGrid recommends using the SMTP API for sending emails.
For an explanation of the benefits of each, refer to http://docs.sendgrid.com/documentation/get-started/integrate/examples/smtp-vs-rest/.

This library implements a common interface to make it very easy to use either API.

## Mail Pre-Usage ##

Before we begin using the library, its important to understand a few things about the library architecture...

* The SendGrid Mail object is the means of setting mail data. In general, data can be set in three ways for most elements:
  1. set - reset the data, and initialize it to the given element. This will destroy previous data
  2. set (List) - for array based elements, we provide a way of passing the entire array in at once. This will also destroy previous data.
  3. add - append data to the list of elements.

* Sending an email is as simple as :
  1. Creating a SendGrid Instance
  1. Creating a SendGrid Mail object, and setting its data
  1. Sending the mail using either SMTP API or Web API.

## Mail Usage ##

To begin using this library, you must first include it

```php
include 'path/to/sendgrid-php/SendGrid_loader.php';
```

Then, initialize the SendGrid object with your SendGrid credentials

```php
$sendgrid = new SendGrid('username', 'password');
```

Create a new SendGrid Mail object and add your message details

```php
$mail = new SendGrid\Mail();
$mail->addTo('foo@bar.com')->
       setFrom('me@bar.com')->
       setSubject('Subject goes here')->
       setText('Hello World!')->
       setHtml('<strong>Hello World!</strong>');
```

Send it using the API of your choice (SMTP or Web)

```php
$sendgrid->smtp->send($mail);
```
Or 

```php
$sendgrid->web->send($mail);
```