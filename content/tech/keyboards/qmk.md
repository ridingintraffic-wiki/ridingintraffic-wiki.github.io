---
date: 2023-04-11T
title: "qmk"
tags: [ qmk]
categories: [ keyboards ]
---

## setting left or right master
some splits will have a left or right set as the master in the main keyboard `config.h`  
Overwriting this is more involved that just resetting it.  You need to detect the variable and then undef it.  like so:
```
    #ifdef EE_HANDS
        #undef EE_HANDS
    #endif
    #ifdef MASTER_RIGHT
        #undef MASTER_RIGHT
    #endif
    #define MASTER_LEFT
```