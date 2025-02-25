Why I Chose This Solution
Handling a 1 TB log file is a challenge because we can’t just load the entire file into memory—it would be too slow and use up all the system resources. So, the best approach is to process the file line by line, filtering out only the logs that match the given date.

In my solution, I use BufferedReader to read the file efficiently. Instead of storing all logs in memory, I check each line as it’s read. If the line starts with the requested date, I write it to an output file using BufferedWriter. This way, we only keep one line in memory at a time, making it highly scalable.

What Other Approaches I Considered
Loading the File into Memory (Rejected)

One idea was to read the entire file into a list (List<String>), filter logs, and then write them to an output file.
Problem: This would work for small files, but for a 1 TB file, it’s impossible. Even if we had enough RAM, it would be incredibly slow.
Using an Indexed Database (Partially Viable)

If we had frequent queries for specific dates, storing logs in a database like SQLite or Elasticsearch with indexing would make searches much faster.
Problem: This requires preprocessing—we’d have to first insert all logs into a database, which isn’t practical for a single-use extraction.
Using Multi-threading (Optional for Future)

If the log file were split across multiple smaller files (e.g., one per day), we could process them in parallel using multiple threads.
Problem: Since we have a single large file, threading won’t help much unless we implement file chunking, which adds complexity.
Why My Solution is the Best Choice Here
✅ Memory Efficient: Reads and processes logs one line at a time instead of loading everything into memory.
✅ Simple & Reliable: The logic is straightforward—scan the file, filter, and write to output. No complex indexing or extra setup.
✅ Scales Well: Can handle logs of any size without crashing due to memory issues.
✅ Fast Execution: Uses efficient buffered reading/writing to minimize disk I/O overhead.

Possible Future Optimizations
Use Multi-threading: If logs were stored in separate files per day, we could parallelize the search.
Pre-indexing: If frequent queries are expected, we could build an index of byte offsets for each day, enabling faster lookups.
Compression Handling: If logs are stored in .gz format, we can extend the solution to read directly from compressed files.
Would you like me to modify this to support compressed logs or make it multi-threaded? 🚀
