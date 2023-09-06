# Contributing

- [Setup](#setup)
- [Creating new themes](#creating-new-themes)
- [Adding localizations](#adding-localizations)

Thanks for considering to contribute!

GitHub's API for Discussions is currently only available through the GraphQL
API, which currently requires authentication for all requests. With the way
giscus works, you'll need to create a GitHub App in order to get it
running on your machine. Follow the [self-hosting guide][self-hosting] to get
it running.

## Setup

To contribute to giscus, follow these steps:

1. [Fork][fork] the repository to your GitHub account.
2. Clone the repository to your device (or use something like Codespaces).
3. Create a new branch in the repository.
4. Make your modifications.
5. Commit your modifications and push the branch.
6. [Create a PR][pr] from the branch in your fork to giscus' `main` branch.

This project is built with [Next.js][next.js] and `yarn` as the package manager.
Here are some commands that you can use:

- `yarn`: install dependencies
- `yarn dev`: compile and hot-reload for development
- `yarn build`: compile and minify for production
- `yarn lint`: lint and fix files
- `yarn start`: serve the compiled build in production mode

## Creating new themes

If you want to submit your custom theme to giscus, create a new file in
[`styles/themes`][themes-dir]. The file name (without `.css`) will be the
theme's key. You can use the other theme files as reference (see
[`custom_example.css`][example]). Once you've added the theme file, add the key
and name to `Theme` in [`lib/variables.ts`][variables] to register it. Please
also update the `config.json` in each localization in the [`locales`][locales]
directory to include a `theme=your_theme_key` key.

If you want to customize the syntax themes, you can change the CSS variables
that start with the `--color-prettylights-syntax-` prefix. See the
[`custom_example.css`][example] file for more details.

To support both light and dark mode based on the user's system preferences, you
can use the `@media (prefers-color-scheme: dark)` query. For more details, see
the [`preferred_color_scheme`][preferred-color-scheme] theme file.

Several [classes prefixed with `gsc-`][gsc-classes] are used in the HTML
generated by giscus. You can take advantage of this to further customize your
theme. Note that the classes and HTML structure are subject to change, as
updates to giscus may require modifications to the HTML. You'll need to make
sure that your theme is up-to-date.

If you want to use a custom theme without submitting it to giscus, you can do
so by using a [custom theme URL][custom-theme-url]. Note that you cannot
`@import` a syntax theme and must inline it in your CSS. That said, if you
create a nice theme, I'd appreciate it if you create a PR instead so others can
use it easily.

## Adding localizations

If your language is not yet supported by giscus, please contribute a
localization! Follow these steps to add a new localization:

1. Copy one of the directories in [locales][locales] and rename the new
   directory into your language's [code][language-codes].
2. Open `common.json` and `config.json` inside the directory.
3. Start translating the strings. Make sure to follow your language's
   [plural rules][plural-rules] for translation keys with an object as the value
   (e.g. those that require `{{ count }}`).
4. Copy one of the README files and name it `README.[code].md`, e.g.
   `README.id.md` and translate the content. Add your language to the new README
   and all the existing READMEs, ordered by the language code.
5. Edit [`i18n.tsx`][i18n-tsx] and update the following variables:
   - `availableLanguages`: include your language code and name.
   - `rtlLanguages`: include your language code if it is a right-to-left
     language.
   - `dateFormatters`, `shortDateFormatters`, `shortDateYearFormatters`, and
     `relativeTimeFormatters`: include new objects with your language code,
     following the existing languages.
6. Edit [`i18n.js`][i18n-js] and include your language.
7. In all of the aforementioned files, make sure that the language list is
   sorted by the language code.
8. [Create a PR][pr] with your localization updates.

[self-hosting]: SELF-HOSTING.md
[fork]: https://github.com/giscus/giscus/fork
[pr]: https://github.com/giscus/giscus/compare
[next.js]: https://github.com/vercel/next.js
[themes-dir]: styles/themes
[example]: styles/themes/custom_example.css
[variables]: lib/variables.ts
[preferred-color-scheme]: styles/themes/preferred_color_scheme.css
[gsc-classes]: https://github.com/giscus/giscus/search?l=TSX&q=gsc
[custom-theme-url]: https://github.com/giscus/giscus/blob/main/ADVANCED-USAGE.md#data-theme
[locales]: locales/
[language-codes]: https://unicode-org.github.io/cldr-staging/charts/latest/supplemental/languages_and_scripts.html
[plural-rules]: https://unicode-org.github.io/cldr-staging/charts/latest/supplemental/language_plural_rules.html
[i18n-tsx]: lib/i18n.tsx
[i18n-js]: i18n.js