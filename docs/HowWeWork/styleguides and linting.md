# Styleguides and Linting

As a team we do not want to spend time being sticklers when it comes to code styling. As questions arise we are able to look to larger companies as they often have public styleguides which contain best practices for specific languages. We have also set up several linters to makes sure that code is working properly before being merged into main branches.  

## Languages and Styleguides

Below are the standard languages we use for the work within our department as well as links to current top standards for styleguides and coding best practices.

- HTML
    - https://google.github.io/styleguide/htmlcssguide.html#HTML

- Javascript
    - https://airbnb.io/javascript/

- CSS
    - https://google.github.io/styleguide/htmlcssguide.html#CSS

- Twig
    - https://twig.symfony.com/doc/2.x/coding_standards.html

- PHP
    - https://www.php-fig.org/psr/psr-1/ 
    - https://www.php-fig.org/psr/psr-12/

- Python
    - https://peps.python.org/pep-0008/

- JSON
    - https://google.github.io/styleguide/jsoncstyleguide.xml

- JSON-LD
    - https://json-ld.org/spec/latest/json-ld-api-best-practices/

- YAML
    - https://www.tutorialspoint.com/yaml/yaml_quick_guide.htm

- MarkDown
    - https://google.github.io/styleguide/docguide/style.html

## Linting

We currently have linters set up for the following all using super-lint: 

- Javascript using eslint
- CSS using stylelint
- PHP using the PHP Internal Linter
- Python using pylint

We also have special rules set up for Javascript and CSS

### Javascript Rules (eslint)

```
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "double"],
    "semi": ["error", "always"]
```

### CSS Rules (stylelint)

```

"indentation": [
    2,
    {
    "except": ["value"],
    "severity": "error",
    "ignore": ["param"],
    "indentClosingBrace": false
    }

    "declaration-colon-space-after": "always-single-line",
    "declaration-colon-newline-after": "always-multi-line",
    "no-descending-specificity": null,
    "max-nesting-depth": 2,
    "declaration-no-important": true,
    "declaration-block-no-duplicate-properties": true

```