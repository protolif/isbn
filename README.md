isbn
====

Version 3.0

## Introduction

This library provides methods to manipulate ISBNs. As of version 2.0 there has been a near complete rewrite of this library but this time there are tests. A few methods have been removed. Here is what remains:

## Prerequisites: 0

**ISBN.from_image has been deprecated** as of version 3.0.
OCR dependencies have been removed to make this a stand-alone library.


#### Recommendation:

Support barcode reading via Zbar, a lightweight, cross-platform, C library,
with LGPLv2 licensing. It will return a string for use with ISBN.from_string

    $ sudo yum install zbar            # on RedHat or CentOS (EPEL repo)
    $ sudo apt-get install libzbar0    # on Debian or Ubuntu
    $ sudo emerge zbar                 # on Gentoo
    $ brew install zbar                # on Mac OS X with Homebrew (https://brew.sh)
    $ brew install zbar                # on Windows 10 (WSL) with Linuxbrew (https://linuxbrew.sh)

It even has a convenient Ruby wrapper: https://rubygems.org/gems/zbar

However, not every application of ISBN necessitates OCR, so we should not depend on it.
This feature may be re-released as a separate gem at a later date.

## Installing ISBN

#### Installing via Bundler

Add to your `Gemfile`:

```
gem 'isbn'
```

Then run:

```
bundle install
```

#### Installing via RubyGems

Run:

```
gem install isbn
```
## Using ISBN

* `ISBN.ten` will return a 10 digit isbn if you give it a 10 or 13 digit isbn
    - it will raise a `No10DigitISBNAvailable` error if given an isbn starting with 979
   because 979 isbns do NOT have a 10 digit counterpart.
* `ISBN.thirteen` will return a 13 digit isbn if you give it 10 or thirteen digit isbn

* `ISBN.as_used` will convert an isbn into the used book version for that isbn
    - for isbns starting with 978 it returns an isbn starting with 290
    - for isbns starting with 979 it returns an isbn starting with 291

* `ISBN.as_new` will convert an isbn into the new book version for that isbn
    - for isbns starting with 290 it returns an isbn starting with 978
    - for isbns starting with 291 it returns an isbn starting with 979

* `ISBN.valid?` will compare the check digit of the passed in isbn with that of one it computes

* `ISBN.from_string` fetches isbn from string
