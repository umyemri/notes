Large Dataset processing - limitations of each architecture:
- R: no bigger files than 2 GB.
  - it loads everything into memory.
    - some solutions for this: https://rstudio-pubs-static.s3.amazonaws.com/72295_692737b667614d369bd87cb0f51c9a4b.html
- SAS: huge files are relative.
  - dependent on your CPU and Disk Bandwidth
- Python: depends on your library usage and how you are storing data.
  - i.e. don't rely on memory storage. sip data, process, write it, iterate.
- SQL: huge files are relative.
  - dependent on your server utility and other operations
  - also dependant on your server handlers, and if they have data quota requirements.
- [AWK / SED / GREP](https://adamdrake.com/command-line-tools-can-be-235x-faster-than-your-hadoop-cluster.html): extremely agile, but very complicated.

Majority of my time: spent waiting for things to compress, decompress or tarnsfer.
