---
layout: post
title: "Incremental rules in Rego"
date: 2020-02-04 13:37:00 +0100
categories: opa
---

So a lot of the stuff I've been working on lately has revolved around Open Policy Agent (OPA). Though I'm planning a longer writeup on the subject
I'll use this blog to post some of my notes while I exlore this great piece of tehnology.

### Incremental rule - sets

A common pattern when writing Rego policies is to use [incremental rules](https://www.openpolicyagent.org/docs/latest/policy-cheatsheet/#incremental) to build a set of values. This is tremendously useful for e.g. returning a message for each violation of a defined policy:

```
deny[reason] {
    input.role != "admin"
    reason = "User not an admin"
}

deny[reason] {
    time.weekday(time.now_ns()) == "Sunday"
    reason = "Access not allowed on Sundays"
}
```
Any non-admin trying to access the requested resource on a Sunday would now not only be denied, but could also be given an explanation as to why:

```
"deny": [
    "Access not allowed on Sundays",
    "User not an admin"
]
```
See full example on the [Rego Playground](https://play.openpolicyagent.org/p/sAG0hfF1Fd).

### Incremental rules - maps

Not as commonly used, but certainly just as useful - incremental rules can also be used to build up maps. This could be used similarily to build up key/value pairs of reasons or violations, but might just as well be used for data transformations. Consider the following input provided to OPA:

```
{
    "street": "High street 32",
    "zip": "11766"
}
```
We could create an incremental map rule to gradually build a structured address object with values in a normalized format:

```
address["zip"] = zip_numeric {
    zip_numeric = to_number(input.zip)
}

address["street_name"] = streetname {
    streetname = trim(concat(" ", regex.find_n(`[^\d]+`, input.street, -1)), " ")
}

address["street_number"] = streetnumber {
    numbers := regex.find_n(`\d+$`, input.street, 1)
    streetnumber = to_number(numbers[0])
}
```
Which would increment the address rule map as follows:

```
{
    "address": {
        "street_name": "High street",
        "street_number": 32,
        "zip": 11766
    }
}
```
Again, see full example on the [Rego Playground](https://play.openpolicyagent.org/p/5DvgKi3Y1x).