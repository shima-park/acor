# ACOR (Aho-Corasick automation On Redis)
Golang implementation of Aho-Corasick algorithm, working on redis

[![Current Release](https://img.shields.io/github/release/skyoo2003/acor.svg)](https://github.com/skyoo2003/acor/releases/latest)
[![Build Status](https://travis-ci.org/skyoo2003/acor.svg?branch=master)](https://travis-ci.org/skyoo2003/acor)
[![godoc](http://img.shields.io/badge/godoc-reference-blue.svg?style=flat)](https://godoc.org/github.com/skyoo2003/acor)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)


* Refered to project : [judou/redis-ac-keyword](https://github.com/judou/redis-ac-keywords)
* Aho-Corasick algorithm's paper link : [Efficient string matching: an aid to bibliographic search](http://dl.acm.org/citation.cfm?id=360855)
* Aho-Corasick Wikipedia : [Aho-Corasick algorithm wiki](https://en.wikipedia.org/wiki/Aho%E2%80%93Corasick_algorithm)

# Prerequisite

* Golang 1.7+
* Redis 3.x+
* (Optional) Docker

# Redis docker container

If there is no redis docker image, import the image and run the docker container.

```
$ sh run-redis.sh
```

# Usage

```
package main

import (
	"fmt"
	"github.com/skyoo2003/acor"
)

func main() {
	args := &acor.AhoCorasickArgs{
		Addr:     "localhost:6379",
		Password: "",
		DB:       0,
		Name:     "sample",
	}
	ac := acor.Create(args)
	defer ac.Close()

	keywords := []string{"he", "her", "him"}
	for _, k := range keywords {
		ac.Add(k)
	}

	matched := ac.Find("he is him")
	fmt.Println(matched)

    ac.Flush() // If you want to remove all of data 
}
```

# Contribution

If you want to participate, you can create an issue or request a 'Pull Request'.

Welcome any and all suggestions.

# License

MIT License
