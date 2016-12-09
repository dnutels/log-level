# log-level

A small Node library that determines your current log level.

## Overview

Most logging libraries are just that -- _logging_ libraries. This one is different. It doesn't try to log your messages or connect to some fancy cloud-based aggregation service.

Instead -- it provides you an API that allows you to determine, in code, what your current level is -- based on `process.evn.LOG_LEVEL` environmental variable.

This way you can align your various logging modules (morgan, winston and custom, for instance) to the same value.

## Custom Decision Function

You can, alternatively, override the function that determines the log level:

```
const LOG_LEVEL = require('log-level/custom');

LOG_LEVEL.init((level) => {
    let result;
    
    switch(level) {
    case 'TRACE':
        result = process.env.MY_LOG_LEVEL === 'trace';
        break;
    case 'DEBUG':
        result = process.env.MY_LOG_LEVEL === 'my-info';
        break;
    default:
        ...
        break;
    }
});
```

which would then allow you to call the same API:

```
if (LOG_LEVEL.INFO) {
    // do something when the log level is set to INFO
}
```
