# Learnings from :Different

## Debug Month

### Day 2

- Always have validations in frontend and backend because if we only validate in the frontend, A browser running in someone's computer is not a trusted environment, which is why we can't rely on front-end validations only. a malicious actor can manually craft a GQL request to bypass validations
- TypeScript -> JavaScript transpilation changes line numbers. callstacks by default show you the transpiled JS. if you enable a source map, it will show you the original TS code. that way you don't have to do a rebuilt of the code every time you want to debug.

### Day 3, 4 - CPU Spike in MongoDB QA

- Typically, database CPU goes high due to heavy queries (or occasionally due to reindexing)
- High disk usage would indicate heavy queries but here we didn't have a disk I/O graph in datadog to confirm that
- Considering that there was a disk latency spike and a memory spike at the same time as the CPU spike, we can infer that it was in fact a heavy query
- Is it fine to consume 100ms+ for a single mongo-DB query?
  - It should consume single-digit time. Furthermore, it was discussed that if the following query was executed 10 times it would consume one second which is time-consuming.
- A query would be heavy if - it has to traverse a large number of records and/or returns a large result set

### Day 5 - GB vs GiB

- 1 GB is defined as 1000³ (1,000,000,000) bytes and 1 GiB as 1024³ (1,073,741,824) bytes, That means one 1 GB equals 0.93 GiB
- This strange state of ambiguity is rooted in the fact that while computer data is generally measured in binary code, the prefixes used to measure that data (kilo, mega, tera, peta, etc.) derive from the metric system. A metric “kilo” equals 1,000, but a binary “kilo” equals 1,024
- IEC developed a new international standard of measurement using non-metric prefixes for the binary measurements. Under this new standard a kB held its metric value (1,000 bytes) while a brand-new unit of measure, the kibibyte, represented the binary version (1,024 bytes). 1 GB is equal to 0.93 GiB
- Kibibytes (KiB) were joined by their counterparts, mebibyte (the binary version of megabyte), gibibyte, tebibyte, pebibyte, and so on down the line
- Windows operating systems report in GiB but present these numbers as GB—hence all that hard drive capacity uncertainty (and lawsuits). Mac OS shows memory capacity using the digital version of GB (and has since the Snow Leopard release in 2009).
- So, if you send a 100 GB file, you’ll actually be charged for 93 GiB worth of data.

#### Conclusion

- GB is the traditional, metric style of measurement with 1 GB equaling 1,000³ bytes.
- GiB is the binary method; which is the way computers measure data at 1024³ bytes.

### Day 6, 7 - Logging

- Errors should be logged as errors, not log/info
- Log the entire exception (which contains the full trace) not just e.message
- The original exception call stack is lost when you throw a new exception.

### Day 8 - Mobile Bugs

- A simulator is designed to create an environment that contains all of the software variables and configurations that will exist in an app's actual production environment. In contrast, an emulator attempts to mimic all of the hardware features of a production environment and software features.
