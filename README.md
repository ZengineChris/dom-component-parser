# dom-component-parser

[![Latest Version on NPM](https://img.shields.io/npm/v/dom-component-parser.svg?style=flat-square)](https://npmjs.com/package/dom-component-parser)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/spatie/dom-component-parser/master.svg?style=flat-square)](https://travis-ci.org/spatie/dom-component-parser)

Sometimes you want to be able to quickly set up a JavaScript component in your dome with some settings. Libraries like [Vue.js](https://github.com/vuejs/vue) provide a powerful API to create custom components, but is quite heavy for cases like mounting third party libraries to your DOM.

Say we want to mount a hypothetical `Uploader` component on all `.js-uploader` nodes:

```html
<div
    class="js-uploader"
    data-url="http://my-site.com/upload1"
    data-multiple
></div>
<div
    class="js-uploader"
    data-url="http://my-site.com/upload2"
></div>
```

Now let's retrieve the DOM node and read out the options in JavaScript:

```js
for (let node of document.querySelectorAll('.js-uploader')) {
    const url = element.getAttribute('data-url');
    const multiple = element.getAttribute('data-multiple') === '' ? true : false;

    if (!url) throw new Error();

    new Uploader(element, { url, multiple });
}
```

The `dom-component-parser` cleans up the above process by declaring a component name and options object shape.

```js
import component from 'dom-component-parser';

component('uploader', {
    url: 'required', // `required` is a special flag, will throw an error if missing
    multiple: false, // Defaults to false
}).forEach(({ node, options }) => new Uploader(node, options));
```

Spatie is a webdesign agency based in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## Install

You can install the package via npm:

```bash
$ npm install dom-component-parser
```

## Usage

```html
<div class="js-my-uploader" data-upload-url="http://example.com"></div>
```

```js
import component from 'dom-component-parser';

const myUploaders = component('my-uploader', { uploadUrl: '' });
// => [ { node: <DOMNode>, options: { uploadUrl: 'http://example.com' } } ]
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ npm run test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please contact [Sebastian De Deyne](https://github.com/sebastiandedeyne) instead of using the issue tracker.

## Credits

- [Sebastian De Deyne](https://github.com/sebastiandedeyne)
- [All Contributors](../../contributors)

## About Spatie
Spatie is a webdesign agency based in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
