---
layout: post
title:      "First Portfolio Project (Ruby CLI Gem - Stocks)"
date:       2020-06-21 20:30:04 -0400
permalink:  first_portfolio_project_ruby_cli_gem_-_stocks
---


We are coming to the end of project week, submits are due at midnight, and what a week it has been.

Three to four weeks into the software engineering bootcamp, my classmate and I have been tasked with showcasi.ng what we have learned from procedural and object oriented ruby.

After many long hours of lessons, study groups, reviewing notes, scouring the web for additional resources, and consuming hours of ruby videos, I am proud to confidently say that I know how to create a ruby CLI gem. I have learned how to walk the talk and even talk the talk (the part which I found the hardest).

It's one thing learning how to write code, but another when you actually understanding what you're doing, what each thing is called, and able to explain it to another.

I decided to create a ruby CLI gem around stocks, my initial flow / idea was grand:
    1. CLI welcomes the user with a greeting
    2. User is prompted to input a response:
        ** Type ticker if you would like to browse through a list of stocks.
        ** Type quote if you would like to see a stocks' price.
        ** Type profile if you would like a company profile of a stock.
    3. User is able to go back to main menu by typing "main menu".
    4. If user types "ticker", user will be shown a list of all stocks.
        ** Coming soon, user will have the option to enter a company name to show the ticker for that company **
    5. If user types "quote", user will be prompted to insert a stock symbol, ex "AAPL", and will receive a quote for pricing information.
    6. If user types "profile", user will be prompted to insert a stock symbol, ex "AAPL", to receive company information.
    7. If user types an invalid stock symbol, program should return "invalid symbol, try again".
    8. User should be able to exit the program by typing "exit" and the program will say, "Thank you, come again!"

Now, my CLI does work and function properly, however the API that I chose seemed to make things much more difficult than they should have been. This file was by the hardest to complete for me, so that altered my CLI flow just a bit, and made me limit functionality to just the stock ticker and company profile for now.

For example, the API url is structured as follows:

base_url + class_api + user_input + api_token

I had to initialize several variable for each section of the api and interpolate arguments on instance methods to get a valid stock symbol for the API's requiring that, here is how I started this file..

```
class Stocks::API

    attr_accessor :base_url, :profile, :quote, :api_key, :ticker

    def initialize
        @base_url = "https://finnhub.io/api/v1"
        @profile = "/stock/profile2?symbol="
        @ticker = "/stock/symbol?exchange=US&token=brm2kafrh5re8ma1q70g"
        @quote = "/quote?symbol="
        @api_key = "&token=brm2kafrh5re8ma1q70g"
    end
```

I decided to start with the ticker class because that API was the simplest, all I needed to do to receive the list was concatenate base_url + ticker_api since no user input was required for the API url, then iterate over each hash within the hash returned by json (found this out thanks to binding.pry). Here is what this looks like:

```
    def ticker_api
        response = RestClient.get(@base_url + @ticker)
        json = JSON(response)
            ticker_array = []
            json.each do |hash|
                ticker_hash = {}
                ticker_hash[:description] = hash["description"]
                ticker_hash[:symbol] = hash["symbol"]
                ticker_array.push(ticker_hash)
            end
        Stocks::Ticker.create_from_collection(ticker_array)
    end
```

Next, I moved onto the company profile class, and that's where I began to struggle since I needed to write in the API code in such a way that took in the stock symbol and placed it between the profile_api and api_token portions of the url. Now, I'm sure sure there are ways to clean this up a bit, but here is what the code looks like:

```
 def profile_api(symbol)
        @pro_api = @base_url << @profile << "#{symbol}" << @api_key
        response = RestClient.get(@pro_api)
        json = JSON(response)
				company_profile = json.each{|company_profile| puts company_profile}
        profile_array = []
				profile_array << company_profile
	end
```

Whew, that was a doozy, next up - more API functionality with stock quotes, company news, analysts reccomendations, and more!

