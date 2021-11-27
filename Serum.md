## Safe Serum 
I think I have a version of both Serum and Anchor that work or at least compile.
There are three projects in github:
* [Serum Dex](https://github.com/charles-e/bh-serumdex)
* [Anchor](https://github.com/charles-e/bh-anchor18)
* [Serum 0.4.0](https://github.com/charles-e/bh-serum-4.0.0)

You need all three of the projects sitting in the same directory. The serum dex project depends on anchor and anchor depends on the serum 0.4.0.

All of the projects have been migrated from solana to safecoin crates.  

Where necessary I updated to the latest clap beta and corrected a few clap derive macro references.

I have run succesfully the "crank" (serum smoketest) program successfully against the dev cluster.