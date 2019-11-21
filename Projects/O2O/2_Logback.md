---
title: 'O2O: logback tutorial'
date: 2019-11-10T22:59:01.309Z
tags: ['Database', 'Java', 'Tomcat', 'logback', 'log', 'O2O', 'Web']
categories: ['CS']
---

# Logback
## Description
`Logback` is a log module.
![Logback-2019-8-1-12-20-49.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-8-1-12-20-49.png)

![Logback-2019-8-1-12-21-24.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-8-1-12-21-24.png)

> logger, appender, layout are tags of logback

## Configuration
1. Create a `logback.xml` in `resources` package

![Logback-2019-11-10-12-31-22.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-12-31-22.png)

2. Defines some properties of the logback configuration.

![Logback-2019-11-10-12-52-52.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-12-52-52.png)

3. Defines the appenders.

![Logback-2019-11-10-13-1-13.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-13-1-13.png)

![Logback-2019-11-10-14-3-39.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-14-3-39.png)

Info, Error is the same as Debug.
![Logback-2019-11-10-14-4-14.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-14-4-14.png)

![Logback-2019-11-10-14-7-21.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-14-7-21.png)

4. Defines the logger

![Logback-2019-11-10-14-19-22.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-14-19-22.png)

![Logback-2019-11-10-14-19-41.png](https://raw.githubusercontent.com/Luorinz/images/master/Logback-2019-11-10-14-19-41.png)

> Debug: __We should change all MaxHistory to maxHistory in the appenders.__
> Debug: __We should change all append-ref to appender-ref in the appenders.__

## Practice

1. Initialize a Logger instance in the `AreaController`.

![2_Logback-2019-11-10-14-28-29.png](https://raw.githubusercontent.com/Luorinz/images/master/2_Logback-2019-11-10-14-28-29.png)

2. Add some test info statements in the function.

![2_Logback-2019-11-10-14-48-50.png](https://raw.githubusercontent.com/Luorinz/images/master/2_Logback-2019-11-10-14-48-50.png)

3. Start Tomcat and visit `localhost:8080/superadmin/listarea`, Check the console and the file.
![2_Logback-2019-11-10-14-49-12.png](https://raw.githubusercontent.com/Luorinz/images/master/2_Logback-2019-11-10-14-49-12.png)


Here we can search `catalina.base` to get to the directory of our log files.
![2_Logback-2019-11-10-14-52-23.png](https://raw.githubusercontent.com/Luorinz/images/master/2_Logback-2019-11-10-14-52-23.png)

![2_Logback-2019-11-10-14-51-30.png](https://raw.githubusercontent.com/Luorinz/images/master/2_Logback-2019-11-10-14-51-30.png)

> If the log is out of date(1 day), it will generate new directories and gz file to contnain old logs.
