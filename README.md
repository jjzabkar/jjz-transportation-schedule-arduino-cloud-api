# transportationScheduleArduinoCloudApi

# Diagrams

https://docs.google.com/presentation/d/1M1SldzzU6LN8LIzJGItlPCNjDmj-g8ZgxEO3X7hq0IQ/

# Transit Stops And Route Information

* Mountlake Terrace FS - Bay 6 Stop # 2765 - S bound
	howLongItTakesToGetToStationFromEdmondsHomeInSeconds: 600 (10 minutes)
	Routes: [ 410, 413, 415, 435, 511, 512, 513]
	Arrival Info:
		http://pugetsound.onebusaway.org/where/standard/stop.action?id=29_2765
	Complete Timetable:
		http://pugetsound.onebusaway.org/where/standard/schedule.action?id=29_2765
			
* Shoreline P&R
  Aurora Ave N & N 192nd St Stop # 75730 - S bound
	howLongItTakesToGetToStationFromEdmondsHomeInSeconds: 600 (10 minutes)
	Routes: [ 301, E Line ]
	Arrival Info:
		http://pugetsound.onebusaway.org/where/standard/stop.action?id=1_75730
	Complete Timetable:
		http://pugetsound.onebusaway.org/where/standard/schedule.action?id=1_75730

* Edmonds Station Sounder
  Edmonds Station Stop # S_ED
	howLongItTakesToGetToStationFromEdmondsHomeInSeconds:600 (10 minutes)
	Routes: [ Sounder Everett - Seattle ]
	Arrival Info:
		http://pugetsound.onebusaway.org/where/standard/stop.action?id=40_S_ED
	Complete Timetable:
		http://pugetsound.onebusaway.org/where/standard/schedule.action?id=40_S_ED

# API curl examples

	$ curl -s 'https://jhipstercfdemojjz4.cfapps.io/api/foos' -H 'Authorization: Bearer 12fa07b7-33ac-44e5-a9b8-e92f22057f5e' -H 'Accept: application/json'| jq .
	[
	  {
	    "id": 1003,
	    "bar": "bar1"
	  }
	]
	
	curl -s 'http://jhipstercfdemojjz4.cfapps.io/api/foos' -H 'Authorization: Bearer 12fa07b7-33ac-44e5-a9b8-e92f22057f5e' -H 'Accept: application/json'| jq .
	[
	  {
	    "id": 1003,
	    "bar": "bar1"
	  }
	]
	
# Model

* Station - a place to board transportation (aka bus stop)
* Route - a route that connects to a station (i.e. 'E Line')
* Arrival Time Status - when a route will arrive at a station: now, soon, late, unknown, off

## Relationships

* Multiple stations
* Multiple routes per station
* Multiple arrival times per route

## Mock JSON Configuration

API to configure stations is JHipster Angular interface.  Also used for testing via UI.

Sorted by:
1. station.id,
2. station.nextRouteArrivalTimes.status
3. station.estimatedArrivalTiems.estimatedArrivalTime

	"station": {
	  "id": 1,
	  "name":"Mountlake Terrace P&R",
	  "nextRouteArrivalTimes": [
		{
		  "id": 435,
		  "name": "435",
		  "status" : "now",
		  "estimatedArrivalTime" : 1234444444
		},{
		  "id": 413,
		  "name": "435",
		  "status" : "now",
		  "estimatedArrivalTime" : 1235555555
		},
		...
	  ],
	  "howLongItTakesToGetToStationFromEdmondsHomeInSeconds":600,
	  "outputSlots":8  /* how many items to output in CSV */
	}
	

## Sample API Output, CSV

	1,now,now,soon,late,late,late,off,off,
	2,now,late,off,off
	3,now,off

## Sample API Output, JSON

{
  1: {
    "name":"Mountlake Terrace P&R",
    "routes":[
    	{ "435": "good"
    
    ]
  }
}


# Design Ideas

* http://hackaday.com/2014/09/15/leds-turn-this-paper-map-into-a-tram-tracker/
* http://www.instructables.com/id/10x5-RGB-LED-Matrix-with-only-5-IO-pins/
* http://www.lib.utexas.edu/maps/topo/washington/txu-pclmaps-topo-wa-seattle-1895.jpg
* 24 Hours of King County Metro https://vimeo.com/88172380
* http://www.seattlesubway.org/template_files/big-map.png