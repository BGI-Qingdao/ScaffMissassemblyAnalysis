# INSTALL

## step 1 , download all source codes.

>  git clone --recursive  https://github.com/BGI-Qingdao/ScaffMissassemblyAnalysis.git 

or 

> git clone https://github.com/BGI-Qingdao/ScaffMissassemblyAnalysis.git

> cd ScaffMissassemblyAnalysis/

> git submodule init

> git submodule update

## step 2 , compile source code

>  cd codes && make && cd -

# PREPARE

* make sure your scaffolds are generated by scaff_infos way.

    * you must have your contig file and corresponding scaff_infos file .

    * your scaffold are generated by ScaffInfo2Seq with your contig file and  corresponding scaff_infos file.

        * your min_n paramters are also needed  .

* use quast to evaluate your contigs .

* use quast to evaluate you  scaffolds.


# USAGE 

## create a clean folder for your project

> mkdir test && cd test 

## run pipeline with correct arguments 

> installed_path/ScaffNGAReason.sh quast_contig.tsv quast_scaffold.tsv xxx.scaff_infos min_n

## example 

> xxx/ScaffNGAReason.sh  chr21_quast/contigs_reports/all_alignments_chr21.tsv \\\
>  chr21_ogc1/contigs_reports/all_alignments_chr21_noverlap_new-scaff_seqs.tsv \\\
>  test/chr21_noverlap_new.scaff_infos 10

## output example 

```
    ##############################################
Misassembly now type  freq is :
     83 GapError10K
     14 GapError1K
    540 NewContigMissassembly
     46 NewWrongRef
    721 Overlap1K
      1 SeedContigRepeat
    840 UnMatch
    104 WrongOrder
    563 WrongOrientation
    734 WrongRef
##############################################
Log detail is :
 Total  5880
 InScaff  3646
 InContig 2234                   <---these are the standalone contig's missassemblies , which are all ignored. 
 SuccDetect   3646
 ErrorDetect  0
##############################################

Done !

```

# BRIEF 

       this script used to classify each missassmbly of quast_NGA of scaffold.
       current support types are :
           +--standalone contig missassmbly
           |
           +--in scaffold missassbbly
             +
             |
             +-- UnMatch (contig repeat/contig unaligned/contig misassembly ...)
             |
             +-- WrongRef  ( not major ref )
             |
             +-- WrongOrder  ( scaffold rank 1 but not ref rank 1/-1 )
             |
             +-- WrongOrientation (Order correct but orientation diff in ref)
             |
             +-- GapError
             |     |
             |     +--GapError1K (Order & orientation correct , n < 10 , gap_diff>1K)
             |     |
             |     +--GapError10K
             |     |
             |     +--Overlap1K
             |
             +-- Specical
                   |
                   +-- NewContigMiss
                   |
                   +-- NewWrongRef
                   |
                   +-- SeedContigRepeat

       each missambly will belong to one of those types .
