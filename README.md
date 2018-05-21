# eno

A structured data notation language for everyone.

```eno
                                      {
# Le Demo                               "Le Demo": {
                                          "Un saludo en español": "Hola",
Un saludo en español: Hola                "A greeting in english": "Hello",
A greeting in english: Hello              "Films": {
                                            "魔女の宅急便": {
## Films                                      "Rating": "5 Stars"
                              =>            },
魔女の宅急便:                                 "Los amantes del círculo polar": {
Rating = 5 Stars                              "Rating": "⭐⭐⭐⭐⭐"
                                            }
Los amantes del círculo polar:            }
Rating = ⭐⭐⭐⭐⭐                         }
                                      }
```
---
## Overview

- eno is a **structured, plain-text notation** language, related in many ways to its ancestors and relatives *JSON*, *YAML*, *TOML*, *ArchieML*, *Markdown*, and others
- Through its **simple syntax and versatile nature** it targets a wide audience, both in regards to cultural background as well as technical ability
- Documents authored as eno comprise of *elements* that map to **ubiquitous structural types** in all programing languages
- On a syntactic level there are no types in eno, **only textual representations**
- eno provides a high-grade **API to validate and obtain fully customizable types** on the application level instead
- All eno implementations feature **100% internationalized, hand written, human language error messages**
- eno **notation is hybrid - sequential AND associative**, the API lets you interpret documents (or sections therein) either way
- There is no indentation and **all whitespace is optional**, as are empty lines

---
```eno
> A more technical usecase

command:
| ./configure -foo
\             --format bar
\             --hex #bc
\             out.tmpl              {
| sudo make                   =>      "command": "./configure -foo --format bar -- hex #bc out.tmpl\nsudo make\nsudo make install",
| sudo make install                   "json payload": "{\n  \"result\":200\n}"
                                    }
-- json payload
{
  "result": 200
}
-- json payload
```
---

## Filename Extension

eno documents use the extension `.eno`

## MIME Type

On the internet eno documents are transferred as `text/eno`

---
```eno
                                    {
                                      "default": {
# default                               "id": null,
id:                                     "settings": {
## settings                               "hyperservice": "disabled"
hyperservice: disabled                  }
                            =>        },
# production << default               "production": {
id: prod                                "id": "prod",
## settings                             "settings": {
ultraservice: enabled                     "hyperservice": "disabled",
                                          "ultraservice": "enabled"
                                        }
                                      }
                                    }
```
---

## Design Notes

>On whitespace:
>
> The whole idea with ignoring whitespace at the begin, end,
> between different connected lines and between relevant tokens is:
> When you write on paper you don't care if something is "a little to the
> right, left, further down or whatever". As long as "words" or whatever you
> write on paper are clearly separated and graspable by their intent,
> everything is fine. So this is how eno should behave as well.
