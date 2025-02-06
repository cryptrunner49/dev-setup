# Ruby on Rails 8 setup

## Create a new rails project

```bash
rails new webapp --database=postgresql
cd webapp
```

## Add tailwindcss

### Add the gems to the Gemfile

```ruby
gem "tailwindcss-ruby", "~> 3.4"
gem "tailwindcss-rails", "~> 3.3"
```

### Install the gems

```bash
bin/bundle install
```

### Install Tailwind CSS

```bundle
bin/rails tailwindcss:install
```

### Build the files and run the server

```bash
bin/dev
```

### Test tailwind

```html
<h1 class="text-3xl font-bold underline">
    Hello world!
</h1>
```
