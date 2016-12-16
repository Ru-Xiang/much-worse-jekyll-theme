---
layout: page
permalink: /downloads/
libspark:

    - version: "1.0.1"
      src-name: "libble-spark-1.0.1.zip"
      src: "https://github.com/LIBBLE/LIBBLE-Spark/archive/1.0.1.zip"
      release-name: "libble-spark_2.11-1.0.1.jar"
      release: "https://libble.github.io/mvn-repo/libble/libble-spark_2.11/1.0.1/libble-spark_2.11-1.0.1.jar"
      release-note:  "prebuild on spark-2.0.1"
      date: "2016-11-09"

    - version: "0.0.1"
      src-name: "libble-spark-0.0.1.zip"
      src: "https://github.com/LIBBLE/LIBBLE-Spark/archive/0.0.1.zip"
      release-name: "libble-spark_2.10-0.0.1.jar"
      release: "https://libble.github.io/mvn-repo/libble/libble-spark_2.10/0.0.1/libble-spark_2.10-0.0.1.jar"
      release-note:  "prebuild on spark-2.0.1"
      date: "2016-06-03"





---



## Downloads:

{% assign thumbnail="left" %}

### [LIBBLE-Spark](#libble-spark)

<ul class="listing">

{% for lib in page.libspark %}

 <li class="listing-item">

Version-{{lib.version}}    

 <time datetime="{{ lib.date | date:"%Y-%m-%d" }}"> {{ lib.date | date:"%Y-%m-%d" }}</time> <br/>

Codes: <a href="{{lib.src}}"> {{lib.src-name}}</a> <br/>

Release: <a href="{{lib.release}}"> {{lib.release-name}}</a>({%if lib.release-note %}({{lib.release-note}}){%endif%}

<br/>

<br/>

</li>

{% endfor %}

</ul>

