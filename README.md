# Sanitization Exercise #2 - JavaScript attack prevention

In this exercise we want to prevent the user from entering HTML tags of any kind, especially the injection of Javascript `<script>` tags into 
our database. 

Why? Because this tags could get get loaded and displayed on another page to another user. And then the JavaScript is actually executed (!) on that users page and can potentially read out confidential information from this user and send it to anywhere.

The common method to prevent Javascript injection is: "escaping". Escaping basically means: Convert all HTML special chars into HTML entities.

Example: The user is allowed to fill in anything he wants into a comment field. We inserts a `<script>` tag. In the backend this tag in the comment will be converted into the string "&lt;script&gt;".

In that way we prevent that somebody can inject a script tag into our database which then could get loaded & executed on a page.


## Escape all your text input fields to prevent tag injections

* Start your app, open the /register form in the browser
    * Enter some text into the About Me field and use HTML tags within it, e.g. `Hello <b>world</b> out there`
    * Submit the form
* Console.log the received data in your POST route
    * You should see the HTML tags entered
* Now escape() the aboutMe field using .escape() in your validator middleware
* Enter again an HTML tag in the About Me field and submit the form
* Check again the Console.log of the received POST data
    * Check that the HTML tags are now transformed into HTML entities, e.g. < is transformed into `&lt;`


## Bonus Task: Password strength checker

* Match a password with regex to contain AT LEAST:
    * one number
    * one lowercase character
    * one uppercase character
    * one special sign out of `[!@#$%^&*+]`
=> Research / google: Regular Expressions > lookahead
    * Lookahead patterns are used to chain multiple pattern checks (?=...)(?=...)
    * So lookahead patterns are typically used to check if the pattern matches "this condition AND that condition AND that other condition, etc" 
=> Research: JavaScript regex patterns for testing "password strength"
    * Now test out your password pattern on regexr.com first
        * Please note that lookahead patterns do NOT SELECT the pattern in the text if it was found
        * You have to check the right upper field "Match", which will indicate if the pattern was found or not
    * If it does work on regexr.com
        * Implement your RegEx in your registration form to validate the password field 
