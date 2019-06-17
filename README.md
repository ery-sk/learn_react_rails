# Railsアプリケーションに後から部分的にReactを導入する

```sh
ruby -v
# ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin17]

rails -v
# Rails 5.2.3

bundler -v
# Bundler version 1.17.2

node -v
# v12.4.0

yarn -v
# 1.16.0
```

## 普通にアプリケーションを作成する

```sh
rails new . -T -O
rails g controller hello index
```
```rb
# config/routes.rb
Rails.application.routes.draw do
  root 'hello#index'
end
```
```sh
# 確認
bin/rails s
```

## 適当なjQueryを使う
```sh
echo "gem 'jquery-rails'" >> Gemfile
bundle
```
```js
//= require jquery
```
```html
<%= button_tag 'Hello', type: 'button', id: 'hello-jquery' %>
```
```coffee
$ ->
  $('#hello-jquery').click ->
    alert('Hello jQuery')
```
```sh
# 確認
bin/rails s
```

## WebpackerとReactの導入
```sh
echo "gem 'webpacker'" >> Gemfile
echo "gem 'react-rails'" >> Gemfile
bundle
rails webpacker:install
rails webpacker:install:react
```
```sh
ls bin/
# bundle			setup			webpack
# rails			spring			webpack-dev-server
# rake			update			yarn
```

## jQueryとReactの共存確認

```html
<!-- app/views/layouts/application.html.erb -->
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```

```js
// app/javascript/packs/application.js
require('./hello_react.jsx')
```

起動

```sh
$ bin/webpack-dev-server
$ bin/rails s
```
<img width="1280" alt="index" src="https://user-images.githubusercontent.com/38872854/59580219-361c4180-910b-11e9-838c-44858bca0372.png">

🎉🎉🎉🎉🎉🎉
