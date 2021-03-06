# Validating Vue 3 Forms

## L2 - Setting Up

### Cleaning Up

This is working great so far, but I want to do a bit of a cleanup with how we are setting up our email constant, and briefly talk about JavaScript deconstructing.

Notice how the useFieldmethod returns an object. In this object there are quite a few properties, and we’re capturing them all (as a full object) inside the email constant.

```javaScript
const email = useField(...)
```

Then, we go ahead and access those properties of the email object in our return statement, and pass return them like so:

```javaScript
return {
  onSubmit,
  email: email.value,
  emailError: email.errorMessage
}
```

This perfectly ok to do, and this verboseness can sometimes lead to code clarity, which is always a good thing. But often when working with the Composition API you will notice that most resources will make use of JavaScript deconstructing.

Deconstructing in itself is beyond the scope of this course, but MDN has [a great article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) that explains it in detail.

The previous example, written using JavaScript deconstructing, looks like this:

```javaScript
const { value, errorMessage } = useField(...)

return {
  onSubmit,
  email: value,
  emailError: errorMessage
}
```

The property value and errorMessage of the object returned by useField are now readily available to us as variables, so we can pass them directly into the return statement.

There’s one last bit I want to show you before we move on. There are times we will need to rename these properties for clarity, or because they may conflict with one another. In JavaScript, we can rename a deconstructed property by adding a : colon after the property in the deconstructed syntax, and the new name.

Let me show you a working example. Let’s rename the value to email, and the errorMessage to emailError.

```javaScript
const { value: email, errorMessage: emailError } = useField(...)

return {
  onSubmit,
  email: email,
  emailError: emailError
}
```

Both syntaxes are completely fine, so feel free to use whichever makes more sense to you with our examples.

## L6 Lazy Validation

### Listening to change and not input

Input: Fires every time the user adds or deletes a character in the field.

Change: Fires once the field loses focus

### Handling changes in multiple inputs

If your form consists of several inputs, the approach of using handleChange for each one of them may become cumbersome as we have learned in previous lessons.

In these cases, there is a function named setFieldValue that can be extracted from the useForm composition function.

You may be wondering why you would need to use this magic method instead of directly updating the form’s model. The setFieldValue function will trigger the validation rules on the form’s field who was modified, which would not be the case if we modified it directly.

For more information on setFieldValue please check out the [official docs](https://vee-validate.logaretm.com/v4/api/use-form#composable-api).
