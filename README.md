# Trend

Ruby client for [Trend](https://trendapi.org), the anomaly detection and forecasting API

[![Build Status](https://travis-ci.org/ankane/trend.svg?branch=master)](https://travis-ci.org/ankane/trend)

## Getting Started

Add this line to your application’s Gemfile:

```ruby
gem 'trend'
```

### Anomaly Detection

Detect anomalies in a time series

```ruby
# generate series
series = {}
date = Date.parse("2018-04-01")
28.times do
  series[date] = rand(100)
  date += 1
end

# add an anomaly on Apr 21
series[date - 8] = 999

Trend.anomalies(series)
```

Works great with libraries like [Groupdate](https://github.com/ankane/groupdate)

```ruby
series = User.group_by_day(:created_at).count
Trend.anomalies(series)
```

### Forecasting

Get future predictions for a time series

```ruby
series = {}
date = Date.parse("2018-04-01")
28.times do
  series[date] = date.wday
  date += 1
end

Trend.forecast(series)
```

Also works great with Groupdate

```ruby
series = User.group_by_day(:created_at).count
Trend.forecast(series)
```

Specify the number of predictions to return

```ruby
Trend.forecast(series, count: 3)
```

### Correlation [experimental]

Get the correlation between two time series

```ruby
Trend.correlation(series, series2)
```

## Authentication

An API key is needed for more than 1000 requests per day per IP. [Email us](mailto:hi@trendapi.org) to get one.

If you have one, set `ENV["TREND_API_KEY"]` or use:

```ruby
Trend.api_key = "secret"
```

## History

View the [changelog](https://github.com/ankane/trend/blob/master/CHANGELOG.md)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/ankane/trend/issues)
- Fix bugs and [submit pull requests](https://github.com/ankane/trend/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features

To get started with development and testing:

```sh
git clone https://github.com/ankane/trend.git
cd trend
bundle install
rake test
```
