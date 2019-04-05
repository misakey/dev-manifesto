# Conventions

## Backend

### HTTP 

All HTTP responses should set a valid HTTP code that fits the reality of the response. 
If you have a doubt on which code to use, feel free to ask!

### Error conventions

Backend errors follow these two conventions: 

Return the HTTP error code that fits
Return a JSON object of this shape:
```
{
  "error_code": "an_error_code_that_wont_evolve_for_the_frontend",
  "error_description": "A human readable description of the error, useful for debugging." 
}
```

### API Format

For each API that don't need to follow a specific standard (like OAuth for the authentication), we aim to implement the [JSON:API](https://jsonapi.org/) specs.

### Emailing 

All email we send should follow email's RFC.
Particulary we should implement an HTML and a plain text version of the content

## Internationalization (I18N)

Most of the I18N should be done in frontend. So the backend will send to frontend translation tokens.
For the few cases that are not working in frontend (like sending emails), the I18N should be possible too (and as much as possible the language should be defined by the frontend)

### Frontend

We use I18Next as a frontend I18N framework.