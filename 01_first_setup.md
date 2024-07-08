# prepare blog directory

## Install temporary jekyll to create blog blueprint

`jekyll` のブログ作成ようのテンポラリディレクトリを作成。
`jekyll new` コマンドのあと、削除しても良い。

```bash
mkdir jekyll_base
```

以下の `Gemfile` を作る。

```ruby
cd jekyll_base
source 'https://rubygems.org'

gem 'jekyll'
```

## install gems

gem のインストール。

```bash
bundle config path vendor
bundle install
```

## Create blog files

ブログ作成、

```bash
bundle exec jekyll new ../techno
```

このあとは、 `jekyll_base` を消しても良い。
今後は、上で作った `techno` のディレクトリ以下のみを使う。

# ブログ環境の構築

## install theme and github page plugin

`Gemfile` を以下のように変更する。

- `jekyll` のコメントアウト
- `minima` のコメントアウト
- `github-pages` のコメントアウトを解除
- `webrick` を追加
- `beautiful-jekyll-theme` を追加

`Gemfile` は以下のようになる。

```ruby
source "https://rubygems.org"
# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
# gem "jekyll", "~> 4.3.3"
# This is the default theme for new Jekyll sites. You may change this to anything you like.
# gem "minima", "~> 2.5"
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins
gem 'webrick'
# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "beautiful-jekyll-theme"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
```

## install gems

gems のインストール

```bash
cd ../techno

bundle config path vendor
bundle install
```

## github page 用 CI のセットアップ

`jekyll.yml` を `.github/workflows` ディレクトリへコピーする。

```bash
mkdir -p .github/workflows
cp ../jekyll_setup/jekyll.yml .github/workflows
```