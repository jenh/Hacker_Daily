# Hacker_Daily
Flash briefing example in Python with some json parsing

This is example code from a daily flash briefing skill for Amazon devices. It reads out the most recent five CVEs (updated hourly) from the CVE (Common Vulnerabilities and Exposures) database hosted by NIST. It also places a link in the cards associated with the briefing, which is a little less painful -- if less amusing -- than listening to Alexa read out an entire software vulnerability description.

I'm sharing this because, when I was creating my first daily briefings, I had a hard time finding examples of the correct json format and it took longer than the five minutes it should take to create one searching for examples. 

Amazon Alexa Flash Briefings are pretty simple, as you can see here -- on the Amazon side, you create a new Flash Briefing, describe it, and point it to a json file. Alexa will only allow five items in a flash briefing. You can see an example in `cve.json.`

So, you really just have to worry about writing the file with the data you need and updating it as necessary. A lot of people use Lambda, but I already have a server set up, so it was a lot quicker to write a Python script and run a cronjob to automatically update it.

The code to create the json is `flash-cve.py`, which pulls down a data source, parses it, and drops `cve.json` into the current directory. 

In the production version, it pops the output into /var/www/html/ on my web server so that Alexa can grab it when a user requests it -- and you can "set it and forget it" by running the script every hour as a cronjob:

  */60 * * * * python /path/to/my/flash-cve.py

I've also included the `skill.json` file, but you don't really need that for your own daily briefing if you use the Alexa Developer UI...just including for completeness. Links and images have been removed.

You can enable Hacker Daily (and/or any of the other Alexa apps I've built -- Radio Time Warp, Arcade Party, and Future Poetry are pretty fun) on your Alexa device (including a smartphone with the Alexa app installed!) from here: [https://www.amazon.com/s?k=puzzling+plans+alexa&ref=nb_sb_noss_2](https://www.amazon.com/s?k=puzzling+plans+alexa&ref=nb_sb_noss_2).

