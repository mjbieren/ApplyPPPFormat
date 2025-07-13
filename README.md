# Apply Phylopypruner format (APPPFormat)
This step is necessary because Phylopypruner requires a specific format.
OSG added the correct format to the alignment files; however, IQTree removed this format from the tree output files. Apply Phylopypruner Format does this for you.
It then moves the tree files to the output folder and copies the alignment files to the exact location.

It needs a taxonomic group file as guidance for the species/strain names (See [TaxonomicGroupFiles](https://github.com/mjbieren/ApplyPPPFormat/tree/main/TaxonomicGroupFiles) for examples). It doesn't matter how many taxonomic groups there are; the tool needs to know the header and strain format (which should be consistent).

To run it, edit the [APPPFormat.sh](https://github.com/mjbieren/ApplyPPPFormat/blob/main/APPPFormat.sh) and run it.
This tool can run with just 1 cpu and output files can not be bigger than 1gb of RAM. It can run on any 64-bit machine on the front end and is super fast. 5% of the time is spent on the calculations. 95% of the time, it parses the input file (loading to memory) and writes the output files, which is heavily dependent on the speed of your disks and/or your network speed.

## APPPFormat (Apply Phylopypruner Format)
This tool was created using the Boost library (version 1.88). It is developed in Visual Studio 2019 with the GCC compiler (For remote Linux). I've compiled two different (static) executables (they are portable!) under Debian 12 ([APPPFormat_Static_Debian.out](https://github.com/mjbieren/ApplyPPPFormat/blob/main/Sources/Executables/APPPFormat_Static_Debian.out)), and Rocky Linux 8, which is based on Linux Red Hat ([APPFormat_Static_HPC.out](https://github.com/mjbieren/ApplyPPPFormat/blob/main/Sources/Executables/APPPFormat_Static_HPC.out)).

Either create your own executable using the corresponding [source files](https://github.com/mjbieren/ApplyPPPFormat/tree/main/Sources/main) or use one of the existing executables.

### Command line options
Program format:
```
APPPFormat.out -i [PathToTrees] -t [FileExtensionOfTrees] -r [OutputFolderPath] -g [TaxonomicGroupFilePath] -m [MafftFilesPath:NOT REQUIRED]
```

### Options

| Flag | Description |
|------|-------------|
| `-i` | Path to the directory containing Newick tree files (required) |
| `-t` | Extension of the tree files (e.g., `.treefile`) (required) |
| `-g` | Taxonomic group file used to identify replacement positions for underscores (`_`) with `@` (required) |
| `-r` | Output directory where processed files will be saved (required) |
| `-m` | Path to MAFFT alignment files (optional). Matching files with `.mafft` extension will be moved and renamed to `.fa` in the output folder |
