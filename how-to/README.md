# How do I ...



## ...start a new Rails app?


  $ gem install suspenders
  $ suspenders the-name-of-your-project-here
  $ cd the-name-of-your-project-here/
  $ bin/setup
  $ rake


## ...feature-test a Rails app's Javascript?

Use capybara-webkit_. In your ``Gemfile``:

```ruby
gem "capybara-webkit"
```

In `spec/support/capybara_webkit.rb` (for Rspec):

```ruby
Capybara.javascript_driver = :webkit

Capybara::Webkit.configure do |config|
  config.block_unknown_urls
end
```

When writing a spec, you must set the `:js` flag for that test to make use of capybara-webkit. For example, in `spec/features/user_signs_in_spec.rb`:

```ruby
feature "Authentication", :js do
  scenario "A user signing in" do
    create(:user, email: "me@example.com", password: "sekrit")

    sign_in_as email: "me@example.com", password: "sekrit"

    expect(page).to have_text("Welcome!")
  end
end
```
