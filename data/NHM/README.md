# README

## Metadata

This data was taken from the open access collection records offered by the Natural History Museum (London, United Kingdom).

On the search page of data.nhm.ac.uk, the keywords searched for were :"Homo sapiens France" on 2019-12-13.

The link to the resource data you requested on https://data.nhm.ac.uk is available at: [https://data.nhm.ac.uk/downloads/09974a6c-5e2b-4480-91d8-6ad030f3b207_4a1f3c3569284abf764e22c645b00abbe88d994e.zip](https://data.nhm.ac.uk/downloads/09974a6c-5e2b-4480-91d8-6ad030f3b207_4a1f3c3569284abf764e22c645b00abbe88d994e.zip).

A DOI has been created for this data: [https://doi.org/10.5519/qd.8ru3rv2a](https://doi.org/10.5519/qd.8ru3rv2a)

Please ensure you reference this DOI when citing this data.

## Photos

The photos avaliable are listed on the metadata file above, and are all licensed under a Creative Commons 4.0 license.

We only download the first photo of each, and rename as the download id (column 2).

```bash
for i in $(cat data.csv | cut -f 2,8 -d ',' | cut -f 1 -d '|' | awk -F "," '$2 != ""' | tail -n 39); do 
  hash="$(echo "$i" | cut -d, -f 2)"
  name="$(echo "$i" | cut -d, -f 1)"
  wget "$hash" -O DCIM"$name".jpg
done
```
