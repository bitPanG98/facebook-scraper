# Facebook Friend Mapper

![Map Example](https://raw.githubusercontent.com/jcontini/facebook-scraper/master/example.jpg)

## First: A Warning
Use of this tool likely violates Facebook's terms & conditions. When using it, Facebook will knows who you are (because you have to log in), and can pretty easily see that you're using a tool like this in an unsanctioned way. Therefore by using this software, you put your own Facebook profile at risk, as Facebook may decide to ban you from the platform altogether. I cannot be held responsible for this or any other outcomes that may occur as a result of the use of this software.

I personally built this to help centralize information about my contacts. Specifically, I wanted to make a map of all of my contacts (including Facebook friends), so that I could more easily see where they are living on the globe, and get in touch with them when I'm passing through.

## How it works
This tool will only extract the data that your friends have already explicitly made it available to you. If the amount or content of the data freaks you (like it did to me!), then it's a good reminder for us all to check our profiles/privacy settings to make sure that we only share what we want others to be able to see.

It works like this:
1. Open your friends list page (on m.facebook.com), save it (index.html) create a list of all of your friends as `index.json`
2. Download each of your friends profiles (on mbasic.facebook.com) and parse/organize all data as `profiles.json`
3. Look for the 'Current City' and 'Address' fields on each profile and save them to `locations.json`.
4. Geocode each unique location and add Latitude/Longitude to `locations.json`. It uses the Mapbox Geocoding API to do this, so you need a Mapbox API key. Be sure to either use pipenv environments with a `.env` file, or open the python file to manually put in your Mapbox API key.
5. Creates a map! Using `template-map.html` as a base, the script will create `friends-map.html` with your Mapbox API key, and map out `locations.json` which is now enriched with geodata. The result is a moveable, searchable map as you see in the example screenshot.
 
## Installation
You'll need to have python, pip, and [Google Chrome](https://www.google.com/chrome/) installed to use this tool. Once that's all set up:

1. Clone this repository
2. `cd` into the cloned folder 
3. Run `pipenv install` to install dependencies
4. Create a `.env` file for pipenv and set these variables:
```
fb_user
fb_pass
mapbox_token
```

I personally used Jupyter Notebook to run the script (you'll see the notebook file in the repo), but it's not required at all.

## Extract profile data & create the map
1. Run `pipenv shell` to activate the virtual environment. This is optional if you already have the required packages installed in your environment.
2. Run `python extract.py` to run the full process of indexing, downloading, parsing, geocoding, and mapping your friends. You can optionally use any of these flags to perform only certain actions:

- `-- index` Sign in, create friends list index only
- `-- download` Download profile for each friend in index
- `-- parse` Extract profiles HTML into profiles.json
- `--geocode` Geocode addresses to coordinates
- `--map` Make the map!