source "https://rubygems.org"
# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!

# 使用 github-pages gem 来确保版本一致性
gem "github-pages", "~> 232", group: :jekyll_plugins

# 如果你想使用 GitHub Pages，移除 "gem jekyll" 并取消注释下面的行
# gem "github-pages", group: :jekyll_plugins

# 如果你有任何插件，把它们放在这里！
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.17.0"
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

# Add required standard library gems for Ruby 3.4+
gem "csv"
gem "logger"
gem "base64"
gem "bigdecimal"

# 添加必要的 Jekyll 插件
gem "jekyll-sitemap", "~> 1.4.0"
gem "jekyll-seo-tag", "~> 2.8.0"
