# Best Practices

A guide for programming well.

## General

* These are not to be blindly followed; strive to understand these and ask when in doubt.
* Don't duplicate the functionality of a built-in library.
* Don't swallow exceptions or "fail silently."
* Don't write code that guesses at future functionality.
* Exceptions should be exceptional.
* Keep the code simple.

## Object-Oriented Design

* Avoid global variables.
* Avoid long parameter lists.
* Limit collaborators of an object (entities an object depends on).
* Limit an object's dependencies (entities that depend on an object).
* Prefer composition over inheritance.
* Prefer small methods. Between one and five lines is best.
* Prefer small classes with a single, well-defined responsibility. When a class exceeds 100 lines, it may be doing too many things.
* [Tell, don't ask].

[Tell, don't ask]: https://robots.thoughtbot.com/tell-dont-ask

## Ruby

* Avoid optional parameters. Does the method do too much?
* Avoid monkey-patching.
* Generate necessary [Bundler binstubs] for the project, such as `rake` and `rspec`, and add them to version control.
* Prefer classes to modules when designing functionality that is shared by multiple models.
* Prefer `private` when indicating scope. Use `protected` only with comparison methods like `def ==(other)`, `def <(other)`, and `def >(other)`.

[Bundler binstubs]: https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs

## Ruby Gems

* Declare dependencies in the `<PROJECT_NAME>.gemspec` file.
* Reference the `gemspec` in the `Gemfile`.
* Use [Appraisal] to test the gem against multiple versions of gem dependencies (such as Rails in a Rails engine).
* Use [Bundler] to manage the gem's dependencies.
* Use [Travis CI] for Continuous Integration, indicators showing whether GitHub pull requests can be merged, and to test against multiple Ruby versions.

[Appraisal]: https://github.com/thoughtbot/appraisal
[Bundler]: http://bundler.io
[Travis CI]: http://travis-ci.org

## Rails

* [Add foreign key constraints][fkey] in migrations.
* Avoid bypassing validations with methods like `save(validate: false)`, `update_attribute`, and `toggle`.
* Avoid instantiating more than one object in controllers.
* Avoid naming methods after database columns in the same class.
* Don't change a migration after it has been merged into master if the desired change can be solved with another migration.
* Don't reference a model class directly from a view.
* Don't return false from `ActiveModel` callbacks, but instead raise an exception.
* Don't use instance variables in partials. Pass local variables to partials from view templates.
* Don't use SQL or SQL fragments (`where('inviter_id IS NOT NULL')`) outside of models.
* Generate necessary [Spring binstubs] for the project, such as `rake` and `rspec`, and add them to version control.
* If there are default values, set them in migrations.
* Keep `db/schema.rb` or `db/development_structure.sql` under version control.
* Use only one instance variable in each view.
* Use SQL, not `ActiveRecord` models, in migrations.
* Use the [`.ruby-version`] file convention to specify the Ruby version and patch level for a project.
* Use `_url` suffixes for named routes in mailer views and [redirects].  Use `_path` suffixes for named routes everywhere else.
* Use a [class constant rather than the stringified class name][class constant in association] for `class_name` options on ActiveRecord association macros.
* Validate the associated `belongs_to` object (`user`), not the database column (`user_id`).
* Use `db/seeds.rb` for data that is required in all environments.
* Use `dev:prime` rake task for development environment seed data.
* Prefer `cookies.signed` over `cookies` to [prevent tampering].
* Prefer `Time.current` over `Time.now`
* Prefer `Date.current` over `Date.today`
* Prefer `Time.zone.parse("2014-07-04 16:05:37")` over `Time.parse("2014-07-04 16:05:37")`
* Use `ENV.fetch` for environment variables instead of `ENV[]`so that unset environment variables are detected on deploy.
* [Use blocks][date-block] when declaring date and time attributes in FactoryGirl factories.
* Use `touch: true` when declaring `belongs_to` relationships.

[date-block]: /best-practices/samples/ruby.rb#L10
[fkey]: http://robots.thoughtbot.com/referential-integrity-with-foreign-keys
[`.ruby-version`]: https://gist.github.com/fnichol/1912050
[redirects]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.30
[Spring binstubs]: https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs
[prevent tampering]: http://blog.bigbinary.com/2013/03/19/cookies-on-rails.html
[class constant in association]: https://github.com/thoughtbot/guides/blob/master/style/rails/sample.rb

## Testing

* Avoid `any_instance` in rspec-mocks and mocha. Prefer [dependency injection].
* Avoid `its`, `specify`, and `before` in RSpec.
* Avoid `let` (or `let!`) in RSpec. Prefer extracting helper methods, but do not re-implement the functionality of `let`. [Example][avoid-let].
* Avoid using `subject` explicitly *inside of an* RSpec `it` block. [Example][subject-example].
* Avoid using instance variables in tests.
* Disable real HTTP requests to external services with `WebMock.disable_net_connect!`.
* Don't test private methods.
* Test background jobs with a [`Delayed::Job` matcher].
* Use [stubs and spies] \(not mocks\) in isolated tests.
* Use a single level of abstraction within scenarios.
* Use an `it` example or test method for each execution path through the method.
* Use [assertions about state] for incoming messages.
* Use stubs and spies to assert you sent outgoing messages.
* Use a [Fake] to stub requests to external services.
* Use integration tests to execute the entire app.
* Use non-[SUT] methods in expectations when possible.

[dependency injection]: http://en.wikipedia.org/wiki/Dependency_injection
[subject-example]: ../style/testing/unit_test_spec.rb
[avoid-let]: ../style/testing/avoid_let_spec.rb
[`Delayed::Job` matcher]: https://gist.github.com/3186463
[stubs and spies]: http://robots.thoughtbot.com/post/159805295/spy-vs-spy
[assertions about state]: https://speakerdeck.com/skmetz/magic-tricks-of-testing-railsconf?slide=51
[Fake]: http://robots.thoughtbot.com/post/219216005/fake-it
[SUT]: http://xunitpatterns.com/SUT.html

## Bundler

* Specify the [Ruby version] to be used on the project in the `Gemfile`.
* Use a [pessimistic version] in the `Gemfile` for gems that follow semantic versioning, such as `rspec`, `factory_girl`, and `capybara`.
* Use a [versionless] `Gemfile` declarations for gems that are safe to update often, such as pg, thin, and debugger.
* Use an [exact version] in the `Gemfile` for fragile gems, such as Rails.

[Ruby version]: http://bundler.io/v1.3/gemfile_ruby.html
[exact version]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[pessimistic version]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[versionless]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle

## Web

* Avoid a flash of Unstyled Text, even when no cache is available.
* Avoid rendering delays caused by synchronous loading.
* Use `https` instead of `http` when linking to assets.

## JavaScript

* Use the latest stable JavaScript syntax with a transpiler, such as [babel].
* Include a `to_param` or `href` attribute when serializing ActiveRecord models, and use that when constructing URLs client side, rather than the ID.
* Prefer `data-*` attributes over `id` and `class` attributes when targeting HTML elements.
* Avoid targeting HTML elements using classes intended for styling purposes.

[babel]: https://babeljs.io/

## HTML

* Use `<button>` tags over `<a>` tags for actions.

## CSS

- Document the project's CSS architecture (the README, component library or style guide are good places to do this), including things such as:
- - Organization of stylesheet directories and Sass partials
- - Selector naming convention
- - Code linting tools and configuration
- - Browser support
- Use Sass.
- Use [Autoprefixer][autoprefixer] to generate vendor prefixes based on the project-specific browser support that is needed.
- Prefer `overflow: auto` to `overflow: scroll`, because `scroll` will always display scrollbars outside of macOS, even when content fits in the container.

[autoprefixer]: https://github.com/postcss/autoprefixer

## Sass

* When using [sass-rails], use the provided [asset-helpers][asset-helpers] (e.g. `image-url` and `font-url`), so that Rails' Asset Pipeline will re-write the correct paths to assets.
* Prefer mixins to `@extend`.

[sass-rails]: https://github.com/rails/sass-rails
[asset-helpers]: https://github.com/rails/sass-rails#asset-helpers

## Browsers

* Avoid supporting versions of Internet Explorer before IE11.

## Objective-C

* Setup new projects using [Liftoff](https://github.com/thoughtbot/liftoff) and follow provided directory structure.
* Prefer categories on `Foundation` classes to helper methods.
* Prefer string constants to literals when providing keys or key paths to methods.

## Ruby JSON APIs

* Review the recommended practices outlined in Heroku's [HTTP API Design Guide] before designing a new API.
* Use a fast JSON parser, e.g. [`oj`][oj]
* Write integration tests for your API endpoints. When the primary consumer ofthe API is a JavaScript client maintained within the same code base as the provider of the API, write [feature specs]. Otherwise write [request specs].

[HTTP API Design Guide]: https://github.com/interagent/http-api-design
[oj]: https://github.com/ohler55/oj
[feature specs]: https://www.relishapp.com/rspec/rspec-rails/docs/feature-specs/feature-spec
[request specs]: https://www.relishapp.com/rspec/rspec-rails/docs/request-specs/request-spec
