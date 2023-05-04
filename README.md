# Actor - Ultimate Yelp Scraper

## Yelp scraper

The Yelp data scraper supports the following features:

-   Get reviews - Get reviews of businesses without any limits!

-   Retrieve business information - Address, images, menu, reviews and many different information are ready for your consumption.

-   Search any keyword - Search for any keyword you want to find on Yelp.

-   Search any location - If you need to search on a specific location, just type it!

-   Scrape events - Any event information can be find right away.

-   Scrape users - Retrieve any user information from their profiles.

-   Scrape collections - User collections can be directly retrieved. If you need to get the collection information, get it right away!

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/yelp-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Yelp that should be visited. Possible fields are:

- `search`: (Optional) (String) Keyword that you want to search on Yelp.

- `searchLocation`: (Optional) (String) Location that you want to initiate the search on Yelp.

- `startUrls`: (Optional) (Array) List of Yelp URLs. You should only provide business detail, event detail, event or business search, collections, collection detail or user detail URLs.

- `includeReviews`: (Optional) (Boolean) This will add all the reviews that Yelp provides into the detail objects. Please keep in mind that the time and resources the actor uses will increase proportionally by the number of reviews.

- `endPageForReviews`: (Optional) (Number) Final number of review page that you want to scrape. Default is `Infinite`. This is applies to user and business reviews individually.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

- `customMapFunction`: (Optional) (String) Function that takes each objects handle as argument and returns object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to have a scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detail requests. If actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.02-0.12 compute units.

### Yelp Scraper Input example

```json
{
  "startUrls":[
    "https://www.yelp.com/biz/maxs-restaurant-glendale-glendale-3",
    "https://www.yelp.com/user_details?userid=a_UbCGv_MTAHFs3P_zxUDA",
    "https://www.yelp.com/search?find_desc=max&find_loc=Los+Angeles%2C+CA",
    "https://www.yelp.com/collection/qGqt9YpsLBCH5nruuVCK2A/Food",
    "https://www.yelp.com/collections/user?userid=a_UbCGv_MTAHFs3P_zxUDA",
    "https://www.yelp.com/events/la/browse?start_date=20230215",
    "https://www.yelp.com/events/monterey-park-monterey-park-strong-star-ballroom-shooting-community-resources"
  ],
  "search":"max",
  "searchLocation":"Los Angeles",
  "maxItems": 20,
  "includeReviews": true,
  "endPage":1,
  "endPageForReviews":1,
  "proxy":{
    "useApifyProxy":true
  }
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Yelp Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Yelp actor.

## Scraped Yelp Properties

The structure of each item in Yelp looks like this:

### Business Detail

```json
{
	"type": "business",
	"url": "https://www.yelp.com/biz/good-grill-express-los-angeles-2",
	"title": "Good Grill Express",
	"rating": 3,
	"reviewCount": 43,
	"priceRange": "$$",
	"categories": [
		"Mexican",
		"Seafood",
		"American (Traditional)"
	],
	"address": {
		"city": "Los Angeles",
		"regionCode": "CA",
		"addressLine1": "210 E Olympic Blvd 108-127",
		"addressLine2": "Ste 127-108",
		"addressLine3": null,
		"postalCode": "90015",
		"formatted": "210 E Olympic Blvd 108-127\nSte 127-108\nLos Angeles, CA 90015"
	},
	"primaryPhoto": "https://s3-media0.fl.yelpcdn.com/bphoto/zAlILeeK6Q0ktjJWclRHkA/o.jpg",
	"reviews": [
		{
			"userName": "Martha C.",
			"userUrl": "https://www.yelp.com/user_details?userid=P6YMG4c5Tb73K9NXoab6og",
			"isElite": false,
			"rating": 5,
			"date": "2017-07-05T00:00:00.000Z",
			"review": "I have a business downtown Los Angeles and have been ordering here now for about 2 years or more. <br>They have a wide variety on their menu. There prices are good and there food has always been good as well as the great customer service that I always receive from the ordering to the great delivery service.<br><br>Never no complaints from me! I dont eat out at alot of places here downtown because they are not safe and clean, but this place I TRUST and recommend. you wont be sorry!<br><br>Thanks Good Grill for the good food, and good customers service from the beging to the end!!<br><br>Martha"
		},
		{
			"userName": "Julie M.",
			"userUrl": "https://www.yelp.com/user_details?userid=HlU-aUCVVaSFVjiO3VSZ2g",
			"isElite": false,
			"rating": 1,
			"date": "2022-04-02T00:00:00.000Z",
			"review": "So sad to come in and pay 10 bucks for two drinks and not allowed to use the restroom. Not one single customer is in the store and I was refused to use the restroom."
		},
		{
			"userName": "Margarita R.",
			"userUrl": "https://www.yelp.com/user_details?userid=yyyAARK_4FkL5WWgzLRwHg",
			"isElite": false,
			"rating": 1,
			"date": "2021-10-12T00:00:00.000Z",
			"review": "I should&#39;ve paid attention to the reviews. Food got yo or table in about 5 minutes or less and was cold. What does that tell you. Stale old food, and that&#39;s what it tasted like"
		},
		{
			"userName": "Sparkles D.",
			"userUrl": "https://www.yelp.com/user_details?userid=RVyNRipJXhEQko_eztWYyg",
			"isElite": true,
			"rating": 1,
			"date": "2018-02-17T00:00:00.000Z",
			"review": "Found this piece of metal in my food. Super disappointed  because the food was good up until that point."
		},
		{
			"userName": "Jocelyn Z.",
			"userUrl": "https://www.yelp.com/user_details?userid=0V704SWBbvJbRSKA6ufbbw",
			"isElite": false,
			"rating": 1,
			"date": "2019-07-26T00:00:00.000Z",
			"review": "They have the worst attitude. <br>Why have a restaurant and treat people like crap?<br>I understand that the breakfast menu is over at 11am <br>But how in the world do you try to charge someone for a steak and egg for 16$ when it&#39;s 11.95$? <br>Is not like the food is well serve when it&#39;s delivered anyway."
		},
		{
			"userName": "Diego R.",
			"userUrl": "https://www.yelp.com/user_details?userid=WTVr3jCQq6pZWkMFAXnhZw",
			"isElite": false,
			"rating": 1,
			"date": "2018-04-29T00:00:00.000Z",
			"review": "My wife and I were visiting the Santee Mall (or whatever they call it) and, after scoring a parking spot, we wandered into this little shopping mall to see what was in there. Around that time, I told my wife I needed to find a bathroom. This restaurant had one so I told her, &#34;Why don&#39;t we eat here for lunch?&#34; <br><br>I waited in line for the lavatory while my wife waited in line to order something. A lady who worked there approached me and I mentioned to her I was going to use the bathroom but my wife was in line. She seemed to tell me I couldn&#39;t use the bathroom. I pointed at my wife and said, &#34;We&#39;re ordering something.&#34; She walked away as if she didn&#39;t understand, so my wife told the lady (who was now behind the counter) we were ordering food so me using the bathroom was a non-issue. <br><br>Nonetheless, she chased my wife and I away, telling us we had to eat there in order to use the bathroom. Not only is that ridiculous, but we were planning on eating there anyway.....except we didn&#39;t, because we don&#39;t appreciate being treated like caca.<br><br>I have no idea what the food is like, but the customer service reeks. I really should have demanded to talk with the manager but I really needed to pee. What I did instead was I went down the hall to The Coffee Bean, where they not only treated me like a valued customer but also they gave me a token to use the public bathrooms down the hall.<br><br>I just find it disheartening that &#34;Bad Grill Express&#34; is not interested in my money or patronage.....I mean, I&#39;m pretty gringo so I hope it&#39;s not just Mexicans who are welcome."
		},
		{
			"userName": "Irene G.",
			"userUrl": "https://www.yelp.com/user_details?userid=8UKHone_AqY3UuLebfSbfQ",
			"isElite": false,
			"rating": 5,
			"date": "2020-03-11T00:00:00.000Z",
			"review": "I&#39;ve eaten here about two times already such good burgers and the service here is amazing ! Super friendly crew. Will always come back for more"
		},
		{
			"userName": "Erika T.",
			"userUrl": "https://www.yelp.com/user_details?userid=oYbv5vLasDJK74T2sKXUAQ",
			"isElite": false,
			"rating": 1,
			"date": "2018-07-17T00:00:00.000Z",
			"review": "Very bad customer service try paying for a<br>Coffee $1 and some change. Was giving the cashier some pennies and she gave me a bad attitude saying she was no longer gonna get change (pennies) how is it if money is money never again buy from them. Not the first time the cashier gives attitude. And she&#39;s the owners husband her name is mari. Bad service"
		},
		{
			"userName": "Daniel C.",
			"userUrl": "https://www.yelp.com/user_details?userid=t05CiT0Wjond7aXq6uUVwg",
			"isElite": true,
			"rating": 5,
			"date": "2015-07-02T00:00:00.000Z",
			"review": "Needed something different for lunch, and we had a menu from this place so, I ordered the Tuna Salad w/ chips. The order was delivered within 20 minutes or so and for $8.75, the portions were pretty good. <br><br>I really liked the taste of the salad and the chips with salsa were good, but there was a strange charge...I forget the exact wording, but it said something along the lines of &#34;upcharge&#34; or &#34;rounding up&#34;. Ummm...what the fro, yo? <br><br>I definitely need to ask about that before ordering again...which I would like to do, because what you see on the menu is what you get. And THAT my friends is a beautiful thing in this age of false advertising.<br><br>Update 7/3 - Ordered the veggie omelet with a side of bacon and extra crispy hash browns. Man...what a great way to start the morning! Loaded with bell peppers and onions and melted cheese on top...very clean and very filling!! And my hashbrowns were ACTUALLY crispy! The only hiccup was that I asked for a side of bacon and they put it in my omelet instead...it actually made it better, so hoorayyyyy!! They knew what I wanted even when I didn&#39;t! <br><br>Great great food and decent prices!! I&#39;m definitely ordering breakfast from here more often!!"
		},
		{
			"userName": "Rivka C.",
			"userUrl": "https://www.yelp.com/user_details?userid=ddUU4Z05Gf1EC7M4s_hQCQ",
			"isElite": false,
			"rating": 1,
			"date": "2019-07-26T00:00:00.000Z",
			"review": "These people deserve 0 stars!!! Super rude customer service. We were ordering over the phone and they wanted to charge us $16 for my coworkers steak and eggs because she made a little change and my salad a total of $30 plus. When we asked why and I calculated the amount we just decided to order the salad. The guy said either we pay the $30 or nothing I was trying to get more of an explanation and he hung up on me. <br>They have no right to be this rude when we are trying to give them business. They are scammers they tell you  your order is ready right after you have ordered and they don&#39;t allow any changes to you order and will charge you more and take advantage of you if you substitute or change anything minor in your order!! <br>Do yourselves a favor and do not eat here their food is not that good and they are not afraid of being super rude and kicking you out. I hope this place loses all their business for this kind of behavior."
		}
	],
	"operationHours": {
		"Mon": [
			"9:00 AM - 3:00 PM"
		],
		"Tue": [
			"9:00 AM - 3:00 PM"
		],
		"Wed": [
			"9:00 AM - 3:00 PM"
		],
		"Thu": [
			"9:00 AM - 3:00 PM"
		],
		"Fri": [
			"9:00 AM - 3:00 PM"
		],
		"Sat": [
			"9:00 AM - 3:00 PM"
		],
		"Sun": [
			"9:00 AM - 3:00 PM"
		]
	},
	"amenities": [
		"Offers Delivery",
		"Offers Takeout",
		"No Reservations",
		"Masks required",
		"Staff wears masks",
		"Accepts Credit Cards",
		"Accepts Apple Pay",
		"Accepts Cryptocurrency",
		"Outdoor Seating",
		"Moderate Noise",
		"Good for Groups",
		"Good For Kids",
		"Good for Lunch",
		"Street Parking, Validated Parking",
		"Waiter Service",
		"Wheelchair Accessible",
		"TV",
		"Covered Outdoor Seating",
		"Offers Catering",
		"No Wi-Fi",
		"No Happy Hour",
		"No Alcohol",
		"No Drive-Thru",
		"No Heated Outdoor Seating",
		"No Private Dining",
		"Bike Parking",
		"Plastic-free packaging",
		"Provides reusable tableware"
	],
	"about": "Established in 1990.\n\nWe have come a long way serviring to our local business and visitors from all around the world. They like our delicious food good prices and prompt clean service. We like to serve and been friendly to all. Our commitment id dedicated to improve quality food ingredients and a really healthy environment. We have had uninterrupted A+ Grade from the health department. We Love You. Thank You for your patronage.\n\nEnnio Zepeda and Staff.",
	"faq": [
		{
			"question": "Does Good Grill Express offers delivery or takeout?",
			"answer": " They offer  takeout.  "
		},
		{
			"question": "What forms of payment are accepted at Good Grill Express?",
			"answer": "        Good Grill Express accepts credit cards. "
		},
		{
			"question": "How is Good Grill Express rated?",
			"answer": "Good Grill Express has 3.0 stars from 43 reviews."
		},
		{
			"question": "Does Good Grill Express have outdoor seating?",
			"answer": "Yes, they have outdoor seating"
		},
		{
			"question": "What are some popular dishes to order at Good Grill Express?",
			"answer": " The following dishes are the most popular here <ul>  <li> <a href=\"https://www.yelp.com/menu/good-grill-express-los-angeles-2/item/wet-burrito-asada-chicken-guac\"> Wet Burrito Asada / Chicken / Guac </a> has 5 review mentions  and 1 photo uploads on Yelp! </li>  <li> <a href=\"https://www.yelp.com/menu/good-grill-express-los-angeles-2/item/chicken-soup-w-rice\"> Chicken Soup W/ Rice </a> has 1 review mentions  and 1 photo uploads on Yelp! </li>  <li> <a href=\"https://www.yelp.com/menu/good-grill-express-los-angeles-2/item/chicken-taquitos-3\"> Chicken Taquitos </a> has 1 review mentions  and 2 photo uploads on Yelp! </li>  <li> <a href=\"https://www.yelp.com/menu/good-grill-express-los-angeles-2/item/tuna-salad-w-chips\"> Tuna Salad W/ Chips </a> has 1 review mentions  and 2 photo uploads on Yelp! </li>  <li> <a href=\"https://www.yelp.com/menu/good-grill-express-los-angeles-2/item/baked-chicken-1-4-platter\"> Baked Chicken (1/4) Platter </a> has 1 review mentions on Yelp! </li>  </ul> "
		},
		{
			"question": "Is Good Grill Express good for kids?",
			"answer": "Yes, they are rated good for kids.  \n\n\n\n\n "
		},
		{
			"question": "What are my parking options at Good Grill Express?",
			"answer": "They have           nearby street parking and offer validated parking. "
		},
		{
			"question": "What kind of meals is Good Grill Express known for?",
			"answer": "They are great for lunch."
		},
		{
			"question": "How long has Good Grill Express been on Yelp?",
			"answer": "Good Grill Express has been on yelp since 2011/07/26."
		},
		{
			"question": "Where is Good Grill Express?",
			"answer": "Good Grill Express is located at 210 E Olympic Blvd 108-127, Los Angeles, CA."
		}
	],
	"questions": [],
	"ratingDistribution": {
		"1": 19,
		"2": 1,
		"3": 3,
		"4": 5,
		"5": 15
	},
	"menu": "http://www.goodgrillexpress.net",
	"website": "http://www.goodgrillexpress.net",
	"phoneNumber": "(213) 749-2345"
}
```

### Event Detail

```json
{
	"type": "event",
	"url": "https://www.yelp.com/events/monterey-park-monterey-park-strong-star-ballroom-shooting-community-resources",
	"title": "Monterey Park Strong: Star Ballroom Shooting - Community Resources",
	"image": "https://s3-media0.fl.yelpcdn.com/ephoto/Y0fY94JB0CZI9hK1nSXVXw/300s.jpg",
	"categories": [
		"Other",
		"Official Yelp Events"
	],
	"business": {
		"url": "",
		"name": null,
		"reviewCount": null,
		"rating": null,
		"location": "Monterey Park, CA 91754"
	},
	"fromDate": "2023-01-23T08:00:00.000Z",
	"toDate": "2023-02-20T08:00:00.000Z",
	"price": "",
	"description": "Our thoughts are with everyone in San Gabriel Valley affected by the Monterey Park Star Ballroom Shooting on Lunar New Year's Eve. In a time of what is supposed to be celebration, we are heartbroken by this tragedy of gun violence. As we mourn the loss of precious life and rebuild the community spirit, many in the Yelp community have asked how they can support our neighbors in need. #MontereyParkStrong #MPKStrongBelow are ways you can help the victims and their families.DONATIONS:All-Victims Fundgofundme.com/f/monterey-…***Sponsored by Advancing Social Justice Southern California. All proceeds contributed to the fund will go to the many individuals affectedClassroom of Compassion Public Alter Fundgofundme.com/f/classroom…***The Los Angeles-based nonprofit, Classroom of Compassion, will be creating 10 public altars to honor the ten victims lost ********************BUSINESSES OFFERING SUPPORT:Nomad Ice Pops  I  415 S Mission Dr San Gabriel, CA 91776yelp.com/biz/nomad-ice-p…***20% of sales will go to victim relief funds for the rest of the monthArcadia Donuts  I  34 Las Tunas Dr Arcadia, CA 91007yelp.com/biz/arcadia-don…***A fundraiser is being held Arcadia Donuts on Thursday in honor Yu (Andy) Kao, happening Thursday, January 26 - 28, until sold outLangley Center  I  400 N. Emerson Ave., Monterey Park, CA 91754.***A Survivors Resource Center has been established from January 23 - 28. If you have any questions or need assistance please call (626)307-1395********************EVENTS / MEMORIALS:JAN 23 - JAN 26 - Community Healing Circle  I  Asian Mental Health Projectinstagram.com/p/CnvQfMaP…***Free community circles this week for the APIDA community. This is a space for people to grieve, mourn, love, process and heal in response to the Monterey Park Lunar New Year Massacre and years of enduring Anti-Asian hate. Sign up in our bio or at bit.ly/APIDA-healingJAN 24, 5:30 PM - Candlelight Vigil  I  Monterey Park City Hallmontereypark.ca.gov/Arch…***Hosted by the City of Monterey Park. People are encouraged to bring flowers or candles to Monterey Park's City Hall, at 320 W. Newmark AveJAN 25, 6:00 PM - Candlelight Vigil  I  Star Dance Studioinstagram.com/p/CnvjWrJr…***Hosted by Compassion in SGV at Star Dance Studio, 122 W Garvey Ave #B, Monterey Park, CA 91754. If you have any questions or would like to help, please email us at hello@compassioninsgv.orgMonterey Park City Hall  I  320 W Newmark Ave Monterey Park, CA 91754***A memorial honoring the victims and survivors has been established for our community to mourn********************Other resources that you think should be added? Send us an email at sgv@yelp.com********************SOURCES:montereypark.ca.gov/Civi…gofundme.com/c/act/monte…instagram.com/montereypa…instagram.com/p/CnulzJRv…youtube.com/watch?v=jn6s…",
	"subscribers": [
		{
			"name": "Leonard A.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/XsKjcaG1b96hewUndgDfsg/60s.jpg",
			"friendCount": 1100,
			"reviewCount": 720,
			"isElite": true
		},
		{
			"name": "Sarni N.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/AYSvaB-BGsnCmeizwTyr8w/60s.jpg",
			"friendCount": 412,
			"reviewCount": 114,
			"isElite": true
		},
		{
			"name": "Anna S.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/ikSr3K87jCAQNsamJJNKgg/60s.jpg",
			"friendCount": 15,
			"reviewCount": 89,
			"isElite": true
		},
		{
			"name": "Gillian A.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/QTEskPPJqMAsXluQcBVKtQ/60s.jpg",
			"friendCount": 291,
			"reviewCount": 810,
			"isElite": true
		},
		{
			"name": "Darylynn D.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/2aUizo8RIgz78W9SQTyKCg/60s.jpg",
			"friendCount": 349,
			"reviewCount": 2825,
			"isElite": true
		},
		{
			"name": "Donna B.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/lWz3Qh4R8GS8NgwT0nzyAw/60s.jpg",
			"friendCount": 401,
			"reviewCount": 1597,
			"isElite": true
		},
		{
			"name": "Shawn T.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/CB1P5-kR6BvBNYPyMEsA3w/60s.jpg",
			"friendCount": 67,
			"reviewCount": 372,
			"isElite": true
		},
		{
			"name": "Becky L.",
			"avatar": "https://s3-media0.fl.yelpcdn.com/photo/bvJmP6e_AnaWbDI6Kdo4jg/60s.jpg",
			"friendCount": 341,
			"reviewCount": 553,
			"isElite": true
		}
	],
	"submittedBy": {
		"name": "Thuy Dan T.",
		"avatar": "https://s3-media0.fl.yelpcdn.com/photo/D_DV155q-AD94rEkooGvbA/30s.jpg",
		"friendCount": 4331,
		"reviewCount": 862,
		"isElite": true
	}
}
```

### User Detail

```json
{
	"type": "user",
	"url": "https://www.yelp.com/user_details?userid=a_UbCGv_MTAHFs3P_zxUDA",
	"title": "Ane V.",
	"avatar": "https://s3-media0.fl.yelpcdn.com/photo/aKMVOguNPIMH30QTjwao0Q/ls.jpg",
	"location": "From Los Angeles, CA",
	"friendsCount": 242,
	"imagesCount": 6342,
	"reviewsCount": 701,
	"reviews": [],
	"ratingDistribution": {
		"1": 6,
		"2": 12,
		"3": 87,
		"4": 166,
		"5": 430
	},
	"memberSince": "October 2020",
	"isElite": false
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that is available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
