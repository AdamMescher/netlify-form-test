# netlify-form-test

### Testing Netlify static site form submissions

## Working Example

[Live Site](https://zealous-kepler-45c703.netlify.com/)

<form> code:

```html
<form name="contact" method="POST" data-netlify="true">
    <label for="full-name">Your Name<input required name="name" type="text" id="name" /></label>
    <label for="email">Your Email<input required name="email" type="email" id="email" /> </label>
    <label for="phone">Your Phone Number (optional)<input name="phone" type="tel" id="phone" /> </label>
    <label for="body">Message<textarea required name="body" id="body"></textarea></label>
    <div data-netlify-recaptcha></div>
    <input class="submit-btn" type="submit" value="Just Gonna Send It"/>
</form>
```



### Docs and Common Problems

[Netlify Form Docs](https://www.netlify.com/docs/form-handling/)

[Why my forms were blank](https://stackoverflow.com/a/49859661)

our service requires a plain html version of your form, with a name parameter as well as the netlify or data-netlify=true parameter; this is what prepares your site to accept form submissions

If you see the form in your dashboard, yet get a blank submission when you are sure data was POSTed, this probably has one of three causes:

Netlify did not correctly process your field names from the html version of your form. The service will only properly handle the fields which we see in that html version at deploy time.
Netlify does matching by field name at submission time, so make sure that what your site sends to us then matches up between with your deployed html copy of the form. This happens automatically for pure html (no JS) forms since you are POSTing from the file which is the canonical "definition" of your form fields; however for javascript forms you need to take care that the names match up. Put another way, you cannot later add new fields dynamically in javascript and send them (Netlify will accept all fields, as you have seen; but will not store them or notify you about ones that were not processed at deploy time!)
One more quirk that could get in the way: having multiple copies of a form with the same name in your deploy. Only one will be processed, so if you happen to have an errant <form name=test netlify></form> in another html file (or even the same one!) - it could be the one that we process rather than the other form also named test. So, make sure that you only send a single html definition of your form. Note that some frameworks like gatsby render your jsx down into html before deploy, meaning that if you have a plain html file form definition in your deploy - it could be processed instead of the copy gatsby built.
