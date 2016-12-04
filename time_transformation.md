## Odoo Date & datetime

>`Date`和`Datetime`在Odoo ORM框架和数据库中用`UTC`形式表示，并被当作字符串定义为`DEFAULT_SERVER_DATE_FORMAT`、`DEFAULT_SERVER_DATETIME_FORMAT`

```
DEFAULT_SERVER_DATE_FORMAT = "%Y-%m-%d"
DEFAULT_SERVER_TIME_FORMAT = "%H:%M:%S"
DEFAULT_SERVER_DATETIME_FORMAT = "%s %s" % (
    DEFAULT_SERVER_DATE_FORMAT,
    DEFAULT_SERVER_TIME_FORMAT)
```

由于经常涉及到时间的传输（app客户端），需转化为用户时间，故封装如下：

```
# -*- coding: utf-8 -*-

import datetime
import pytz
from odoo.tools import DEFAULT_SERVER_DATE_FORMAT, DEFAULT_SERVER_DATETIME_FORMAT


def datetime_utc2local(utc_datetime, user=None):
    """
        将 Odoo UTC 时间转化为用户所在时区时间，以便在web上显示或者传输给app
        参数: user res.users
             utc_datetime DEFAULT_SERVER_DATETIME_FORMAT
        返回： local_dt_str DEFAULT_SERVER_DATETIME_FORMAT
    """
    if user:
        tz_name = user.env.context.get('tz') or 'Asia/Chongqing'
    else:
        tz_name = 'Asia/Chongqing'

    tz_local = pytz.timezone(tz_name)
    tz_utc = pytz.timezone('UTC')
    # todo re judges whether the utc_datetime is in the right format
    utc_dt = datetime.datetime.strptime(utc_datetime, DEFAULT_SERVER_DATETIME_FORMAT)

    local_dt = tz_utc.localize(utc_dt).astimezone(tz_local)
    local_dt_str = datetime.datetime.strftime(local_dt, DEFAULT_SERVER_DATETIME_FORMAT)

    return local_dt_str


def datetime_local2utc(local_datetime, user=None):
    """
        将用户所在时区日期时间转化为 UTC日期时间，以便存储在Odoo
        参数: user res.users;
             local_datetime DEFAULT_SERVER_DATETIME_FORMAT
        返回： utc_dt_str DEFAULT_SERVER_DATETIME_FORMAT
    """
    if user:
        tz_name = user.env.context.get('tz') or 'Asia/Chongqing'
    else:
        tz_name = 'Asia/Chongqing'

    tz_local = pytz.timezone(tz_name)
    tz_utc = pytz.timezone('UTC')
    # todo re judges whether the local_datetime is in the right format
    local_dt = datetime.datetime.strptime(local_datetime, DEFAULT_SERVER_DATETIME_FORMAT)
    utc_dt = tz_local.localize(local_dt).astimezone(tz_utc)
    utc_dt_str = datetime.datetime.strftime(utc_dt, DEFAULT_SERVER_DATETIME_FORMAT)

    return utc_dt_str

```
