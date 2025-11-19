# frozen_string_literal: true

source "https://rubygems.org"

gem "jekyll-theme-chirpy", "~> 6.4", ">= 6.4.2"

group :test do
  gem "html-proofer", "~> 5.1"
end

# Add the critical dependencies that were missing
gem "nokogiri", "~> 1.18"
gem "pdf-reader", "~> 2.15"
gem "typhoeus", "~> 1.5"
gem "tiff", "~> 0.1"
gem "ttfunk", "~> 1.8"
gem "ruby-rc4", "~> 0.1"
gem "afm", "~> 1.0"
gem "hashery", "~> 2.1"
gem "io-event", "~> 1.14"
gem "metrics", "~> 0.15"
gem "traces", "~> 0.18"
gem "fiber-local", "~> 1.1"
gem "fiber-storage", "~> 1.0"
gem "fiber-annotation", "~> 0.2"
gem "console", "~> 1.34"
gem "zeitwerk", "~> 2.7"
gem "yell", "~> 2.2"
gem "async", "~> 2.34"
gem "benchmark", "~> 0.5"
gem "rainbow", "~> 3.1"
gem "ethon", "~> 0.15"
gem "Ascii85", "~> 2.0"

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]

# Specify Ruby version
ruby "3.4.4"