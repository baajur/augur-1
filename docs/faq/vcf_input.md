# Using VCF Input

If you would like to run augur on whole-genome bacterial data, you probably would like to start with VCF sequence data. (Note that if you have bacterial SNP data, this may be in Fasta format.)

### Format

All of your samples should be combined into one VCF file, where each sample has its own column. As always, it's crucial that the sequence names in your VCF file (at the top of each column) match the sequence names in your meta data file. The VCF file can be uncompressed (ending in `.vcf`) or compressed (ending in `.vcf.gz`).

_When combining multiple VCF files, double-check that the column names remain the same! Many programs change them when combining. If they do not match the names given in your metadata file, it will not work!_

### Reference file

You will also need the reference sequence to which your VCF file maps. This is a Fasta file that contains one full-length genome with positions that correspond to the positions in your VCF file.

### Masking sites

_(Optional)_ If you have areas of your genome that you would like to exclude from analysis (perhaps because they are repetitive or recombinant), you can provide a file in BED format which lists regions to 'mask' (exclude), and run the `augur mask` function. 

An example of this format is below. It does not matter what is in the `Chrom`, `locus tag` or `Comment` fields.

```
Chrom   ChromStart  ChromEnd    locus tag   Comment
NC_000962   23182   23269   IG18_Rv0018c-Rv0019c
NC_000962   33582   33794   Rv0031  remnant of A transposase
NC_000962   80194   80623   IG71_Rv0071-Rv0072
```

### Restricting Gene Translation

_(Optional)_ Bacteria can have thousands of genes, and translating all of them can take quite a bit of time. If you wouldn't like to translate all of them, you can provide a list of genes that you'd like to include in the analysis, and only these will be processed. For example, you might include a list of genes that are associated with drug-resistance. 

To do this, simply create a file with a list of the genes you'd like to include, with one gene name per line. You can then pass this to `augur translate`.