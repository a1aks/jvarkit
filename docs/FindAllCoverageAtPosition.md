# FindAllCoverageAtPosition

Find depth at specific position in a list of BAM files. My colleague Estelle asked: in all the BAM we sequenced, can you give me the depth at a given position ?


## Usage

```
Usage: findallcoverageatposition [options] Files
  Options:
    -filter, --filter
      A filter expression. Reads matching the expression will be filtered-out. 
      Empty String means 'filter out nothing/Accept all'. See https://github.com/lindenb/jvarkit/blob/master/src/main/resources/javacc/com/github/lindenb/jvarkit/util/bio/samfilter/SamFilterParser.jj 
      for a complete syntax.
      Default: mapqlt(1) || MapQUnavailable() || Duplicate() || FailsVendorQuality() || NotPrimaryAlignment() || SupplementaryAlignment()
    --groupby
      Group Reads by
      Default: sample
      Possible Values: [readgroup, sample, library, platform, center, sample_by_platform, sample_by_center, sample_by_platform_by_center, any]
    -h, --help
      print help and exit
    --helpFormat
      What kind of help
      Possible Values: [usage, markdown, xml]
    -o, --out
      Output file. Optional . Default: stdout
    -f, --posfile
      File containing positions. if file suffix is '.bed': all positions in 
      the range will be scanned.
    -p, --position
      -p chrom:pos . Multiple separated by space. Add this chrom/position. 
      Required 
      Default: <empty string>
    --version
      print version and exit

```


## Keywords

 * bam
 * coverage
 * search
 * depth



## See also in Biostars

 * [https://www.biostars.org/p/259223](https://www.biostars.org/p/259223)


## Compilation

### Requirements / Dependencies

* java compiler SDK 1.8 http://www.oracle.com/technetwork/java/index.html (**NOT the old java 1.7 or 1.6**) . Please check that this java is in the `${PATH}`. Setting JAVA_HOME is not enough : (e.g: https://github.com/lindenb/jvarkit/issues/23 )
* GNU Make >= 3.81
* curl/wget
* git
* xsltproc http://xmlsoft.org/XSLT/xsltproc2.html (tested with "libxml 20706, libxslt 10126 and libexslt 815")


### Download and Compile

```bash
$ git clone "https://github.com/lindenb/jvarkit.git"
$ cd jvarkit
$ make findallcoverageatposition
```

The *.jar libraries are not included in the main jar file, so you shouldn't move them (https://github.com/lindenb/jvarkit/issues/15#issuecomment-140099011 ).
The required libraries will be downloaded and installed in the `dist` directory.

### edit 'local.mk' (optional)

The a file **local.mk** can be created edited to override/add some definitions.

For example it can be used to set the HTTP proxy:

```
http.proxy.host=your.host.com
http.proxy.port=124567
```
## Source code 

[https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/misc/FindAllCoverageAtPosition.java](https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/misc/FindAllCoverageAtPosition.java)


<details>
<summary>Git History</summary>

```
Sun Jun 25 16:43:47 2017 +0200 ; loop over gene in region ; https://github.com/lindenb/jvarkit/commit/a491397b51bb7149fcdccad8c5dab9bdf6fd83fa
Mon May 15 10:41:51 2017 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/c13a658b2ed3bc5dd6ade57190e1dab05bf70612
Sat Apr 29 18:45:47 2017 +0200 ; partition ; https://github.com/lindenb/jvarkit/commit/7d72633d50ee333fcad0eca8aaa8eec1a475cc4d
Wed Apr 5 13:49:50 2017 +0200 ; cont, fix bug in findallcovatpos ; https://github.com/lindenb/jvarkit/commit/7db18c7fe90fd5bf64d3ff3a4505607a1974ce6b
Thu Mar 30 17:38:36 2017 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/bba625df69e00a0aa54de192cdce6fda110a65b4
Tue Jul 12 16:26:04 2016 +0200 ; bim2vcf ; https://github.com/lindenb/jvarkit/commit/6df744a561505df03f56e0b18d75587f032fcdbe
Mon Nov 16 12:21:53 2015 +0100 ; blastfilterjs ; https://github.com/lindenb/jvarkit/commit/6b885d465b47f339d323f909c2ae7a88641f08a4
Fri Nov 28 12:48:02 2014 +0100 ; typo ; https://github.com/lindenb/jvarkit/commit/4869a203808dbd7871aa6a272b412d491fd1f5ce
Fri Nov 28 12:44:44 2014 +0100 ; find all coverages ; https://github.com/lindenb/jvarkit/commit/a8c96e489787bf94d752e6bbd7c091175617459b
```

</details>

## Contribute

- Issue Tracker: [http://github.com/lindenb/jvarkit/issues](http://github.com/lindenb/jvarkit/issues)
- Source Code: [http://github.com/lindenb/jvarkit](http://github.com/lindenb/jvarkit)

## License

The project is licensed under the MIT license.

## Citing

Should you cite **findallcoverageatposition** ? [https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md](https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md)

The current reference is:

[http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

> Lindenbaum, Pierre (2015): JVarkit: java-based utilities for Bioinformatics. figshare.
> [http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

 
## Input

The input is a file containing a list of path to the bam.
 
## Example

```
$ find ./testdata/ -type f -name "*.bam" | \
 java -jar dist/findallcoverageatposition.jar -p rotavirus:100


#File              CHROM      POS  SAMPLE  DEPTH  M    I  D  N  S   H  P  EQ  X  Base(A)  Base(C)  Base(G)  Base(T)  Base(N)  Base(^)  Base(-)
./testdata/S4.bam  rotavirus  100  S4      126    126  0  0  0  29  0  0  0   0  5        0        0        121      0        0        0
./testdata/S1.bam  rotavirus  100  S1      317    317  1  0  0  50  0  0  0   0  27       0        1        289      0        1        0
./testdata/S2.bam  rotavirus  100  S2      311    311  0  1  0  60  0  0  0   0  29       1        0        281      0        0        1
./testdata/S3.bam  rotavirus  100  S3      446    446  1  0  0  86  0  0  0   0  39       0        1        406      0        1        0

```

## See also

 * [https://twitter.com/pjacock/status/538300664334798848](https://twitter.com/pjacock/status/538300664334798848)
 * [https://twitter.com/yokofakun/status/538300434109456385](https://twitter.com/yokofakun/status/538300434109456385)
 * [https://twitter.com/pjacock/status/538299549455233024](https://twitter.com/pjacock/status/538299549455233024)
 * FindAVariation

## History

 * 2017: moved to jcommander

