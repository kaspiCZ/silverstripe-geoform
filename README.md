# geoform

## Maintainers

 * Andre Lohmann (Nickname: andrelohmann)
  <lohmann dot andre at googlemail dot com>

## Requirements

Silverstripe 3.2.x

## Introduction

Install like any other Module.

Set the Google Api Key inside geoform/_config.php

Alter the Database and add the Following Functions:

```
DROP FUNCTION IF EXISTS geodistance;
delimiter //
CREATE FUNCTION geodistance (lat1 DOUBLE, lng1 DOUBLE, lat2 DOUBLE, lng2 DOUBLE) RETURNS DOUBLE NO SQL
BEGIN
DECLARE radius DOUBLE;
DECLARE distance DOUBLE;
DECLARE vara DOUBLE;
DECLARE varb DOUBLE;
DECLARE varc DOUBLE;
SET lat1 = RADIANS(lat1);
SET lng1 = RADIANS(lng1);
SET lat2 = RADIANS(lat2);
SET lng2 = RADIANS(lng2);
SET radius = 6371.0;
SET varb = SIN((lat2 - lat1) / 2.0);
SET varc = SIN((lng2 - lng1) / 2.0);
SET vara = SQRT((varb * varb) + (COS(lat1) * COS(lat2) * (varc * varc)));
SET distance = radius * (2.0 * ASIN(CASE WHEN 1.0 < vara THEN 1.0 ELSE vara END));
RETURN distance;
END;
//
delimiter ;
```

### Notice
This repository uses the git flow paradigm.
After each release cycle, do not forget to push tags, master and develop to the remote origin
```
git push --tags
git push origin develop
git push origin master
```