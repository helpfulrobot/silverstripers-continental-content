# Continental Content Module

A SilverStripe module which allows you to have contents specific for locations, and serve these contents for users by checking their location. 

# Installing 

Use composer to install the module. 

`composer require silverstripers/continental-content dev-master`

# Configuring 

After installing the module on your SilverStripe site, you have to manually specify which data objects you want the module to decorate with in order to have different contents. 

```
SiteTree:
  extensions:
    - ContinentalContent
```

You have the freedom to decorate any object, in this YAML i am decorating the SiteTree object, which is the base object of SilverStripe pages. 

### Setting up location

Once you've done the above you can set up the locations which you want to have different contents for. 

```
ContinentalContent:
  continents:
    - Gb
    - NZ
    - AU
```


## Seperate URLS 

If you want to have separate urls for each location eg: site.com/uk/home, site.com/nz/home etc. You can allow that with another config. 

```
ContinentalContent:
  custom_urls: 'Y'
```

## Webserver cant read the visitors IP ? (Higher Level Customizations)

Sometimes this can happen, if you are using several load balancers to and have your website behind them and your load balancers wont pass the end clients IP. In this can use can set up a form and ask your users to select the location they are coming from. 

```
ContinentalContent:
  proxy_ip: '0.0.0.0'
```

set up the IP which your webserver gets all the time. 

make a function like the following in Page_Controller class. 

```
function LocationDetected(){
  return !(ContinentalContent::IsViewingThroughProxy() && ContinentalContent::CurrentContinent() == CONTINENTAL_DEFAULT);
}
```

If the above returns true you can draw a location selector to select the visitor's location. 

# Setting up IP database

The module can use three types of database to detect a user's location. It can use one of these three data feeds. 

http://dev.maxmind.com/geoip/legacy/geolite/
http://lite.ip2location.com/
https://db-ip.com/db/

visit yoursite.com/dev/tasks and you will get three build task options to import data from the feeds, and those contains further instructions on downloading the feeds etc. 





