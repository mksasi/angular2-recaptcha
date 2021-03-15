![Travis](https://travis-ci.org/mksasi/angular2-recaptcha.svg?branch=master)

# Angular 11 : TypeScript component for Google reCaptcha 2

This is just very simple Angular 2 component that implements Google [reCaptcha 2](https://www.google.com/recaptcha/intro/index.html).

Based on [xmaestro/angular2-recaptcha](https://github.com/xmaestro/angular2-recaptcha). Updated to Angular 11 by [mksasi](https://github.com/mksasi/angular2-recaptcha)

Installation
--------------------------------------

Install it from npm:

```bash
npm install @mksasi/angular2-recaptcha
```

Usage
--------------------------------------

### SystemJS config

```js
System.config({
    map: {
        'angular2-recaptcha': 'node_modules/angular2-recaptcha'
    },
    packages: {
        app: {
            format: 'register',
            defaultExtension: 'js'
        },
        'angular2-recaptcha': {defaultExtension: 'js', main:'index'}
    }
});
```

### Module

```typescript
...
import { ReCaptchaModule } from 'angular2-recaptcha';
...
```

```typescript
 ...
@NgModule({
  imports: [...,ReCaptchaModule]
  })
  ...
```

### View

Use in template like below

```html
 <re-captcha site_key="<GOOGLE_RECAPTCHA_KEY>"></re-captcha>
```

Where **site_key** is the Google reCaptcha public key. Optional parameters as follows:
 * **language** One of the ISO language values supported by Google: https://developers.google.com/recaptcha/docs/language Note that due to the design of the reCaptcha API, only the first component on a page can change the language from default English.
 * **theme** Either `light` (default) or `dark`.
 * **type** Either `image` (default) or `audio`.
 * **size** Either `normal` (default), `compact` or `invisible`.
 * **tabindex** Tabindex for navigation, default 0.
 * **global** If true, the reCaptcha script will be loaded from www.recaptcha.net instead of www.google.com


## Callback

To catch the success callback, you will need to subscribe to the `captchaResponse` event. The response token will be passed in the `$event` parameter.
To wait for component to be loaded subscribe to `loaded` event.

```html
<re-captcha (captchaResponse)="handleCorrectCaptcha($event)" (loaded)="sendCaptchaExecuteHere()" site_key="<GOOGLE_RECAPTCHA_KEY>"></re-captcha>
```

The event `captchaExpired` is triggered when the displayed image has expired. It does not have any event parameters.

## Methods

To access the methods, use [@ViewChild](https://angular.io/docs/ts/latest/api/core/index/ViewChild-decorator.html).

### Import
```typescript
import { ViewChild } from '@angular/core';
import { ReCaptchaComponent } from 'angular2-recaptcha';

export class RegisterComponent {
  @ViewChild(ReCaptchaComponent) captcha: ReCaptchaComponent;
}
```

### Usage
You can request a new captcha to be displayed:
```typescript
this.captcha.reset();
```

The previous response can be retrieved:
```typescript
let token = this.captcha.getResponse();
```
