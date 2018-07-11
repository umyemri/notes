Large Dataset processing - limitations of each architecture:
- R: no bigger files than 2 GB.
  - it loads everything into memory.
- SAS: huge files are relative.
  - dependent on your CPU and Disk Bandwidth
- Python: depends on your library usage and how you are storing data.
  - i.e. don't rely on memory storage. sip data, process, write it, iterate.
- SQL: huge files are relative.
  - dependent on your server utility and other operations
- [AWK / SED / GREP](https://adamdrake.com/command-line-tools-can-be-235x-faster-than-your-hadoop-cluster.html): extremely agile, but very complicated.
