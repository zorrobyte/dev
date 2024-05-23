Datar-Gionis-Indyk-Motwani (DGIM) Algorithm
===

Suppose there is a long stream of bits and we want
to estimate, allowing for some error, the count of
the number of bits.
The Data-Gionis-Indyk-Motwani (DGIM) algorithm
does this with $O( \frac{1}{\epsilon} \lg^2 n)$ storage bits for an
$n$ sized window with estimates within a $1+\epsilon$ range.



References
---

* ch. 4 "Mining Data Streams" of "Mining Massive Datasets" by Leskovec, Rajaraman and Ullman
* "Maintaining Stream Statistics Over Sliding Windows" by Datar, Gionis, Indyk, Motwani
