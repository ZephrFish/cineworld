cineworld
================

I plan on integrating this repository with my UnlmtdCalc app in order to add api calls and personalisation to the application

What is this?
------------

`cineworld` offers an easy-to-use Python wrapper to interact with the
[Cineworld API](https://www.cineworld.co.uk/developer/api/cinemas). Before you try and
use the API, make sure you sign up to get an API Key.

In order to cut down on boilerplate code, you can then save your API key in the
`cineworld_api_key.py` file.

Also, note that this package is in no way associated or endorsed by
[cineworld.co.uk](http://www.cineworld.co.uk/)

Prerequisites
------------

fuzzywuzzy at https://github.com/seatgeek/fuzzywuzzy

Provides fuzzy searching capabilities

Installation
------------

Download the source and use the python executable:

    python setup.py install

Or, if you want to help develop the package, just `git clone` the Github
repository:

    git clone https://github.com/oracal/cineworld.git


Usage
-----

Without saving your API key in the `cineworld_api_key.py` file:

    >>> from cineworld import CW
    >>> CW('my_api_key').film_search('some movie here')

With your API key saved:

    >>> from cineworld import CW
    >>> CW().film_search('some movie here')

**NOTE**: Documentation from this point forward will assume you have saved your
Cineworld Developer API Key to the `cineworld_api_key.py` file (which
you should consider doing in order to cut down on boilerplate code).


### Methods

* `get_film_list`  -- Get a list of all current films
<pre><code>
    >>> cw = CW()
    >>> cw.get_film_list()
	[{u'edi': 39523, u'title': u'3D - Harry Potter And The Deathly Hallows Pt 2'}, {u'edi': 40501, u'title': u'3D - Transformers: Dark Of The Moon'}, ...]
</code></pre>

* `film_search`  -- Custom implemented search to find a list of films relating to the search term, returns an ordered list with strongest match first.
<pre><code>
    >>> cw = CW()
    >>> cw.film_search('harry potter')
    [{'edi': 39523, 'strength': 90, 'title': '3D - Harry Potter And The Deathly Hallows Pt 2'}, {'edi': 35231, 'strength': 90, 'title': '2D - Harry Potter And The Deathly Hallows Pt 2'}]
</code></pre>

* `get_film_id`  -- Get film id, choosing the strongest match generated from the film_search() function, allows you to specify 3D or 2D.
<pre><code>
    >>> cw = CW()
    >>> cw.get_film_id('harry potter', True)
    39523
	>>> cw.get_film_id('harry potter', False)
	35231
</code></pre>

* `get_film_info`  -- Get film info.
<pre><code>
    >>> cw = CW()
    >>> cw.get_film_info(39523)
    [{'advisory': 'Contains moderate threat, injury detail and language', 'film_url': 'http://www.cineworld.co.uk/films/4401', ...}]
</code></pre>


Tests
-----

In order to run the tests for `cineworld.py`, make sure you have the [mock library](http://pypi.python.org/pypi/mock) installed.


License
-------

MIT
