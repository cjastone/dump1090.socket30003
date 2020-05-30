# dump1090.socket30003.rangview.pl

An updated version of the original [rangeview.pl](https://github.com/tedsluis/dump1090.socket30003#help-page-rangeviewpl) by [tedsluis](https://github.com/tedsluis).

Provides a visual representation of the range of your RDL-SDR and antenna for ADS-B traffic.

**rangeview.pl**
* Reads the flight positions from files in CSV format as output by dump1090 and creates a range/altitude view map.
* The range/altitude view shows the maximum range of your antenna for every altitude zone.
* KML output support (Google Earth format).

Corrections and enhancements over original script:
* Corrects an issue with the original script that results in an error when run
* Corrects an issue with inaccurate results on the left-hand half of the map when separated into multiple altitude zones
* Draws a complete solid outline with internal translucent shading for better viewing in Google Earth
* Provides time/date stamp and slightly more detailed data in layers
* Automatically creates a CSV file in the same format as socket30003 output containing "high scores" for the specified number of direction zones

[![Dump1090 rangeview](/images/rangemap.png)


## Help page rangeview.pl
````
This rangeview.pl script creates location data
for a range/altitude view which can be displayed in a modified
fork of dump1090-mutability or Google Earth / Maps.

The script creates two output files:
rangeview.csv) A file with location data in CSV format can be
imported in to tools like http://www.gpsvisualizer.com.
rangeview.kml) A file with location data in KML format, which
can be imported into a modified dump1090-mutability or Google
Earth / Maps.

This script uses the output file(s) of the 'socket30003.pl'
script, which are by default stored in /tmp in this format:
dump1090-<hostname/ip_address>-YYMMDD.txt

It will read the files one by one and it will automatically use
the correct units (feet, meter, mile, nautical mile of kilometer)
for 'altitude' and 'distance' when the input files contain
column headers with the unit type between parentheses. When
the input files doesn't contain column headers (as produced
by older versions of 'socket30003.pl' script) you can specify
the units. Otherwise this script will use the default units.

The flight position data is sorted in to altitude zones. For
each zone and for each direction the most remote location is
saved. The most remote locations per altitude zone will be
written to a file as a track.

Syntax: rangeview.pl

Optional parameters:
  -data <data directory>  The data files are stored in
                          '/tmp' by default.
  -log  <data directory>  The log files are stored in
                          '/tmp' by default.
  -output <output         The output file is stored in
            directory>    '/tmp' by default.
  -file <filename>        The output file name. The extension
                          (.kml or .csv) determines the
                          file structure!  
                          'rangeview.kml' by default.
  -filemask <mask>        Specify a filemask.
                          The default filemask is 'dump*.txt'.
  -override               Override output file if exists.
                          Default is 'no'.
  -timestamp              Add timestamp to output file name.
                          Default is 'no'.
  -sequencenumber         Add sequence number to output file name.
                          Default is 'no'.
  -max <altitude>         Upper limit. Default is '12000 meter'.
                          Higher values in the input data will be skipped.
  -min <altitude>         Lower limit. Default is '0 meter'.
                          Lower values in the input data will be skipped.
  -directions <number>    Number of compass direction (pie slices).
                          Minimal 8, maximal 7200. Default = '1440'.
  -zones <number>         Number of altitude zones.
                          Minimal 1, maximum 99.
                          Default = '24'.
  -lon <lonitude>         Location of your antenna.
  -lat <latitude>          
  -distanceunit <unit>,[<unit>]
                          Type of unit: kilometer, nauticalmile,
                          mile or meter. First unit is for the
                          incoming source, the file(s) with flight
                          positions. The second unit is for the
                          output file. No unit means it is the
                          same as incoming.
                          Default distance unit's are:
                          'kilometer,kilometer'.
  -altitudeunit <unit>[,<unit>]
                          Type of unit: feet or meter. First unit
                          is for the incoming source, the file(s)
                          with flight positions. The second unit
                          is for the output file. No unit means it
                          is the same as incoming.
                          Default altitude unit's are:
                          'meter,meter'.
  -debug                  Displays raw socket messages.
  -verbose                Displays verbose log messages.
  -help                   This help page.

notes:
  - The default values can be changed within the config file 'socket30003.cfg'.
  - The source units will be overruled in case the input file header contains unit information.

Examples:
  rangeview.pl
  rangeview.pl -distanceunit kilometer,nauticalmile -altitudeunit meter,feet
  rangeview.pl -data /home/pi/data -log /home/pi/log -output /home/pi/result
````

### Output rangeview.pl
* Default output file: /tmp/rangeview.csv
````
type,new_track,name,color,trackpoint,altitudezone,destination,hex_ident,Altitude(meter),latitude,longitude,date,time,angle,distance(kilometer)
T,1,Altitude zone 1: 00000-  500,7fffff00,1,     0,-718,484646,357,52.00493,5.08865,2017/01/10,10:46:15.738,-179.72,8
T,0,Altitude zone 1: 00000-  500,7fffff00,2,     0,-717,484646,357,52.00616,5.08808,2017/01/10,10:46:17.164,-179.32,8
T,0,Altitude zone 1: 00000-  500,7fffff00,3,     0,-714,484646,357,52.00788,5.08722,2017/01/10,10:46:19.740,-178.7,8
T,0,Altitude zone 1: 00000-  500,7fffff00,4,     0,-713,484646,357,52.00914,5.08667,2017/01/10,10:46:21.041,-178.28,8
T,0,Altitude zone 1: 00000-  500,7fffff00,5,     0,-711,484646,357,52.01039,5.08604,2017/01/10,10:46:22.622,-177.79,8
T,0,Altitude zone 1: 00000-  500,7fffff00,6,     0,-709,484646,357,52.01125,5.08560,2017/01/10,10:46:23.892,-177.44,8
T,0,Altitude zone 1: 00000-  500,7fffff00,7,     0,-708,484646,357,52.01230,5.08518,2017/01/10,10:46:25.244,-177.09,8
T,0,Altitude zone 1: 00000-  500,7fffff00,8,     0,-706,484646,357,52.01335,5.08461,2017/01/10,10:46:26.625,-176.62,8
T,0,Altitude zone 1: 00000-  500,7fffff00,9,     0,-704,484646,357,52.01463,5.08400,2017/01/10,10:46:28.031,-176.09,7
T,0,Altitude zone 1: 00000-  500,7fffff00,10,    0,-702,484646,357,52.01579,5.08345,2017/01/10,10:46:29.475,-175.59,7
T,0,Altitude zone 1: 00000-  500,7fffff00,11,    0,-700,484646,357,52.01683,5.08293,2017/01/10,10:46:30.940,-175.11,7
````

* Default output file: /tmp/rangeview.kml
````
<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<kml xmlns=\"http://www.opengis.net/kml/2.2\">
  <Document>
    <name>Range: [date/time]</name><Style id=\"track-1\">
      <LineStyle>
        <color>ff135beb</color>
        <width>3</width>
      </LineStyle>
    </Style>
	<Style id=\"fill-1\">
      <LineStyle>
        <color>000000</color>
        <width>0</width>
      </LineStyle>
      <PolyStyle>
        <color>55135beb</color>
      </PolyStyle>
    </Style>
    <Placemark>
      <name>Layer x (outline)</name>
      <description>x feet/meter - y feet/meter</description>
      <styleUrl>#track-1</styleUrl>
      <LineString>
        <altitudeMode>clampToGround</altitudeMode>
        <coordinates>
5.08865,52.00493,357
5.08808,52.00616,357
5.08722,52.00788,357
5.08667,52.00914,357
5.08604,52.01039,357
5.08560,52.01125,357
5.08518,52.01230,357
5.08461,52.01335,357
5.08400,52.01463,357
5.08345,52.01579,357
5.08293,52.01683,357
		</coordinates>
      </LineString>
    </Placemark>
	<Placemark>
	  <name>Layer x (fill)</name>
	  <description>x feet/meter - y feet/meter</description>
	  <styleUrl>#fill-1</styleUrl>
	  <Polygon>
	    <altitudeMode>clampToGround</altitudeMode>
	    <outerBoundaryIs>
		  <LinearRing>
		    <coordinates>
5.08865,52.00493,357
5.08808,52.00616,357
5.08722,52.00788,357
5.08667,52.00914,357
5.08604,52.01039,357
5.08560,52.01125,357
5.08518,52.01230,357
5.08461,52.01335,357
5.08400,52.01463,357
5.08345,52.01579,357
5.08293,52.01683,357
		</coordinates>
          </LinearRing>
        </outerBoundaryIs>
      </Polygon>	  
    </Placemark>
</Document>
</kml>
````
### Run rangview.pl

Process the flight data log from dump1090 and create a range view map.  

Be sure you have collected data for a couple of days!  

````
$ cd
$ cd socket30003
$ ./rangview.pl
10Jan17 20:30:38 pid=8562  I pi Log file: '/tmp/rangeview-170110.log'
The altitude will be converted from 'meter' to 'meter'.
The distance will be converted from 'kilometer' to 'kilometer.
10Jan17 20:30:38 pid=8562  I pi Output file: '/tmp/rangeview.csv'
10Jan17 20:30:38 pid=8562  I pi The maximum altitude is 12000 meter.
10Jan17 20:30:38 pid=8562  I pi The minimal altitude is 0 meter.
10Jan17 20:30:38 pid=8562  I pi The number of compass directions (pie slices) is 1440.
10Jan17 20:30:38 pid=8562  I pi The number of altitude zones is 24.
10Jan17 20:30:38 pid=8562  I pi The latitude/longitude location of the antenna is: 52.085624,5.0890591.
10Jan17 20:30:38 pid=8562  I pi An altitude zone is 500 meter.
10Jan17 20:30:38 pid=8562  I pi The following files fit with the filemask '*dump*.txt*':
10Jan17 20:30:38 pid=8562  I pi     /tmp/dump1090-ted1090-5-170110.txt
10Jan17 20:30:38 pid=8562  I pi     /tmp/dump1090-ted1090-5-170109.txt
10Jan17 20:30:38 pid=8562  I pi processing '/tmp/dump1090-ted1090-5-170110.txt':
10Jan17 20:32:47 pid=8562  I pi   -header units:altitude=meter,distance=kilometer,ground_speed=kilometerph, position 1-1591682. processed.
10Jan17 20:32:47 pid=8562  I pi processing '/tmp/dump1090-ted1090-5-170109.txt':
10Jan17 20:33:33 pid=8562  I pi   -header units:altitude=meter,distance=kilometer,ground_speed=kilometerph, position 1-580075. processed.
10Jan17 20:33:33 pid=8562  I pi Number of files read: 2
10Jan17 20:33:33 pid=8562  I pi Number of position processed: 2171757 and positions within range processed: 2060038
10Jan17 20:33:35 pid=8562  I pi   1,Altitude zone:     0-   499,Directions:  406/ 1440,Positions processed:      8128,Positions processed per direction: min:     1,max:   545,avg:     5,real avg:    20
10Jan17 20:33:35 pid=8562  I pi   2,Altitude zone:   500-   999,Directions:  524/ 1440,Positions processed:     33499,Positions processed per direction: min:     0,max:   778,avg:    23,real avg:    64
10Jan17 20:33:35 pid=8562  I pi   3,Altitude zone:  1000-  1499,Directions:  734/ 1440,Positions processed:     37874,Positions processed per direction: min:     0,max:   766,avg:    26,real avg:    51
10Jan17 20:33:35 pid=8562  I pi   4,Altitude zone:  1500-  1999,Directions: 1114/ 1440,Positions processed:     40865,Positions processed per direction: min:     2,max:   627,avg:    28,real avg:    36
10Jan17 20:33:35 pid=8562  I pi   5,Altitude zone:  2000-  2499,Directions: 1241/ 1440,Positions processed:     45281,Positions processed per direction: min:    23,max:   618,avg:    31,real avg:    36
10Jan17 20:33:35 pid=8562  I pi   6,Altitude zone:  2500-  2999,Directions: 1299/ 1440,Positions processed:     40231,Positions processed per direction: min:    29,max:   670,avg:    27,real avg:    30
10Jan17 20:33:35 pid=8562  I pi   7,Altitude zone:  3000-  3499,Directions: 1373/ 1440,Positions processed:     55566,Positions processed per direction: min:    18,max:   469,avg:    38,real avg:    40
10Jan17 20:33:36 pid=8562  I pi   8,Altitude zone:  3500-  3999,Directions: 1410/ 1440,Positions processed:     42652,Positions processed per direction: min:    16,max:   292,avg:    29,real avg:    30
10Jan17 20:33:36 pid=8562  I pi   9,Altitude zone:  4000-  4499,Directions: 1387/ 1440,Positions processed:     42639,Positions processed per direction: min:     4,max:   222,avg:    29,real avg:    30
10Jan17 20:33:36 pid=8562  I pi  10,Altitude zone:  4500-  4999,Directions: 1374/ 1440,Positions processed:     45339,Positions processed per direction: min:    20,max:   267,avg:    31,real avg:    33
10Jan17 20:33:36 pid=8562  I pi  11,Altitude zone:  5000-  5499,Directions: 1356/ 1440,Positions processed:     43614,Positions processed per direction: min:    18,max:   322,avg:    30,real avg:    32
10Jan17 20:33:36 pid=8562  I pi  12,Altitude zone:  5500-  5999,Directions: 1322/ 1440,Positions processed:     42356,Positions processed per direction: min:    11,max:   330,avg:    29,real avg:    32
10Jan17 20:33:36 pid=8562  I pi  13,Altitude zone:  6000-  6499,Directions: 1388/ 1440,Positions processed:     45874,Positions processed per direction: min:    12,max:   623,avg:    31,real avg:    33
10Jan17 20:33:36 pid=8562  I pi  14,Altitude zone:  6500-  6999,Directions: 1275/ 1440,Positions processed:     47050,Positions processed per direction: min:    17,max:   686,avg:    32,real avg:    36
10Jan17 20:33:36 pid=8562  I pi  15,Altitude zone:  7000-  7499,Directions: 1301/ 1440,Positions processed:     55586,Positions processed per direction: min:    28,max:   686,avg:    38,real avg:    42
10Jan17 20:33:36 pid=8562  I pi  16,Altitude zone:  7500-  7999,Directions: 1411/ 1440,Positions processed:     45161,Positions processed per direction: min:    26,max:   514,avg:    31,real avg:    32
10Jan17 20:33:36 pid=8562  I pi  17,Altitude zone:  8000-  8499,Directions: 1416/ 1440,Positions processed:     44739,Positions processed per direction: min:    13,max:   567,avg:    31,real avg:    31
10Jan17 20:33:37 pid=8562  I pi  18,Altitude zone:  8500-  8999,Directions: 1415/ 1440,Positions processed:     56940,Positions processed per direction: min:    43,max:   829,avg:    39,real avg:    40
10Jan17 20:33:37 pid=8562  I pi  19,Altitude zone:  9000-  9499,Directions: 1440/ 1440,Positions processed:    101448,Positions processed per direction: min:    96,max:   479,avg:    70,real avg:    70
10Jan17 20:33:37 pid=8562  I pi  20,Altitude zone:  9500-  9999,Directions: 1422/ 1440,Positions processed:     69574,Positions processed per direction: min:    59,max:   428,avg:    48,real avg:    48
10Jan17 20:33:37 pid=8562  I pi  21,Altitude zone: 10000- 10499,Directions: 1440/ 1440,Positions processed:    181891,Positions processed per direction: min:   112,max:   748,avg:   126,real avg:   126
10Jan17 20:33:37 pid=8562  I pi  22,Altitude zone: 10500- 10999,Directions: 1440/ 1440,Positions processed:    363296,Positions processed per direction: min:   177,max:  1431,avg:   252,real avg:   252
10Jan17 20:33:37 pid=8562  I pi  23,Altitude zone: 11000- 11499,Directions: 1440/ 1440,Positions processed:    226620,Positions processed per direction: min:   178,max:  2577,avg:   157,real avg:   157
10Jan17 20:33:37 pid=8562  I pi  24,Altitude zone: 11500- 11999,Directions: 1440/ 1440,Positions processed:    343815,Positions processed per direction: min:   240,max:   975,avg:   238,real avg:   238
````
You can find the result in '/tmp/rangview.kml'.

The ouput may be viewed using Google Earth or Google Maps.
