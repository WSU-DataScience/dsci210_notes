Introduction
============

What is OpenRefine?
-------------------

OpenRefine is described as "a power tool for working with messy data"
`David
Huynh <http://web.archive.org/web/20141021040915/http://davidhuynh.net/spaces/nicar2011/tutorial.pdf>`__
- but what does this mean? It is probably easiest to describe the kinds
of data OpenRefine is good at working with and the sorts of problems it
can help you solve.

OpenRefine is most useful where you have data in a simple tabular format
such as a spreadsheet, a comma separated values file (csv) or a tab
delimited file (tsv) but with internal inconsistencies either in data
formats, or where data appears, or in terminology used. OpenRefine can
be used to standardize and clean data across your file. It can help you:

-  Get an overview of a data set
-  Resolve inconsistencies in a data set, for example standardizing date
   formatting
-  Help you split data up into more granular parts, for example
   splitting up cells with multiple authors into separate cells
-  Match local data up to other data sets, for example in matching local
   subjects against the Library of Congress Subject Headings
-  Enhance a data set with data from other sources

Some common scenarios might be:

-  Where you want to know how many times a particular value (name,
   publisher, subject) appears in a column in your data
-  Where you want to know how values are distributed across your whole
   data set
-  Where you have a list of dates which are formatted in different ways,
   and want to change all the dates in the list to a single common date
   format. For example:

.. csv-table:: Example table
    :header: Data you have, Desired data

    1st January 2014   , 2014-01-01
    01/01/2014         , 2014-01-01
    Jan 1 2014         , 2014-01-01
    2014-01-01         , 2014-01-01

-  Where you have a list of names or terms that differ from each other
   but refer to the same people, places or concepts. For example:

+-----------------+----------------+
| Data you have   | Desired data   |
+=================+================+
| London          | London         |
+-----------------+----------------+
| London]         | London         |
+-----------------+----------------+
| London,]        | London         |
+-----------------+----------------+
| london          | London         |
+-----------------+----------------+

-  Where you have several bits of data combined together in a single
   column, and you want to separate them out into individual bits of
   data with one column for each bit of the data. For example going from
   a single address field (in the first column), to each part of the
   address in a separate field:

+--------------+---------+---------+---------+---------+---------+---------+---------+---------+
| Address in   | Institu | Library | Address | Address | Town/Ci | Region  | Country | Postcod |
| single field | tion    | name    | 1       | 2       | ty      |         |         | e       |
+==============+=========+=========+=========+=========+=========+=========+=========+=========+
| University   | Univers | Llyfrge | Llanbad |         | Aberyst | Ceredig | United  | SY23    |
| of Wales,    | ity     | ll      | arn     |         | wyth    | ion     | Kingdom | 3AS     |
| Llyfrgell    | of      | Thomas  | Fawr    |         |         |         |         |         |
| Thomas Parry | Wales   | Parry   |         |         |         |         |         |         |
| Library,     |         | Library |         |         |         |         |         |         |
| Llanbadarn   |         |         |         |         |         |         |         |         |
| Fawr,        |         |         |         |         |         |         |         |         |
| ABERYSTWYTH, |         |         |         |         |         |         |         |         |
| Ceredigion,  |         |         |         |         |         |         |         |         |
| SY23 3AS,    |         |         |         |         |         |         |         |         |
| United       |         |         |         |         |         |         |         |         |
| Kingdom      |         |         |         |         |         |         |         |         |
+--------------+---------+---------+---------+---------+---------+---------+---------+---------+
| University   | Univers | Queen   | Meston  |         | Aberdee |         | United  | AB24    |
| of Aberdeen, | ity     | Mother  | Walk    |         | n       |         | Kingdom | 3UE     |
| Queen Mother | of      | Library |         |         |         |         |         |         |
| Library,     | Abderde |         |         |         |         |         |         |         |
| Meston Walk, | en      |         |         |         |         |         |         |         |
| ABERDEEN,    |         |         |         |         |         |         |         |         |
| AB24 3UE,    |         |         |         |         |         |         |         |         |
| United       |         |         |         |         |         |         |         |         |
| Kingdom      |         |         |         |         |         |         |         |         |
+--------------+---------+---------+---------+---------+---------+---------+---------+---------+
| University   | Univers | Barnes  | Medical | Edgbast | Birming | West    | United  | B15 2TT |
| of           | ity     | Library | School  | on      | ham     | Midland | Kingdom |         |
| Birmingham,  | of      |         |         |         |         | s       |         |         |
| Barnes       | Birming |         |         |         |         |         |         |         |
| Library,     | ham     |         |         |         |         |         |         |         |
| Medical      |         |         |         |         |         |         |         |         |
| School,      |         |         |         |         |         |         |         |         |
| Edgbaston,   |         |         |         |         |         |         |         |         |
| BIRMINGHAM,  |         |         |         |         |         |         |         |         |
| West         |         |         |         |         |         |         |         |         |
| Midlands,    |         |         |         |         |         |         |         |         |
| B15 2TT,     |         |         |         |         |         |         |         |         |
| United       |         |         |         |         |         |         |         |         |
| Kingdom      |         |         |         |         |         |         |         |         |
+--------------+---------+---------+---------+---------+---------+---------+---------+---------+
| University   | Univers | Library | Gibbett |         | Coventr |         | United  | CV4 7AL |
| of Warwick,  | ity     |         | Hill    |         | y       |         | Kingdom |         |
| Library,     | of      |         | Road    |         |         |         |         |         |
| Gibbett Hill | Warwick |         |         |         |         |         |         |         |
| Road,        |         |         |         |         |         |         |         |         |
| COVENTRY,    |         |         |         |         |         |         |         |         |
| CV4 7AL,     |         |         |         |         |         |         |         |         |
| United       |         |         |         |         |         |         |         |         |
| Kingdom      |         |         |         |         |         |         |         |         |
+--------------+---------+---------+---------+---------+---------+---------+---------+---------+

-  Where you want to add to your data from an external data source:

+--------------------+-----------------+-----------------+
| Data you have      | Date of Birth   | Date of Death   |
|                    | from VIAF       | from VIAF       |
|                    | (Virtual        | (Virtual        |
|                    | International   | International   |
|                    | Authority File) | Authority File) |
+====================+=================+=================+
| Braddon, M. E.     | 1835            | 1915            |
| (Mary Elizabeth)   |                 |                 |
+--------------------+-----------------+-----------------+
| Rossetti, William  | 1829            | 1919            |
| Michael            |                 |                 |
+--------------------+-----------------+-----------------+
| Prest, Thomas      | 1810            | 1879            |
| Peckett            |                 |                 |
+--------------------+-----------------+-----------------+
