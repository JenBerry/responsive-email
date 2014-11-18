Here I will make a responive HTML email template. It will have two columns which condense down to one column on smaller screens.
```
_________________					_________
| Header		|					|Header |
|_______________|			|\		|_______|
|Column1|Column2|	--------| \		|Column1|
|		|		|	--------| /		|		|
|		|		|			|/		|		|
|_______|_______|					|_______|
|Footer			|					|Column2|
|_______________|					|		|
									|		|
									|_______|
									|Footer |
									|_______|
```

It will work on almost all the email clients I can test with Litmus (https://litmus.com). The only clients causing problems are old versions of Lotus notes, but it will still be readable.

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
