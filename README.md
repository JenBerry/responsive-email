# Responsive email template.
## The objective
Here I will make a responive HTML email template. It will have two columns which condense down to one column on smaller screens.
```
_________________                   _________
| Header        |                   |Header |
|_______________|           |\      |_______|
|Column1|Column2|   --------| \     |Column1|
|       |       |   --------| /     |       |
|       |       |           |/      |       |
|_______|_______|                   |_______|
|Footer         |                   |Column2|
|_______________|                   |       |
                                    |       |
                                    |_______|
                                    |Footer |
                                    |_______|
```

It will work on almost all the email clients I can test with Litmus (https://litmus.com), including all versions of Outlook and Gmail. The only clients causing problems are old versions of Lotus notes, but it will still be readable.

I will also test the email directly in the following clients:

- Web
  - Gmail on Chrome
  - Yahoomail on Chrome
  - Outlook on Chrome
- Desktop
  - Apple Mail
- Mobile
  - Gmail app for Android
  - Android Mail

## Cerberus: basic template
http://tedgoas.github.io/Cerberus/

Looking on the web for something that will do this. I find Cerberus

At first glance, Cerberus appears to be exactly what we want, but on closer inspection we can see that it is not. Their first template does exactly what we want, but only in clients that support media queries, so not gmail. Their second template does work on gmail, but doesn't exhibit the desired behaiour of two columns condensing down to one.

Gmail is a client we simply can't ignore. Litmus ranks it as #2 in the world (http://emailclientmarketshare.com/). So I will have to find my own solution. However I did take a few styling ideas from Cerberus to help fix known problems

## The basics

So, lets try a basic, responsive email. No columns or funny business to start.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Responsive Email</title>
</head>
<body style="margin: 0; padding: 0; width:100%; height:100%;">
  <table class="email_body" width="100%" cellspacing="0" cellpadding="10" border="0" bgcolor="#A6A3FC">
    <tr>
      <td align="center">
        <table class="wrapper" style="max-width:600px;" cellspacing="0" cellpadding="10" border="0" bgcolor="#C0C0FF">
          <tr>
            <td>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facilis fugit possimus sunt reiciendis sequi eligendi pariatur sapiente, expedita amet quaerat et molestiae deserunt? Asperiores assumenda id, voluptatum illo minus rem fuga, delectus cupiditate vitae enim tempore consequuntur ipsam doloremque, recusandae facere ipsum error eum harum minima nisi! Earum modi aspernatur soluta aliquid doloribus minus accusamus animi quis vel. Nihil itaque doloribus ducimus aliquam voluptatibus molestiae adipisci iusto quos quisquam sint quae deserunt quasi ipsum ea praesentium optio tempore eos qui asperiores atque, deleniti nobis laboriosam ut quis? Nihil quas debitis qui dicta illum. Sunt accusantium, repudiandae aperiam culpa praesentium est!
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
</body>
</html>
```

We use the strict XHTML doctype as this is what your email client is likely to be using. The head is what you would expect for a responsive page, although many clients will discard this too.

So we have an `email_body` table, which will fill the available width of the email. It's contents are aligned `center` to center the email wrapper in the email window.
And we have a `wrapper` table, set to a max-width of 600px.
Both tables have a cellpadding of 10px, and background colours to help us see what is going on.

Lets see what Litmus makes of this.

Firstly we can see that most of the desktop clients are ignoring our min-width

![alt text](email1/Outlook-2011.png "Outlook 2011")

Thunderbird is the only one to get it right.
![alt text](email1/Thunderbird.png "Thunderbird")

As for Lotus notes 8...
![alt text](email1/Lotus-Notes-8.png "Lotus Notes 8")
Well lets just not go there...

Secondly we can see the treatment of the text alignment is inconsistent. Some Clients, such as older versions of outlook and some web based clients running on internet explorer, are centering the text of the `wrapper` table, rather than just centering the `wrapper` table in the `email_body`. Fortunately this is an easy fix, just add `align="left"` to the `email_body` table
![alt text](email1/Gmail-ie.png "Gmail (Explorer)")

On the bright side. All the mobiles and tablets are working pretty much how we would like them too.
![alt text](email1/Iphone-6+.png "Ipone 6 Plus")
